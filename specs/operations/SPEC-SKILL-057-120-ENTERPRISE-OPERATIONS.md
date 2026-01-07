# Skill Specification: Enterprise Operations Platform

> **Skills Covered**: SKILL-057, SKILL-058, SKILL-089, SKILL-116, SKILL-117, SKILL-118, SKILL-119, SKILL-120
> **Category**: Operations / Enterprise
> **Phase**: Phase 2 - Group 5 (Enterprise Operations)
> **Priority**: P2 (Enhanced)
> **Status**: SPECIFIED
> **Last Updated**: January 2026
> **Research Source**: Research Phase 2 Group 5.txt (~12,500 lines)

---

## 📋 EXECUTIVE SUMMARY

The Enterprise Operations Platform delivers **8 core enterprise-scale skills** that transform Citadel OS into a multi-tenant SaaS powerhouse for large-scale property management companies:

- **80% automation** of operational processes
- **25% reduction** in labor costs through optimized scheduling
- **99.9% uptime** with multi-tenant isolation
- **<200ms P95** API response time
- **10,000+ properties** per tenant support

### Skills Overview

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-057** | Multi-Brand Management | Tenant | White-label portals, brand theming, asset isolation |
| **SKILL-058** | Regional Access Control | Security | Hierarchical RBAC, geographic scope, audit trails |
| **SKILL-089** | Staff Shift Planning | Scheduling | Constraint optimization, labor compliance, mobile |
| **SKILL-116** | Portfolio Rollup Reporting | Analytics | Multi-currency consolidation, drill-down dashboards |
| **SKILL-117** | SLA Monitoring | Operations | Threshold alerts, escalation workflows, dashboards |
| **SKILL-118** | Vendor Scorecard | Procurement | Weighted KPI scoring, automated tiering |
| **SKILL-119** | Inventory Forecasting | Supply Chain | Demand prediction, reorder optimization |
| **SKILL-120** | Bulk Operations | Data | Idempotent batches, partial failure handling |

---

## 🏗️ ARCHITECTURE ALIGNMENT NOTES

### Layer Mapping (Citadel OS 6-Layer Stack)

| Component | Citadel OS Layer | Implementation |
|-----------|------------------|----------------|
| Enterprise Portal UI | Layer 6: Applications | React + Next.js + TypeScript |
| Enterprise Domain | Layer 5: Domain Bundles | Multi-tenant operations bundle |
| Enterprise Skills | Layer 4: Skills Layer | SKILL.md files |
| API Gateway | Layer 3: Hot Path | Rust/Axum (tenant routing) |
| Tenant Data | Layer 2: Cold Path | PostgreSQL + RLS |
| Event Infrastructure | Layer 1: Infrastructure | Temporal + Kafka + Redis |

### Execution Path Classification

| Skill | Path | Reasoning |
|-------|------|-----------|
| SKILL-057 (Multi-Brand) | **Cold** | Tenant provisioning, configuration |
| SKILL-058 (Access Control) | **Hot** | Real-time permission checks (<50ms) |
| SKILL-089 (Scheduling) | **Hybrid** | Constraint solver + real-time updates |
| SKILL-116 (Reporting) | **Cold** | Aggregation, consolidation |
| SKILL-117 (SLA Monitor) | **Hot** | Real-time threshold checks |
| SKILL-118 (Vendor Score) | **Cold** | Batch KPI calculations |
| SKILL-119 (Forecasting) | **Cold** | ML prediction pipelines |
| SKILL-120 (Bulk Ops) | **Hybrid** | Batch + real-time progress |

### MCP Server Requirements

```yaml
mcp_servers:
  # Multi-Brand Management
  - mcp://enterprise/tenant-provision    # Tenant lifecycle
  - mcp://enterprise/brand-config        # Theme/branding
  
  # Regional Access Control
  - mcp://enterprise/permissions         # RBAC evaluation
  - mcp://enterprise/audit-log           # Compliance tracking
  
  # Staff Scheduling
  - mcp://enterprise/schedule-optimize   # Constraint solver
  - mcp://enterprise/shift-manage        # Real-time updates
  
  # Portfolio Reporting
  - mcp://enterprise/rollup-report       # Consolidation
  - mcp://enterprise/currency-convert    # FX rates
  
  # Operations
  - mcp://enterprise/sla-monitor         # Threshold tracking
  - mcp://enterprise/vendor-score        # KPI calculation
  - mcp://enterprise/inventory-forecast  # Demand prediction
  - mcp://enterprise/bulk-process        # Batch operations
```

### Infrastructure Alignment Verification

| Research Spec | Citadel OS Architecture | Status |
|---------------|------------------------|--------|
| Node.js/TypeScript Backend | ⚠️ Adjustment | Use Python/FastAPI + Rust/Axum |
| PostgreSQL + RLS | ✅ Aligned | Primary with TigerBeetle for financial |
| Redis Cluster | ✅ Aligned | Caching, rate limiting |
| Apache Kafka | ⚠️ Adjustment | Use Redpanda (Kafka-compatible) |
| Temporal | ✅ Aligned | Workflow orchestration |
| AWS ECS/Fargate | ✅ Aligned | Container orchestration |
| Auth0 | ✅ Aligned | Authentication |
| Casbin | ✅ Aligned | RBAC/ABAC engine |

---

## 📊 SKILL SPECIFICATIONS

### SKILL-057: Multi-Brand Management

#### Purpose
White-label architecture supporting unlimited brand configurations with tenant-scoped theming, automated SSL certificates, and complete asset isolation.

#### Technical Architecture
```python
from dataclasses import dataclass
from datetime import datetime
from typing import Dict, Optional, List
import boto3

@dataclass
class TenantConfiguration:
    tenant_id: str
    subdomain: str
    custom_domain: Optional[str]
    ssl_certificate_arn: Optional[str]
    brand_config: "BrandConfig"
    tier: str  # 'basic', 'professional', 'enterprise'
    resource_limits: "ResourceLimits"
    created_at: datetime
    status: str

@dataclass
class BrandConfig:
    primary_color: str
    secondary_color: str
    logo_url: str
    favicon_url: str
    font_family: str
    custom_css: Optional[str]

@dataclass
class ResourceLimits:
    max_users: int
    max_properties: int
    api_rate_limit: int
    storage_quota_gb: int


class TenantManagementService:
    """
    Multi-tenant provisioning with white-label support.
    Creates tenant environments in minutes, not hours.
    """
    
    TIER_CONFIGS = {
        'basic': ResourceLimits(50, 100, 100, 10),
        'professional': ResourceLimits(200, 500, 500, 50),
        'enterprise': ResourceLimits(1000, 10000, 2000, 500)
    }
    
    def __init__(self):
        self.route53 = boto3.client('route53')
        self.acm = boto3.client('acm')
        self.s3 = boto3.client('s3')
        self.db = PostgreSQLClient()
    
    async def provision_tenant(
        self,
        organization_name: str,
        subdomain: str,
        tier: str,
        brand_config: BrandConfig,
        custom_domain: Optional[str] = None
    ) -> TenantConfiguration:
        """Provision new tenant with automated infrastructure."""
        
        # Validate subdomain availability
        if await self._subdomain_exists(subdomain):
            raise SubdomainConflict(subdomain)
        
        # Create tenant record
        tenant = TenantConfiguration(
            tenant_id=str(uuid.uuid4()),
            subdomain=subdomain,
            custom_domain=custom_domain,
            ssl_certificate_arn=None,
            brand_config=brand_config,
            tier=tier,
            resource_limits=self.TIER_CONFIGS[tier],
            created_at=datetime.utcnow(),
            status='provisioning'
        )
        
        await self.db.save_tenant(tenant)
        
        # Provision infrastructure (parallel)
        await asyncio.gather(
            self._setup_database_schema(tenant),
            self._configure_dns_routing(tenant),
            self._provision_ssl_certificate(tenant),
            self._setup_s3_bucket(tenant),
            self._configure_cdn(tenant)
        )
        
        # Apply Row-Level Security
        await self._apply_rls_policies(tenant)
        
        # Initialize brand assets
        await self._upload_brand_assets(tenant, brand_config)
        
        tenant.status = 'active'
        await self.db.update_tenant(tenant)
        
        return tenant
    
    async def _setup_database_schema(self, tenant: TenantConfiguration):
        """Create tenant-specific schema with RLS policies."""
        
        await self.db.execute(f"""
            -- Set tenant context for all connections
            CREATE OR REPLACE FUNCTION set_tenant_context(tenant_uuid UUID)
            RETURNS void AS $$
            BEGIN
                PERFORM set_config('app.current_tenant', tenant_uuid::text, false);
            END;
            $$ LANGUAGE plpgsql;
            
            -- Enable RLS on core tables
            ALTER TABLE properties ENABLE ROW LEVEL SECURITY;
            ALTER TABLE users ENABLE ROW LEVEL SECURITY;
            ALTER TABLE schedules ENABLE ROW LEVEL SECURITY;
            
            -- Create tenant isolation policy
            CREATE POLICY tenant_isolation_{tenant.tenant_id.replace('-', '_')} 
            ON properties FOR ALL 
            USING (tenant_id = current_setting('app.current_tenant')::uuid);
        """)
    
    async def update_brand_config(
        self,
        tenant_id: str,
        brand_config: BrandConfig
    ) -> TenantConfiguration:
        """Update tenant branding with zero-downtime."""
        
        tenant = await self.db.get_tenant(tenant_id)
        
        # Upload new assets to S3
        await self._upload_brand_assets(tenant, brand_config)
        
        # Invalidate CDN cache
        await self._invalidate_cdn_cache(tenant, ['/*'])
        
        tenant.brand_config = brand_config
        await self.db.update_tenant(tenant)
        
        return tenant
```

#### Tenant Isolation Model
```
┌─────────────────────────────────────────────────────────────┐
│                    Shared Infrastructure                     │
├─────────────────────────────────────────────────────────────┤
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Tenant A   │  │   Tenant B   │  │   Tenant C   │      │
│  │  brand-a.com │  │  brand-b.com │  │  brand-c.com │      │
│  ├──────────────┤  ├──────────────┤  ├──────────────┤      │
│  │ RLS Policy A │  │ RLS Policy B │  │ RLS Policy C │      │
│  │ tenant_id=A  │  │ tenant_id=B  │  │ tenant_id=C  │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│                          ▼                                   │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              PostgreSQL (Shared)                     │   │
│  │  + Row-Level Security per tenant                     │   │
│  │  + Tenant-aware indexes                              │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

---

### SKILL-058: Regional Access Control

#### Purpose
Hierarchical RBAC with geographic scope inheritance (Global → Region → Property → Unit), tenant-scoped permissions, and comprehensive audit trails.

#### Technical Architecture
```python
from enum import Enum
from dataclasses import dataclass
from typing import List, Set, Optional

class ScopeLevel(Enum):
    GLOBAL = 'global'
    TENANT = 'tenant'
    REGION = 'region'
    PROPERTY = 'property'
    UNIT = 'unit'

@dataclass
class Permission:
    resource: str        # e.g., 'properties', 'schedules'
    action: str          # e.g., 'read', 'write', 'delete'
    scope_level: ScopeLevel
    scope_ids: Set[str]  # IDs at the scope level

@dataclass
class Role:
    id: str
    name: str
    permissions: List[Permission]
    inherits_from: Optional[str]  # Parent role ID

@dataclass
class UserRole:
    user_id: str
    tenant_id: str
    role_id: str
    scope_level: ScopeLevel
    scope_ids: Set[str]


class HierarchicalRBACService:
    """
    Multi-tenant RBAC with role hierarchy.
    Senior roles inherit permissions from junior roles.
    """
    
    ROLE_HIERARCHY = {
        'global_admin': None,
        'tenant_admin': 'global_admin',
        'regional_manager': 'tenant_admin',
        'property_manager': 'regional_manager',
        'staff_member': 'property_manager'
    }
    
    def __init__(self):
        self.casbin = CasbinEnforcer()
        self.redis = RedisClient()
        self.db = PostgreSQLClient()
        self.audit_logger = AuditLogger()
    
    async def check_permission(
        self,
        user_id: str,
        tenant_id: str,
        resource: str,
        action: str,
        resource_id: str
    ) -> bool:
        """Check permission with caching (<50ms target)."""
        
        # Cache key for permission check
        cache_key = f"perm:{tenant_id}:{user_id}:{resource}:{action}:{resource_id}"
        
        # Check cache first
        cached = await self.redis.get(cache_key)
        if cached is not None:
            return cached == 'true'
        
        # Set tenant context
        await self.db.execute(
            "SELECT set_tenant_context($1)",
            [tenant_id]
        )
        
        # Get user roles
        user_roles = await self._get_user_roles(user_id, tenant_id)
        
        # Get resource scope (which region/property does it belong to)
        resource_scope = await self._get_resource_scope(resource, resource_id)
        
        # Check permission with hierarchy
        allowed = False
        for user_role in user_roles:
            if await self._check_role_permission(
                user_role, resource, action, resource_scope
            ):
                allowed = True
                break
        
        # Cache result (5 minutes TTL)
        await self.redis.setex(cache_key, 300, 'true' if allowed else 'false')
        
        # Audit log
        await self.audit_logger.log(
            event='permission_check',
            user_id=user_id,
            tenant_id=tenant_id,
            resource=resource,
            action=action,
            resource_id=resource_id,
            allowed=allowed
        )
        
        return allowed
    
    async def _check_role_permission(
        self,
        user_role: UserRole,
        resource: str,
        action: str,
        resource_scope: dict
    ) -> bool:
        """Check permission considering role hierarchy and scope."""
        
        role = await self.db.get_role(user_role.role_id)
        
        # Check direct permissions
        for perm in role.permissions:
            if perm.resource == resource and perm.action == action:
                # Check scope overlap
                if self._scopes_overlap(
                    user_role.scope_level, user_role.scope_ids,
                    resource_scope
                ):
                    return True
        
        # Check inherited permissions
        if role.inherits_from:
            parent_role = await self.db.get_role(role.inherits_from)
            return await self._check_inherited_permission(
                parent_role, resource, action, resource_scope
            )
        
        return False
    
    async def assign_regional_role(
        self,
        user_id: str,
        tenant_id: str,
        role_name: str,
        region_ids: Set[str]
    ) -> UserRole:
        """Assign user to regional role with scope."""
        
        role = await self.db.get_role_by_name(role_name)
        
        user_role = UserRole(
            user_id=user_id,
            tenant_id=tenant_id,
            role_id=role.id,
            scope_level=ScopeLevel.REGION,
            scope_ids=region_ids
        )
        
        await self.db.save_user_role(user_role)
        
        # Invalidate permission cache
        await self._invalidate_user_cache(user_id, tenant_id)
        
        await self.audit_logger.log(
            event='role_assigned',
            user_id=user_id,
            tenant_id=tenant_id,
            role=role_name,
            scope='regional',
            scope_ids=list(region_ids)
        )
        
        return user_role
```

#### Role Hierarchy
```
┌────────────────────────────────────────────────────────────┐
│                    GLOBAL ADMINISTRATOR                     │
│               Platform-wide access (all tenants)           │
└─────────────────────────┬──────────────────────────────────┘
                          ▼
┌────────────────────────────────────────────────────────────┐
│                    TENANT ADMINISTRATOR                     │
│              Complete access within tenant scope            │
└─────────────────────────┬──────────────────────────────────┘
                          ▼
┌────────────────────────────────────────────────────────────┐
│                    REGIONAL MANAGER                         │
│              Access to assigned geographic regions          │
└─────────────────────────┬──────────────────────────────────┘
                          ▼
┌────────────────────────────────────────────────────────────┐
│                    PROPERTY MANAGER                         │
│              Access to assigned properties only             │
└─────────────────────────┬──────────────────────────────────┘
                          ▼
┌────────────────────────────────────────────────────────────┐
│                    STAFF MEMBER                             │
│              Task-specific access, own schedules            │
└────────────────────────────────────────────────────────────┘
```

---

### SKILL-089: Staff Shift Planning

#### Purpose
Constraint-based scheduling optimization processing thousands of variables (labor laws, skills, preferences) to create optimal schedules in <5 seconds.

#### Technical Architecture
```python
from ortools.sat.python import cp_model
from dataclasses import dataclass
from datetime import datetime, timedelta
from typing import List, Dict, Set
import numpy as np

@dataclass
class Employee:
    id: str
    name: str
    skills: Set[str]
    max_hours_per_week: int
    availability: Dict[str, List[tuple]]  # day -> [(start, end)]
    preferences: "EmployeePreferences"

@dataclass
class Shift:
    id: str
    property_id: str
    date: datetime
    start_time: datetime
    end_time: datetime
    required_skills: Set[str]
    min_staff: int
    max_staff: int

@dataclass
class ConstraintResult:
    schedule_id: str
    total_shifts_filled: int
    constraint_satisfaction: float
    labor_law_compliant: bool
    employee_assignments: List[Dict]
    unfilled_shifts: List[str]
    optimization_time_ms: int


class ConstraintBasedScheduler:
    """
    OR-Tools constraint solver for workforce scheduling.
    Processes thousands of variables in <5 seconds.
    """
    
    HARD_CONSTRAINTS = [
        'max_consecutive_days',    # Max 6 consecutive workdays
        'minimum_rest_period',     # 8 hours between shifts
        'overtime_threshold',      # 40 hours/week
        'skill_requirements',      # Required skills per shift
        'minimum_staffing'         # Min staff per shift
    ]
    
    SOFT_CONSTRAINTS = [
        'employee_preferences',    # Preferred shifts
        'workload_balance',        # Fair distribution
        'consecutive_shifts',      # Minimize split shifts
        'commute_distance'         # Minimize travel
    ]
    
    def __init__(self):
        self.model = cp_model.CpModel()
        self.db = PostgreSQLClient()
        self.redis = RedisClient()
    
    async def generate_schedule(
        self,
        tenant_id: str,
        property_ids: List[str],
        period_start: datetime,
        period_end: datetime
    ) -> ConstraintResult:
        """Generate optimized schedule using constraint programming."""
        
        start_time = datetime.utcnow()
        
        # Load data
        employees = await self._load_employees(tenant_id, property_ids)
        shifts = await self._load_shifts(property_ids, period_start, period_end)
        
        # Create constraint model
        model = cp_model.CpModel()
        
        # Decision variables: assignment[employee][shift] = 1 if assigned
        assignments = {}
        for e in employees:
            for s in shifts:
                var_name = f'assign_{e.id}_{s.id}'
                assignments[(e.id, s.id)] = model.NewBoolVar(var_name)
        
        # HARD CONSTRAINTS
        
        # 1. Skill requirements
        for shift in shifts:
            skilled_employees = [
                e for e in employees 
                if shift.required_skills.issubset(e.skills)
            ]
            model.Add(
                sum(assignments[(e.id, shift.id)] for e in skilled_employees) 
                >= shift.min_staff
            )
        
        # 2. Minimum rest period (8 hours)
        for employee in employees:
            for i, shift1 in enumerate(shifts):
                for shift2 in shifts[i+1:]:
                    rest_hours = (shift2.start_time - shift1.end_time).seconds / 3600
                    if rest_hours < 8:
                        model.AddBoolOr([
                            assignments[(employee.id, shift1.id)].Not(),
                            assignments[(employee.id, shift2.id)].Not()
                        ])
        
        # 3. Max consecutive days (6 days)
        for employee in employees:
            for day_start in range((period_end - period_start).days - 6):
                consecutive_shifts = [
                    assignments[(employee.id, s.id)]
                    for s in shifts
                    if day_start <= (s.date - period_start).days <= day_start + 6
                ]
                model.Add(sum(consecutive_shifts) <= 6)
        
        # 4. Weekly hours limit
        for employee in employees:
            weekly_hours = sum(
                assignments[(employee.id, s.id)] * 
                int((s.end_time - s.start_time).seconds / 3600)
                for s in shifts
            )
            model.Add(weekly_hours <= employee.max_hours_per_week)
        
        # SOFT CONSTRAINTS (weighted in objective)
        preference_bonus = []
        for employee in employees:
            for shift in shifts:
                if self._is_preferred_shift(employee, shift):
                    preference_bonus.append(
                        assignments[(employee.id, shift.id)] * 10
                    )
        
        # Workload balance
        workload_vars = []
        for employee in employees:
            hours = sum(
                assignments[(employee.id, s.id)] * 
                int((s.end_time - s.start_time).seconds / 3600)
                for s in shifts
            )
            workload_vars.append(hours)
        
        # Objective: maximize preference bonus, minimize workload variance
        model.Maximize(sum(preference_bonus))
        
        # Solve
        solver = cp_model.CpSolver()
        solver.parameters.max_time_in_seconds = 5  # <5s constraint
        status = solver.Solve(model)
        
        # Extract results
        employee_assignments = []
        for employee in employees:
            for shift in shifts:
                if solver.Value(assignments[(employee.id, shift.id)]) == 1:
                    employee_assignments.append({
                        'employee_id': employee.id,
                        'shift_id': shift.id,
                        'date': shift.date.isoformat(),
                        'start': shift.start_time.isoformat(),
                        'end': shift.end_time.isoformat()
                    })
        
        optimization_time = (datetime.utcnow() - start_time).total_seconds() * 1000
        
        return ConstraintResult(
            schedule_id=str(uuid.uuid4()),
            total_shifts_filled=len(employee_assignments),
            constraint_satisfaction=self._calculate_satisfaction(solver),
            labor_law_compliant=status == cp_model.OPTIMAL,
            employee_assignments=employee_assignments,
            unfilled_shifts=self._get_unfilled(shifts, assignments, solver),
            optimization_time_ms=int(optimization_time)
        )
```

#### Scheduling Constraints
| Constraint Type | Rule | Enforcement |
|----------------|------|-------------|
| Max Consecutive Days | 6 days max | Hard (mandatory) |
| Minimum Rest | 8 hours between shifts | Hard (mandatory) |
| Weekly Hours | 40 hours max (configurable) | Hard (mandatory) |
| Skill Coverage | Required skills per shift | Hard (mandatory) |
| Employee Preferences | Preferred shift times | Soft (weighted) |
| Workload Balance | Fair distribution | Soft (weighted) |

---

### SKILL-116: Portfolio Rollup Reporting

#### Purpose
Multi-currency financial consolidation with intercompany eliminations, real-time dashboards, and drill-down analytics from portfolio to unit level.

#### Technical Architecture
```python
from decimal import Decimal
from dataclasses import dataclass
from datetime import datetime
from typing import Dict, List, Optional
import asyncio

@dataclass
class PortfolioMetrics:
    total_revenue: Decimal
    total_noi: Decimal
    total_expenses: Decimal
    occupancy_rate: float
    adr: Decimal  # Average Daily Rate
    revpar: Decimal  # Revenue per Available Room
    currency: str
    
@dataclass
class PropertyFinancials:
    property_id: str
    revenue: Decimal
    expenses: Decimal
    noi: Decimal
    currency: str
    occupancy: float

@dataclass
class ConsolidatedReport:
    report_id: str
    tenant_id: str
    period: str
    base_currency: str
    portfolio_metrics: PortfolioMetrics
    by_region: Dict[str, PortfolioMetrics]
    by_property: List[PropertyFinancials]
    intercompany_eliminations: Decimal
    fx_adjustments: Decimal
    generated_at: datetime


class PortfolioReportingService:
    """
    Real-time portfolio consolidation with <200ms response.
    Supports multi-currency and intercompany eliminations.
    """
    
    def __init__(self):
        self.db = PostgreSQLClient()
        self.redis = RedisClient()
        self.fx_service = FXRateService()
    
    async def generate_consolidated_report(
        self,
        tenant_id: str,
        period_start: datetime,
        period_end: datetime,
        base_currency: str = 'USD'
    ) -> ConsolidatedReport:
        """Generate consolidated portfolio report."""
        
        # Get all properties for tenant
        properties = await self.db.get_tenant_properties(tenant_id)
        
        # Parallel data collection
        financials, fx_rates = await asyncio.gather(
            self._collect_financials(properties, period_start, period_end),
            self.fx_service.get_rates(base_currency)
        )
        
        # Convert to base currency
        converted = []
        total_revenue = Decimal('0')
        total_expenses = Decimal('0')
        total_rooms = 0
        total_occupied = 0
        
        for f in financials:
            rate = fx_rates.get(f.currency, Decimal('1'))
            converted_f = PropertyFinancials(
                property_id=f.property_id,
                revenue=f.revenue * rate,
                expenses=f.expenses * rate,
                noi=(f.revenue - f.expenses) * rate,
                currency=base_currency,
                occupancy=f.occupancy
            )
            converted.append(converted_f)
            
            total_revenue += converted_f.revenue
            total_expenses += converted_f.expenses
            
            prop = next(p for p in properties if p.id == f.property_id)
            total_rooms += prop.room_count
            total_occupied += int(prop.room_count * f.occupancy)
        
        # Calculate intercompany eliminations
        eliminations = await self._calculate_eliminations(
            tenant_id, period_start, period_end
        )
        
        # Calculate portfolio metrics
        occupancy_rate = total_occupied / total_rooms if total_rooms > 0 else 0
        days = (period_end - period_start).days
        available_room_nights = total_rooms * days
        adr = total_revenue / total_occupied if total_occupied > 0 else Decimal('0')
        revpar = total_revenue / available_room_nights if available_room_nights > 0 else Decimal('0')
        
        portfolio_metrics = PortfolioMetrics(
            total_revenue=total_revenue - eliminations,
            total_noi=total_revenue - total_expenses - eliminations,
            total_expenses=total_expenses,
            occupancy_rate=occupancy_rate,
            adr=adr,
            revpar=revpar,
            currency=base_currency
        )
        
        # Group by region
        by_region = await self._aggregate_by_region(converted, properties)
        
        return ConsolidatedReport(
            report_id=str(uuid.uuid4()),
            tenant_id=tenant_id,
            period=f"{period_start.date()} to {period_end.date()}",
            base_currency=base_currency,
            portfolio_metrics=portfolio_metrics,
            by_region=by_region,
            by_property=converted,
            intercompany_eliminations=eliminations,
            fx_adjustments=self._calculate_fx_impact(financials, converted),
            generated_at=datetime.utcnow()
        )
    
    async def get_drilldown(
        self,
        tenant_id: str,
        level: str,  # 'portfolio', 'region', 'property', 'unit'
        entity_id: Optional[str] = None
    ) -> Dict:
        """Interactive drill-down from portfolio to unit level."""
        
        if level == 'portfolio':
            return await self._get_portfolio_summary(tenant_id)
        elif level == 'region':
            return await self._get_region_detail(tenant_id, entity_id)
        elif level == 'property':
            return await self._get_property_detail(tenant_id, entity_id)
        elif level == 'unit':
            return await self._get_unit_detail(tenant_id, entity_id)
        
        raise ValueError(f"Invalid drill-down level: {level}")
```

---

### SKILL-117: SLA Monitoring

#### Purpose
Configurable SLA definitions with threshold-based alerting, escalation workflows, and real-time performance dashboards.

#### Technical Architecture
```python
from dataclasses import dataclass
from datetime import datetime
from typing import Dict, List, Optional
from enum import Enum

class AlertSeverity(Enum):
    INFO = 'info'
    WARNING = 'warning'
    CRITICAL = 'critical'

@dataclass
class SLADefinition:
    id: str
    name: str
    metric_name: str
    threshold_warning: float
    threshold_critical: float
    comparison: str  # 'lt', 'gt', 'lte', 'gte'
    window_minutes: int
    escalation_policy_id: str

@dataclass
class SLAViolation:
    id: str
    sla_id: str
    tenant_id: str
    property_id: Optional[str]
    current_value: float
    threshold_value: float
    severity: AlertSeverity
    detected_at: datetime
    resolved_at: Optional[datetime]


class SLAMonitoringService:
    """
    Real-time SLA monitoring with escalation workflows.
    Detects violations within 30 seconds.
    """
    
    DEFAULT_SLAS = [
        SLADefinition(
            id='response_time',
            name='API Response Time',
            metric_name='api_p95_latency',
            threshold_warning=150,
            threshold_critical=200,
            comparison='gt',
            window_minutes=5,
            escalation_policy_id='ops_team'
        ),
        SLADefinition(
            id='uptime',
            name='System Availability',
            metric_name='uptime_percentage',
            threshold_warning=99.5,
            threshold_critical=99.0,
            comparison='lt',
            window_minutes=60,
            escalation_policy_id='engineering'
        ),
        SLADefinition(
            id='maintenance_response',
            name='Maintenance Response Time',
            metric_name='maintenance_response_hours',
            threshold_warning=4,
            threshold_critical=8,
            comparison='gt',
            window_minutes=480,
            escalation_policy_id='maintenance_mgr'
        )
    ]
    
    async def check_sla(
        self,
        tenant_id: str,
        sla: SLADefinition
    ) -> Optional[SLAViolation]:
        """Check single SLA and create violation if breached."""
        
        # Get current metric value
        current_value = await self._get_metric_value(
            tenant_id, 
            sla.metric_name,
            sla.window_minutes
        )
        
        # Check threshold
        is_warning = self._compare(current_value, sla.threshold_warning, sla.comparison)
        is_critical = self._compare(current_value, sla.threshold_critical, sla.comparison)
        
        if is_critical:
            severity = AlertSeverity.CRITICAL
        elif is_warning:
            severity = AlertSeverity.WARNING
        else:
            return None  # No violation
        
        violation = SLAViolation(
            id=str(uuid.uuid4()),
            sla_id=sla.id,
            tenant_id=tenant_id,
            property_id=None,
            current_value=current_value,
            threshold_value=sla.threshold_critical if is_critical else sla.threshold_warning,
            severity=severity,
            detected_at=datetime.utcnow(),
            resolved_at=None
        )
        
        await self.db.save_violation(violation)
        
        # Trigger escalation
        await self._trigger_escalation(violation, sla)
        
        return violation
    
    async def _trigger_escalation(
        self,
        violation: SLAViolation,
        sla: SLADefinition
    ):
        """Trigger escalation workflow based on severity."""
        
        policy = await self.db.get_escalation_policy(sla.escalation_policy_id)
        
        if violation.severity == AlertSeverity.CRITICAL:
            # Immediate notification to all levels
            await asyncio.gather(
                self._notify_slack(policy.slack_channel, violation),
                self._notify_pagerduty(policy.pagerduty_service, violation),
                self._send_email(policy.email_list, violation)
            )
        elif violation.severity == AlertSeverity.WARNING:
            # Standard notification
            await self._notify_slack(policy.slack_channel, violation)
```

---

### SKILL-118: Vendor Scorecard

#### Purpose
Weighted KPI scoring with customizable metrics, automated tier assignments, and integration with procurement workflows.

#### Technical Architecture
```python
from dataclasses import dataclass
from decimal import Decimal
from typing import Dict, List
from datetime import datetime

@dataclass
class VendorKPI:
    name: str
    weight: Decimal  # 0.0 to 1.0
    score: Decimal   # 1 to 5 scale
    threshold_green: float   # >= green is good
    threshold_yellow: float  # >= yellow is warning
    # < yellow is red

@dataclass
class VendorScorecard:
    vendor_id: str
    tenant_id: str
    period: str
    kpis: List[VendorKPI]
    composite_score: Decimal
    tier: str  # 'strategic', 'preferred', 'transactional', 'at_risk'
    calculated_at: datetime


class VendorScorecardService:
    """
    Weighted KPI scoring with automated tier assignment.
    Composite score = Σ(KPI_score × weight)
    """
    
    DEFAULT_KPIS = [
        {'name': 'on_time_delivery', 'weight': Decimal('0.30')},
        {'name': 'quality_score', 'weight': Decimal('0.25')},
        {'name': 'cost_competitiveness', 'weight': Decimal('0.20')},
        {'name': 'responsiveness', 'weight': Decimal('0.15')},
        {'name': 'compliance', 'weight': Decimal('0.10')}
    ]
    
    TIER_THRESHOLDS = {
        'strategic': Decimal('4.5'),
        'preferred': Decimal('3.5'),
        'transactional': Decimal('2.5'),
        'at_risk': Decimal('0')
    }
    
    async def calculate_scorecard(
        self,
        tenant_id: str,
        vendor_id: str,
        period_start: datetime,
        period_end: datetime
    ) -> VendorScorecard:
        """Calculate vendor scorecard with weighted KPIs."""
        
        # Collect KPI data
        kpis = []
        for kpi_config in self.DEFAULT_KPIS:
            raw_value = await self._collect_kpi_data(
                vendor_id, kpi_config['name'], period_start, period_end
            )
            
            # Convert to 1-5 scale
            score = self._normalize_to_scale(raw_value, kpi_config['name'])
            
            # Determine thresholds
            kpi = VendorKPI(
                name=kpi_config['name'],
                weight=kpi_config['weight'],
                score=score,
                threshold_green=4.0,
                threshold_yellow=3.0
            )
            kpis.append(kpi)
        
        # Calculate composite score
        composite = sum(kpi.score * kpi.weight for kpi in kpis)
        
        # Determine tier
        tier = self._determine_tier(composite)
        
        scorecard = VendorScorecard(
            vendor_id=vendor_id,
            tenant_id=tenant_id,
            period=f"{period_start.date()} to {period_end.date()}",
            kpis=kpis,
            composite_score=composite,
            tier=tier,
            calculated_at=datetime.utcnow()
        )
        
        await self.db.save_scorecard(scorecard)
        
        # Trigger tier change workflow if needed
        previous = await self.db.get_previous_scorecard(vendor_id)
        if previous and previous.tier != tier:
            await self._handle_tier_change(vendor_id, previous.tier, tier)
        
        return scorecard
    
    def _determine_tier(self, score: Decimal) -> str:
        """Assign vendor tier based on composite score."""
        
        for tier, threshold in self.TIER_THRESHOLDS.items():
            if score >= threshold:
                return tier
        return 'at_risk'
```

---

### SKILL-119: Inventory Forecasting

#### Purpose
Demand-based prediction using historical consumption, seasonal adjustments, and automated reorder calculations.

#### Technical Architecture
```python
from sklearn.ensemble import GradientBoostingRegressor
from prophet import Prophet
import pandas as pd
import numpy as np
from dataclasses import dataclass
from datetime import datetime
from typing import List, Dict

@dataclass
class InventoryForecast:
    item_id: str
    property_id: str
    forecast_date: datetime
    predicted_demand: int
    confidence_lower: int
    confidence_upper: int
    reorder_point: int
    suggested_order_qty: int
    lead_time_days: int

@dataclass
class ForecastResult:
    property_id: str
    forecasts: List[InventoryForecast]
    items_below_reorder: List[str]
    total_order_value: float
    generated_at: datetime


class InventoryForecastingService:
    """
    ML-powered demand forecasting with Prophet/XGBoost.
    Accounts for seasonality and lead times.
    """
    
    def __init__(self):
        self.db = PostgreSQLClient()
        self.redis = RedisClient()
    
    async def generate_forecast(
        self,
        tenant_id: str,
        property_id: str,
        forecast_days: int = 30
    ) -> ForecastResult:
        """Generate demand forecast for all inventory items."""
        
        items = await self.db.get_inventory_items(property_id)
        forecasts = []
        items_below_reorder = []
        
        for item in items:
            # Get historical consumption
            history = await self._get_consumption_history(item.id, days=365)
            
            if len(history) < 30:
                # Not enough data, use simple average
                forecast = self._simple_forecast(item, history, forecast_days)
            else:
                # Use Prophet for time series forecasting
                forecast = await self._prophet_forecast(item, history, forecast_days)
            
            forecasts.append(forecast)
            
            # Check against current stock
            current_stock = await self._get_current_stock(item.id)
            if current_stock <= forecast.reorder_point:
                items_below_reorder.append(item.id)
        
        # Calculate total order value
        total_value = sum(
            f.suggested_order_qty * await self._get_unit_cost(f.item_id)
            for f in forecasts
            if f.item_id in items_below_reorder
        )
        
        return ForecastResult(
            property_id=property_id,
            forecasts=forecasts,
            items_below_reorder=items_below_reorder,
            total_order_value=total_value,
            generated_at=datetime.utcnow()
        )
    
    async def _prophet_forecast(
        self,
        item,
        history: List[Dict],
        forecast_days: int
    ) -> InventoryForecast:
        """Use Prophet for seasonal demand forecasting."""
        
        # Prepare data
        df = pd.DataFrame(history)
        df.columns = ['ds', 'y']
        
        # Fit Prophet model
        model = Prophet(
            yearly_seasonality=True,
            weekly_seasonality=True,
            daily_seasonality=False
        )
        model.fit(df)
        
        # Make future predictions
        future = model.make_future_dataframe(periods=forecast_days)
        forecast = model.predict(future)
        
        # Get prediction for lead time + safety stock period
        lead_time = item.lead_time_days or 7
        safety_days = 7
        
        predicted_demand = int(forecast.tail(forecast_days)['yhat'].sum())
        confidence_lower = int(forecast.tail(forecast_days)['yhat_lower'].sum())
        confidence_upper = int(forecast.tail(forecast_days)['yhat_upper'].sum())
        
        # Calculate reorder point
        daily_avg = predicted_demand / forecast_days
        reorder_point = int(daily_avg * (lead_time + safety_days))
        
        # Suggested order quantity (Economic Order Quantity simplified)
        suggested_qty = max(predicted_demand, item.min_order_qty or 1)
        
        return InventoryForecast(
            item_id=item.id,
            property_id=item.property_id,
            forecast_date=datetime.utcnow(),
            predicted_demand=predicted_demand,
            confidence_lower=confidence_lower,
            confidence_upper=confidence_upper,
            reorder_point=reorder_point,
            suggested_order_qty=suggested_qty,
            lead_time_days=lead_time
        )
```

---

### SKILL-120: Bulk Operations

#### Purpose
Idempotent batch processing with partial failure handling, progress tracking, and HTTP 207 Multi-Status responses.

#### Technical Architecture
```python
from dataclasses import dataclass
from datetime import datetime
from typing import List, Dict, Any, Optional
from enum import Enum
import asyncio

class OperationStatus(Enum):
    QUEUED = 'queued'
    PROCESSING = 'processing'
    COMPLETED = 'completed'
    PARTIAL_SUCCESS = 'partial_success'
    FAILED = 'failed'

@dataclass
class BulkOperationRequest:
    idempotency_key: str
    tenant_id: str
    operation_type: str  # 'create', 'update', 'delete'
    items: List[Dict[str, Any]]
    options: "BulkOptions"

@dataclass
class BulkOptions:
    chunk_size: int = 100
    max_retries: int = 3
    timeout_seconds: int = 300
    rollback_on_failure: bool = False

@dataclass
class ItemResult:
    item_id: str
    status: int  # HTTP status code
    message: str
    data: Optional[Dict] = None

@dataclass
class BulkOperationResult:
    operation_id: str
    idempotency_key: str
    status: OperationStatus
    total_items: int
    successful_items: int
    failed_items: int
    results: List[ItemResult]
    started_at: datetime
    completed_at: Optional[datetime]


class IdempotentBulkProcessor:
    """
    Idempotent batch processing with partial failure handling.
    Returns HTTP 207 Multi-Status for mixed results.
    """
    
    def __init__(self):
        self.db = PostgreSQLClient()
        self.redis = RedisClient()
        self.queue = BullMQClient()
    
    async def process_bulk_operation(
        self,
        request: BulkOperationRequest
    ) -> BulkOperationResult:
        """Process bulk operation with idempotency guarantee."""
        
        # Check for existing operation (idempotency)
        existing = await self.redis.get(f"bulk:{request.idempotency_key}")
        if existing:
            return BulkOperationResult.from_json(existing)
        
        # Create operation record
        operation_id = str(uuid.uuid4())
        result = BulkOperationResult(
            operation_id=operation_id,
            idempotency_key=request.idempotency_key,
            status=OperationStatus.PROCESSING,
            total_items=len(request.items),
            successful_items=0,
            failed_items=0,
            results=[],
            started_at=datetime.utcnow(),
            completed_at=None
        )
        
        # Process in chunks
        chunks = [
            request.items[i:i + request.options.chunk_size]
            for i in range(0, len(request.items), request.options.chunk_size)
        ]
        
        all_results = []
        for chunk in chunks:
            chunk_results = await self._process_chunk(
                request.tenant_id,
                request.operation_type,
                chunk,
                request.options
            )
            all_results.extend(chunk_results)
            
            # Update progress
            await self._publish_progress(
                operation_id,
                len(all_results),
                result.total_items
            )
        
        # Aggregate results
        successful = sum(1 for r in all_results if r.status < 400)
        failed = sum(1 for r in all_results if r.status >= 400)
        
        result.results = all_results
        result.successful_items = successful
        result.failed_items = failed
        result.completed_at = datetime.utcnow()
        
        if failed == 0:
            result.status = OperationStatus.COMPLETED
        elif successful == 0:
            result.status = OperationStatus.FAILED
        else:
            result.status = OperationStatus.PARTIAL_SUCCESS
        
        # Cache result for idempotency (24 hours)
        await self.redis.setex(
            f"bulk:{request.idempotency_key}",
            86400,
            result.to_json()
        )
        
        return result
    
    async def _process_chunk(
        self,
        tenant_id: str,
        operation_type: str,
        items: List[Dict],
        options: BulkOptions
    ) -> List[ItemResult]:
        """Process a chunk of items with parallel execution."""
        
        results = await asyncio.gather(
            *[
                self._process_item(tenant_id, operation_type, item, options)
                for item in items
            ],
            return_exceptions=True
        )
        
        item_results = []
        for i, result in enumerate(results):
            if isinstance(result, Exception):
                item_results.append(ItemResult(
                    item_id=items[i].get('id', f'item_{i}'),
                    status=500,
                    message=str(result),
                    data=None
                ))
            else:
                item_results.append(result)
        
        return item_results
    
    def generate_207_response(self, result: BulkOperationResult) -> Dict:
        """Generate HTTP 207 Multi-Status response."""
        
        return {
            'status': 207,
            'operation_id': result.operation_id,
            'results': [
                {
                    'item_id': r.item_id,
                    'status': r.status,
                    'message': r.message,
                    'data': r.data
                }
                for r in result.results
            ],
            'summary': {
                'total': result.total_items,
                'successful': result.successful_items,
                'failed': result.failed_items,
                'processing_time_ms': int(
                    (result.completed_at - result.started_at).total_seconds() * 1000
                )
            }
        }
```

---

## 🗄️ DATABASE SCHEMA

### PostgreSQL Tables with RLS

```sql
-- Tenants table
CREATE TABLE tenants (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    subdomain VARCHAR(63) UNIQUE NOT NULL,
    custom_domain VARCHAR(255),
    tier VARCHAR(20) NOT NULL DEFAULT 'basic',
    brand_config JSONB NOT NULL DEFAULT '{}',
    resource_limits JSONB NOT NULL,
    status VARCHAR(20) NOT NULL DEFAULT 'provisioning',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Properties with RLS
CREATE TABLE properties (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL REFERENCES tenants(id),
    region_id UUID NOT NULL,
    name VARCHAR(255) NOT NULL,
    address JSONB NOT NULL,
    room_count INTEGER,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

ALTER TABLE properties ENABLE ROW LEVEL SECURITY;

CREATE POLICY tenant_isolation_properties ON properties
FOR ALL USING (tenant_id = current_setting('app.current_tenant')::uuid);

-- User roles with hierarchy
CREATE TABLE user_roles (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL,
    tenant_id UUID NOT NULL REFERENCES tenants(id),
    role_name VARCHAR(50) NOT NULL,
    scope_level VARCHAR(20) NOT NULL, -- 'global', 'tenant', 'region', 'property', 'unit'
    scope_ids UUID[] NOT NULL DEFAULT '{}',
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Schedules with RLS
CREATE TABLE schedules (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL REFERENCES tenants(id),
    property_id UUID NOT NULL REFERENCES properties(id),
    period_start DATE NOT NULL,
    period_end DATE NOT NULL,
    status VARCHAR(20) NOT NULL DEFAULT 'draft',
    optimization_score DECIMAL(5,2),
    created_at TIMESTAMPTZ DEFAULT NOW()
);

ALTER TABLE schedules ENABLE ROW LEVEL SECURITY;

CREATE POLICY tenant_isolation_schedules ON schedules
FOR ALL USING (tenant_id = current_setting('app.current_tenant')::uuid);

-- Employee assignments
CREATE TABLE schedule_assignments (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    schedule_id UUID NOT NULL REFERENCES schedules(id),
    employee_id UUID NOT NULL,
    shift_date DATE NOT NULL,
    start_time TIME NOT NULL,
    end_time TIME NOT NULL,
    property_id UUID NOT NULL REFERENCES properties(id)
);

-- Vendor scorecards
CREATE TABLE vendor_scorecards (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL REFERENCES tenants(id),
    vendor_id UUID NOT NULL,
    period_start DATE NOT NULL,
    period_end DATE NOT NULL,
    kpis JSONB NOT NULL,
    composite_score DECIMAL(3,2),
    tier VARCHAR(20) NOT NULL,
    calculated_at TIMESTAMPTZ DEFAULT NOW()
);

ALTER TABLE vendor_scorecards ENABLE ROW LEVEL SECURITY;

CREATE POLICY tenant_isolation_scorecards ON vendor_scorecards
FOR ALL USING (tenant_id = current_setting('app.current_tenant')::uuid);

-- Bulk operation logs
CREATE TABLE bulk_operations (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    idempotency_key VARCHAR(64) UNIQUE NOT NULL,
    tenant_id UUID NOT NULL REFERENCES tenants(id),
    operation_type VARCHAR(20) NOT NULL,
    status VARCHAR(20) NOT NULL,
    total_items INTEGER NOT NULL,
    successful_items INTEGER DEFAULT 0,
    failed_items INTEGER DEFAULT 0,
    results JSONB,
    started_at TIMESTAMPTZ DEFAULT NOW(),
    completed_at TIMESTAMPTZ
);

-- Indexes
CREATE INDEX idx_properties_tenant_region ON properties(tenant_id, region_id);
CREATE INDEX idx_schedules_tenant_period ON schedules(tenant_id, period_start, period_end);
CREATE INDEX idx_user_roles_user_tenant ON user_roles(user_id, tenant_id);
CREATE INDEX idx_bulk_ops_idempotency ON bulk_operations(idempotency_key);
```

---

## 📊 PERFORMANCE REQUIREMENTS

| Skill | Response Time | Throughput | Availability |
|-------|--------------|------------|--------------|
| SKILL-057 (Multi-Brand) | <60s provision | 100 tenants/day | 99.9% |
| SKILL-058 (Access Control) | <50ms check | 50K checks/sec | 99.99% |
| SKILL-089 (Scheduling) | <5s optimization | 100 schedules/min | 99.9% |
| SKILL-116 (Reporting) | <200ms dashboard | 1K reports/min | 99.9% |
| SKILL-117 (SLA Monitor) | <30s detection | Real-time | 99.99% |
| SKILL-118 (Vendor Score) | <10s calculation | 1K scorecards/hr | 99.5% |
| SKILL-119 (Forecasting) | <30s forecast | 100 forecasts/min | 99.5% |
| SKILL-120 (Bulk Ops) | <30s/10K items | 10K ops/batch | 99.9% |

---

## 🔐 SECURITY CONSIDERATIONS

### Data Isolation
- Row-Level Security (RLS) on all tenant tables
- Tenant context validation on every request
- Encrypted data at rest (AES-256)

### Access Control
- Hierarchical RBAC with Casbin
- SSO/MFA via Auth0
- Zero-trust architecture

### Compliance
- SOC 2 Type II certification
- GDPR data residency
- Comprehensive audit trails

---

## 📁 FILE LOCATIONS

```
specs/operations/
└── SPEC-SKILL-057-120-ENTERPRISE-OPERATIONS.md (this file)

knowledge/operations/
└── KD-PHASE2-G5-enterprise-operations.md (research source)

skills/operations/
├── SKILL-057-multi-brand-management.md
├── SKILL-058-regional-access-control.md
├── SKILL-089-staff-shift-planning.md
├── SKILL-116-portfolio-rollup-reporting.md
├── SKILL-117-sla-monitoring.md
├── SKILL-118-vendor-scorecard.md
├── SKILL-119-inventory-forecasting.md
└── SKILL-120-bulk-operations.md
```

---

## 🚀 IMPLEMENTATION ROADMAP

| Week | Milestone |
|------|-----------|
| 1-2 | SKILL-057 (Multi-Brand) + SKILL-058 (Access Control) |
| 3-4 | SKILL-089 (Scheduling) + OR-Tools integration |
| 5-6 | SKILL-116 (Reporting) + SKILL-117 (SLA) |
| 7-8 | SKILL-118 (Vendor) + SKILL-119 (Forecasting) + SKILL-120 (Bulk) |

---

**Status**: ✅ SPECIFIED - Ready for Engineering Implementation

