# Engineering Specification: Cross-Cutting Platform Features
## Phase 1 Group 6 - Foundation Services

| Metadata | Value |
|----------|-------|
| **Specification ID** | SPEC-PLATFORM-001 |
| **Skills Covered** | SKILL-059, SKILL-060, SKILL-061, SKILL-042 |
| **Gap Reference** | Phase 1 Group 6 |
| **Version** | 1.0.0 |
| **Status** | SPECIFIED |
| **Created** | 2026-01-07 |
| **Author** | Citadel OS Engineering |

---

## 1. Executive Summary

This specification defines the cross-cutting platform features that serve as the foundational nervous system for the Citadel OS property management platform. These four skills provide essential services that all other business capabilities depend upon:

| Skill ID | Skill Name | Category | Priority |
|----------|------------|----------|----------|
| SKILL-059 | Permission Management | Platform | P0 |
| SKILL-060 | Audit Logging | Platform | P0 |
| SKILL-061 | Notification Management | Platform | P0 |
| SKILL-042 | Analytics Dashboard | Platform | P0 |

### Business Value

- **Permission Management**: Zero-trust security with role-based access control supporting multi-tenant property management
- **Audit Logging**: SOC 2 and GDPR compliance with immutable audit trails
- **Notification Management**: Multi-channel communication (email, SMS, push, in-app, WhatsApp) with 99.5% delivery rate
- **Analytics Dashboard**: Real-time KPI visualization with <2s dashboard load times

---

## 2. Architecture Alignment Notes

### 2.1 Layer Mapping (Citadel OS 6-Layer Stack)

```
┌─────────────────────────────────────────────────────────────┐
│ Layer 6: Applications                                        │
│ - Analytics Dashboard UI (React 19 + Next.js 15)            │
│ - Admin Portal for Permissions                               │
│ - Notification Center UI                                     │
├─────────────────────────────────────────────────────────────┤
│ Layer 5: Domain Bundles                                      │
│ - Platform Bundle (cross-cutting services)                   │
├─────────────────────────────────────────────────────────────┤
│ Layer 4: Skills Layer (THIS SPECIFICATION)                   │
│ - SKILL-059: Permission Management                           │
│ - SKILL-060: Audit Logging                                   │
│ - SKILL-061: Notification Management                         │
│ - SKILL-042: Analytics Dashboard                             │
├─────────────────────────────────────────────────────────────┤
│ Layer 3: Hot Path (AI Reasoning)                             │
│ - AI-powered anomaly detection in audit logs                 │
│ - Smart notification prioritization                          │
│ - Predictive analytics recommendations                       │
├─────────────────────────────────────────────────────────────┤
│ Layer 2: Cold Path (Financial Guarantees)                    │
│ - TigerBeetle: Audit event persistence (immutable)           │
│ - Formance: Permission audit trail ledger                    │
│ - Temporal: Notification workflow orchestration              │
├─────────────────────────────────────────────────────────────┤
│ Layer 1: Infrastructure                                      │
│ - AWS (Primary), Latitude.sh (Brazil Edge)                   │
│ - ECS/Fargate (NOT Kubernetes)                               │
│ - PostgreSQL + Redis + Redpanda                              │
└─────────────────────────────────────────────────────────────┘
```

### 2.2 Execution Path Classification

| Skill | Path | Reasoning |
|-------|------|-----------|
| SKILL-059 Permission Management | **COLD** | Deterministic RBAC rules, zero tolerance for permission errors |
| SKILL-060 Audit Logging | **COLD** | Compliance-critical, immutable records, financial-grade integrity |
| SKILL-061 Notification Management | **HYBRID** | Cold for delivery guarantees, Hot for smart prioritization |
| SKILL-042 Analytics Dashboard | **HYBRID** | Cold for financial metrics, Hot for predictive insights |

### 2.3 MCP Server Requirements

```yaml
mcp_servers:
  # Permission Management
  - mcp://permission-check
    description: "RBAC permission evaluation"
    operations: [check_permission, get_user_roles, validate_resource_access]
    
  - mcp://role-management
    description: "Role CRUD operations"
    operations: [create_role, update_role, assign_user_role]
    
  # Audit Logging
  - mcp://audit-write
    description: "Immutable audit event recording"
    operations: [log_event, log_security_alert, log_compliance_event]
    backed_by: TigerBeetle (immutable ledger)
    
  - mcp://audit-read
    description: "Audit log queries"
    operations: [query_events, generate_compliance_report, search_logs]
    
  # Notification Management
  - mcp://notification-send
    description: "Multi-channel notification dispatch"
    operations: [send_notification, schedule_notification, bulk_send]
    backed_by: Temporal workflows
    
  - mcp://notification-preferences
    description: "User notification settings"
    operations: [get_preferences, update_preferences, manage_quiet_hours]
    
  # Analytics Dashboard
  - mcp://analytics-read
    description: "KPI and metrics queries"
    operations: [get_dashboard_data, query_kpis, get_trends]
    
  - mcp://analytics-realtime
    description: "Real-time metrics streaming"
    operations: [subscribe_metrics, get_live_data]
    backed_by: Redpanda (streaming)
```

### 2.4 Infrastructure Alignment Verification

| Research Spec | Citadel OS Architecture | Alignment Action |
|--------------|------------------------|------------------|
| Kubernetes (EKS) | **ECS/Fargate** | Use ECS/Fargate for container orchestration |
| Python/FastAPI | **Rust/Axum** (API Gateway) | API Gateway in Rust, services can use Python |
| Apache Kafka | **Redpanda** | Use Redpanda for event streaming |
| PostgreSQL | **PostgreSQL** ✓ | Confirmed alignment |
| Redis | **Redis** ✓ | Confirmed alignment |
| Auth0/Cognito | **AWS Cognito** (primary) | Use Cognito for identity federation |
| DataDog | **OpenTelemetry + Grafana** | Use open-source observability stack |

---

## 3. System Architecture

### 3.1 High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         API Gateway (Rust/Axum)                          │
│                    Rate Limiting │ JWT Validation │ Routing              │
└─────────────────────────────────────────────────────────────────────────┘
                                      │
          ┌───────────────────────────┼───────────────────────────┐
          │                           │                           │
          ▼                           ▼                           ▼
┌─────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│   Permission    │     │    Audit Logging    │     │   Notification      │
│    Service      │     │      Service        │     │     Service         │
│   (Python)      │     │     (Rust)          │     │    (Python)         │
├─────────────────┤     ├─────────────────────┤     ├─────────────────────┤
│ • RBAC Engine   │     │ • Event Capture     │     │ • Multi-Channel     │
│ • Role Mgmt     │     │ • Immutable Store   │     │ • Preferences       │
│ • Permission    │     │ • Compliance        │     │ • Templates         │
│   Caching       │     │   Reporting         │     │ • Delivery Track    │
└────────┬────────┘     └──────────┬──────────┘     └──────────┬──────────┘
         │                         │                           │
         │              ┌──────────┴──────────┐                │
         │              │                     │                │
         ▼              ▼                     ▼                ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                        Analytics Service (Python)                        │
│           Real-time KPIs │ Dashboard Generation │ Trend Analysis         │
└─────────────────────────────────────────────────────────────────────────┘
                                      │
┌─────────────────────────────────────┼───────────────────────────────────┐
│                             Data Layer                                   │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌───────────┐            │
│  │PostgreSQL │  │   Redis   │  │ Redpanda  │  │TigerBeetle│            │
│  │(Primary)  │  │ (Cache)   │  │(Streaming)│  │(Audit Log)│            │
│  └───────────┘  └───────────┘  └───────────┘  └───────────┘            │
└─────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Service Communication Patterns

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Event-Driven Communication                            │
└─────────────────────────────────────────────────────────────────────────┘

Permission Service ──► Redpanda ──► Audit Service
                        │
                        ├──► Notification Service (permission changes)
                        │
                        └──► Analytics Service (access metrics)

All Services ──► Redpanda ──► Audit Service (event capture)

Notification Service ──► Temporal ──► External Providers
                                       ├── Amazon SES (Email)
                                       ├── Twilio (SMS)
                                       ├── FCM (Push)
                                       └── WhatsApp Business API
```

---

## 4. SKILL-059: Permission Management

### 4.1 Functional Requirements

| Requirement ID | Description | Priority |
|---------------|-------------|----------|
| PERM-001 | Role-based access control (RBAC) with hierarchical roles | P0 |
| PERM-002 | Property-level permission scoping (multi-tenant) | P0 |
| PERM-003 | Resource-level fine-grained permissions | P0 |
| PERM-004 | Permission inheritance and role hierarchy | P1 |
| PERM-005 | Real-time permission caching (<50ms lookups) | P0 |
| PERM-006 | Audit trail for all permission changes | P0 |
| PERM-007 | API-level authorization enforcement | P0 |
| PERM-008 | Multi-factor authentication integration | P1 |

### 4.2 Data Model

```sql
-- Role definitions with hierarchy
CREATE TABLE roles (
    role_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL REFERENCES tenants(tenant_id),
    role_name VARCHAR(100) NOT NULL,
    description TEXT,
    hierarchy_level INTEGER NOT NULL DEFAULT 0,
    parent_role_id UUID REFERENCES roles(role_id),
    is_system_role BOOLEAN DEFAULT FALSE,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW(),
    created_by UUID NOT NULL,
    
    CONSTRAINT uk_tenant_role UNIQUE (tenant_id, role_name)
);

-- Permission definitions
CREATE TABLE permissions (
    permission_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    permission_name VARCHAR(100) NOT NULL UNIQUE,
    resource_type VARCHAR(50) NOT NULL,  -- 'property', 'booking', 'financial', etc.
    action VARCHAR(50) NOT NULL,          -- 'read', 'write', 'delete', 'admin'
    description TEXT,
    is_sensitive BOOLEAN DEFAULT FALSE,   -- Requires MFA
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Role-Permission mapping
CREATE TABLE role_permissions (
    role_id UUID NOT NULL REFERENCES roles(role_id) ON DELETE CASCADE,
    permission_id UUID NOT NULL REFERENCES permissions(permission_id) ON DELETE CASCADE,
    granted_at TIMESTAMPTZ DEFAULT NOW(),
    granted_by UUID NOT NULL,
    
    PRIMARY KEY (role_id, permission_id)
);

-- User-Role assignments with property scoping
CREATE TABLE user_roles (
    user_role_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(user_id),
    role_id UUID NOT NULL REFERENCES roles(role_id),
    property_scope UUID[],  -- NULL = all properties, array = specific properties
    valid_from TIMESTAMPTZ DEFAULT NOW(),
    valid_until TIMESTAMPTZ,  -- NULL = indefinite
    assigned_at TIMESTAMPTZ DEFAULT NOW(),
    assigned_by UUID NOT NULL,
    
    CONSTRAINT uk_user_role_scope UNIQUE (user_id, role_id, property_scope)
);

-- Permission cache tracking
CREATE TABLE permission_cache_invalidations (
    invalidation_id BIGSERIAL PRIMARY KEY,
    user_id UUID,
    role_id UUID,
    invalidated_at TIMESTAMPTZ DEFAULT NOW(),
    reason VARCHAR(100)
);

-- Indexes for performance
CREATE INDEX idx_user_roles_user ON user_roles(user_id) WHERE valid_until IS NULL OR valid_until > NOW();
CREATE INDEX idx_role_permissions_role ON role_permissions(role_id);
CREATE INDEX idx_permissions_resource ON permissions(resource_type, action);
```

### 4.3 Permission Check Algorithm

```python
# permission_engine.py
from typing import Optional, Set
from dataclasses import dataclass
from redis import Redis
import hashlib
import json

@dataclass
class PermissionContext:
    user_id: str
    resource_type: str
    action: str
    property_id: Optional[str] = None
    resource_id: Optional[str] = None

@dataclass
class PermissionResult:
    granted: bool
    reason: str
    cached: bool
    evaluation_time_ms: float

class PermissionEngine:
    """
    COLD PATH: Deterministic RBAC evaluation with aggressive caching.
    Zero tolerance for permission errors - fail closed.
    """
    
    CACHE_TTL = 900  # 15 minutes
    
    def __init__(self, db, redis: Redis):
        self.db = db
        self.redis = redis
    
    def check_permission(self, ctx: PermissionContext) -> PermissionResult:
        """
        Permission evaluation flow:
        1. Check cache (99% hit rate target)
        2. If miss, evaluate from database
        3. Cache result with invalidation tracking
        4. Log decision to audit service
        """
        import time
        start = time.monotonic()
        
        # Step 1: Check cache
        cache_key = self._build_cache_key(ctx)
        cached = self.redis.get(cache_key)
        
        if cached:
            result = json.loads(cached)
            return PermissionResult(
                granted=result['granted'],
                reason=result['reason'],
                cached=True,
                evaluation_time_ms=(time.monotonic() - start) * 1000
            )
        
        # Step 2: Evaluate from database
        granted, reason = self._evaluate_permission(ctx)
        
        # Step 3: Cache result
        self.redis.setex(
            cache_key,
            self.CACHE_TTL,
            json.dumps({'granted': granted, 'reason': reason})
        )
        
        # Step 4: Log to audit (async via Redpanda)
        self._emit_audit_event(ctx, granted, reason)
        
        return PermissionResult(
            granted=granted,
            reason=reason,
            cached=False,
            evaluation_time_ms=(time.monotonic() - start) * 1000
        )
    
    def _evaluate_permission(self, ctx: PermissionContext) -> tuple[bool, str]:
        """
        Hierarchical RBAC evaluation:
        1. Get user's active roles
        2. Apply property scope filtering
        3. Check permission inheritance through role hierarchy
        4. Evaluate final permission
        """
        # Get user's roles (including inherited)
        roles = self._get_user_effective_roles(ctx.user_id, ctx.property_id)
        
        if not roles:
            return False, "No active roles assigned"
        
        # Get required permission
        permission = self._get_permission(ctx.resource_type, ctx.action)
        
        if not permission:
            return False, f"Unknown permission: {ctx.resource_type}:{ctx.action}"
        
        # Check if any role grants this permission
        for role in roles:
            if self._role_has_permission(role, permission['permission_id']):
                return True, f"Granted via role: {role['role_name']}"
        
        return False, "Permission not granted by any assigned role"
    
    def _get_user_effective_roles(self, user_id: str, property_id: Optional[str]) -> list:
        """Get all roles for user, filtered by property scope."""
        query = """
            WITH RECURSIVE role_hierarchy AS (
                -- Base: directly assigned roles
                SELECT r.role_id, r.role_name, r.hierarchy_level, r.parent_role_id,
                       ur.property_scope
                FROM user_roles ur
                JOIN roles r ON ur.role_id = r.role_id
                WHERE ur.user_id = %s
                  AND r.is_active = TRUE
                  AND (ur.valid_until IS NULL OR ur.valid_until > NOW())
                
                UNION ALL
                
                -- Recursive: parent roles (inherited permissions)
                SELECT r.role_id, r.role_name, r.hierarchy_level, r.parent_role_id,
                       rh.property_scope
                FROM roles r
                JOIN role_hierarchy rh ON r.role_id = rh.parent_role_id
                WHERE r.is_active = TRUE
            )
            SELECT DISTINCT role_id, role_name, hierarchy_level, property_scope
            FROM role_hierarchy
            WHERE property_scope IS NULL 
               OR %s = ANY(property_scope)
               OR %s IS NULL
            ORDER BY hierarchy_level DESC
        """
        return self.db.execute(query, [user_id, property_id, property_id])
    
    def _build_cache_key(self, ctx: PermissionContext) -> str:
        """Build deterministic cache key."""
        key_data = f"{ctx.user_id}:{ctx.resource_type}:{ctx.action}:{ctx.property_id or 'all'}"
        return f"perm:{hashlib.sha256(key_data.encode()).hexdigest()[:16]}"
    
    def invalidate_user_cache(self, user_id: str):
        """Invalidate all cached permissions for a user."""
        # Pattern-based deletion (use with caution in production)
        pattern = f"perm:*{user_id}*"
        for key in self.redis.scan_iter(match=pattern):
            self.redis.delete(key)
        
        # Track invalidation
        self._emit_cache_invalidation_event(user_id=user_id)
```

### 4.4 API Endpoints

```yaml
openapi: 3.0.3
info:
  title: Permission Management API
  version: 1.0.0

paths:
  /api/v1/permissions/check:
    post:
      summary: Check if user has permission
      operationId: checkPermission
      requestBody:
        content:
          application/json:
            schema:
              type: object
              required: [user_id, resource_type, action]
              properties:
                user_id:
                  type: string
                  format: uuid
                resource_type:
                  type: string
                  enum: [property, booking, financial, task, user, report]
                action:
                  type: string
                  enum: [read, write, delete, admin]
                property_id:
                  type: string
                  format: uuid
                resource_id:
                  type: string
                  format: uuid
      responses:
        '200':
          description: Permission check result
          content:
            application/json:
              schema:
                type: object
                properties:
                  granted:
                    type: boolean
                  reason:
                    type: string
                  evaluation_time_ms:
                    type: number

  /api/v1/roles:
    get:
      summary: List all roles for tenant
      parameters:
        - name: tenant_id
          in: query
          required: true
          schema:
            type: string
            format: uuid
    post:
      summary: Create new role
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/CreateRole'

  /api/v1/users/{user_id}/roles:
    get:
      summary: Get user's assigned roles
    post:
      summary: Assign role to user
    delete:
      summary: Remove role from user

components:
  schemas:
    CreateRole:
      type: object
      required: [role_name, permissions]
      properties:
        role_name:
          type: string
          maxLength: 100
        description:
          type: string
        parent_role_id:
          type: string
          format: uuid
        permissions:
          type: array
          items:
            type: string
            format: uuid
```

### 4.5 Performance Requirements

| Metric | Target | Measurement |
|--------|--------|-------------|
| Permission check latency (cached) | <10ms | P95 |
| Permission check latency (uncached) | <50ms | P95 |
| Cache hit rate | >95% | Average |
| Throughput | 10,000 req/sec | Peak |
| Availability | 99.99% | Monthly |

---

## 5. SKILL-060: Audit Logging

### 5.1 Functional Requirements

| Requirement ID | Description | Priority |
|---------------|-------------|----------|
| AUD-001 | Capture all user actions and system events | P0 |
| AUD-002 | Immutable storage with cryptographic integrity | P0 |
| AUD-003 | SOC 2 Type II compliance support | P0 |
| AUD-004 | GDPR audit trail requirements | P0 |
| AUD-005 | Real-time security alerting | P0 |
| AUD-006 | 7-year retention with tiered storage | P1 |
| AUD-007 | Full-text search across audit logs | P1 |
| AUD-008 | Compliance report generation | P0 |

### 5.2 Audit Event Schema

```typescript
// audit_event.ts
interface AuditEvent {
  // Event identification
  event_id: string;           // UUID v7 (time-ordered)
  event_timestamp: string;    // ISO 8601 with timezone
  event_type: AuditEventType;
  event_category: EventCategory;
  
  // Actor information
  actor: {
    user_id: string;
    session_id: string;
    ip_address: string;
    user_agent: string;
    auth_method: 'jwt' | 'api_key' | 'service_account';
    mfa_verified: boolean;
  };
  
  // Resource information
  resource: {
    type: string;             // 'property', 'booking', 'user', etc.
    id: string;
    tenant_id: string;
    property_id?: string;
  };
  
  // Action details
  action: {
    name: string;             // 'create', 'update', 'delete', 'access'
    result: 'success' | 'failure' | 'partial';
    failure_reason?: string;
  };
  
  // Change tracking (for mutations)
  changes?: {
    field: string;
    old_value: any;
    new_value: any;
    sensitive: boolean;       // If true, values are masked
  }[];
  
  // Context and correlation
  context: {
    correlation_id: string;   // Request trace ID
    service_name: string;
    service_version: string;
    environment: string;
  };
  
  // Integrity
  integrity: {
    hash: string;             // SHA-256 of event content
    previous_hash: string;    // Chain integrity
    signature?: string;       // Optional cryptographic signature
  };
}

type AuditEventType = 
  | 'authentication'
  | 'authorization'
  | 'data_access'
  | 'data_mutation'
  | 'system_event'
  | 'security_alert'
  | 'compliance_event';

type EventCategory =
  | 'user_management'
  | 'permission_management'
  | 'property_management'
  | 'booking_management'
  | 'financial_transaction'
  | 'notification'
  | 'system_admin';
```

### 5.3 TigerBeetle Integration for Immutable Audit

```rust
// audit_ledger.rs
// Using TigerBeetle for immutable, high-throughput audit event storage

use tigerbeetle_client::{Client, Account, Transfer};
use sha2::{Sha256, Digest};

/// Audit Event stored in TigerBeetle
/// We use TigerBeetle's transfer model to create an immutable chain
pub struct AuditLedger {
    client: Client,
    // Special account IDs for audit categories
    audit_root_account: u128,
}

impl AuditLedger {
    /// Record an audit event as an immutable transfer
    /// Each event references the previous via pending_id (chain integrity)
    pub async fn record_event(&self, event: &AuditEvent) -> Result<u128, AuditError> {
        // Calculate event hash for integrity
        let event_hash = self.calculate_hash(event);
        
        // Create transfer representing the audit event
        let transfer = Transfer {
            id: event.event_id.as_u128(),
            debit_account_id: self.audit_root_account,
            credit_account_id: self.get_category_account(event.event_category),
            amount: 1,  // Each event counts as 1
            pending_id: event.integrity.previous_hash.as_u128(), // Chain link
            user_data_128: event_hash,  // Store hash in user_data
            user_data_64: event.event_timestamp.timestamp() as u64,
            user_data_32: event.actor.user_id.as_u32_hash(),
            timeout: 0,  // Immediate (not pending)
            ledger: AUDIT_LEDGER_ID,
            code: event.event_type.to_code(),
            flags: TransferFlags::none(),
        };
        
        self.client.create_transfers(&[transfer]).await?;
        
        Ok(transfer.id)
    }
    
    /// Verify chain integrity by checking hash links
    pub async fn verify_chain(&self, start_id: u128, end_id: u128) -> Result<bool, AuditError> {
        let transfers = self.client
            .lookup_transfers(&self.get_id_range(start_id, end_id))
            .await?;
        
        let mut previous_hash = 0u128;
        for transfer in transfers {
            if transfer.pending_id != previous_hash {
                return Ok(false);  // Chain broken
            }
            previous_hash = transfer.user_data_128;
        }
        
        Ok(true)
    }
    
    fn calculate_hash(&self, event: &AuditEvent) -> u128 {
        let mut hasher = Sha256::new();
        hasher.update(serde_json::to_vec(event).unwrap());
        let hash = hasher.finalize();
        // Take first 128 bits
        u128::from_be_bytes(hash[..16].try_into().unwrap())
    }
}
```

### 5.4 PostgreSQL Audit Tables (Searchable Store)

```sql
-- Main audit events table (partitioned by month)
CREATE TABLE audit_events (
    event_id UUID PRIMARY KEY,
    event_timestamp TIMESTAMPTZ NOT NULL,
    event_type VARCHAR(50) NOT NULL,
    event_category VARCHAR(50) NOT NULL,
    
    -- Actor
    actor_user_id UUID,
    actor_session_id UUID,
    actor_ip_address INET,
    actor_user_agent TEXT,
    actor_auth_method VARCHAR(20),
    actor_mfa_verified BOOLEAN DEFAULT FALSE,
    
    -- Resource
    resource_type VARCHAR(50) NOT NULL,
    resource_id UUID,
    tenant_id UUID NOT NULL,
    property_id UUID,
    
    -- Action
    action_name VARCHAR(50) NOT NULL,
    action_result VARCHAR(20) NOT NULL,
    failure_reason TEXT,
    
    -- Changes (JSONB for flexibility)
    changes JSONB,
    
    -- Context
    correlation_id UUID NOT NULL,
    service_name VARCHAR(100) NOT NULL,
    service_version VARCHAR(20),
    environment VARCHAR(20) NOT NULL,
    
    -- Integrity
    event_hash BYTEA NOT NULL,
    previous_hash BYTEA,
    tigerBeetle_id NUMERIC(39) NOT NULL,  -- Reference to immutable store
    
    -- Metadata
    created_at TIMESTAMPTZ DEFAULT NOW()
) PARTITION BY RANGE (event_timestamp);

-- Create monthly partitions
CREATE TABLE audit_events_2026_01 PARTITION OF audit_events
    FOR VALUES FROM ('2026-01-01') TO ('2026-02-01');

CREATE TABLE audit_events_2026_02 PARTITION OF audit_events
    FOR VALUES FROM ('2026-02-01') TO ('2026-03-01');

-- Function to auto-create monthly partitions
CREATE OR REPLACE FUNCTION create_audit_partition()
RETURNS void AS $$
DECLARE
    partition_date DATE;
    partition_name TEXT;
    start_date DATE;
    end_date DATE;
BEGIN
    partition_date := DATE_TRUNC('month', NOW() + INTERVAL '1 month');
    partition_name := 'audit_events_' || TO_CHAR(partition_date, 'YYYY_MM');
    start_date := partition_date;
    end_date := partition_date + INTERVAL '1 month';
    
    EXECUTE format(
        'CREATE TABLE IF NOT EXISTS %I PARTITION OF audit_events
         FOR VALUES FROM (%L) TO (%L)',
        partition_name, start_date, end_date
    );
END;
$$ LANGUAGE plpgsql;

-- Indexes for common query patterns
CREATE INDEX idx_audit_tenant_time ON audit_events (tenant_id, event_timestamp DESC);
CREATE INDEX idx_audit_user_time ON audit_events (actor_user_id, event_timestamp DESC);
CREATE INDEX idx_audit_resource ON audit_events (resource_type, resource_id, event_timestamp DESC);
CREATE INDEX idx_audit_correlation ON audit_events (correlation_id);
CREATE INDEX idx_audit_category_time ON audit_events (event_category, event_timestamp DESC);

-- Full-text search index
CREATE INDEX idx_audit_fts ON audit_events USING gin(
    to_tsvector('english', 
        COALESCE(action_name, '') || ' ' || 
        COALESCE(resource_type, '') || ' ' ||
        COALESCE(failure_reason, '')
    )
);
```

### 5.5 Security Alerting Rules

```python
# security_alerting.py
from dataclasses import dataclass
from typing import Callable
from datetime import timedelta

@dataclass
class AlertRule:
    rule_id: str
    name: str
    description: str
    severity: str  # 'critical', 'high', 'medium', 'low'
    condition: Callable
    cooldown: timedelta
    notification_channels: list[str]

SECURITY_ALERT_RULES = [
    AlertRule(
        rule_id="SEC-001",
        name="Multiple Failed Logins",
        description="5+ failed login attempts within 5 minutes",
        severity="high",
        condition=lambda events: (
            len([e for e in events 
                 if e.event_type == 'authentication' 
                 and e.action.result == 'failure']) >= 5
        ),
        cooldown=timedelta(minutes=15),
        notification_channels=['security_team', 'slack_security']
    ),
    
    AlertRule(
        rule_id="SEC-002",
        name="Geographic Anomaly",
        description="Login from two countries within 1 hour",
        severity="critical",
        condition=lambda events: detect_geo_anomaly(events),
        cooldown=timedelta(hours=1),
        notification_channels=['security_team', 'pagerduty']
    ),
    
    AlertRule(
        rule_id="SEC-003",
        name="Permission Escalation",
        description="User granted admin role",
        severity="high",
        condition=lambda events: any(
            e.event_category == 'permission_management' 
            and 'admin' in str(e.changes).lower()
            for e in events
        ),
        cooldown=timedelta(minutes=5),
        notification_channels=['security_team', 'compliance_team']
    ),
    
    AlertRule(
        rule_id="SEC-004",
        name="Mass Data Export",
        description="Large data export detected",
        severity="medium",
        condition=lambda events: any(
            e.action.name == 'export' 
            and e.context.get('record_count', 0) > 1000
            for e in events
        ),
        cooldown=timedelta(hours=1),
        notification_channels=['security_team']
    ),
    
    AlertRule(
        rule_id="SEC-005",
        name="After Hours Access",
        description="Sensitive data access outside business hours",
        severity="low",
        condition=lambda events: any(
            is_outside_business_hours(e.event_timestamp)
            and e.resource.type in ['financial', 'pii']
            for e in events
        ),
        cooldown=timedelta(hours=8),
        notification_channels=['security_team']
    ),
]
```

### 5.6 Compliance Report Generator

```python
# compliance_reports.py
from datetime import datetime, timedelta
from typing import Optional
import pandas as pd

class ComplianceReportGenerator:
    """Generate SOC 2 and GDPR compliance reports from audit logs."""
    
    def generate_soc2_report(
        self, 
        tenant_id: str,
        start_date: datetime,
        end_date: datetime
    ) -> dict:
        """
        Generate SOC 2 Type II report covering:
        - Security (CC6): Access controls, system operations
        - Availability (A1): System monitoring, incident response
        - Confidentiality (C1): Data protection controls
        """
        return {
            "report_type": "SOC 2 Type II",
            "tenant_id": tenant_id,
            "period": {
                "start": start_date.isoformat(),
                "end": end_date.isoformat()
            },
            "sections": {
                "CC6_Security": self._generate_security_section(tenant_id, start_date, end_date),
                "A1_Availability": self._generate_availability_section(tenant_id, start_date, end_date),
                "C1_Confidentiality": self._generate_confidentiality_section(tenant_id, start_date, end_date),
            },
            "summary": {
                "total_events": self._count_events(tenant_id, start_date, end_date),
                "security_alerts": self._count_security_alerts(tenant_id, start_date, end_date),
                "access_reviews_completed": self._count_access_reviews(tenant_id, start_date, end_date),
                "policy_violations": self._count_policy_violations(tenant_id, start_date, end_date)
            },
            "generated_at": datetime.utcnow().isoformat()
        }
    
    def generate_gdpr_data_access_report(
        self,
        tenant_id: str,
        data_subject_id: str,
        start_date: Optional[datetime] = None
    ) -> dict:
        """
        Generate GDPR Article 15 data access report.
        Lists all access to a data subject's personal data.
        """
        if start_date is None:
            start_date = datetime.utcnow() - timedelta(days=365)
        
        access_events = self._query_data_subject_access(
            tenant_id, data_subject_id, start_date
        )
        
        return {
            "report_type": "GDPR Data Subject Access Report",
            "data_subject_id": data_subject_id,
            "period": {
                "start": start_date.isoformat(),
                "end": datetime.utcnow().isoformat()
            },
            "access_events": [
                {
                    "timestamp": e.event_timestamp.isoformat(),
                    "accessor": e.actor.user_id,
                    "access_type": e.action.name,
                    "data_accessed": e.resource.type,
                    "purpose": e.context.get('purpose', 'Not specified'),
                    "legal_basis": e.context.get('legal_basis', 'Legitimate interest')
                }
                for e in access_events
            ],
            "summary": {
                "total_access_events": len(access_events),
                "unique_accessors": len(set(e.actor.user_id for e in access_events)),
                "data_types_accessed": list(set(e.resource.type for e in access_events))
            },
            "generated_at": datetime.utcnow().isoformat()
        }
```

---

## 6. SKILL-061: Notification Management

### 6.1 Functional Requirements

| Requirement ID | Description | Priority |
|---------------|-------------|----------|
| NOT-001 | Multi-channel delivery (email, SMS, push, in-app, WhatsApp) | P0 |
| NOT-002 | User preference management | P0 |
| NOT-003 | Template-based content with localization | P0 |
| NOT-004 | Delivery tracking and retry logic | P0 |
| NOT-005 | Quiet hours enforcement | P1 |
| NOT-006 | Rate limiting and anti-spam | P0 |
| NOT-007 | Scheduled notifications | P1 |
| NOT-008 | Bulk notification support | P1 |

### 6.2 Data Model

```sql
-- Notification templates with localization
CREATE TABLE notification_templates (
    template_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL REFERENCES tenants(tenant_id),
    template_name VARCHAR(100) NOT NULL,
    event_type VARCHAR(100) NOT NULL,  -- 'booking_confirmed', 'payment_received', etc.
    channel VARCHAR(20) NOT NULL,       -- 'email', 'sms', 'push', 'in_app', 'whatsapp'
    locale VARCHAR(10) NOT NULL DEFAULT 'en-US',
    
    -- Template content
    subject_template TEXT,              -- For email
    body_template TEXT NOT NULL,        -- Liquid/Jinja2 template
    action_url_template TEXT,           -- Deep link template
    
    -- Metadata
    is_active BOOLEAN DEFAULT TRUE,
    version INTEGER DEFAULT 1,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW(),
    
    CONSTRAINT uk_template UNIQUE (tenant_id, template_name, channel, locale)
);

-- User notification preferences
CREATE TABLE user_notification_preferences (
    preference_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(user_id),
    tenant_id UUID NOT NULL,
    
    -- Channel preferences per event type (JSONB for flexibility)
    -- Example: {"booking_confirmed": {"email": true, "sms": false, "push": true}}
    channel_preferences JSONB NOT NULL DEFAULT '{}',
    
    -- Quiet hours
    quiet_hours_enabled BOOLEAN DEFAULT FALSE,
    quiet_hours_start TIME,
    quiet_hours_end TIME,
    quiet_hours_timezone VARCHAR(50) DEFAULT 'UTC',
    
    -- Digest preferences
    digest_frequency VARCHAR(20) DEFAULT 'immediate',  -- 'immediate', 'hourly', 'daily'
    
    -- Contact info
    preferred_locale VARCHAR(10) DEFAULT 'en-US',
    
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW(),
    
    CONSTRAINT uk_user_preferences UNIQUE (user_id, tenant_id)
);

-- Notification queue (for processing)
CREATE TABLE notification_queue (
    notification_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL,
    
    -- Recipient
    user_id UUID NOT NULL,
    channel VARCHAR(20) NOT NULL,
    recipient_address TEXT NOT NULL,  -- Email, phone, device token, etc.
    
    -- Content
    template_id UUID REFERENCES notification_templates(template_id),
    subject TEXT,
    body TEXT NOT NULL,
    action_url TEXT,
    
    -- Metadata
    event_type VARCHAR(100) NOT NULL,
    event_data JSONB,                   -- Context data for template
    correlation_id UUID NOT NULL,
    
    -- Scheduling
    scheduled_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    priority INTEGER DEFAULT 5,         -- 1=highest, 10=lowest
    
    -- Status tracking
    status VARCHAR(20) NOT NULL DEFAULT 'pending',
    attempts INTEGER DEFAULT 0,
    max_attempts INTEGER DEFAULT 3,
    last_attempt_at TIMESTAMPTZ,
    delivered_at TIMESTAMPTZ,
    failure_reason TEXT,
    
    -- Provider tracking
    provider_name VARCHAR(50),
    provider_message_id TEXT,
    
    created_at TIMESTAMPTZ DEFAULT NOW(),
    
    CONSTRAINT chk_status CHECK (status IN ('pending', 'processing', 'delivered', 'failed', 'cancelled'))
) PARTITION BY HASH (user_id);

-- Create hash partitions for distribution
CREATE TABLE notification_queue_0 PARTITION OF notification_queue
    FOR VALUES WITH (modulus 4, remainder 0);
CREATE TABLE notification_queue_1 PARTITION OF notification_queue
    FOR VALUES WITH (modulus 4, remainder 1);
CREATE TABLE notification_queue_2 PARTITION OF notification_queue
    FOR VALUES WITH (modulus 4, remainder 2);
CREATE TABLE notification_queue_3 PARTITION OF notification_queue
    FOR VALUES WITH (modulus 4, remainder 3);

-- Indexes
CREATE INDEX idx_queue_status_scheduled ON notification_queue (status, scheduled_at) 
    WHERE status = 'pending';
CREATE INDEX idx_queue_user ON notification_queue (user_id, created_at DESC);
CREATE INDEX idx_queue_correlation ON notification_queue (correlation_id);
```

### 6.3 Temporal Workflow for Notification Delivery

```python
# notification_workflow.py
from temporalio import workflow, activity
from temporalio.common import RetryPolicy
from datetime import timedelta
from dataclasses import dataclass

@dataclass
class NotificationRequest:
    notification_id: str
    tenant_id: str
    user_id: str
    event_type: str
    event_data: dict
    channels: list[str]  # ['email', 'sms', 'push']
    priority: int = 5

@workflow.defn
class NotificationDeliveryWorkflow:
    """
    Temporal workflow for reliable multi-channel notification delivery.
    Handles retries, failover, and delivery tracking.
    """
    
    @workflow.run
    async def run(self, request: NotificationRequest) -> dict:
        results = {}
        
        # Step 1: Load user preferences
        preferences = await workflow.execute_activity(
            load_user_preferences,
            args=[request.user_id, request.tenant_id],
            start_to_close_timeout=timedelta(seconds=10)
        )
        
        # Step 2: Check quiet hours
        if await self._is_quiet_hours(preferences):
            if request.priority > 3:  # Not urgent
                # Schedule for after quiet hours
                await workflow.sleep(self._get_quiet_hours_delay(preferences))
        
        # Step 3: Process each channel
        for channel in request.channels:
            if not self._channel_enabled(preferences, request.event_type, channel):
                results[channel] = {"status": "skipped", "reason": "disabled_by_user"}
                continue
            
            try:
                result = await workflow.execute_activity(
                    deliver_notification,
                    args=[request, channel],
                    retry_policy=RetryPolicy(
                        initial_interval=timedelta(seconds=1),
                        backoff_coefficient=2.0,
                        maximum_interval=timedelta(minutes=5),
                        maximum_attempts=3
                    ),
                    start_to_close_timeout=timedelta(seconds=30)
                )
                results[channel] = {"status": "delivered", "provider_id": result}
                
            except Exception as e:
                results[channel] = {"status": "failed", "error": str(e)}
                
                # Try fallback channel
                fallback = self._get_fallback_channel(channel)
                if fallback and fallback not in results:
                    try:
                        result = await workflow.execute_activity(
                            deliver_notification,
                            args=[request, fallback],
                            start_to_close_timeout=timedelta(seconds=30)
                        )
                        results[fallback] = {"status": "delivered_via_fallback", "provider_id": result}
                    except:
                        pass
        
        # Step 4: Record delivery status
        await workflow.execute_activity(
            record_delivery_status,
            args=[request.notification_id, results],
            start_to_close_timeout=timedelta(seconds=10)
        )
        
        return results

@activity.defn
async def deliver_notification(request: NotificationRequest, channel: str) -> str:
    """Deliver notification via specific channel."""
    
    if channel == "email":
        return await send_email(request)
    elif channel == "sms":
        return await send_sms(request)
    elif channel == "push":
        return await send_push(request)
    elif channel == "whatsapp":
        return await send_whatsapp(request)
    elif channel == "in_app":
        return await send_in_app(request)
    else:
        raise ValueError(f"Unknown channel: {channel}")

async def send_email(request: NotificationRequest) -> str:
    """Send email via Amazon SES."""
    import boto3
    
    ses = boto3.client('ses', region_name='us-east-1')
    
    template = await load_template(request.tenant_id, request.event_type, 'email')
    content = render_template(template, request.event_data)
    
    response = ses.send_email(
        Source=f"Citadel OS <notifications@{request.tenant_domain}>",
        Destination={'ToAddresses': [request.recipient_email]},
        Message={
            'Subject': {'Data': content['subject']},
            'Body': {
                'Html': {'Data': content['body_html']},
                'Text': {'Data': content['body_text']}
            }
        },
        Tags=[
            {'Name': 'tenant_id', 'Value': request.tenant_id},
            {'Name': 'event_type', 'Value': request.event_type}
        ]
    )
    
    return response['MessageId']

async def send_sms(request: NotificationRequest) -> str:
    """Send SMS via Twilio."""
    from twilio.rest import Client
    
    client = Client(TWILIO_SID, TWILIO_AUTH_TOKEN)
    
    template = await load_template(request.tenant_id, request.event_type, 'sms')
    content = render_template(template, request.event_data)
    
    message = client.messages.create(
        body=content['body'],
        from_=TWILIO_FROM_NUMBER,
        to=request.recipient_phone,
        status_callback=f"{WEBHOOK_BASE}/api/v1/notifications/webhook/twilio"
    )
    
    return message.sid

async def send_whatsapp(request: NotificationRequest) -> str:
    """Send WhatsApp message via Twilio/WhatsApp Business API."""
    from twilio.rest import Client
    
    client = Client(TWILIO_SID, TWILIO_AUTH_TOKEN)
    
    template = await load_template(request.tenant_id, request.event_type, 'whatsapp')
    content = render_template(template, request.event_data)
    
    message = client.messages.create(
        body=content['body'],
        from_=f"whatsapp:{WHATSAPP_FROM_NUMBER}",
        to=f"whatsapp:{request.recipient_phone}"
    )
    
    return message.sid
```

### 6.4 Channel Configuration

```yaml
# notification_channels.yaml
channels:
  email:
    provider: amazon_ses
    config:
      region: us-east-1
      configuration_set: citadel-notifications
      bounce_topic: arn:aws:sns:us-east-1:xxx:email-bounces
      complaint_topic: arn:aws:sns:us-east-1:xxx:email-complaints
    rate_limits:
      per_second: 100
      per_day_per_user: 50
    templates:
      format: html
      engine: jinja2
      
  sms:
    provider: twilio
    config:
      account_sid: ${TWILIO_ACCOUNT_SID}
      auth_token: ${TWILIO_AUTH_TOKEN}
      messaging_service_sid: ${TWILIO_MESSAGING_SERVICE}
    rate_limits:
      per_second: 10
      per_day_per_user: 10
    templates:
      format: text
      max_length: 160
      engine: liquid
      
  push:
    provider: firebase_cloud_messaging
    config:
      project_id: ${FCM_PROJECT_ID}
      service_account: ${FCM_SERVICE_ACCOUNT}
    rate_limits:
      per_second: 1000
      per_day_per_user: 100
    templates:
      format: json
      
  whatsapp:
    provider: twilio_whatsapp
    config:
      account_sid: ${TWILIO_ACCOUNT_SID}
      auth_token: ${TWILIO_AUTH_TOKEN}
      whatsapp_number: ${WHATSAPP_NUMBER}
    rate_limits:
      per_second: 5
      per_day_per_user: 20
    templates:
      format: text
      requires_approval: true  # WhatsApp template approval required
      
  in_app:
    provider: internal
    config:
      websocket_endpoint: wss://ws.citadelos.com/notifications
      redis_channel: notifications:in_app
    rate_limits:
      per_second: 1000
      per_day_per_user: 500
    templates:
      format: json
```

---

## 7. SKILL-042: Analytics Dashboard

### 7.1 Functional Requirements

| Requirement ID | Description | Priority |
|---------------|-------------|----------|
| ANA-001 | Real-time KPI calculation and display | P0 |
| ANA-002 | Property performance dashboards | P0 |
| ANA-003 | Financial analytics (RevPAR, ADR, NOI) | P0 |
| ANA-004 | Operational metrics tracking | P1 |
| ANA-005 | Custom dashboard creation | P1 |
| ANA-006 | Automated report generation | P1 |
| ANA-007 | Trend analysis and forecasting | P2 |
| ANA-008 | Real-time WebSocket updates | P0 |

### 7.2 KPI Calculation Engine

```python
# kpi_engine.py
from dataclasses import dataclass
from decimal import Decimal
from datetime import date, datetime, timedelta
from typing import Optional

@dataclass
class PropertyKPIs:
    property_id: str
    period_start: date
    period_end: date
    
    # Revenue metrics
    total_revenue: Decimal
    adr: Decimal                    # Average Daily Rate
    revpar: Decimal                 # Revenue Per Available Rental
    occupancy_rate: Decimal         # Percentage
    
    # Booking metrics
    total_bookings: int
    average_los: Decimal            # Length of Stay
    booking_lead_time: Decimal      # Days in advance
    cancellation_rate: Decimal
    
    # Financial metrics
    gross_booking_value: Decimal
    net_operating_income: Decimal
    operating_expenses: Decimal
    expense_ratio: Decimal
    
    # Operational metrics
    average_response_time: timedelta
    guest_satisfaction_score: Decimal
    maintenance_completion_rate: Decimal
    
    calculated_at: datetime

class KPICalculator:
    """
    Real-time KPI calculation engine.
    Combines Cold Path (financial accuracy) with Hot Path (AI insights).
    """
    
    def __init__(self, db, tigerbeetle, redis):
        self.db = db
        self.tigerbeetle = tigerbeetle
        self.redis = redis
    
    async def calculate_property_kpis(
        self,
        property_id: str,
        period_start: date,
        period_end: date
    ) -> PropertyKPIs:
        """Calculate all KPIs for a property in a given period."""
        
        # Get booking data
        bookings = await self._get_bookings(property_id, period_start, period_end)
        
        # Get financial data from TigerBeetle (COLD PATH - guaranteed accuracy)
        financials = await self._get_financials_from_ledger(property_id, period_start, period_end)
        
        # Get property info
        property_info = await self._get_property_info(property_id)
        
        # Calculate available nights
        total_nights = (period_end - period_start).days
        available_nights = total_nights - await self._get_blocked_nights(property_id, period_start, period_end)
        
        # Calculate occupied nights
        occupied_nights = sum(
            (min(b.checkout_date, period_end) - max(b.checkin_date, period_start)).days
            for b in bookings
            if b.status == 'completed'
        )
        
        # Revenue metrics
        total_revenue = financials.total_revenue
        occupancy_rate = Decimal(occupied_nights) / Decimal(available_nights) if available_nights > 0 else Decimal(0)
        adr = total_revenue / Decimal(occupied_nights) if occupied_nights > 0 else Decimal(0)
        revpar = total_revenue / Decimal(available_nights) if available_nights > 0 else Decimal(0)
        
        # Booking metrics
        total_bookings = len(bookings)
        average_los = Decimal(sum(b.length_of_stay for b in bookings)) / Decimal(total_bookings) if total_bookings > 0 else Decimal(0)
        booking_lead_time = Decimal(sum((b.checkin_date - b.created_at.date()).days for b in bookings)) / Decimal(total_bookings) if total_bookings > 0 else Decimal(0)
        
        cancelled = len([b for b in bookings if b.status == 'cancelled'])
        cancellation_rate = Decimal(cancelled) / Decimal(total_bookings) if total_bookings > 0 else Decimal(0)
        
        # Financial metrics
        gross_booking_value = financials.gross_booking_value
        operating_expenses = financials.total_expenses
        net_operating_income = total_revenue - operating_expenses
        expense_ratio = operating_expenses / total_revenue if total_revenue > 0 else Decimal(0)
        
        # Operational metrics
        operational = await self._get_operational_metrics(property_id, period_start, period_end)
        
        return PropertyKPIs(
            property_id=property_id,
            period_start=period_start,
            period_end=period_end,
            total_revenue=total_revenue,
            adr=adr.quantize(Decimal('0.01')),
            revpar=revpar.quantize(Decimal('0.01')),
            occupancy_rate=(occupancy_rate * 100).quantize(Decimal('0.1')),
            total_bookings=total_bookings,
            average_los=average_los.quantize(Decimal('0.1')),
            booking_lead_time=booking_lead_time.quantize(Decimal('0.1')),
            cancellation_rate=(cancellation_rate * 100).quantize(Decimal('0.1')),
            gross_booking_value=gross_booking_value,
            net_operating_income=net_operating_income,
            operating_expenses=operating_expenses,
            expense_ratio=(expense_ratio * 100).quantize(Decimal('0.1')),
            average_response_time=operational.avg_response_time,
            guest_satisfaction_score=operational.satisfaction_score,
            maintenance_completion_rate=operational.maintenance_rate,
            calculated_at=datetime.utcnow()
        )
    
    async def _get_financials_from_ledger(
        self,
        property_id: str,
        start: date,
        end: date
    ) -> 'FinancialSummary':
        """
        Query TigerBeetle for authoritative financial data.
        This is the COLD PATH - guaranteed accuracy from double-entry ledger.
        """
        # Get property's account IDs
        accounts = await self._get_property_accounts(property_id)
        
        # Query TigerBeetle for account balances
        balances = await self.tigerbeetle.get_account_balances(
            account_ids=[
                accounts.revenue_account,
                accounts.expense_account,
                accounts.receivables_account
            ]
        )
        
        # Query transfers for period-specific data
        transfers = await self.tigerbeetle.get_account_transfers(
            account_id=accounts.revenue_account,
            timestamp_min=int(datetime.combine(start, datetime.min.time()).timestamp()),
            timestamp_max=int(datetime.combine(end, datetime.max.time()).timestamp())
        )
        
        return FinancialSummary(
            total_revenue=sum(t.amount for t in transfers if t.credit_account_id == accounts.revenue_account),
            total_expenses=sum(t.amount for t in transfers if t.debit_account_id == accounts.expense_account),
            gross_booking_value=sum(t.amount for t in transfers if t.code == TransferCode.BOOKING_PAYMENT)
        )
```

### 7.3 Real-Time Dashboard Updates

```python
# dashboard_websocket.py
from fastapi import WebSocket, WebSocketDisconnect
from redis.asyncio import Redis
import json
import asyncio

class DashboardWebSocketManager:
    """
    WebSocket manager for real-time dashboard updates.
    Uses Redis Pub/Sub for cross-instance coordination.
    """
    
    def __init__(self, redis: Redis):
        self.redis = redis
        self.active_connections: dict[str, list[WebSocket]] = {}
    
    async def connect(self, websocket: WebSocket, user_id: str, dashboard_id: str):
        """Accept WebSocket connection and subscribe to updates."""
        await websocket.accept()
        
        key = f"{user_id}:{dashboard_id}"
        if key not in self.active_connections:
            self.active_connections[key] = []
        self.active_connections[key].append(websocket)
        
        # Subscribe to Redis channel for this dashboard
        pubsub = self.redis.pubsub()
        await pubsub.subscribe(f"dashboard:{dashboard_id}")
        
        # Start listening for updates
        asyncio.create_task(self._listen_for_updates(websocket, pubsub, dashboard_id))
        
        # Send initial dashboard data
        initial_data = await self._get_dashboard_data(user_id, dashboard_id)
        await websocket.send_json({
            "type": "initial_data",
            "data": initial_data
        })
    
    async def _listen_for_updates(self, websocket: WebSocket, pubsub, dashboard_id: str):
        """Listen for Redis pub/sub messages and forward to WebSocket."""
        try:
            async for message in pubsub.listen():
                if message['type'] == 'message':
                    data = json.loads(message['data'])
                    await websocket.send_json({
                        "type": "update",
                        "widget_id": data.get('widget_id'),
                        "data": data.get('data'),
                        "timestamp": data.get('timestamp')
                    })
        except WebSocketDisconnect:
            await pubsub.unsubscribe(f"dashboard:{dashboard_id}")
    
    async def broadcast_kpi_update(self, property_id: str, kpi_type: str, value: dict):
        """Broadcast KPI update to all subscribed dashboards."""
        # Find all dashboards watching this property
        dashboard_ids = await self._get_dashboards_for_property(property_id)
        
        for dashboard_id in dashboard_ids:
            await self.redis.publish(
                f"dashboard:{dashboard_id}",
                json.dumps({
                    "widget_id": f"kpi_{kpi_type}_{property_id}",
                    "data": value,
                    "timestamp": datetime.utcnow().isoformat()
                })
            )
```

### 7.4 Dashboard Data Model

```sql
-- User dashboards
CREATE TABLE dashboards (
    dashboard_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL REFERENCES tenants(tenant_id),
    user_id UUID NOT NULL REFERENCES users(user_id),
    
    dashboard_name VARCHAR(200) NOT NULL,
    description TEXT,
    dashboard_type VARCHAR(50) NOT NULL,  -- 'executive', 'property', 'financial', 'operational'
    
    -- Layout configuration
    layout JSONB NOT NULL DEFAULT '[]',   -- Widget positions and sizes
    
    -- Filters
    default_date_range VARCHAR(20) DEFAULT '30d',
    property_filter UUID[],               -- NULL = all properties
    
    -- Sharing
    is_public BOOLEAN DEFAULT FALSE,
    shared_with UUID[],                   -- User IDs
    
    -- Metadata
    is_default BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Dashboard widgets
CREATE TABLE dashboard_widgets (
    widget_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    dashboard_id UUID NOT NULL REFERENCES dashboards(dashboard_id) ON DELETE CASCADE,
    
    widget_type VARCHAR(50) NOT NULL,     -- 'kpi_card', 'line_chart', 'bar_chart', 'table', 'map'
    widget_name VARCHAR(200) NOT NULL,
    
    -- Data configuration
    data_source VARCHAR(100) NOT NULL,    -- 'revenue', 'occupancy', 'bookings', etc.
    kpi_id VARCHAR(100),                  -- Reference to KPI definition
    aggregation VARCHAR(20),              -- 'sum', 'avg', 'count', 'max', 'min'
    group_by VARCHAR(50),                 -- 'day', 'week', 'month', 'property'
    
    -- Visualization config
    config JSONB NOT NULL DEFAULT '{}',
    
    -- Position (grid-based layout)
    position_x INTEGER NOT NULL DEFAULT 0,
    position_y INTEGER NOT NULL DEFAULT 0,
    width INTEGER NOT NULL DEFAULT 4,     -- Grid units
    height INTEGER NOT NULL DEFAULT 3,
    
    -- Refresh settings
    refresh_interval INTEGER DEFAULT 60,  -- Seconds, NULL = manual only
    
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- KPI definitions
CREATE TABLE kpi_definitions (
    kpi_id VARCHAR(100) PRIMARY KEY,
    kpi_name VARCHAR(200) NOT NULL,
    kpi_category VARCHAR(50) NOT NULL,    -- 'revenue', 'operational', 'financial', 'guest'
    
    description TEXT,
    formula TEXT,                         -- Human-readable formula
    unit VARCHAR(20),                     -- 'currency', 'percentage', 'count', 'duration'
    
    -- Calculation settings
    calculation_method VARCHAR(50) NOT NULL,
    source_tables TEXT[],
    
    -- Display settings
    format_pattern VARCHAR(50),           -- '#,##0.00', '0.0%', etc.
    trend_direction VARCHAR(10),          -- 'up_good', 'down_good', 'neutral'
    
    -- Thresholds for alerts
    warning_threshold DECIMAL,
    critical_threshold DECIMAL,
    
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Pre-populate standard KPIs
INSERT INTO kpi_definitions (kpi_id, kpi_name, kpi_category, description, calculation_method, unit, format_pattern, trend_direction) VALUES
('revpar', 'RevPAR', 'revenue', 'Revenue Per Available Rental', 'total_revenue / available_nights', 'currency', '$#,##0.00', 'up_good'),
('adr', 'ADR', 'revenue', 'Average Daily Rate', 'total_revenue / occupied_nights', 'currency', '$#,##0.00', 'up_good'),
('occupancy', 'Occupancy Rate', 'revenue', 'Percentage of available nights occupied', 'occupied_nights / available_nights * 100', 'percentage', '0.0%', 'up_good'),
('noi', 'NOI', 'financial', 'Net Operating Income', 'total_revenue - operating_expenses', 'currency', '$#,##0.00', 'up_good'),
('expense_ratio', 'Expense Ratio', 'financial', 'Operating expenses as percentage of revenue', 'operating_expenses / total_revenue * 100', 'percentage', '0.0%', 'down_good'),
('avg_response_time', 'Avg Response Time', 'operational', 'Average time to respond to guest inquiries', 'avg(response_time)', 'duration', '0.0h', 'down_good'),
('guest_satisfaction', 'Guest Satisfaction', 'guest', 'Average guest review score', 'avg(review_score)', 'score', '0.0', 'up_good'),
('cancellation_rate', 'Cancellation Rate', 'revenue', 'Percentage of bookings cancelled', 'cancelled_bookings / total_bookings * 100', 'percentage', '0.0%', 'down_good');
```

---

## 8. Performance Requirements

### 8.1 Service-Level Objectives

| Service | Latency (P95) | Throughput | Availability | Error Rate |
|---------|--------------|------------|--------------|------------|
| Permission Service | <50ms | 10,000 req/s | 99.99% | <0.01% |
| Audit Service | <100ms (write) | 1M events/day | 99.999% | <0.001% |
| Notification Service | <500ms (queue) | 100K/hour | 99.5% | <0.5% |
| Analytics Service | <2s (dashboard) | 1,000 concurrent | 99.9% | <0.1% |

### 8.2 Caching Strategy

```yaml
caching_layers:
  # L1: In-memory (per service instance)
  application_cache:
    technology: Python lru_cache / Rust moka
    ttl: 60s
    max_size: 1000 entries
    use_cases:
      - Permission decisions (hot paths)
      - Template compilations
      - KPI definitions
  
  # L2: Distributed cache
  redis_cache:
    technology: Redis Cluster
    nodes: 6 (3 primary, 3 replica)
    memory: 32GB total
    ttl_by_type:
      permission_decisions: 15min
      user_preferences: 5min
      dashboard_data: 2min
      kpi_calculations: 1min
  
  # L3: CDN (for static/semi-static)
  cloudfront:
    ttl: 24h
    use_cases:
      - Dashboard assets
      - Report PDFs
      - Template previews
```

---

## 9. Security Requirements

### 9.1 Authentication & Authorization

```yaml
authentication:
  provider: AWS Cognito
  methods:
    - jwt_bearer
    - api_key (service accounts)
  mfa:
    required_for:
      - admin roles
      - financial operations
      - permission changes
  session:
    idle_timeout: 30min
    absolute_timeout: 8h
    
authorization:
  model: RBAC with property scoping
  enforcement:
    - API Gateway (coarse-grained)
    - Service level (fine-grained)
    - Resource level (object-level)
  audit:
    all_decisions: true
    failure_alerts: true
```

### 9.2 Data Protection

```yaml
encryption:
  at_rest:
    algorithm: AES-256-GCM
    key_management: AWS KMS
    rotate_keys: 90 days
    
  in_transit:
    tls_version: "1.3"
    cipher_suites: [TLS_AES_256_GCM_SHA384]
    certificate_management: AWS ACM
    
pii_handling:
  classification:
    - email: PII
    - phone: PII
    - ip_address: PII
    - name: PII
  masking:
    in_logs: true
    in_exports: configurable
  retention:
    gdpr_compliant: true
    default: 7 years
    pii_on_delete: pseudonymize
```

---

## 10. Testing Strategy

### 10.1 Test Coverage Requirements

| Component | Unit Tests | Integration | E2E | Coverage Target |
|-----------|-----------|-------------|-----|-----------------|
| Permission Engine | 95% | 85% | 100% critical paths | 90% |
| Audit Service | 98% | 90% | 100% compliance paths | 95% |
| Notification Service | 90% | 85% | 80% | 85% |
| Analytics Service | 90% | 85% | 80% | 85% |

### 10.2 Test Scenarios

```python
# test_permission_engine.py
import pytest
from permission_engine import PermissionEngine, PermissionContext

class TestPermissionEngine:
    """COLD PATH tests - zero tolerance for permission errors."""
    
    @pytest.mark.parametrize("user_role,resource,action,expected", [
        ("admin", "property", "delete", True),
        ("property_manager", "property", "read", True),
        ("property_manager", "property", "delete", False),
        ("guest", "booking", "read", True),
        ("guest", "financial", "read", False),
    ])
    async def test_permission_check_by_role(self, user_role, resource, action, expected):
        """Test permission decisions are deterministic."""
        engine = PermissionEngine(db=mock_db, redis=mock_redis)
        
        result = await engine.check_permission(PermissionContext(
            user_id="test-user",
            resource_type=resource,
            action=action
        ))
        
        assert result.granted == expected
    
    async def test_permission_cache_invalidation(self):
        """Verify cache invalidation propagates correctly."""
        engine = PermissionEngine(db=mock_db, redis=mock_redis)
        
        # First check - populates cache
        result1 = await engine.check_permission(PermissionContext(
            user_id="test-user",
            resource_type="property",
            action="read"
        ))
        assert result1.cached == False
        
        # Second check - from cache
        result2 = await engine.check_permission(PermissionContext(
            user_id="test-user",
            resource_type="property",
            action="read"
        ))
        assert result2.cached == True
        
        # Invalidate and re-check
        await engine.invalidate_user_cache("test-user")
        
        result3 = await engine.check_permission(PermissionContext(
            user_id="test-user",
            resource_type="property",
            action="read"
        ))
        assert result3.cached == False
    
    async def test_property_scope_enforcement(self):
        """Verify property-level scoping works correctly."""
        engine = PermissionEngine(db=mock_db, redis=mock_redis)
        
        # User has access to property A, not property B
        result_a = await engine.check_permission(PermissionContext(
            user_id="scoped-user",
            resource_type="property",
            action="read",
            property_id="property-a"
        ))
        assert result_a.granted == True
        
        result_b = await engine.check_permission(PermissionContext(
            user_id="scoped-user",
            resource_type="property",
            action="read",
            property_id="property-b"
        ))
        assert result_b.granted == False
```

---

## 11. Deployment Configuration

### 11.1 ECS/Fargate Task Definitions

```yaml
# permission-service-task.yaml
family: permission-service
networkMode: awsvpc
requiresCompatibilities:
  - FARGATE
cpu: '1024'
memory: '2048'

containerDefinitions:
  - name: permission-service
    image: ${ECR_REGISTRY}/permission-service:${VERSION}
    portMappings:
      - containerPort: 8080
        protocol: tcp
    environment:
      - name: SERVICE_NAME
        value: permission-service
      - name: LOG_LEVEL
        value: INFO
      - name: REDIS_CLUSTER_ENDPOINT
        value: ${REDIS_ENDPOINT}
      - name: DB_HOST
        value: ${RDS_ENDPOINT}
    secrets:
      - name: DB_PASSWORD
        valueFrom: arn:aws:secretsmanager:us-east-1:xxx:secret:rds-password
      - name: REDIS_AUTH_TOKEN
        valueFrom: arn:aws:secretsmanager:us-east-1:xxx:secret:redis-auth
    healthCheck:
      command: ["CMD-SHELL", "curl -f http://localhost:8080/health || exit 1"]
      interval: 30
      timeout: 5
      retries: 3
      startPeriod: 60
    logConfiguration:
      logDriver: awslogs
      options:
        awslogs-group: /ecs/permission-service
        awslogs-region: us-east-1
        awslogs-stream-prefix: ecs

# Auto-scaling configuration
service:
  desiredCount: 3
  launchType: FARGATE
  platformVersion: LATEST
  
  deploymentConfiguration:
    maximumPercent: 200
    minimumHealthyPercent: 100
    deploymentCircuitBreaker:
      enable: true
      rollback: true
  
  autoScaling:
    minCapacity: 3
    maxCapacity: 20
    targetTrackingPolicies:
      - metricType: ECSServiceAverageCPUUtilization
        targetValue: 70
        scaleInCooldown: 300
        scaleOutCooldown: 60
      - metricType: ECSServiceAverageMemoryUtilization
        targetValue: 80
        scaleInCooldown: 300
        scaleOutCooldown: 60
```

### 11.2 Infrastructure as Code

```hcl
# main.tf - Cross-cutting services infrastructure

module "permission_service" {
  source = "./modules/ecs-service"
  
  service_name    = "permission-service"
  container_image = "${var.ecr_registry}/permission-service:${var.version}"
  
  cpu    = 1024
  memory = 2048
  
  desired_count = 3
  min_capacity  = 3
  max_capacity  = 20
  
  health_check_path = "/health"
  
  environment_variables = {
    SERVICE_NAME = "permission-service"
    REDIS_ENDPOINT = module.redis.endpoint
  }
  
  secrets = {
    DB_PASSWORD = aws_secretsmanager_secret.rds_password.arn
  }
  
  vpc_id     = module.vpc.vpc_id
  subnet_ids = module.vpc.private_subnet_ids
  
  tags = local.common_tags
}

module "audit_service" {
  source = "./modules/ecs-service"
  
  service_name    = "audit-service"
  container_image = "${var.ecr_registry}/audit-service:${var.version}"
  
  # Higher resources for write-heavy workload
  cpu    = 2048
  memory = 4096
  
  desired_count = 2
  min_capacity  = 2
  max_capacity  = 15
  
  health_check_path = "/health"
  
  environment_variables = {
    SERVICE_NAME        = "audit-service"
    TIGERBEETLE_CLUSTER = module.tigerbeetle.cluster_addresses
    REDPANDA_BROKERS    = module.redpanda.broker_addresses
  }
  
  vpc_id     = module.vpc.vpc_id
  subnet_ids = module.vpc.private_subnet_ids
  
  tags = local.common_tags
}

module "notification_service" {
  source = "./modules/ecs-service"
  
  service_name    = "notification-service"
  container_image = "${var.ecr_registry}/notification-service:${var.version}"
  
  cpu    = 1024
  memory = 2048
  
  desired_count = 2
  min_capacity  = 2
  max_capacity  = 10
  
  health_check_path = "/health"
  
  environment_variables = {
    SERVICE_NAME     = "notification-service"
    TEMPORAL_ADDRESS = module.temporal.frontend_address
    SES_REGION       = var.aws_region
  }
  
  secrets = {
    TWILIO_AUTH_TOKEN = aws_secretsmanager_secret.twilio_auth.arn
    FCM_SERVICE_KEY   = aws_secretsmanager_secret.fcm_key.arn
  }
  
  vpc_id     = module.vpc.vpc_id
  subnet_ids = module.vpc.private_subnet_ids
  
  tags = local.common_tags
}

module "analytics_service" {
  source = "./modules/ecs-service"
  
  service_name    = "analytics-service"
  container_image = "${var.ecr_registry}/analytics-service:${var.version}"
  
  # Higher CPU for calculations
  cpu    = 2048
  memory = 4096
  
  desired_count = 2
  min_capacity  = 2
  max_capacity  = 8
  
  health_check_path = "/health"
  
  environment_variables = {
    SERVICE_NAME        = "analytics-service"
    REDIS_ENDPOINT      = module.redis.endpoint
    TIGERBEETLE_CLUSTER = module.tigerbeetle.cluster_addresses
  }
  
  vpc_id     = module.vpc.vpc_id
  subnet_ids = module.vpc.private_subnet_ids
  
  tags = local.common_tags
}
```

---

## 12. Migration & Rollout Plan

### 12.1 Phased Rollout

| Phase | Duration | Scope | Success Criteria |
|-------|----------|-------|------------------|
| Phase 1 | Week 1-2 | Permission Service | <50ms P95, 99.99% availability |
| Phase 2 | Week 3-4 | Audit Logging | 100% event capture, chain integrity |
| Phase 3 | Week 5-6 | Notification Service | 99.5% delivery rate |
| Phase 4 | Week 7-8 | Analytics Dashboard | <2s load time, real-time updates |

### 12.2 Rollback Procedures

```yaml
rollback_triggers:
  automatic:
    - error_rate > 5% for 5 minutes
    - latency_p95 > 3x baseline for 10 minutes
    - availability < 99% for 5 minutes
  
  manual:
    - security incident
    - data integrity issue
    - compliance violation

rollback_procedure:
  1. Trigger: Automatic or manual
  2. Action: ECS rolls back to previous task definition
  3. Duration: <5 minutes
  4. Notification: PagerDuty + Slack
  5. Investigation: Post-mortem within 24h
```

---

## 13. Appendix

### 13.1 Glossary

| Term | Definition |
|------|------------|
| RBAC | Role-Based Access Control |
| ADR | Average Daily Rate |
| RevPAR | Revenue Per Available Rental |
| NOI | Net Operating Income |
| MCP | Multi-Channel Protocol (Citadel OS skill interface) |
| Cold Path | Deterministic processing with guaranteed accuracy |
| Hot Path | AI-powered reasoning with probabilistic outputs |

### 13.2 Related Documents

- `docs/architecture/LAYER4_SKILLS_ARCHITECTURE.md` - Skills framework details
- `docs/COMPLETE_TECHNICAL_ARCHITECTURE.md` - Full system architecture
- `docs/ARCHITECTURE_ALIGNMENT_GUIDE.md` - Technology mapping guide
- `specs/financial/SPEC-SKILL-028-035-FINANCIAL-CORE.md` - Financial core (integration point)

### 13.3 Change Log

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0.0 | 2026-01-07 | Citadel OS Engineering | Initial specification |

---

**Specification Status: COMPLETE**

This specification is ready for implementation. All architecture alignment checks have been verified against the Citadel OS reference architecture.

