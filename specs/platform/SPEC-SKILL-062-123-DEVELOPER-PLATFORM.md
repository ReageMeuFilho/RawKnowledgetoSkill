# Skill Specification: Developer Platform

> **Skills Covered**: SKILL-062, SKILL-063, SKILL-121, SKILL-122, SKILL-123
> **Category**: Platform / Developer Experience
> **Phase**: Phase 2 - Group 6 (Developer Platform)
> **Priority**: P2 (Enhanced)
> **Status**: SPECIFIED
> **Last Updated**: January 2026
> **Research Source**: Research Phase 2 Group 6.txt (~10,600 lines)

---

## 📋 EXECUTIVE SUMMARY

The Developer Platform delivers **5 core developer experience skills** that transform Citadel OS into a comprehensive third-party ecosystem enabler:

- **<30 min** developer onboarding (signup to first API call)
- **99.9%** API uptime with <200ms P95 latency
- **Zero** security incidents (SOC 2 compliant)
- **50+** active third-party integrations (target Q4 2026)
- **300%** increase in integrations within 18 months

### Skills Overview

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-062** | API Key Management | Authentication | Self-service generation, rotation, permissions |
| **SKILL-063** | Webhook Management | Integration | HMAC signatures, retry logic, delivery guarantees |
| **SKILL-121** | API Rate Limiting | Traffic Control | Token bucket algorithm, tiered limits |
| **SKILL-122** | API Usage Analytics | Observability | Real-time dashboards, P95 tracking |
| **SKILL-123** | Sandbox Environment | Development | Isolated testing, mock data, magic values |

---

## 🏗️ ARCHITECTURE ALIGNMENT NOTES

### Layer Mapping (Citadel OS 6-Layer Stack)

| Component | Citadel OS Layer | Implementation |
|-----------|------------------|----------------|
| Developer Portal UI | Layer 6: Applications | React + Next.js + TypeScript |
| Developer Domain | Layer 5: Domain Bundles | Developer platform bundle |
| Developer Skills | Layer 4: Skills Layer | SKILL.md files |
| API Gateway | Layer 3: Hot Path | Rust/Axum (high-performance) |
| Key Storage | Layer 2: Cold Path | PostgreSQL + AWS KMS |
| Event Infrastructure | Layer 1: Infrastructure | Temporal + Redis + Redpanda |

### Execution Path Classification

| Skill | Path | Reasoning |
|-------|------|-----------|
| SKILL-062 (API Keys) | **Cold** | Key lifecycle management, database-backed |
| SKILL-063 (Webhooks) | **Hybrid** | Temporal workflows + real-time delivery |
| SKILL-121 (Rate Limiting) | **Hot** | Real-time token bucket checks (<5ms) |
| SKILL-122 (Analytics) | **Cold** | Time-series aggregation, ClickHouse |
| SKILL-123 (Sandbox) | **Cold** | Environment provisioning |

### MCP Server Requirements

```yaml
mcp_servers:
  # Key Management
  - mcp://developer/api-keys           # Key lifecycle operations
  - mcp://developer/permissions        # Permission scoping
  
  # Webhook Management
  - mcp://developer/webhooks           # Webhook configuration
  - mcp://developer/webhook-deliver    # Event delivery
  
  # Rate Limiting
  - mcp://developer/rate-limits        # Limit configuration
  - mcp://developer/quota-status       # Current usage
  
  # Analytics
  - mcp://developer/usage-metrics      # API usage data
  - mcp://developer/dashboard          # Dashboard generation
  
  # Sandbox
  - mcp://developer/sandbox            # Environment management
  - mcp://developer/mock-data          # Test data generation
```

### Infrastructure Alignment Verification

| Research Spec | Citadel OS Architecture | Status |
|---------------|------------------------|--------|
| Rust/Axum (API Gateway) | ✅ Aligned | Hot Path gateway |
| Python 3.11+ (Services) | ✅ Aligned | FastAPI services |
| PostgreSQL | ✅ Aligned | Primary database |
| Redis Cluster | ✅ Aligned | Rate limiting state |
| ClickHouse | ✅ Aligned | Analytics storage |
| Temporal | ✅ Aligned | Webhook workflows |
| AWS KMS | ✅ Aligned | Key encryption |
| ECS/Fargate | ⚠️ Note | Research mentions K8s/Helm, we use ECS |

---

## 📊 SKILL SPECIFICATIONS

### SKILL-062: API Key Management

#### Purpose
Self-service API key generation with prefix-based identification (`sk_live_`, `pk_test_`), zero-downtime rotation with 24-hour overlap, and granular permission scoping.

#### Technical Architecture
```python
from dataclasses import dataclass
from datetime import datetime, timedelta
from typing import List, Optional
import secrets
import hashlib
import boto3

@dataclass
class APIKey:
    id: str
    prefix: str
    key_hash: str
    user_id: str
    environment: str  # 'live' or 'test'
    permissions: List[str]
    created_at: datetime
    last_used_at: Optional[datetime]
    expires_at: Optional[datetime]
    status: str  # 'active', 'rotating', 'revoked', 'expired'

class APIKeyManagementService:
    """
    Self-service API key management with zero-downtime rotation.
    Achieves <500ms key generation, 24-hour overlap for rotation.
    """
    
    KEY_PREFIXES = {
        'live': 'sk_live_',
        'test': 'pk_test_'
    }
    
    def __init__(self):
        self.kms_client = boto3.client('kms')
        self.db = PostgreSQLClient()
        self.audit_logger = AuditLogger()
    
    async def generate_key(
        self,
        user_id: str,
        environment: str,
        permissions: List[str],
        name: Optional[str] = None
    ) -> APIKey:
        """Generate a new API key with prefix-based identification."""
        
        # Validate user has permission to create keys
        await self._validate_user_permissions(user_id, permissions)
        
        # Check key limit (max 10 per environment)
        existing_keys = await self.db.count_keys(user_id, environment)
        if existing_keys >= 10:
            raise KeyLimitExceeded("Maximum 10 keys per environment")
        
        # Generate cryptographically secure key
        prefix = self.KEY_PREFIXES[environment]
        random_part = secrets.token_urlsafe(32)
        full_key = f"{prefix}{random_part}"
        
        # Hash for storage (never store raw key)
        key_hash = hashlib.sha256(full_key.encode()).hexdigest()
        
        # Encrypt key for return using KMS envelope encryption
        encrypted_key = await self._encrypt_with_kms(full_key)
        
        key = APIKey(
            id=str(uuid.uuid4()),
            prefix=prefix,
            key_hash=key_hash,
            user_id=user_id,
            environment=environment,
            permissions=permissions,
            created_at=datetime.utcnow(),
            last_used_at=None,
            expires_at=None,
            status='active'
        )
        
        await self.db.save_key(key)
        await self.audit_logger.log('key_created', key.id, user_id)
        
        return key, full_key  # Return full key only once
    
    async def rotate_key(
        self,
        key_id: str,
        overlap_hours: int = 24
    ) -> APIKey:
        """Zero-downtime key rotation with overlap period."""
        
        old_key = await self.db.get_key(key_id)
        if not old_key:
            raise KeyNotFound(key_id)
        
        # Generate new key
        new_key, full_key = await self.generate_key(
            user_id=old_key.user_id,
            environment=old_key.environment,
            permissions=old_key.permissions
        )
        
        # Mark old key as rotating with overlap
        old_key.status = 'rotating'
        old_key.expires_at = datetime.utcnow() + timedelta(hours=overlap_hours)
        await self.db.update_key(old_key)
        
        # Schedule automatic revocation after overlap
        await self._schedule_revocation(old_key.id, overlap_hours)
        
        await self.audit_logger.log('key_rotation_started', key_id, old_key.user_id)
        
        return new_key, full_key
    
    async def validate_key(self, api_key: str) -> Optional[APIKey]:
        """Validate API key and check permissions."""
        
        # Hash the incoming key
        key_hash = hashlib.sha256(api_key.encode()).hexdigest()
        
        # Look up by hash
        key = await self.db.get_key_by_hash(key_hash)
        
        if not key:
            return None
        
        # Check status
        if key.status == 'revoked':
            return None
        
        if key.status == 'expired' or (key.expires_at and key.expires_at < datetime.utcnow()):
            return None
        
        # Update last used
        key.last_used_at = datetime.utcnow()
        await self.db.update_key(key)
        
        return key
    
    async def _encrypt_with_kms(self, plaintext: str) -> bytes:
        """Encrypt using AWS KMS envelope encryption."""
        
        response = self.kms_client.encrypt(
            KeyId='alias/api-keys',
            Plaintext=plaintext.encode()
        )
        return response['CiphertextBlob']
```

#### Key Lifecycle States
```
┌─────────┐   Create    ┌────────┐   Rotate   ┌──────────┐
│ Pending │ ──────────► │ Active │ ─────────► │ Rotating │
└─────────┘             └────────┘            └──────────┘
                            │                      │
                            │ Compromise           │ Overlap
                            ▼                      │ Expires
                       ┌─────────────┐             │
                       │ Compromised │             │
                       └─────────────┘             ▼
                            │                ┌─────────┐
                            └──────────────► │ Revoked │
                                             └─────────┘
```

#### Permission Scopes
| Scope | Description | Access Level |
|-------|-------------|--------------|
| `read_only` | GET requests only | Minimal |
| `write` | All HTTP methods | Standard |
| `reservations:read` | Read reservations | Resource-specific |
| `webhooks:write` | Manage webhooks | Resource-specific |
| `analytics:read` | View usage metrics | Resource-specific |

---

### SKILL-063: Webhook Management

#### Purpose
Event-driven webhook system with HMAC-SHA256 signature verification, exponential backoff retry logic (immediate → 30s → 5m → 1h → 24h), and circuit breaker patterns for reliability.

#### Technical Architecture
```python
from temporalio import workflow, activity
from temporalio.common import RetryPolicy
import hmac
import hashlib

class WebhookDeliveryService:
    """
    Reliable webhook delivery with HMAC signatures.
    Achieves >99% delivery rate with automatic retries.
    """
    
    RETRY_INTERVALS = [0, 30, 300, 3600, 86400]  # seconds
    
    def __init__(self):
        self.temporal = TemporalClient()
        self.redis = RedisClient()
        self.db = PostgreSQLClient()
    
    def generate_signature(
        self,
        payload: bytes,
        secret: str,
        timestamp: int
    ) -> str:
        """Generate HMAC-SHA256 signature with timestamp."""
        
        # Create signed payload string
        signed_payload = f"{timestamp}.{payload.decode()}"
        
        # Generate HMAC
        signature = hmac.new(
            secret.encode(),
            signed_payload.encode(),
            hashlib.sha256
        ).hexdigest()
        
        return f"sha256={signature}"
    
    async def deliver_webhook(
        self,
        event_type: str,
        payload: dict,
        endpoint_id: str
    ) -> str:
        """Queue webhook for delivery via Temporal workflow."""
        
        endpoint = await self.db.get_webhook_endpoint(endpoint_id)
        if not endpoint or not endpoint.enabled:
            raise EndpointDisabled(endpoint_id)
        
        # Check circuit breaker
        if await self._is_circuit_open(endpoint_id):
            raise CircuitBreakerOpen(endpoint_id)
        
        # Create webhook event
        event = WebhookEvent(
            id=str(uuid.uuid4()),
            event_type=event_type,
            payload=payload,
            endpoint_id=endpoint_id,
            created_at=datetime.utcnow(),
            status='queued'
        )
        
        await self.db.save_webhook_event(event)
        
        # Start Temporal workflow for delivery
        await self.temporal.start_workflow(
            WebhookDeliveryWorkflow.run,
            event.id,
            id=f"webhook-{event.id}",
            task_queue="webhook-delivery"
        )
        
        return event.id


@workflow.defn
class WebhookDeliveryWorkflow:
    """Temporal workflow for reliable webhook delivery."""
    
    @workflow.run
    async def run(self, event_id: str) -> dict:
        """Execute webhook delivery with retries."""
        
        event = await workflow.execute_activity(
            get_webhook_event,
            event_id,
            start_to_close_timeout=timedelta(seconds=30)
        )
        
        for attempt, interval in enumerate(RETRY_INTERVALS):
            if interval > 0:
                await asyncio.sleep(interval)
            
            result = await workflow.execute_activity(
                deliver_webhook_http,
                event,
                start_to_close_timeout=timedelta(seconds=30),
                retry_policy=RetryPolicy(maximum_attempts=1)
            )
            
            if result.success:
                await workflow.execute_activity(
                    mark_webhook_delivered,
                    event_id,
                    start_to_close_timeout=timedelta(seconds=30)
                )
                return {"status": "delivered", "attempts": attempt + 1}
            
            if result.permanent_failure:
                # 404/410 - disable endpoint
                await workflow.execute_activity(
                    disable_webhook_endpoint,
                    event.endpoint_id,
                    start_to_close_timeout=timedelta(seconds=30)
                )
                return {"status": "endpoint_disabled"}
        
        # Max retries exhausted
        await workflow.execute_activity(
            mark_webhook_failed,
            event_id,
            start_to_close_timeout=timedelta(seconds=30)
        )
        return {"status": "failed", "attempts": len(RETRY_INTERVALS)}


@activity.defn
async def deliver_webhook_http(event: WebhookEvent) -> DeliveryResult:
    """HTTP delivery activity with signature verification."""
    
    endpoint = await db.get_webhook_endpoint(event.endpoint_id)
    
    # Generate timestamp and signature
    timestamp = int(datetime.utcnow().timestamp())
    payload_bytes = json.dumps(event.payload).encode()
    signature = generate_signature(payload_bytes, endpoint.secret, timestamp)
    
    headers = {
        "Content-Type": "application/json",
        "X-Hub-Signature-256": signature,
        "X-Webhook-Timestamp": str(timestamp),
        "X-Webhook-ID": event.id,
        "X-Webhook-Event": event.event_type
    }
    
    try:
        async with aiohttp.ClientSession() as session:
            async with session.post(
                endpoint.url,
                data=payload_bytes,
                headers=headers,
                timeout=aiohttp.ClientTimeout(total=30)
            ) as response:
                if response.status in (200, 201, 202, 204):
                    return DeliveryResult(success=True)
                elif response.status in (404, 410):
                    return DeliveryResult(success=False, permanent_failure=True)
                else:
                    return DeliveryResult(success=False, status_code=response.status)
    except asyncio.TimeoutError:
        return DeliveryResult(success=False, error="timeout")
    except Exception as e:
        return DeliveryResult(success=False, error=str(e))
```

#### Webhook Event Types
| Event Category | Event Type | Trigger |
|----------------|------------|---------|
| **Reservations** | `reservation.created` | New booking |
| | `reservation.updated` | Booking modified |
| | `reservation.cancelled` | Booking cancelled |
| **Payments** | `payment.succeeded` | Payment captured |
| | `payment.failed` | Payment declined |
| | `payout.sent` | Owner payout processed |
| **Messaging** | `message.received` | Guest message |
| | `message.sent` | Auto-reply sent |
| **Operations** | `task.completed` | Work order finished |
| | `review.received` | New guest review |

#### Retry Strategy
```
Attempt 1: Immediate (0s)
    │
    ▼ Failure
Attempt 2: +30 seconds
    │
    ▼ Failure
Attempt 3: +5 minutes
    │
    ▼ Failure
Attempt 4: +1 hour
    │
    ▼ Failure
Attempt 5: +24 hours
    │
    ▼ Failure
Mark as FAILED, notify developer
```

---

### SKILL-121: API Rate Limiting

#### Purpose
Token bucket algorithm with burst handling, tiered limits by subscription plan, and transparent communication via standard HTTP headers.

#### Technical Architecture
```rust
// Rust implementation for high-performance rate limiting
use redis::AsyncCommands;
use std::time::{Duration, SystemTime, UNIX_EPOCH};

pub struct TokenBucket {
    redis: redis::Client,
}

impl TokenBucket {
    pub async fn check_rate_limit(
        &self,
        key: &str,
        tier: &RateTier,
    ) -> Result<RateLimitResult, Error> {
        let mut conn = self.redis.get_async_connection().await?;
        
        let bucket_key = format!("ratelimit:{}", key);
        let now = SystemTime::now()
            .duration_since(UNIX_EPOCH)?
            .as_secs_f64();
        
        // Lua script for atomic token bucket operations
        let script = redis::Script::new(r#"
            local bucket_key = KEYS[1]
            local capacity = tonumber(ARGV[1])
            local refill_rate = tonumber(ARGV[2])
            local now = tonumber(ARGV[3])
            
            local bucket = redis.call('HMGET', bucket_key, 'tokens', 'last_refill')
            local tokens = tonumber(bucket[1]) or capacity
            local last_refill = tonumber(bucket[2]) or now
            
            -- Calculate tokens to add
            local elapsed = now - last_refill
            local tokens_to_add = elapsed * refill_rate
            tokens = math.min(capacity, tokens + tokens_to_add)
            
            if tokens >= 1 then
                -- Consume token
                tokens = tokens - 1
                redis.call('HMSET', bucket_key, 'tokens', tokens, 'last_refill', now)
                redis.call('EXPIRE', bucket_key, 3600)
                return {1, tokens, capacity}
            else
                -- Rate limited
                local wait_time = (1 - tokens) / refill_rate
                return {0, tokens, capacity, wait_time}
            end
        "#);
        
        let result: Vec<f64> = script
            .key(&bucket_key)
            .arg(tier.capacity)
            .arg(tier.refill_rate)
            .arg(now)
            .invoke_async(&mut conn)
            .await?;
        
        if result[0] == 1.0 {
            Ok(RateLimitResult {
                allowed: true,
                remaining: result[1] as u32,
                limit: result[2] as u32,
                reset_at: now + (tier.capacity as f64 / tier.refill_rate),
                retry_after: None,
            })
        } else {
            Ok(RateLimitResult {
                allowed: false,
                remaining: 0,
                limit: result[2] as u32,
                reset_at: now + result[3],
                retry_after: Some(Duration::from_secs_f64(result[3])),
            })
        }
    }
}

pub struct RateTier {
    pub name: String,
    pub capacity: u32,      // Burst capacity
    pub refill_rate: f64,   // Tokens per second
}

impl RateTier {
    pub fn from_plan(plan: &str) -> Self {
        match plan {
            "free" => RateTier {
                name: "free".to_string(),
                capacity: 100,
                refill_rate: 1.0,  // 60 req/min
            },
            "starter" => RateTier {
                name: "starter".to_string(),
                capacity: 500,
                refill_rate: 10.0,  // 600 req/min
            },
            "professional" => RateTier {
                name: "professional".to_string(),
                capacity: 2000,
                refill_rate: 50.0,  // 3000 req/min
            },
            "enterprise" => RateTier {
                name: "enterprise".to_string(),
                capacity: 10000,
                refill_rate: 200.0,  // 12000 req/min
            },
            _ => RateTier::from_plan("free"),
        }
    }
}
```

#### Rate Limit Tiers
| Plan | Capacity (Burst) | Rate (req/min) | Cost-Based Ops |
|------|------------------|----------------|----------------|
| Free | 100 | 60 | 10/day |
| Starter | 500 | 600 | 100/day |
| Professional | 2,000 | 3,000 | 1,000/day |
| Enterprise | 10,000 | 12,000 | Unlimited |

#### HTTP Headers
```http
HTTP/1.1 200 OK
X-RateLimit-Limit: 500
X-RateLimit-Remaining: 423
X-RateLimit-Reset: 1704628800

HTTP/1.1 429 Too Many Requests
X-RateLimit-Limit: 500
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1704628800
Retry-After: 45
Content-Type: application/json

{
  "error": "rate_limit_exceeded",
  "message": "Too many requests. Please retry after 45 seconds.",
  "retry_after": 45
}
```

---

### SKILL-122: API Usage Analytics

#### Purpose
Real-time usage dashboards with P95 latency tracking, error rate monitoring (4xx/5xx categorization), and usage-based billing integration.

#### Technical Architecture
```python
from clickhouse_driver import Client as ClickHouseClient
from datetime import datetime, timedelta
from typing import List, Dict

class APIUsageAnalyticsService:
    """
    Real-time API usage analytics with ClickHouse.
    Handles 1M+ events/day with sub-second queries.
    """
    
    def __init__(self):
        self.clickhouse = ClickHouseClient(host='clickhouse')
        self.redis = RedisClient()
    
    async def record_request(self, metrics: RequestMetrics):
        """Record API request metrics for analytics."""
        
        # Insert into ClickHouse (batched)
        await self.clickhouse.execute(
            """
            INSERT INTO api_metrics (
                timestamp, api_key_id, user_id, endpoint,
                method, status_code, latency_ms, request_size,
                response_size, error_type
            ) VALUES
            """,
            [(
                metrics.timestamp,
                metrics.api_key_id,
                metrics.user_id,
                metrics.endpoint,
                metrics.method,
                metrics.status_code,
                metrics.latency_ms,
                metrics.request_size,
                metrics.response_size,
                metrics.error_type
            )]
        )
        
        # Update real-time counters in Redis
        pipe = self.redis.pipeline()
        minute_key = f"metrics:{metrics.user_id}:{metrics.timestamp.strftime('%Y%m%d%H%M')}"
        pipe.hincrby(minute_key, 'requests', 1)
        pipe.hincrby(minute_key, f'status_{metrics.status_code}', 1)
        pipe.hincrby(minute_key, 'total_latency', metrics.latency_ms)
        pipe.expire(minute_key, 86400)  # 24 hour retention for real-time
        await pipe.execute()
    
    async def get_dashboard_metrics(
        self,
        user_id: str,
        time_range: str = '24h'
    ) -> DashboardMetrics:
        """Get comprehensive dashboard metrics."""
        
        time_filter = self._get_time_filter(time_range)
        
        # Main metrics query
        result = await self.clickhouse.execute(
            f"""
            SELECT
                count() as total_requests,
                avg(latency_ms) as avg_latency,
                quantile(0.95)(latency_ms) as p95_latency,
                quantile(0.50)(latency_ms) as median_latency,
                countIf(status_code >= 400 AND status_code < 500) as client_errors,
                countIf(status_code >= 500) as server_errors,
                sum(request_size) as total_request_bytes,
                sum(response_size) as total_response_bytes
            FROM api_metrics
            WHERE user_id = %(user_id)s
            AND timestamp >= %(time_filter)s
            """,
            {'user_id': user_id, 'time_filter': time_filter}
        )
        
        row = result[0]
        total = row[0]
        
        return DashboardMetrics(
            total_requests=total,
            avg_latency_ms=row[1],
            p95_latency_ms=row[2],
            median_latency_ms=row[3],
            error_rate=(row[4] + row[5]) / total if total > 0 else 0,
            client_error_rate=row[4] / total if total > 0 else 0,
            server_error_rate=row[5] / total if total > 0 else 0,
            total_bandwidth_mb=(row[6] + row[7]) / (1024 * 1024)
        )
    
    async def get_endpoint_breakdown(
        self,
        user_id: str,
        time_range: str = '24h'
    ) -> List[EndpointMetrics]:
        """Get per-endpoint usage breakdown."""
        
        time_filter = self._get_time_filter(time_range)
        
        result = await self.clickhouse.execute(
            f"""
            SELECT
                endpoint,
                count() as requests,
                avg(latency_ms) as avg_latency,
                quantile(0.95)(latency_ms) as p95_latency,
                countIf(status_code >= 400) / count() as error_rate
            FROM api_metrics
            WHERE user_id = %(user_id)s
            AND timestamp >= %(time_filter)s
            GROUP BY endpoint
            ORDER BY requests DESC
            LIMIT 50
            """,
            {'user_id': user_id, 'time_filter': time_filter}
        )
        
        return [
            EndpointMetrics(
                endpoint=row[0],
                requests=row[1],
                avg_latency_ms=row[2],
                p95_latency_ms=row[3],
                error_rate=row[4]
            )
            for row in result
        ]
    
    async def detect_abuse_patterns(self, user_id: str) -> List[AbuseAlert]:
        """Detect potential API abuse patterns."""
        
        alerts = []
        
        # Check for sudden traffic spike
        current_hour = await self._get_hourly_requests(user_id, 0)
        previous_hour = await self._get_hourly_requests(user_id, 1)
        
        if previous_hour > 0 and current_hour > previous_hour * 5:
            alerts.append(AbuseAlert(
                type='traffic_spike',
                severity='medium',
                message=f'5x traffic increase detected ({previous_hour} -> {current_hour})'
            ))
        
        # Check for high error rate
        error_rate = await self._get_error_rate(user_id, hours=1)
        if error_rate > 0.5:
            alerts.append(AbuseAlert(
                type='high_error_rate',
                severity='high',
                message=f'Error rate {error_rate:.1%} exceeds 50% threshold'
            ))
        
        return alerts
```

#### Dashboard Metrics
| Metric | Calculation | Alert Threshold |
|--------|-------------|-----------------|
| Total Requests | Count per time range | - |
| P95 Latency | 95th percentile | >500ms |
| Median Latency | 50th percentile | >200ms |
| Error Rate | (4xx + 5xx) / total | >5% |
| Client Errors | 4xx / total | >10% |
| Server Errors | 5xx / total | >1% |

---

### SKILL-123: Sandbox Environment

#### Purpose
Isolated test environment with production API parity, deterministic mock data, and magic value testing for predictable response scenarios.

#### Technical Architecture
```python
from dataclasses import dataclass
from typing import Dict, Any, Optional
import docker

@dataclass
class SandboxEnvironment:
    id: str
    user_id: str
    status: str  # 'provisioning', 'active', 'suspended', 'terminated'
    url: str
    created_at: datetime
    expires_at: datetime

class SandboxEnvironmentService:
    """
    Isolated sandbox environments with mock data.
    Achieves production parity with complete data isolation.
    """
    
    MAGIC_VALUES = {
        # Reservation testing
        'amount_10000': {'status': 'confirmed', 'confirmation_code': 'TEST_CONF_001'},
        'amount_20000': {'status': 'pending', 'confirmation_code': 'TEST_PEND_001'},
        'amount_99999': {'status': 'failed', 'error': 'card_declined'},
        
        # Payment testing
        'card_4242424242424242': {'result': 'success'},
        'card_4000000000000002': {'result': 'declined'},
        'card_4000000000009995': {'result': 'insufficient_funds'},
        
        # Webhook testing
        'endpoint_success': {'delivery': 'immediate', 'status': 200},
        'endpoint_retry': {'delivery': 'delayed', 'status': 500},
        'endpoint_fail': {'delivery': 'fail', 'status': 404},
    }
    
    def __init__(self):
        self.docker_client = docker.from_env()
        self.db = PostgreSQLClient()
        self.mock_generator = MockDataGenerator()
    
    async def provision_sandbox(
        self,
        user_id: str,
        config: Optional[SandboxConfig] = None
    ) -> SandboxEnvironment:
        """Provision new sandbox environment."""
        
        # Validate user can create sandbox
        existing = await self.db.get_active_sandbox(user_id)
        if existing:
            raise SandboxAlreadyExists(user_id)
        
        sandbox = SandboxEnvironment(
            id=str(uuid.uuid4()),
            user_id=user_id,
            status='provisioning',
            url=f"https://sandbox-{uuid.uuid4().hex[:8]}.api.citadelos.dev",
            created_at=datetime.utcnow(),
            expires_at=datetime.utcnow() + timedelta(days=30)
        )
        
        await self.db.save_sandbox(sandbox)
        
        # Provision Docker container
        container = await self._create_sandbox_container(sandbox)
        
        # Generate mock data
        mock_data = await self.mock_generator.generate(
            properties=10,
            reservations=50,
            guests=30
        )
        
        await self._seed_sandbox_data(sandbox, mock_data)
        
        # Configure magic values
        await self._configure_magic_values(sandbox)
        
        sandbox.status = 'active'
        await self.db.update_sandbox(sandbox)
        
        return sandbox
    
    async def handle_magic_value(
        self,
        sandbox_id: str,
        request: APIRequest
    ) -> Optional[Dict[str, Any]]:
        """Check for magic values and return deterministic response."""
        
        # Check amount-based magic values
        if 'amount' in request.body:
            amount_key = f"amount_{request.body['amount']}"
            if amount_key in self.MAGIC_VALUES:
                return self.MAGIC_VALUES[amount_key]
        
        # Check card-based magic values
        if 'card_number' in request.body:
            card_key = f"card_{request.body['card_number']}"
            if card_key in self.MAGIC_VALUES:
                return self.MAGIC_VALUES[card_key]
        
        # Check webhook endpoint magic values
        if 'webhook_url' in request.body:
            for pattern, response in self.MAGIC_VALUES.items():
                if pattern.startswith('endpoint_') and pattern[9:] in request.body['webhook_url']:
                    return response
        
        return None
    
    async def refresh_mock_data(self, sandbox_id: str) -> SandboxEnvironment:
        """Refresh sandbox with new mock data."""
        
        sandbox = await self.db.get_sandbox(sandbox_id)
        if not sandbox:
            raise SandboxNotFound(sandbox_id)
        
        sandbox.status = 'refreshing'
        await self.db.update_sandbox(sandbox)
        
        # Clear existing data
        await self._clear_sandbox_data(sandbox)
        
        # Generate fresh mock data
        mock_data = await self.mock_generator.generate(
            properties=10,
            reservations=50,
            guests=30
        )
        
        await self._seed_sandbox_data(sandbox, mock_data)
        
        sandbox.status = 'active'
        await self.db.update_sandbox(sandbox)
        
        return sandbox


class MockDataGenerator:
    """Generate realistic mock data for sandbox environments."""
    
    async def generate(
        self,
        properties: int = 10,
        reservations: int = 50,
        guests: int = 30
    ) -> MockDataSet:
        """Generate comprehensive mock dataset."""
        
        # Generate properties
        mock_properties = [
            Property(
                id=f"prop_{i:04d}",
                name=fake.company() + " Rentals",
                address=fake.address(),
                bedrooms=random.randint(1, 5),
                bathrooms=random.randint(1, 3),
                max_guests=random.randint(2, 10),
                nightly_rate=random.randint(100, 500) * 100
            )
            for i in range(properties)
        ]
        
        # Generate guests
        mock_guests = [
            Guest(
                id=f"guest_{i:04d}",
                email=fake.email(),
                first_name=fake.first_name(),
                last_name=fake.last_name(),
                phone=fake.phone_number()
            )
            for i in range(guests)
        ]
        
        # Generate reservations
        mock_reservations = [
            Reservation(
                id=f"res_{i:04d}",
                property_id=random.choice(mock_properties).id,
                guest_id=random.choice(mock_guests).id,
                check_in=fake.future_date(end_date='+30d'),
                check_out=fake.future_date(end_date='+37d'),
                status=random.choice(['confirmed', 'pending', 'checked_in']),
                total_amount=random.randint(500, 3000) * 100
            )
            for i in range(reservations)
        ]
        
        return MockDataSet(
            properties=mock_properties,
            guests=mock_guests,
            reservations=mock_reservations
        )
```

#### Magic Value Reference
| Magic Value | Expected Response |
|-------------|-------------------|
| `amount: 10000` | Confirmed reservation |
| `amount: 20000` | Pending reservation |
| `amount: 99999` | Payment failed |
| `card: 4242...4242` | Payment success |
| `card: 4000...0002` | Card declined |
| `card: 4000...9995` | Insufficient funds |

---

## 🗄️ DATABASE SCHEMA

### PostgreSQL Tables

```sql
-- API Keys
CREATE TABLE api_keys (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    prefix VARCHAR(20) NOT NULL,
    key_hash VARCHAR(64) NOT NULL UNIQUE,
    user_id UUID NOT NULL REFERENCES users(id),
    organization_id UUID REFERENCES organizations(id),
    name VARCHAR(255),
    environment VARCHAR(10) NOT NULL CHECK (environment IN ('live', 'test')),
    permissions JSONB NOT NULL DEFAULT '[]',
    status VARCHAR(20) NOT NULL DEFAULT 'active',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    last_used_at TIMESTAMPTZ,
    expires_at TIMESTAMPTZ,
    rotated_from UUID REFERENCES api_keys(id)
);

-- Webhook Endpoints
CREATE TABLE webhook_endpoints (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id),
    url TEXT NOT NULL,
    secret VARCHAR(64) NOT NULL,
    events JSONB NOT NULL DEFAULT '[]',
    enabled BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    disabled_at TIMESTAMPTZ,
    disable_reason TEXT
);

-- Webhook Events
CREATE TABLE webhook_events (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    endpoint_id UUID NOT NULL REFERENCES webhook_endpoints(id),
    event_type VARCHAR(100) NOT NULL,
    payload JSONB NOT NULL,
    status VARCHAR(20) NOT NULL DEFAULT 'queued',
    attempts INTEGER DEFAULT 0,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    delivered_at TIMESTAMPTZ,
    last_attempt_at TIMESTAMPTZ,
    next_retry_at TIMESTAMPTZ,
    error_message TEXT
);

-- Sandbox Environments
CREATE TABLE sandbox_environments (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id),
    status VARCHAR(20) NOT NULL DEFAULT 'provisioning',
    url TEXT NOT NULL,
    container_id VARCHAR(64),
    config JSONB,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    expires_at TIMESTAMPTZ,
    last_active_at TIMESTAMPTZ
);

-- Indexes
CREATE INDEX idx_api_keys_user ON api_keys(user_id, status);
CREATE INDEX idx_api_keys_hash ON api_keys(key_hash);
CREATE INDEX idx_webhook_events_status ON webhook_events(status, next_retry_at);
CREATE INDEX idx_webhook_events_endpoint ON webhook_events(endpoint_id, created_at DESC);
CREATE INDEX idx_sandbox_user ON sandbox_environments(user_id, status);
```

### ClickHouse Analytics Schema

```sql
CREATE TABLE api_metrics (
    timestamp DateTime64(3),
    api_key_id UUID,
    user_id UUID,
    endpoint String,
    method String,
    status_code UInt16,
    latency_ms UInt32,
    request_size UInt32,
    response_size UInt32,
    error_type Nullable(String),
    ip_address String,
    user_agent String
) ENGINE = MergeTree()
PARTITION BY toYYYYMM(timestamp)
ORDER BY (user_id, timestamp)
TTL timestamp + INTERVAL 2 YEAR;

-- Materialized view for real-time aggregations
CREATE MATERIALIZED VIEW api_metrics_hourly
ENGINE = SummingMergeTree()
PARTITION BY toYYYYMM(hour)
ORDER BY (user_id, endpoint, hour)
AS SELECT
    user_id,
    endpoint,
    toStartOfHour(timestamp) as hour,
    count() as requests,
    sum(latency_ms) as total_latency,
    countIf(status_code >= 400) as errors
FROM api_metrics
GROUP BY user_id, endpoint, hour;
```

---

## 📊 PERFORMANCE REQUIREMENTS

| Skill | Response Time | Throughput | Availability |
|-------|--------------|------------|--------------|
| SKILL-062 (API Keys) | <500ms generation | 100 ops/sec | 99.9% |
| SKILL-063 (Webhooks) | <30s delivery | 1M events/day | 99.9% |
| SKILL-121 (Rate Limiting) | <5ms check | 100K checks/sec | 99.99% |
| SKILL-122 (Analytics) | <2s dashboard | 10K queries/min | 99.5% |
| SKILL-123 (Sandbox) | <60s provision | 100 envs/hour | 99.5% |

---

## 🧪 TESTING STRATEGY

### Unit Tests
- API key generation and validation
- HMAC signature generation/verification
- Token bucket algorithm
- Mock data generation

### Integration Tests
- Key rotation workflow
- Webhook delivery pipeline
- Rate limit enforcement
- Sandbox provisioning

### Performance Tests
- 100K concurrent rate limit checks
- 1M webhook events/day
- Dashboard query performance

### Security Tests
- Key leak detection
- HMAC timing-safe comparison
- Sandbox isolation

---

## 🔐 SECURITY CONSIDERATIONS

### Data Protection
- API keys encrypted with AWS KMS envelope encryption
- Webhook secrets stored securely
- PII redaction in analytics

### Compliance
- SOC 2 Type II certification target
- GDPR data retention policies
- Comprehensive audit logging

### Access Control
| Role | API Keys | Webhooks | Analytics |
|------|----------|----------|-----------|
| Developer | Own keys only | Own endpoints | Own data |
| Admin | Organization keys | Organization | Organization |
| Platform | Read-only audit | Delivery status | Aggregate only |

---

## 📁 FILE LOCATIONS

```
specs/platform/
└── SPEC-SKILL-062-123-DEVELOPER-PLATFORM.md (this file)

knowledge/platform/
└── KD-PHASE2-G6-developer-platform.md (research source)

skills/platform/
├── SKILL-062-api-key-management.md
├── SKILL-063-webhook-management.md
├── SKILL-121-api-rate-limiting.md
├── SKILL-122-api-usage-analytics.md
└── SKILL-123-sandbox-environment.md
```

---

## 🚀 IMPLEMENTATION ROADMAP

| Week | Milestone |
|------|-----------|
| 1-2 | SKILL-062 (API Keys) + Infrastructure |
| 3-4 | SKILL-121 (Rate Limiting) + Gateway |
| 5-6 | SKILL-063 (Webhooks) + Temporal |
| 7-8 | SKILL-122 (Analytics) + SKILL-123 (Sandbox) |

---

**Status**: ✅ SPECIFIED - Ready for Engineering Implementation

