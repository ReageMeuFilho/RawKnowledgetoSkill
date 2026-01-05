# Specification → Kortix/Suna Implementation Mapping

> This document shows exactly how each specification from RawKnowledgetoSkill
> translates into Kortix/Suna code and configuration.

---

## Quick Reference

| Specification | Suna Location | Format |
|---------------|---------------|--------|
| Skills | Agent config JSON | `agents/{agent_id}/config.json` |
| Tools | Python files | `backend/core/tools/{tool_name}.py` |
| MCP Servers | MCP registry | `mcp_registry.py` + external server |
| Memory | Supabase migrations | `backend/supabase/migrations/*.sql` |
| Data Schemas | Supabase migrations | `backend/supabase/migrations/*.sql` |
| Integrations | MCP or Composio | `composio_integration/` or MCP |
| Guardrails | Agent config | Part of agent JSON |
| Prompts | Agent config | `system_prompt` field |
| Workflows | Database tables | `workflow_system.sql` |
| Evals | Eval framework | `backend/evals/` |
| Triggers | Webhooks + Workers | `api.py` + `run_worker.py` |

---

## Detailed Mappings

### 1. SKILL → Agent Configuration

**Your Specification** (`registry/verticals/ltr/SKILLS.md`):
```markdown
### SKILL-LTR-001: Maintenance Triage

**Description**: Classify tenant maintenance requests
**Triggers**: Inbound WhatsApp message with maintenance keywords
**Tools Required**: TOOL-001, TOOL-040, TOOL-050
```

**Suna Implementation** (`agents/ltr-maintenance/config.json`):
```json
{
  "agent_id": "ltr-maintenance",
  "name": "Reage LTR Maintenance Agent",
  "description": "Handles tenant maintenance requests for long-term rentals",
  
  "system_prompt": "You are the maintenance assistant for Reage...",
  
  "tools": [
    "send_whatsapp_message",
    "search_tenant_history",
    "create_maintenance_ticket"
  ],
  
  "mcp_servers": [
    "mcp-communication",
    "mcp-database",
    "mcp-operations"
  ],
  
  "guardrails": {
    "forbidden_actions": [
      "Never provide legal advice",
      "Never authorize payments > $500"
    ]
  }
}
```

---

### 2. TOOL → Python File or MCP Server

**Your Specification** (`MASTER_TOOL_REGISTRY.md`):
```markdown
### TOOL-001: send_whatsapp_message

**Decision**: BUY (Twilio)
**Purpose**: Send WhatsApp messages to tenants
**Function Signature**:
def send_whatsapp_message(
    phone: str,
    message: str,
    media_url: Optional[str] = None
) -> MessageResult
```

**Option A: Native Suna Tool** (`backend/core/tools/whatsapp_tool.py`):
```python
from core.agentpress.tool import Tool, ToolResult

class WhatsAppTool(Tool):
    name = "send_whatsapp_message"
    description = "Send WhatsApp message to tenant"
    
    async def execute(
        self,
        phone: str,
        message: str,
        media_url: str = None
    ) -> ToolResult:
        # Twilio implementation
        client = Client(TWILIO_SID, TWILIO_AUTH)
        msg = client.messages.create(
            from_='whatsapp:+14155238886',
            to=f'whatsapp:{phone}',
            body=message,
            media_url=media_url
        )
        return ToolResult(
            success=True,
            data={"message_id": msg.sid}
        )
```

**Option B: MCP Server** (`mcp-servers/communication/server.py`):
```python
from mcp.server import Server
from mcp.types import Tool

server = Server("communication")

@server.tool()
async def send_whatsapp_message(
    phone: str,
    message: str,
    media_url: str = None
) -> dict:
    """Send WhatsApp message via Twilio"""
    # Implementation
    return {"success": True, "message_id": "..."}

if __name__ == "__main__":
    server.run()
```

---

### 3. MEMORY → Supabase Migration

**Your Specification** (`MASTER_MEMORY_REGISTRY.md`):
```markdown
### MEM-003: Issue History

**Purpose**: Track maintenance issues for pattern detection
**Retention**: Forever (legal requirement)
**Schema**:
- issue_id: UUID
- tenant_id: UUID
- description: TEXT
- description_embedding: VECTOR(1536)
- is_recurring: BOOLEAN
```

**Suna Implementation** (`backend/supabase/migrations/20260104_issue_history.sql`):
```sql
-- Migration: Issue History for Reage
-- Spec: MEM-003

CREATE TABLE IF NOT EXISTS maintenance_issues (
    issue_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL REFERENCES tenants(id),
    property_id UUID NOT NULL REFERENCES properties(id),
    
    -- Classification
    category VARCHAR(50) NOT NULL,
    subcategory VARCHAR(50),
    location VARCHAR(100),
    
    -- Content
    description TEXT NOT NULL,
    description_embedding VECTOR(1536),
    
    -- Status
    status VARCHAR(20) DEFAULT 'open',
    urgency VARCHAR(20) DEFAULT 'normal',
    
    -- Pattern detection
    is_recurring BOOLEAN DEFAULT FALSE,
    related_issue_ids UUID[],
    recurrence_count INTEGER DEFAULT 1,
    
    -- Timestamps
    created_at TIMESTAMPTZ DEFAULT NOW(),
    resolved_at TIMESTAMPTZ,
    
    -- Multi-tenant isolation
    account_id UUID NOT NULL REFERENCES accounts(id)
);

-- Vector search index
CREATE INDEX idx_issue_embedding 
ON maintenance_issues 
USING ivfflat (description_embedding vector_cosine_ops);

-- Tenant lookup index
CREATE INDEX idx_issue_tenant 
ON maintenance_issues(tenant_id, created_at DESC);

-- RLS Policy (multi-tenant)
ALTER TABLE maintenance_issues ENABLE ROW LEVEL SECURITY;

CREATE POLICY tenant_isolation ON maintenance_issues
    USING (account_id = current_setting('app.current_account_id')::uuid);
```

---

### 4. WORKFLOW → Database + Code

**Your Specification** (`MASTER_WORKFLOWS_REGISTRY.md`):
```markdown
### WORKFLOW-001: Maintenance Request Flow

**States**: receive → classify → assess → dispatch → confirm → follow_up
**Transitions**:
- receive → classify: Always
- classify → assess: If category identified
- assess → dispatch: If urgency >= normal
- dispatch → confirm: When vendor assigned
```

**Suna Implementation**:

1. **Database** (`migrations/20260104_maintenance_workflow.sql`):
```sql
INSERT INTO workflow_definitions (
    workflow_id,
    name,
    states,
    initial_state
) VALUES (
    'maintenance-request',
    'Maintenance Request Flow',
    '["receive", "classify", "assess", "dispatch", "confirm", "follow_up"]',
    'receive'
);

INSERT INTO workflow_transitions (workflow_id, from_state, to_state, condition) VALUES
('maintenance-request', 'receive', 'classify', 'always'),
('maintenance-request', 'classify', 'assess', 'category_identified'),
('maintenance-request', 'assess', 'dispatch', 'urgency >= normal'),
('maintenance-request', 'dispatch', 'confirm', 'vendor_assigned');
```

2. **Code** (`backend/workflows/maintenance_flow.py`):
```python
from core.workflows import WorkflowEngine

maintenance_workflow = WorkflowEngine.load("maintenance-request")

async def process_maintenance_request(message: str, context: dict):
    state = await maintenance_workflow.get_current_state(context["thread_id"])
    
    if state == "receive":
        # Classify the issue
        classification = await classify_issue(message)
        await maintenance_workflow.transition(
            context["thread_id"],
            "classify",
            data=classification
        )
    # ... handle other states
```

---

### 5. TRIGGER → Webhook + Worker

**Your Specification** (`MASTER_TRIGGERS_REGISTRY.md`):
```markdown
### TRIG-001: Inbound WhatsApp Message

**Event Type**: webhook
**Source**: Twilio
**Endpoint**: POST /webhooks/twilio/whatsapp
**Payload**: { From, Body, MediaUrl0, ... }
```

**Suna Implementation** (`backend/api.py` or `endpoints/webhooks.py`):
```python
from fastapi import APIRouter, Request
from core.agents import AgentService

router = APIRouter()

@router.post("/webhooks/twilio/whatsapp")
async def handle_whatsapp_webhook(request: Request):
    """TRIG-001: Inbound WhatsApp Message"""
    data = await request.form()
    
    phone = data.get("From", "").replace("whatsapp:", "")
    message = data.get("Body", "")
    media_url = data.get("MediaUrl0")
    
    # Identify tenant and property
    tenant = await TenantService.find_by_phone(phone)
    
    if not tenant:
        return {"error": "Unknown sender"}
    
    # Route to appropriate agent
    agent = await AgentService.get_agent_for_property(
        tenant.property_id,
        vertical="ltr"  # or "str" based on property type
    )
    
    # Process message
    response = await agent.process(
        message=message,
        context={
            "tenant_id": tenant.id,
            "property_id": tenant.property_id,
            "phone": phone,
            "media_url": media_url
        }
    )
    
    return response
```

---

### 6. EVAL → Test Suite

**Your Specification** (`MASTER_EVALS_REGISTRY.md`):
```markdown
### EVAL-001: Maintenance Classification - Happy Path

**Input**: "The toilet in the master bathroom is leaking"
**Expected**:
- category: "plumbing"
- item: "toilet"
- location: "master bathroom"
- urgency: "normal"
```

**Suna Implementation** (`backend/evals/test_maintenance.py`):
```python
import pytest
from core.agents import MaintenanceAgent

class TestMaintenanceClassification:
    """EVAL-001 to EVAL-010: Maintenance Classification Tests"""
    
    @pytest.fixture
    def agent(self):
        return MaintenanceAgent(test_mode=True)
    
    @pytest.mark.asyncio
    async def test_eval_001_happy_path(self, agent):
        """EVAL-001: Plumbing issue classification"""
        result = await agent.classify(
            "The toilet in the master bathroom is leaking"
        )
        
        assert result["category"] == "plumbing"
        assert result["item"] == "toilet"
        assert result["location"] == "master bathroom"
        assert result["urgency"] in ["normal", "urgent"]
    
    @pytest.mark.asyncio
    async def test_eval_002_emergency(self, agent):
        """EVAL-002: Emergency detection"""
        result = await agent.classify(
            "There's water flooding from the ceiling!"
        )
        
        assert result["urgency"] == "emergency"
        assert result["escalate"] == True
```

---

## Implementation Order

For each vertical (STR, LTR, HOA), implement in this order:

```
1. Database migrations (MEMORY + DATA specs)
   └── Creates the tables the agent needs

2. Tools (TOOL specs)
   └── Native Python or MCP servers

3. Agent configuration (SKILL + PROMPT + GUARDRAIL specs)
   └── The agent JSON that ties everything together

4. Webhooks/Workers (TRIGGER specs)
   └── Entry points that activate the agent

5. Workflows (WORKFLOW specs)
   └── Multi-step conversation logic

6. Tests (EVAL specs)
   └── Validation before production
```

---

## File Naming Convention

| Spec ID | Suna File |
|---------|-----------|
| `SKILL-LTR-001` | `agents/ltr-maintenance/config.json` |
| `TOOL-001` | `backend/core/tools/whatsapp_tool.py` |
| `MEM-003` | `migrations/20260104_issue_history.sql` |
| `WORKFLOW-001` | `workflows/maintenance_flow.py` |
| `TRIG-001` | `endpoints/webhooks.py::handle_whatsapp` |
| `EVAL-001` | `evals/test_maintenance.py::test_eval_001` |

This naming convention creates traceability from spec to implementation.



