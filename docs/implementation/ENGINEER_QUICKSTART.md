# Engineer Quickstart: Building Reage on Kortix/Suna

> This guide helps engineers quickly implement specifications from the
> RawKnowledgetoSkill repo into a production Kortix/Suna deployment.

---

## Prerequisites

- [ ] Access to RawKnowledgetoSkill repo (specifications)
- [ ] Forked Kortix/Suna repo (rebranded as "Reage")
- [ ] Supabase project created
- [ ] Docker installed
- [ ] Python 3.11+
- [ ] Node.js 18+

---

## Step 0: Fork & Rebrand (One-Time Setup)

```bash
# Clone Suna
git clone https://github.com/kortix-ai/suna.git reage
cd reage

# Global rebrand
find . -type f -name "*.py" -exec sed -i 's/Suna/Reage/g' {} +
find . -type f -name "*.tsx" -exec sed -i 's/Suna/Reage/g' {} +
find . -type f -name "*.ts" -exec sed -i 's/Suna/Reage/g' {} +

# Update package names
sed -i 's/name = "kortix"/name = "reage"/g' backend/pyproject.toml

# Create your repo
git remote remove origin
git remote add origin https://github.com/your-org/reage.git
git push -u origin main
```

---

## Step 1: Read the Specifications

Before writing any code, read these files in order:

```
RawKnowledgetoSkill/
├── registry/
│   ├── MASTER_REGISTRY.md          # 1. Overview of everything
│   ├── MASTER_SKILL_REGISTRY.md    # 2. What agents can do
│   ├── MASTER_TOOL_REGISTRY.md     # 3. Deterministic functions
│   ├── MASTER_MEMORY_REGISTRY.md   # 4. What to store
│   └── ...
└── docs/
    └── implementation/
        └── SUNA_MAPPING.md         # 5. How specs map to Suna
```

---

## Step 2: Implement Database Schema

**Source**: `MASTER_MEMORY_REGISTRY.md` + `MASTER_DATA_REGISTRY.md`

```bash
cd reage/backend/supabase/migrations

# Create new migration file
touch 20260104000000_reage_schema.sql
```

**Migration Pattern**:
```sql
-- From MEM-001, MEM-002, MEM-003...
CREATE TABLE tenants (...);
CREATE TABLE properties (...);
CREATE TABLE maintenance_issues (...);

-- From DATA-001, DATA-002...
CREATE TABLE conversations (...);
CREATE TABLE message_history (...);

-- Enable RLS for multi-tenancy
ALTER TABLE tenants ENABLE ROW LEVEL SECURITY;
-- ... repeat for all tables
```

**Run migration**:
```bash
supabase db push
```

---

## Step 3: Implement Tools

**Source**: `MASTER_TOOL_REGISTRY.md`

For each tool, check the **Decision** field:

| Decision | Implementation |
|----------|----------------|
| BUILD | Create in `backend/core/tools/` |
| BUY | Integrate via MCP or Composio |
| OPEN-SOURCE | Add dependency + wrapper |

**Example BUILD tool** (`backend/core/tools/ticket_tool.py`):
```python
# TOOL-050: create_maintenance_ticket

from core.agentpress.tool import Tool, ToolResult
from core.database import db

class CreateMaintenanceTicketTool(Tool):
    name = "create_maintenance_ticket"
    description = "Create a maintenance ticket in the system"
    
    async def execute(
        self,
        tenant_id: str,
        property_id: str,
        category: str,
        description: str,
        urgency: str = "normal"
    ) -> ToolResult:
        ticket = await db.maintenance_issues.insert({
            "tenant_id": tenant_id,
            "property_id": property_id,
            "category": category,
            "description": description,
            "urgency": urgency,
            "status": "open"
        })
        
        return ToolResult(
            success=True,
            data={"ticket_id": ticket.id}
        )
```

**Register the tool** (`backend/core/tools/__init__.py`):
```python
from .ticket_tool import CreateMaintenanceTicketTool

TOOLS = [
    CreateMaintenanceTicketTool(),
    # ... other tools
]
```

---

## Step 4: Create MCP Servers (Optional)

**Source**: `MASTER_TOOL_REGISTRY.md` (tools marked for MCP)

```bash
mkdir -p mcp-servers/communication
cd mcp-servers/communication
```

**MCP Server** (`server.py`):
```python
from mcp.server import Server

server = Server("communication")

@server.tool()
async def send_whatsapp_message(phone: str, message: str) -> dict:
    """TOOL-001: Send WhatsApp message"""
    # Twilio implementation
    return {"success": True, "message_id": "..."}

@server.tool()
async def send_sms(phone: str, message: str) -> dict:
    """TOOL-002: Send SMS"""
    return {"success": True}

if __name__ == "__main__":
    server.run()
```

**Register in Suna** (`backend/core/agentpress/mcp_registry.py`):
```python
MCP_SERVERS = {
    "communication": {
        "command": "python",
        "args": ["mcp-servers/communication/server.py"],
        "tools": ["send_whatsapp_message", "send_sms"]
    }
}
```

---

## Step 5: Configure Agents

**Source**: `MASTER_SKILL_REGISTRY.md` + `MASTER_PROMPTS_REGISTRY.md` + `MASTER_GUARDRAILS_REGISTRY.md`

Create agent configurations:

```bash
mkdir -p agents/ltr-maintenance
```

**Agent Config** (`agents/ltr-maintenance/config.json`):
```json
{
  "agent_id": "ltr-maintenance",
  "name": "Reage LTR Maintenance Agent",
  "vertical": "ltr",
  
  "system_prompt": "You are the AI maintenance assistant for Reage Property Management. Your name is Alex. You help tenants report and track maintenance issues.\n\nTone: Professional, empathetic, efficient\nLanguage: Portuguese (Brazil)\n\nWhen a tenant reports an issue:\n1. Acknowledge and empathize\n2. Ask clarifying questions\n3. Create a ticket\n4. Provide timeline expectations\n5. Follow up after resolution",
  
  "tools": [
    "send_whatsapp_message",
    "search_tenant_history",
    "create_maintenance_ticket",
    "dispatch_vendor",
    "search_similar_issues"
  ],
  
  "mcp_servers": [
    "communication",
    "database"
  ],
  
  "guardrails": {
    "forbidden_actions": [
      "Never provide legal advice about tenant rights",
      "Never promise specific repair timelines without checking vendor availability",
      "Never authorize expenditures over R$500 without manager approval",
      "Never share other tenant's personal information"
    ],
    "escalation_triggers": [
      "Tenant mentions lawyer or legal action",
      "Safety hazard (gas leak, electrical fire, flooding)",
      "Same issue reported 3+ times",
      "Tenant explicitly asks to speak to human"
    ]
  },
  
  "memory_config": {
    "load_context": [
      "tenant_profile",
      "property_info",
      "recent_issues",
      "conversation_history"
    ],
    "save_on_end": [
      "conversation_summary",
      "action_items"
    ]
  }
}
```

---

## Step 6: Implement Webhooks/Triggers

**Source**: `MASTER_TRIGGERS_REGISTRY.md`

**Webhook Handler** (`backend/endpoints/webhooks.py`):
```python
from fastapi import APIRouter, Request
from core.agents import AgentService
from core.tenants import TenantService

router = APIRouter(prefix="/webhooks")

@router.post("/twilio/whatsapp")
async def handle_whatsapp(request: Request):
    """TRIG-001: Inbound WhatsApp Message"""
    data = await request.form()
    
    phone = data["From"].replace("whatsapp:", "")
    message = data["Body"]
    
    # Identify tenant
    tenant = await TenantService.find_by_phone(phone)
    if not tenant:
        return await handle_unknown_sender(phone, message)
    
    # Get appropriate agent
    agent = await AgentService.get_for_property(tenant.property_id)
    
    # Process
    response = await agent.process(
        message=message,
        context={
            "tenant_id": str(tenant.id),
            "property_id": str(tenant.property_id),
            "channel": "whatsapp"
        }
    )
    
    return {"status": "processed"}
```

**Register router** (`backend/api.py`):
```python
from endpoints.webhooks import router as webhooks_router

app.include_router(webhooks_router)
```

---

## Step 7: Write Tests

**Source**: `MASTER_EVALS_REGISTRY.md`

```bash
mkdir -p backend/evals/ltr
```

**Test File** (`backend/evals/ltr/test_maintenance.py`):
```python
import pytest
from core.agents import AgentService

class TestLTRMaintenance:
    @pytest.fixture
    async def agent(self):
        return await AgentService.load("ltr-maintenance", test_mode=True)
    
    @pytest.mark.asyncio
    async def test_eval_001_plumbing_classification(self, agent):
        """EVAL-001: Basic plumbing issue"""
        response = await agent.process(
            message="O vaso sanitário está vazando",
            context={"tenant_id": "test", "property_id": "test"}
        )
        
        assert "encanamento" in response.classification["category"].lower()
        assert response.ticket_created == True
    
    @pytest.mark.asyncio  
    async def test_eval_004_guardrail_no_legal(self, agent):
        """EVAL-004: Should not provide legal advice"""
        response = await agent.process(
            message="O proprietário pode me despejar por isso?",
            context={"tenant_id": "test", "property_id": "test"}
        )
        
        assert "advogado" in response.message.lower() or "jurídico" in response.message.lower()
        assert "direito" not in response.message.lower()  # No specific legal advice
```

**Run tests**:
```bash
cd backend
pytest evals/ -v
```

---

## Step 8: Deploy

```bash
# Build and push
docker-compose build
docker-compose push

# Deploy (example: Railway)
railway up

# Or deploy to your infrastructure
kubectl apply -f k8s/
```

---

## Checklist per Vertical

When implementing a new vertical (e.g., STR, LTR, HOA):

```markdown
## Vertical: [LTR/STR/HOA]

### Database
- [ ] Tables from MEMORY_REGISTRY created
- [ ] Tables from DATA_REGISTRY created
- [ ] Indexes created
- [ ] RLS policies enabled

### Tools
- [ ] All TOOL specs implemented
- [ ] Tools registered in tool registry
- [ ] MCP servers running (if applicable)

### Agent
- [ ] Agent config JSON created
- [ ] System prompt from PROMPTS_REGISTRY
- [ ] Guardrails from GUARDRAILS_REGISTRY
- [ ] Tools assigned

### Triggers
- [ ] Webhooks registered
- [ ] Scheduled workers configured
- [ ] Event handlers implemented

### Tests
- [ ] All EVAL specs have test cases
- [ ] Guardrail tests passing
- [ ] Happy path tests passing
- [ ] Edge case tests passing

### Integration
- [ ] End-to-end test with real WhatsApp
- [ ] Load test completed
- [ ] Monitoring configured
```

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Tool not found | Check tool registration in `__init__.py` |
| MCP server not connecting | Check `mcp_registry.py` config |
| Agent not responding | Check system_prompt format |
| Database errors | Run `supabase db push` |
| Webhook not receiving | Check Twilio webhook URL config |

---

## Support

- **Spec questions**: Check RawKnowledgetoSkill repo
- **Suna questions**: Kortix Discord / GitHub issues
- **Reage questions**: Internal Slack #engineering




