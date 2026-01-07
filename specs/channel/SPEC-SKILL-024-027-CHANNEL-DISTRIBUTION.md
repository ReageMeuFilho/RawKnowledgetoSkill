# Channel Distribution & OTA Management Platform
## Engineering Specification

**Skills**: SKILL-024, SKILL-025, SKILL-026, SKILL-027
**Category**: Channel Distribution
**Priority**: P0 (Phase 1 MVP)
**Version**: 1.0
**Date**: January 7, 2026
**Stage**: 4 - Final Specification

---

## Executive Summary

This specification defines the engineering requirements for the **Channel Distribution & OTA Management** platform, enabling seamless connectivity and synchronization across major Online Travel Agencies (OTAs) including Airbnb, Vrbo, and Booking.com. The system addresses multi-channel distribution complexity while maintaining data consistency, rate parity compliance, and operational efficiency.

### Skills Covered

| Skill ID | Skill Name | Primary Function |
|----------|------------|------------------|
| SKILL-024 | Channel Connection | OAuth 2.0/API key management, OTA onboarding |
| SKILL-025 | Listing Content Sync | Cross-platform content mapping, photo optimization |
| SKILL-026 | Rate Distribution | Dynamic pricing push, markup application |
| SKILL-027 | Sync Status Monitoring | Real-time health tracking, error categorization |

### Success Criteria

| Objective | Measurement | Target |
|-----------|-------------|--------|
| API Performance | Throughput capacity | 15+ API calls/second |
| Sync Reliability | Success rate | >99.5% |
| Content Accuracy | Validation pass rate | >99% |
| System Availability | Uptime percentage | >99.9% |
| Sync Latency | Content/Rate propagation | <5 minutes |

---

## Architecture Alignment Notes

### Layer Mapping

| Spec Component | Citadel Layer | Technology | Notes |
|----------------|---------------|------------|-------|
| API Gateway | Layer 2 | Rust/Axum | External API exposure |
| Channel Services | Layer 4 | Python (FastAPI) | Internal microservices |
| Event Streaming | Layer 2 | Redpanda | Sync event propagation |
| Workflow Orchestration | Layer 3B | Temporal | OTA sync workflows |
| Content Storage | Layer 2 | MongoDB | Document storage (non-financial) |
| Rate Caching | Layer 2 | Redis | High-frequency lookups |
| Photo Storage | Layer 2 | AWS S3 + CloudFront | CDN delivery |
| Container Orchestration | Layer 2 | AWS ECS/Fargate | Service deployment |

### Execution Path Classification

- **Hot Path Components**: AI-powered content optimization, smart photo selection, intelligent error triage
- **Cold Path Components**: Rate calculations with financial implications, audit logging, reconciliation
- **Hybrid Components**: OTA sync orchestration (AI retry logic + guaranteed delivery)

### MCP Server Requirements

```yaml
mcp_servers:
  - mcp://channel/connect          # OAuth flow initiation
  - mcp://channel/sync-content     # Content sync trigger
  - mcp://channel/push-rates       # Rate distribution
  - mcp://channel/status           # Health monitoring
  - mcp://temporal/trigger_workflow # Workflow orchestration
  - mcp://audit/log                # Immutable audit trail
```

### Compliance with Architecture

- ✅ Uses Temporal for OTA sync workflow orchestration
- ✅ Uses Redpanda for event streaming (not Kafka)
- ✅ Uses ECS/Fargate for container deployment (not Kubernetes)
- ✅ Uses MongoDB for document storage (content, not financial)
- ✅ Uses Redis for caching
- ✅ API Gateway via Rust/Axum for external endpoints
- ✅ Internal services via FastAPI (Python)
- ⚠️ Rate calculations with financial impact route to Treasury OS

---

## 1. System Architecture

### 1.1 High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                          CITADEL OS - LAYER 6                            │
│                        Channel Management Dashboard                       │
│                     (React 18+ / TypeScript / MUI)                       │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                         API GATEWAY (Rust/Axum)                          │
│                   Rate Limiting │ Authentication │ Routing               │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
        ┌───────────────────────────┼───────────────────────────┐
        ▼                           ▼                           ▼
┌───────────────┐         ┌───────────────┐         ┌───────────────┐
│   Channel     │         │   Content     │         │     Rate      │
│  Connection   │         │    Sync       │         │ Distribution  │
│   Service     │         │   Service     │         │   Service     │
│  (SKILL-024)  │         │  (SKILL-025)  │         │  (SKILL-026)  │
└───────────────┘         └───────────────┘         └───────────────┘
        │                         │                         │
        └─────────────────────────┼─────────────────────────┘
                                  │
                                  ▼
                    ┌───────────────────────┐
                    │   Monitoring Service  │
                    │      (SKILL-027)      │
                    └───────────────────────┘
                                  │
        ┌─────────────────────────┼─────────────────────────┐
        ▼                         ▼                         ▼
┌───────────────┐       ┌─────────────────┐       ┌───────────────┐
│   Redpanda    │       │    Temporal     │       │    Redis      │
│    Events     │       │   Workflows     │       │    Cache      │
└───────────────┘       └─────────────────┘       └───────────────┘
                                  │
        ┌─────────────────────────┼─────────────────────────┐
        ▼                         ▼                         ▼
┌───────────────┐       ┌─────────────────┐       ┌───────────────┐
│   Airbnb      │       │     Vrbo        │       │  Booking.com  │
│   Partner     │       │    Expedia      │       │   Connectivity│
│     API       │       │     API         │       │      API      │
└───────────────┘       └─────────────────┘       └───────────────┘
```

### 1.2 Service Decomposition

| Service | Primary Responsibility | Data Ownership | Scaling Strategy |
|---------|----------------------|----------------|------------------|
| Channel Connection | OAuth 2.0/API authentication | Credentials, tokens | Horizontal (2-10 instances) |
| Content Sync | Content mapping, photo optimization | Property content, media | Horizontal (3-15 instances) |
| Rate Distribution | Pricing push, markup application | Rate data, parity rules | Horizontal (2-12 instances) |
| Monitoring | Health tracking, alerting | Metrics, logs | Horizontal (2-6 instances) |

---

## 2. SKILL-024: Channel Connection

### 2.1 Functional Requirements

#### 2.1.1 OAuth 2.0 Authentication Management

```python
# Channel authentication flow
from dataclasses import dataclass
from enum import Enum
from datetime import datetime, timedelta
from typing import Optional

class ChannelType(Enum):
    AIRBNB = "airbnb"
    VRBO = "vrbo"
    BOOKING_COM = "booking_com"

@dataclass
class OAuthCredentials:
    channel: ChannelType
    access_token: str
    refresh_token: str
    expires_at: datetime
    scopes: list[str]
    
    def is_expired(self) -> bool:
        return datetime.utcnow() >= self.expires_at - timedelta(minutes=5)

@dataclass
class APIKeyCredentials:
    channel: ChannelType
    api_key: str
    api_secret: str
    certificate_path: Optional[str]  # For Booking.com
    created_at: datetime
    rotated_at: Optional[datetime]
```

#### 2.1.2 Self-Service OTA Onboarding

```python
# Onboarding workflow using Temporal
from temporalio import workflow, activity
from temporalio.common import RetryPolicy

@activity.defn
async def initiate_oauth_flow(channel: ChannelType, redirect_uri: str) -> str:
    """Generate OAuth authorization URL"""
    oauth_configs = {
        ChannelType.AIRBNB: {
            "auth_url": "https://www.airbnb.com/oauth2/auth",
            "scope": "listings:read listings:write reservations:read"
        }
    }
    config = oauth_configs[channel]
    return f"{config['auth_url']}?client_id={CLIENT_ID}&redirect_uri={redirect_uri}&scope={config['scope']}"

@activity.defn
async def exchange_auth_code(channel: ChannelType, auth_code: str) -> OAuthCredentials:
    """Exchange authorization code for tokens"""
    # Implementation varies by OTA
    pass

@activity.defn
async def import_ota_properties(channel: ChannelType, credentials: OAuthCredentials) -> list[dict]:
    """Import existing properties from OTA"""
    pass

@activity.defn
async def map_properties(ota_properties: list[dict], pms_properties: list[dict]) -> list[dict]:
    """Auto-match OTA listings to PMS properties"""
    pass

@workflow.defn
class ChannelOnboardingWorkflow:
    """Temporal workflow for OTA onboarding"""
    
    @workflow.run
    async def run(self, channel: ChannelType, auth_code: str, pms_properties: list[dict]):
        # Step 1: Exchange auth code
        credentials = await workflow.execute_activity(
            exchange_auth_code,
            args=[channel, auth_code],
            start_to_close_timeout=timedelta(seconds=30),
            retry_policy=RetryPolicy(maximum_attempts=3)
        )
        
        # Step 2: Import OTA properties
        ota_properties = await workflow.execute_activity(
            import_ota_properties,
            args=[channel, credentials],
            start_to_close_timeout=timedelta(minutes=5)
        )
        
        # Step 3: Auto-map properties
        mappings = await workflow.execute_activity(
            map_properties,
            args=[ota_properties, pms_properties],
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        return {
            "credentials": credentials,
            "properties_imported": len(ota_properties),
            "mappings": mappings
        }
```

#### 2.1.3 Connection Health Monitoring

```python
@dataclass
class ConnectionHealth:
    channel: ChannelType
    status: str  # "healthy", "degraded", "error"
    last_check: datetime
    token_valid: bool
    api_response_time_ms: int
    success_rate_24h: float
    rate_limit_remaining: int
    rate_limit_total: int

async def check_connection_health(channel: ChannelType) -> ConnectionHealth:
    """Periodic health check for OTA connection"""
    start_time = datetime.utcnow()
    
    # Test API connectivity
    try:
        response = await ota_client.ping(channel)
        response_time = (datetime.utcnow() - start_time).total_seconds() * 1000
        
        return ConnectionHealth(
            channel=channel,
            status="healthy" if response.ok else "degraded",
            last_check=datetime.utcnow(),
            token_valid=not credentials.is_expired(),
            api_response_time_ms=int(response_time),
            success_rate_24h=await get_success_rate(channel, hours=24),
            rate_limit_remaining=response.headers.get("X-RateLimit-Remaining", 0),
            rate_limit_total=response.headers.get("X-RateLimit-Limit", 0)
        )
    except Exception as e:
        return ConnectionHealth(
            channel=channel,
            status="error",
            last_check=datetime.utcnow(),
            token_valid=False,
            api_response_time_ms=0,
            success_rate_24h=0.0,
            rate_limit_remaining=0,
            rate_limit_total=0
        )
```

### 2.2 API Endpoints

```yaml
# Channel Connection API (via Rust/Axum Gateway)
paths:
  /api/v1/channels:
    get:
      summary: List all connected channels
      responses:
        200:
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/ChannelConnection'

  /api/v1/channels/{channel}/connect:
    post:
      summary: Initiate OAuth connection flow
      parameters:
        - name: channel
          in: path
          required: true
          schema:
            type: string
            enum: [airbnb, vrbo, booking_com]
      responses:
        200:
          content:
            application/json:
              schema:
                type: object
                properties:
                  authorization_url: { type: string }
                  state: { type: string }

  /api/v1/channels/{channel}/callback:
    get:
      summary: OAuth callback handler
      parameters:
        - name: code
          in: query
          required: true
        - name: state
          in: query
          required: true
      responses:
        302:
          description: Redirect to property mapping wizard

  /api/v1/channels/{channel}/health:
    get:
      summary: Get channel connection health
      responses:
        200:
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ConnectionHealth'

  /api/v1/channels/{channel}/refresh:
    post:
      summary: Force token refresh
      responses:
        200:
          description: Token refreshed successfully
```

---

## 3. SKILL-025: Listing Content Sync

### 3.1 Content Processing Pipeline

```python
from dataclasses import dataclass
from typing import Optional
from enum import Enum

class ContentStatus(Enum):
    PENDING = "pending"
    VALIDATING = "validating"
    TRANSFORMING = "transforming"
    SYNCING = "syncing"
    SYNCED = "synced"
    FAILED = "failed"

@dataclass
class PropertyContent:
    property_id: str
    title: dict[str, str]  # Localized titles
    description: dict[str, str]  # Localized descriptions
    photos: list['PropertyPhoto']
    amenities: list[str]  # Unified amenity codes
    house_rules: dict
    location: dict
    bedrooms: int
    bathrooms: float
    max_guests: int
    
@dataclass
class PropertyPhoto:
    photo_id: str
    original_url: str
    optimized_urls: dict[str, str]  # channel -> url
    caption: Optional[str]
    sort_order: int
    dimensions: tuple[int, int]
    file_size_mb: float
```

### 3.2 Photo Optimization Engine

```python
from PIL import Image
import io
from dataclasses import dataclass

@dataclass
class OTAPhotoRequirements:
    min_width: int
    min_height: int
    max_file_size_mb: float
    aspect_ratio: tuple[int, int]
    supported_formats: list[str]

OTA_PHOTO_SPECS = {
    "airbnb": OTAPhotoRequirements(
        min_width=1024, min_height=683, max_file_size_mb=4.0,
        aspect_ratio=(3, 2), supported_formats=["jpeg", "png"]
    ),
    "vrbo": OTAPhotoRequirements(
        min_width=1024, min_height=683, max_file_size_mb=20.0,
        aspect_ratio=(3, 2), supported_formats=["jpeg", "png", "webp"]
    ),
    "booking_com": OTAPhotoRequirements(
        min_width=2048, min_height=1080, max_file_size_mb=10.0,
        aspect_ratio=(16, 9), supported_formats=["jpeg", "png"]
    )
}

async def optimize_photo_for_ota(
    original_image: bytes,
    channel: str,
    quality: int = 85
) -> tuple[bytes, dict]:
    """Optimize photo for specific OTA requirements"""
    spec = OTA_PHOTO_SPECS[channel]
    
    img = Image.open(io.BytesIO(original_image))
    
    # Calculate target dimensions maintaining aspect ratio
    target_ratio = spec.aspect_ratio[0] / spec.aspect_ratio[1]
    current_ratio = img.width / img.height
    
    if current_ratio > target_ratio:
        new_width = int(img.height * target_ratio)
        left = (img.width - new_width) // 2
        img = img.crop((left, 0, left + new_width, img.height))
    else:
        new_height = int(img.width / target_ratio)
        top = (img.height - new_height) // 2
        img = img.crop((0, top, img.width, top + new_height))
    
    # Resize to meet minimum requirements
    if img.width < spec.min_width or img.height < spec.min_height:
        scale = max(spec.min_width / img.width, spec.min_height / img.height)
        img = img.resize((int(img.width * scale), int(img.height * scale)), Image.LANCZOS)
    
    # Compress and save
    output = io.BytesIO()
    img.save(output, format="JPEG", quality=quality, optimize=True)
    
    # Check file size and reduce quality if needed
    while output.tell() / (1024 * 1024) > spec.max_file_size_mb and quality > 50:
        quality -= 5
        output = io.BytesIO()
        img.save(output, format="JPEG", quality=quality, optimize=True)
    
    return output.getvalue(), {
        "width": img.width,
        "height": img.height,
        "file_size_mb": output.tell() / (1024 * 1024),
        "quality": quality
    }
```

### 3.3 Amenity Taxonomy Mapping

```python
# Unified amenity mapping across OTAs
AMENITY_MAPPING = {
    "wifi": {
        "airbnb": 4,
        "vrbo": "WIFI",
        "booking_com": 107
    },
    "pool": {
        "airbnb": 7,
        "vrbo": "POOL",
        "booking_com": 123
    },
    "air_conditioning": {
        "airbnb": 5,
        "vrbo": "AC",
        "booking_com": 11
    },
    "kitchen": {
        "airbnb": 8,
        "vrbo": "KITCHEN",
        "booking_com": 45
    },
    "parking": {
        "airbnb": 9,
        "vrbo": "PARKING",
        "booking_com": 6
    },
    "washer": {
        "airbnb": 33,
        "vrbo": "WASHER",
        "booking_com": 20
    },
    "dryer": {
        "airbnb": 34,
        "vrbo": "DRYER",
        "booking_com": 21
    },
    "pets_allowed": {
        "airbnb": 12,
        "vrbo": "PETS",
        "booking_com": 4
    },
    "hot_tub": {
        "airbnb": 25,
        "vrbo": "HOT_TUB",
        "booking_com": 78
    },
    "bbq_grill": {
        "airbnb": 38,
        "vrbo": "GRILL",
        "booking_com": 132
    }
}

def translate_amenities(unified_codes: list[str], target_channel: str) -> list:
    """Translate unified amenity codes to OTA-specific codes"""
    result = []
    for code in unified_codes:
        if code in AMENITY_MAPPING and target_channel in AMENITY_MAPPING[code]:
            result.append(AMENITY_MAPPING[code][target_channel])
    return result
```

### 3.4 Content Sync Temporal Workflow

```python
@workflow.defn
class ContentSyncWorkflow:
    """Orchestrate content sync across all OTAs"""
    
    @workflow.run
    async def run(self, property_id: str, content: dict, channels: list[str]):
        results = {}
        
        # Validate content first
        validation = await workflow.execute_activity(
            validate_content,
            args=[content],
            start_to_close_timeout=timedelta(seconds=30)
        )
        
        if not validation["valid"]:
            return {"status": "failed", "errors": validation["errors"]}
        
        # Process photos
        optimized_photos = await workflow.execute_activity(
            optimize_all_photos,
            args=[content["photos"], channels],
            start_to_close_timeout=timedelta(minutes=10)
        )
        
        # Sync to each channel in parallel
        sync_tasks = []
        for channel in channels:
            task = workflow.execute_activity(
                sync_content_to_ota,
                args=[property_id, content, optimized_photos, channel],
                start_to_close_timeout=timedelta(minutes=5),
                retry_policy=RetryPolicy(
                    maximum_attempts=3,
                    initial_interval=timedelta(seconds=5),
                    backoff_coefficient=2.0
                )
            )
            sync_tasks.append((channel, task))
        
        # Wait for all syncs
        for channel, task in sync_tasks:
            try:
                result = await task
                results[channel] = {"status": "success", "result": result}
            except Exception as e:
                results[channel] = {"status": "failed", "error": str(e)}
        
        # Emit sync event to Redpanda
        await workflow.execute_activity(
            emit_sync_event,
            args=[property_id, "content_sync", results],
            start_to_close_timeout=timedelta(seconds=10)
        )
        
        return results
```

---

## 4. SKILL-026: Rate Distribution

### 4.1 Dynamic Rate Push Architecture

```python
@dataclass
class RateUpdate:
    property_id: str
    date_range: tuple[date, date]
    base_rate: Decimal
    currency: str
    channel_rates: dict[str, 'ChannelRate']
    restrictions: 'StayRestrictions'

@dataclass
class ChannelRate:
    rate: Decimal
    markup_percentage: Decimal
    commission_rate: Decimal
    push_status: str
    last_pushed: Optional[datetime]

@dataclass
class StayRestrictions:
    minimum_stay: int
    maximum_stay: int
    advance_booking_days: int
    check_in_allowed: list[int]  # Days of week (0-6)
    check_out_allowed: list[int]
```

### 4.2 Channel-Specific Markup Engine

```python
from decimal import Decimal, ROUND_HALF_UP

# Default commission rates by channel
CHANNEL_COMMISSIONS = {
    "airbnb": Decimal("0.15"),      # 15% commission
    "vrbo": Decimal("0.08"),        # 8% commission
    "booking_com": Decimal("0.15"), # 15% commission
    "direct": Decimal("0.00")       # 0% for direct bookings
}

# Default markup buffers to maintain net revenue
DEFAULT_MARKUPS = {
    "airbnb": Decimal("0.05"),      # 5% additional markup
    "vrbo": Decimal("0.03"),        # 3% additional markup
    "booking_com": Decimal("0.02"), # 2% additional markup
    "direct": Decimal("-0.05")      # 5% discount for direct
}

def calculate_channel_rate(
    base_rate: Decimal,
    channel: str,
    custom_markup: Optional[Decimal] = None
) -> dict:
    """Calculate final rate for a specific channel"""
    commission = CHANNEL_COMMISSIONS.get(channel, Decimal("0.15"))
    markup = custom_markup if custom_markup is not None else DEFAULT_MARKUPS.get(channel, Decimal("0.00"))
    
    # Total multiplier = 1 + commission + additional markup
    multiplier = Decimal("1") + commission + markup
    
    final_rate = (base_rate * multiplier).quantize(Decimal("0.01"), rounding=ROUND_HALF_UP)
    
    # Calculate expected net revenue
    net_revenue = (final_rate * (Decimal("1") - commission)).quantize(Decimal("0.01"), rounding=ROUND_HALF_UP)
    
    return {
        "channel": channel,
        "base_rate": float(base_rate),
        "commission_rate": float(commission),
        "markup_rate": float(markup),
        "final_rate": float(final_rate),
        "expected_net_revenue": float(net_revenue),
        "margin_percentage": float((net_revenue - base_rate) / base_rate * 100) if base_rate > 0 else 0
    }
```

### 4.3 Rate Parity Management

```python
@dataclass
class ParityRule:
    rule_id: str
    property_id: str
    rule_type: str  # "strict", "flexible", "channel_specific"
    max_variance_percent: Decimal
    channels: list[str]
    exceptions: list[dict]

async def check_rate_parity(
    property_id: str,
    proposed_rates: dict[str, Decimal],
    parity_rules: list[ParityRule]
) -> dict:
    """Validate rate parity across channels"""
    violations = []
    
    for rule in parity_rules:
        if property_id != rule.property_id:
            continue
            
        if rule.rule_type == "strict":
            # All channels must have same rate
            rates = [proposed_rates[ch] for ch in rule.channels if ch in proposed_rates]
            if len(set(rates)) > 1:
                violations.append({
                    "rule_id": rule.rule_id,
                    "type": "strict_parity_violation",
                    "channels": rule.channels,
                    "rates": {ch: float(proposed_rates[ch]) for ch in rule.channels if ch in proposed_rates}
                })
        
        elif rule.rule_type == "flexible":
            # Rates can vary within tolerance
            rates = [proposed_rates[ch] for ch in rule.channels if ch in proposed_rates]
            if rates:
                min_rate = min(rates)
                max_rate = max(rates)
                variance = ((max_rate - min_rate) / min_rate * 100) if min_rate > 0 else Decimal("0")
                
                if variance > rule.max_variance_percent:
                    violations.append({
                        "rule_id": rule.rule_id,
                        "type": "variance_exceeded",
                        "max_allowed": float(rule.max_variance_percent),
                        "actual_variance": float(variance)
                    })
    
    return {
        "compliant": len(violations) == 0,
        "violations": violations
    }
```

### 4.4 Bulk Rate Distribution Workflow

```python
@workflow.defn
class RateDistributionWorkflow:
    """Temporal workflow for distributing rates to OTAs"""
    
    @workflow.run
    async def run(self, rate_updates: list[dict], channels: list[str]):
        # Step 1: Validate all rates
        validation = await workflow.execute_activity(
            validate_rate_updates,
            args=[rate_updates],
            start_to_close_timeout=timedelta(seconds=30)
        )
        
        if not validation["valid"]:
            return {"status": "failed", "errors": validation["errors"]}
        
        # Step 2: Check rate parity
        parity_check = await workflow.execute_activity(
            check_all_rate_parity,
            args=[rate_updates, channels],
            start_to_close_timeout=timedelta(seconds=30)
        )
        
        if not parity_check["compliant"]:
            # Signal for manual approval if parity violated
            await workflow.wait_condition(
                lambda: self.parity_approved,
                timeout=timedelta(hours=24)
            )
        
        # Step 3: Apply channel markups
        channel_rates = await workflow.execute_activity(
            apply_channel_markups,
            args=[rate_updates, channels],
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        # Step 4: Batch push to OTAs with rate limiting
        results = {}
        for channel in channels:
            result = await workflow.execute_activity(
                push_rates_to_ota,
                args=[channel_rates, channel],
                start_to_close_timeout=timedelta(minutes=10),
                retry_policy=RetryPolicy(
                    maximum_attempts=5,
                    initial_interval=timedelta(seconds=2),
                    backoff_coefficient=2.0,
                    maximum_interval=timedelta(minutes=1)
                )
            )
            results[channel] = result
        
        return results
    
    parity_approved: bool = False
    
    @workflow.signal
    def approve_parity_override(self):
        self.parity_approved = True
```

---

## 5. SKILL-027: Sync Status Monitoring

### 5.1 Real-Time Dashboard Architecture

```python
@dataclass
class SyncMetrics:
    channel: str
    total_syncs_24h: int
    successful_syncs: int
    failed_syncs: int
    success_rate: float
    avg_latency_ms: int
    p99_latency_ms: int
    rate_limit_hits: int
    last_sync: datetime

@dataclass 
class SystemHealth:
    overall_status: str  # "healthy", "degraded", "critical"
    channels: dict[str, 'ChannelHealth']
    active_alerts: list['Alert']
    throughput_current: float  # requests/second
    throughput_limit: float
    queue_depth: int

@dataclass
class ChannelHealth:
    channel: str
    status: str
    connection_status: str
    sync_status: str
    last_successful_sync: datetime
    error_count_24h: int
    degradation_reason: Optional[str]
```

### 5.2 Error Categorization System

```python
from enum import Enum

class ErrorCategory(Enum):
    AUTHENTICATION = "authentication"    # 401, 403
    RATE_LIMIT = "rate_limit"           # 429
    VALIDATION = "validation"           # 400
    NETWORK = "network"                 # Timeout, connection errors
    SERVER = "server"                   # 5xx
    BUSINESS_LOGIC = "business_logic"   # Parity violation, mapping errors

class ErrorSeverity(Enum):
    INFO = "info"
    WARNING = "warning"
    ERROR = "error"
    CRITICAL = "critical"

@dataclass
class SyncError:
    error_id: str
    channel: str
    category: ErrorCategory
    severity: ErrorSeverity
    message: str
    http_status: Optional[int]
    timestamp: datetime
    property_id: Optional[str]
    operation: str  # "content_sync", "rate_push", "availability_update"
    retry_count: int
    max_retries: int
    resolved: bool
    resolution_time: Optional[datetime]

ERROR_RECOVERY_STRATEGIES = {
    ErrorCategory.AUTHENTICATION: {
        "action": "refresh_token",
        "auto_recover": True,
        "max_attempts": 2,
        "escalate_after": timedelta(minutes=15)
    },
    ErrorCategory.RATE_LIMIT: {
        "action": "exponential_backoff",
        "auto_recover": True,
        "initial_delay": timedelta(seconds=2),
        "max_delay": timedelta(minutes=5)
    },
    ErrorCategory.VALIDATION: {
        "action": "flag_for_review",
        "auto_recover": False,
        "escalate_immediately": True
    },
    ErrorCategory.NETWORK: {
        "action": "retry_with_backoff",
        "auto_recover": True,
        "max_attempts": 3
    },
    ErrorCategory.SERVER: {
        "action": "circuit_breaker",
        "auto_recover": True,
        "threshold": 5,  # failures before opening
        "timeout": timedelta(seconds=30)
    }
}
```

### 5.3 Automated Alert System

```python
@dataclass
class AlertRule:
    rule_id: str
    name: str
    condition: str  # Expression to evaluate
    severity: ErrorSeverity
    channels: list[str]  # Notification channels: email, slack, sms
    escalation_time: timedelta
    auto_resolve: bool

DEFAULT_ALERT_RULES = [
    AlertRule(
        rule_id="auth_failure",
        name="Authentication Failure",
        condition="error_category == 'authentication' AND retry_count >= 2",
        severity=ErrorSeverity.ERROR,
        channels=["email", "slack"],
        escalation_time=timedelta(minutes=15),
        auto_resolve=True
    ),
    AlertRule(
        rule_id="sync_failure_rate",
        name="High Sync Failure Rate",
        condition="success_rate < 0.95 AND total_syncs > 10",
        severity=ErrorSeverity.WARNING,
        channels=["slack"],
        escalation_time=timedelta(minutes=30),
        auto_resolve=True
    ),
    AlertRule(
        rule_id="channel_down",
        name="Channel Connection Down",
        condition="connection_status == 'error' AND duration > 5m",
        severity=ErrorSeverity.CRITICAL,
        channels=["email", "slack", "sms"],
        escalation_time=timedelta(minutes=5),
        auto_resolve=True
    ),
    AlertRule(
        rule_id="rate_limit_critical",
        name="Critical Rate Limiting",
        condition="rate_limit_remaining < 0.1 * rate_limit_total",
        severity=ErrorSeverity.WARNING,
        channels=["slack"],
        escalation_time=timedelta(minutes=10),
        auto_resolve=True
    )
]
```

### 5.4 Circuit Breaker Implementation

```python
from enum import Enum
from dataclasses import dataclass, field
from datetime import datetime, timedelta
from collections import deque
from typing import Callable, Any
import asyncio

class CircuitState(Enum):
    CLOSED = "closed"      # Normal operation
    OPEN = "open"          # Blocking requests
    HALF_OPEN = "half_open"  # Testing recovery

@dataclass
class CircuitBreaker:
    name: str
    failure_threshold: int = 5
    success_threshold: int = 3
    timeout: timedelta = timedelta(seconds=30)
    
    state: CircuitState = CircuitState.CLOSED
    failures: deque = field(default_factory=lambda: deque(maxlen=100))
    successes_in_half_open: int = 0
    last_failure_time: Optional[datetime] = None
    
    async def call(self, func: Callable, *args, **kwargs) -> Any:
        if self.state == CircuitState.OPEN:
            if datetime.utcnow() - self.last_failure_time > self.timeout:
                self.state = CircuitState.HALF_OPEN
                self.successes_in_half_open = 0
            else:
                raise CircuitBreakerOpenError(f"Circuit {self.name} is open")
        
        try:
            result = await func(*args, **kwargs)
            self._record_success()
            return result
        except Exception as e:
            self._record_failure()
            raise
    
    def _record_success(self):
        if self.state == CircuitState.HALF_OPEN:
            self.successes_in_half_open += 1
            if self.successes_in_half_open >= self.success_threshold:
                self.state = CircuitState.CLOSED
                self.failures.clear()
        elif self.state == CircuitState.CLOSED:
            # Remove old failures outside window
            pass
    
    def _record_failure(self):
        self.failures.append(datetime.utcnow())
        self.last_failure_time = datetime.utcnow()
        
        if self.state == CircuitState.HALF_OPEN:
            self.state = CircuitState.OPEN
        elif self.state == CircuitState.CLOSED:
            recent_failures = sum(
                1 for f in self.failures 
                if datetime.utcnow() - f < timedelta(minutes=1)
            )
            if recent_failures >= self.failure_threshold:
                self.state = CircuitState.OPEN
```

---

## 6. Data Storage Design

### 6.1 MongoDB Schemas

```javascript
// Property Content Collection
{
  "_id": ObjectId,
  "property_id": "uuid",
  "content": {
    "title": {
      "en": "Ocean View Villa",
      "es": "Villa con Vista al Mar",
      "pt": "Villa com Vista para o Mar"
    },
    "description": {
      "en": "Stunning oceanfront property...",
      "character_count": 485
    },
    "photos": [
      {
        "photo_id": "uuid",
        "original_url": "https://cdn.citadel.io/original/photo1.jpg",
        "optimized_urls": {
          "airbnb": "https://cdn.citadel.io/airbnb/photo1_1920x1280.jpg",
          "vrbo": "https://cdn.citadel.io/vrbo/photo1_2048x1365.jpg",
          "booking_com": "https://cdn.citadel.io/booking/photo1_2048x1080.jpg"
        },
        "caption": "Living Room",
        "sort_order": 1
      }
    ],
    "amenities": {
      "unified_codes": ["wifi", "pool", "air_conditioning", "kitchen"],
      "ota_mappings": {
        "airbnb": [4, 7, 5, 8],
        "vrbo": ["WIFI", "POOL", "AC", "KITCHEN"],
        "booking_com": [107, 123, 11, 45]
      }
    },
    "house_rules": {
      "pets_allowed": true,
      "smoking_allowed": false,
      "events_allowed": false,
      "quiet_hours": { "start": "22:00", "end": "08:00" }
    }
  },
  "ota_sync_status": {
    "airbnb": {
      "listing_id": "12345678",
      "last_sync": ISODate("2026-01-07T10:30:00Z"),
      "sync_status": "success",
      "content_hash": "abc123def456"
    },
    "vrbo": {
      "property_id": "987654321",
      "last_sync": ISODate("2026-01-07T10:32:00Z"),
      "sync_status": "success"
    }
  },
  "created_at": ISODate("2026-01-01T00:00:00Z"),
  "updated_at": ISODate("2026-01-07T10:30:00Z")
}

// Channel Credentials Collection (Encrypted)
{
  "_id": ObjectId,
  "channel": "airbnb",
  "credential_type": "oauth2",
  "encrypted_data": {
    "access_token": "encrypted...",
    "refresh_token": "encrypted...",
    "expires_at": ISODate("2026-01-08T10:30:00Z")
  },
  "metadata": {
    "scopes": ["listings:read", "listings:write", "reservations:read"],
    "created_at": ISODate("2026-01-01T00:00:00Z"),
    "last_refreshed": ISODate("2026-01-07T10:30:00Z")
  }
}

// Sync Log Collection (Time-Series)
{
  "_id": ObjectId,
  "timestamp": ISODate("2026-01-07T10:30:00Z"),
  "channel": "airbnb",
  "operation": "content_sync",
  "property_id": "uuid",
  "status": "success",
  "duration_ms": 1250,
  "response_code": 200,
  "error": null,
  "metadata": {
    "photos_synced": 12,
    "amenities_synced": 8
  }
}
```

### 6.2 Redis Caching Strategy

```python
# Cache key patterns
CACHE_KEYS = {
    "rate": "channel:rate:{property_id}:{channel}:{date}",
    "availability": "channel:availability:{property_id}:{channel}",
    "connection_status": "channel:status:{channel}",
    "rate_limit": "channel:ratelimit:{channel}",
    "content_hash": "channel:contenthash:{property_id}:{channel}"
}

# TTL configurations
CACHE_TTLS = {
    "rate": timedelta(hours=1),
    "availability": timedelta(minutes=5),
    "connection_status": timedelta(minutes=1),
    "rate_limit": timedelta(minutes=5),
    "content_hash": timedelta(hours=24)
}

async def cache_channel_rate(
    property_id: str,
    channel: str,
    date: str,
    rate_data: dict
):
    key = CACHE_KEYS["rate"].format(
        property_id=property_id,
        channel=channel,
        date=date
    )
    await redis.setex(
        key,
        int(CACHE_TTLS["rate"].total_seconds()),
        json.dumps(rate_data)
    )
```

---

## 7. API Gateway (Rust/Axum)

### 7.1 Route Configuration

```rust
// src/routes/channel.rs
use axum::{
    routing::{get, post},
    Router,
    Json,
    extract::{Path, State},
};

pub fn channel_routes() -> Router<AppState> {
    Router::new()
        .route("/api/v1/channels", get(list_channels))
        .route("/api/v1/channels/:channel/connect", post(initiate_connection))
        .route("/api/v1/channels/:channel/callback", get(oauth_callback))
        .route("/api/v1/channels/:channel/health", get(get_health))
        .route("/api/v1/channels/:channel/sync", post(trigger_sync))
        .route("/api/v1/channels/:channel/rates", post(push_rates))
        .route("/api/v1/channels/status", get(get_all_status))
}

async fn list_channels(
    State(state): State<AppState>,
) -> Result<Json<Vec<ChannelInfo>>, ApiError> {
    let channels = state.channel_service.list_connected().await?;
    Ok(Json(channels))
}

async fn initiate_connection(
    State(state): State<AppState>,
    Path(channel): Path<String>,
) -> Result<Json<ConnectionInitResponse>, ApiError> {
    let response = state.channel_service
        .initiate_oauth(&channel)
        .await?;
    Ok(Json(response))
}
```

### 7.2 Rate Limiting Middleware

```rust
// src/middleware/rate_limit.rs
use std::collections::HashMap;
use std::sync::Arc;
use tokio::sync::RwLock;

pub struct RateLimiter {
    limits: HashMap<String, RateLimit>,
    state: Arc<RwLock<HashMap<String, TokenBucket>>>,
}

struct RateLimit {
    requests_per_second: u32,
    burst_size: u32,
}

// Per-channel rate limits based on OTA requirements
const OTA_RATE_LIMITS: &[(&str, u32, u32)] = &[
    ("airbnb", 15, 30),      // 15 req/s, burst 30
    ("vrbo", 50, 100),       // 50 req/s, burst 100
    ("booking_com", 30, 60), // 30 req/s, burst 60
];

impl RateLimiter {
    pub async fn check(&self, channel: &str, key: &str) -> Result<(), RateLimitError> {
        let limit = self.limits.get(channel)
            .ok_or(RateLimitError::UnknownChannel)?;
        
        let mut state = self.state.write().await;
        let bucket = state.entry(key.to_string())
            .or_insert(TokenBucket::new(limit.requests_per_second, limit.burst_size));
        
        if bucket.try_acquire() {
            Ok(())
        } else {
            Err(RateLimitError::Exceeded {
                retry_after: bucket.time_until_available(),
            })
        }
    }
}
```

---

## 8. Infrastructure

### 8.1 ECS/Fargate Service Definitions

```yaml
# ecs-task-definition.yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Channel Distribution Services

Resources:
  ChannelConnectionService:
    Type: AWS::ECS::Service
    Properties:
      ServiceName: channel-connection-service
      Cluster: !Ref ECSCluster
      TaskDefinition: !Ref ChannelConnectionTaskDef
      DesiredCount: 2
      LaunchType: FARGATE
      NetworkConfiguration:
        AwsvpcConfiguration:
          Subnets: !Ref PrivateSubnets
          SecurityGroups: [!Ref ServiceSecurityGroup]
      LoadBalancers:
        - ContainerName: channel-connection
          ContainerPort: 8080
          TargetGroupArn: !Ref ChannelConnectionTG

  ChannelConnectionTaskDef:
    Type: AWS::ECS::TaskDefinition
    Properties:
      Family: channel-connection
      Cpu: '512'
      Memory: '1024'
      NetworkMode: awsvpc
      RequiresCompatibilities: [FARGATE]
      ExecutionRoleArn: !Ref ECSExecutionRole
      TaskRoleArn: !Ref ChannelServiceRole
      ContainerDefinitions:
        - Name: channel-connection
          Image: !Sub '${AWS::AccountId}.dkr.ecr.${AWS::Region}.amazonaws.com/channel-connection:latest'
          Essential: true
          PortMappings:
            - ContainerPort: 8080
          Environment:
            - Name: TEMPORAL_HOST
              Value: !Ref TemporalEndpoint
            - Name: REDIS_HOST
              Value: !Ref RedisEndpoint
            - Name: MONGODB_URI
              Value: !Ref MongoDBConnectionString
          Secrets:
            - Name: OAUTH_CLIENT_SECRET
              ValueFrom: !Sub 'arn:aws:secretsmanager:${AWS::Region}:${AWS::AccountId}:secret:channel-oauth-secrets'
          LogConfiguration:
            LogDriver: awslogs
            Options:
              awslogs-group: /ecs/channel-connection
              awslogs-region: !Ref AWS::Region
              awslogs-stream-prefix: ecs
```

### 8.2 Auto-Scaling Configuration

```yaml
# Auto-scaling policies
  ChannelConnectionScaling:
    Type: AWS::ApplicationAutoScaling::ScalableTarget
    Properties:
      MaxCapacity: 10
      MinCapacity: 2
      ResourceId: !Sub 'service/${ECSCluster}/channel-connection-service'
      RoleARN: !GetAtt AutoScalingRole.Arn
      ScalableDimension: ecs:service:DesiredCount
      ServiceNamespace: ecs

  ChannelConnectionCPUScaling:
    Type: AWS::ApplicationAutoScaling::ScalingPolicy
    Properties:
      PolicyName: ChannelConnectionCPUScaling
      PolicyType: TargetTrackingScaling
      ScalingTargetId: !Ref ChannelConnectionScaling
      TargetTrackingScalingPolicyConfiguration:
        PredefinedMetricSpecification:
          PredefinedMetricType: ECSServiceAverageCPUUtilization
        TargetValue: 70.0
        ScaleInCooldown: 300
        ScaleOutCooldown: 60
```

---

## 9. User Interface Components

### 9.1 Dashboard Component Structure

```typescript
// src/components/channel/ChannelDashboard.tsx
import React from 'react';
import { Grid, Card, CardContent, Typography } from '@mui/material';
import { useChannelStatus, useChannelMetrics } from '@/hooks/useChannel';

interface ChannelDashboardProps {
  propertyId?: string;
}

export const ChannelDashboard: React.FC<ChannelDashboardProps> = ({ propertyId }) => {
  const { data: status, isLoading: statusLoading } = useChannelStatus();
  const { data: metrics, isLoading: metricsLoading } = useChannelMetrics();

  return (
    <Grid container spacing={3}>
      {/* Status Overview Cards */}
      <Grid item xs={12} md={3}>
        <StatusCard
          title="Connected Channels"
          value={status?.connectedCount || 0}
          total={status?.totalChannels || 3}
          icon={<LinkIcon />}
        />
      </Grid>
      
      <Grid item xs={12} md={3}>
        <StatusCard
          title="Sync Success Rate"
          value={`${(metrics?.successRate * 100).toFixed(1)}%`}
          status={metrics?.successRate > 0.99 ? 'success' : 'warning'}
          icon={<SyncIcon />}
        />
      </Grid>
      
      <Grid item xs={12} md={3}>
        <StatusCard
          title="Avg Sync Latency"
          value={`${metrics?.avgLatencyMs}ms`}
          status={metrics?.avgLatencyMs < 5000 ? 'success' : 'warning'}
          icon={<SpeedIcon />}
        />
      </Grid>
      
      <Grid item xs={12} md={3}>
        <StatusCard
          title="Active Alerts"
          value={status?.activeAlerts || 0}
          status={status?.activeAlerts === 0 ? 'success' : 'error'}
          icon={<AlertIcon />}
        />
      </Grid>
      
      {/* Channel Status Grid */}
      <Grid item xs={12}>
        <ChannelStatusGrid channels={status?.channels || []} />
      </Grid>
      
      {/* Recent Sync Activity */}
      <Grid item xs={12} md={8}>
        <SyncActivityFeed propertyId={propertyId} />
      </Grid>
      
      {/* Performance Chart */}
      <Grid item xs={12} md={4}>
        <SyncPerformanceChart metrics={metrics} />
      </Grid>
    </Grid>
  );
};
```

### 9.2 Channel Connection Wizard

```typescript
// src/components/channel/ConnectionWizard.tsx
import React, { useState } from 'react';
import { Stepper, Step, StepLabel, Button, Box } from '@mui/material';

const steps = ['Select Channel', 'Authenticate', 'Map Properties', 'Initial Sync'];

export const ConnectionWizard: React.FC<ConnectionWizardProps> = ({ onComplete }) => {
  const [activeStep, setActiveStep] = useState(0);
  const [selectedChannel, setSelectedChannel] = useState<string | null>(null);
  const [authResult, setAuthResult] = useState<AuthResult | null>(null);
  
  const handleChannelSelect = (channel: string) => {
    setSelectedChannel(channel);
    setActiveStep(1);
  };
  
  const handleAuthComplete = async (code: string) => {
    const result = await channelService.exchangeAuthCode(selectedChannel!, code);
    setAuthResult(result);
    setActiveStep(2);
  };
  
  const renderStepContent = () => {
    switch (activeStep) {
      case 0:
        return (
          <ChannelSelectionGrid
            channels={['airbnb', 'vrbo', 'booking_com']}
            onSelect={handleChannelSelect}
          />
        );
      case 1:
        return (
          <OAuthFlow
            channel={selectedChannel!}
            onComplete={handleAuthComplete}
          />
        );
      case 2:
        return (
          <PropertyMappingWizard
            channel={selectedChannel!}
            authResult={authResult!}
            onComplete={() => setActiveStep(3)}
          />
        );
      case 3:
        return (
          <InitialSyncProgress
            channel={selectedChannel!}
            onComplete={onComplete}
          />
        );
    }
  };
  
  return (
    <Box sx={{ width: '100%' }}>
      <Stepper activeStep={activeStep}>
        {steps.map((label) => (
          <Step key={label}>
            <StepLabel>{label}</StepLabel>
          </Step>
        ))}
      </Stepper>
      <Box sx={{ mt: 4 }}>
        {renderStepContent()}
      </Box>
    </Box>
  );
};
```

---

## 10. Testing Strategy

### 10.1 Unit Tests

```python
# tests/unit/test_rate_calculation.py
import pytest
from decimal import Decimal
from services.rate_distribution import calculate_channel_rate

class TestRateCalculation:
    def test_airbnb_markup(self):
        result = calculate_channel_rate(Decimal("100.00"), "airbnb")
        
        assert result["base_rate"] == 100.00
        assert result["commission_rate"] == 0.15
        assert result["markup_rate"] == 0.05
        assert result["final_rate"] == 120.00  # 100 * 1.20
    
    def test_vrbo_markup(self):
        result = calculate_channel_rate(Decimal("100.00"), "vrbo")
        
        assert result["final_rate"] == 111.00  # 100 * 1.11
    
    def test_direct_booking_discount(self):
        result = calculate_channel_rate(Decimal("100.00"), "direct")
        
        assert result["final_rate"] == 95.00  # 100 * 0.95
    
    def test_custom_markup(self):
        result = calculate_channel_rate(
            Decimal("100.00"),
            "airbnb",
            custom_markup=Decimal("0.10")
        )
        
        assert result["final_rate"] == 125.00  # 100 * 1.25
```

### 10.2 Integration Tests

```python
# tests/integration/test_content_sync.py
import pytest
from unittest.mock import AsyncMock, patch
from workflows.content_sync import ContentSyncWorkflow

@pytest.fixture
def mock_ota_client():
    with patch('services.ota_client.OTAClient') as mock:
        mock.return_value.sync_content = AsyncMock(return_value={"status": "success"})
        yield mock

class TestContentSyncIntegration:
    @pytest.mark.asyncio
    async def test_full_content_sync_workflow(self, mock_ota_client, temporal_client):
        content = {
            "title": {"en": "Test Property"},
            "description": {"en": "A test property description"},
            "photos": [{"url": "https://example.com/photo.jpg"}],
            "amenities": ["wifi", "pool"]
        }
        
        result = await temporal_client.execute_workflow(
            ContentSyncWorkflow.run,
            args=["property-123", content, ["airbnb", "vrbo"]],
            id="test-sync-workflow",
            task_queue="channel-sync"
        )
        
        assert result["airbnb"]["status"] == "success"
        assert result["vrbo"]["status"] == "success"
```

### 10.3 E2E Tests

```typescript
// tests/e2e/channel-connection.spec.ts
import { test, expect } from '@playwright/test';

test.describe('Channel Connection', () => {
  test('should complete Airbnb OAuth flow', async ({ page }) => {
    await page.goto('/channels');
    
    // Click connect button
    await page.click('[data-testid="connect-airbnb"]');
    
    // Should redirect to wizard
    await expect(page).toHaveURL(/\/channels\/connect/);
    
    // Verify OAuth redirect prompt
    await expect(page.locator('[data-testid="oauth-prompt"]')).toBeVisible();
    
    // Simulate OAuth callback
    await page.goto('/channels/airbnb/callback?code=test-auth-code&state=test-state');
    
    // Should proceed to property mapping
    await expect(page.locator('[data-testid="property-mapping"]')).toBeVisible();
  });
  
  test('should display sync status dashboard', async ({ page }) => {
    await page.goto('/channels/status');
    
    // Verify status cards are visible
    await expect(page.locator('[data-testid="connected-channels"]')).toBeVisible();
    await expect(page.locator('[data-testid="sync-success-rate"]')).toBeVisible();
    
    // Verify channel grid
    await expect(page.locator('[data-testid="channel-grid"]')).toBeVisible();
  });
});
```

---

## 11. Deployment & Operations

### 11.1 CI/CD Pipeline

```yaml
# .github/workflows/channel-distribution.yml
name: Channel Distribution CI/CD

on:
  push:
    branches: [main]
    paths:
      - 'services/channel-distribution/**'
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      
      - name: Install dependencies
        run: |
          pip install -r services/channel-distribution/requirements.txt
          pip install -r services/channel-distribution/requirements-test.txt
      
      - name: Run unit tests
        run: pytest services/channel-distribution/tests/unit -v --cov
      
      - name: Run integration tests
        run: pytest services/channel-distribution/tests/integration -v

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1
      
      - name: Login to ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v2
      
      - name: Build and push
        env:
          ECR_REGISTRY: ${{ steps.login-ecr.outputs.registry }}
          IMAGE_TAG: ${{ github.sha }}
        run: |
          docker build -t $ECR_REGISTRY/channel-distribution:$IMAGE_TAG services/channel-distribution
          docker push $ECR_REGISTRY/channel-distribution:$IMAGE_TAG

  deploy:
    needs: build
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - name: Deploy to ECS
        run: |
          aws ecs update-service \
            --cluster citadel-prod \
            --service channel-distribution \
            --force-new-deployment
```

### 11.2 Monitoring & Observability

```yaml
# DataDog dashboard configuration
dashboards:
  - name: Channel Distribution Overview
    widgets:
      - title: Sync Success Rate by Channel
        type: timeseries
        queries:
          - metric: channel.sync.success_rate
            aggregator: avg
            group_by: [channel]
      
      - title: API Latency P99
        type: timeseries
        queries:
          - metric: channel.api.latency.p99
            aggregator: avg
            group_by: [channel, operation]
      
      - title: Active Errors
        type: query_value
        queries:
          - metric: channel.errors.active
            aggregator: sum
      
      - title: Rate Limit Utilization
        type: gauge
        queries:
          - metric: channel.ratelimit.utilization
            aggregator: avg
            group_by: [channel]

alerts:
  - name: High Sync Failure Rate
    query: avg(last_5m):avg:channel.sync.success_rate{*} < 0.95
    message: "Sync success rate dropped below 95%"
    priority: P2
  
  - name: Channel Connection Down
    query: avg(last_5m):avg:channel.connection.status{*} < 1
    message: "Channel connection is down: {{channel.name}}"
    priority: P1
```

---

## 12. Security Considerations

### 12.1 Credential Management

```python
# Credential encryption using AWS KMS
from cryptography.fernet import Fernet
import boto3

class CredentialManager:
    def __init__(self, kms_key_id: str):
        self.kms_client = boto3.client('kms')
        self.kms_key_id = kms_key_id
    
    async def encrypt_credentials(self, credentials: dict) -> bytes:
        """Encrypt credentials using KMS envelope encryption"""
        # Generate data key
        response = self.kms_client.generate_data_key(
            KeyId=self.kms_key_id,
            KeySpec='AES_256'
        )
        
        plaintext_key = response['Plaintext']
        encrypted_key = response['CiphertextBlob']
        
        # Encrypt credentials with data key
        fernet = Fernet(base64.urlsafe_b64encode(plaintext_key))
        encrypted_data = fernet.encrypt(json.dumps(credentials).encode())
        
        # Return encrypted key + encrypted data
        return {
            'encrypted_key': base64.b64encode(encrypted_key).decode(),
            'encrypted_data': base64.b64encode(encrypted_data).decode()
        }
    
    async def decrypt_credentials(self, encrypted: dict) -> dict:
        """Decrypt credentials"""
        encrypted_key = base64.b64decode(encrypted['encrypted_key'])
        encrypted_data = base64.b64decode(encrypted['encrypted_data'])
        
        # Decrypt data key with KMS
        response = self.kms_client.decrypt(CiphertextBlob=encrypted_key)
        plaintext_key = response['Plaintext']
        
        # Decrypt credentials
        fernet = Fernet(base64.urlsafe_b64encode(plaintext_key))
        decrypted = fernet.decrypt(encrypted_data)
        
        return json.loads(decrypted)
```

### 12.2 Audit Logging

```python
# Audit events for compliance
@dataclass
class AuditEvent:
    event_id: str
    timestamp: datetime
    actor_id: str
    actor_type: str  # "user", "system", "api"
    action: str
    resource_type: str
    resource_id: str
    channel: str
    details: dict
    ip_address: Optional[str]
    user_agent: Optional[str]

AUDITED_ACTIONS = [
    "channel.connect",
    "channel.disconnect",
    "credential.create",
    "credential.rotate",
    "content.sync",
    "rate.push",
    "property.map",
    "property.unmap"
]

async def log_audit_event(event: AuditEvent):
    """Log audit event to immutable store"""
    # Log to MongoDB with TTL index for retention
    await audit_collection.insert_one({
        **asdict(event),
        "timestamp": event.timestamp,
        "_retention_date": event.timestamp + timedelta(days=2555)  # 7 years
    })
    
    # Also emit to Redpanda for real-time monitoring
    await redpanda_producer.send(
        "audit.channel",
        json.dumps(asdict(event)).encode()
    )
```

---

## Appendix A: OTA API Reference

### A.1 Rate Limits by Channel

| Channel | Rate Limit | Burst | Reset Window |
|---------|-----------|-------|--------------|
| Airbnb | 15 req/s | 30 | Rolling |
| Vrbo/Expedia | 50 req/s | 100 | Per second |
| Booking.com | 30 req/s | 60 | Per account |

### A.2 Content Constraints

| Field | Airbnb | Vrbo | Booking.com |
|-------|--------|------|-------------|
| Title Max | 50 chars | 80 chars | 100 chars |
| Description Max | 500 chars | 2000 chars | 1000 chars |
| Photo Min | 1024x683 | 1024x683 | 2048x1080 |
| Photo Max Size | 4MB | 20MB | 10MB |
| Max Photos | 100 | 50 | 45 |

---

## Appendix B: Glossary

| Term | Definition |
|------|------------|
| OTA | Online Travel Agency (Airbnb, Vrbo, Booking.com) |
| Rate Parity | Maintaining consistent pricing across channels |
| Channel Manager | Software for managing multi-channel distribution |
| OAuth 2.0 | Standard authorization protocol for API access |
| Circuit Breaker | Pattern to prevent cascading failures |

---

*This specification provides the complete engineering requirements for implementing the Channel Distribution & OTA Management platform as part of the Citadel OS Phase 1 MVP.*

