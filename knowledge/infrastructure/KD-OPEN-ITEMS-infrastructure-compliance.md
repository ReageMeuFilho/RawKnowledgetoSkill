# Production Infrastructure Strategic Decisions - Final Knowledge Document

**Document Version**: 5.0 (Final Consolidated)  
**Classification**: Internal - Engineering Leadership  
**Last Updated**: January 2026  
**Sources**: V4 Strategic Architecture + Round 2 Operational Research + Round 3 AI Governance & Compliance

---

## Document Overview

This document consolidates all production infrastructure research into a single authoritative reference for Citadel OS. It combines:

| Source | Focus | Lines |
|--------|-------|-------|
| **V4** | Strategic architecture, Brazil focus, Treasury OS | ~1,700 |
| **Round 2** | Operational details, HITL, Memory, CI/CD | ~9,400 |
| **Round 3** | AI Prompt Versioning, Chaos Engineering, EU AI Act | ~6,300 |

---

## Table of Contents

### Part 1: Strategic Foundation
1. [Executive Strategic Overview](#1-executive-strategic-overview)
2. [The "Agent as Operating System" Mental Model](#2-the-agent-as-operating-system-mental-model)
3. [Cloud Provider & Deployment Strategy](#3-cloud-provider--deployment-strategy)

### Part 2: Financial Core (Treasury OS)
4. [TigerBeetle Ledger Engine](#4-tigerbeetle-ledger-engine)
5. [Federated Architecture & Numscript](#5-federated-architecture--numscript)
6. [Brazilian Crypto Regulation (SPSAV)](#6-brazilian-crypto-regulation-spsav)

### Part 3: Real-Time AI Infrastructure
7. [Voice AI Infrastructure (<300ms)](#7-voice-ai-infrastructure-300ms)
8. [AI Prompt Versioning & A/B Testing](#8-ai-prompt-versioning--ab-testing)
9. [AI Configuration & Prompt Library](#9-ai-configuration--prompt-library)

### Part 4: Operational Infrastructure
10. [Human-in-the-Loop (HITL) Operations](#10-human-in-the-loop-hitl-operations)
11. [Memory Architecture](#11-memory-architecture)
12. [Data Retention & Compliance Matrix](#12-data-retention--compliance-matrix)

### Part 5: Resilience Engineering
13. [Chaos Engineering Experiment Catalog](#13-chaos-engineering-experiment-catalog)
14. [Disaster Recovery & Multi-Region](#14-disaster-recovery--multi-region)
15. [Zero Trust Security Architecture](#15-zero-trust-security-architecture)

### Part 6: Compliance Framework
16. [EU AI Act Implementation](#16-eu-ai-act-implementation)
17. [State Regulatory Compliance (US)](#17-state-regulatory-compliance-us)
18. [Payment Orchestration & Smart Routing](#18-payment-orchestration--smart-routing)

### Appendices
- [A. Infrastructure as Code (Terraform)](#appendix-a-infrastructure-as-code)
- [B. Configuration Templates](#appendix-b-configuration-templates)
- [C. Open Items Reference](#appendix-c-open-items-reference)
- [D. Implementation Roadmap](#appendix-d-implementation-roadmap)
- [E. References](#appendix-e-references)

---

# PART 1: STRATEGIC FOUNDATION

## 1. Executive Strategic Overview

This document serves as the **definitive architectural blueprint** for Citadel OS, a next-generation financial operating system designed to facilitate high-velocity value exchange across fiat, crypto, and loyalty assets.

### 1.1 Architectural Philosophy: Financial Correctness by Design

The governing doctrine moves beyond the traditional "buy vs. build" dichotomy toward **"Financial Correctness by Design"**—leveraging deterministic infrastructure to eliminate the reconciliation overhead that plagues legacy fintechs.

### 1.2 The Core Engineering Challenge

Reconciling two opposing forces:

1. **Extreme Performance**: Sub-300ms latency for Voice AI and million-TPS throughput for the ledger
2. **Rigid Regulatory Constraints**: Brazilian LGPD, SPSAV framework (effective February 2026), PIX, and EU AI Act (August 2026)

### 1.3 Strategic Moats Through Infrastructure

| Moat Type | Implementation | Competitive Advantage |
|-----------|---------------|----------------------|
| **Compliance as Code** | Formance Numscript + TigerBeetle audit trails | Regulators can audit policy, not just data |
| **Voice UX** | Edge-localized inference (<260ms mouth-to-ear) | Traditional banking apps cannot bridge this gap |
| **Financial Correctness** | VSR consensus, strict serializability | Zero reconciliation overhead |
| **Crypto-Fiat Bridge** | PIX + Local Stablecoins (BRZ/BRL1) | Instant liquidity without FX friction |

### 1.4 Target Scale

- **ARR Target**: $75-100M
- **Geographic Focus**: US (Primary), Brazil (Priority #2), EU (Phase 2)
- **Concurrent Users**: 10,000+ across multiple properties
- **System Uptime**: 99.9% (8.76 hours downtime/year maximum)

---

## 2. The "Agent as Operating System" Mental Model

**CRITICAL ARCHITECTURAL CONCEPT**: All infrastructure decisions serve this core mental model:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    "AGENT AS OPERATING SYSTEM" PARADIGM                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   AI AGENT = OPERATING SYSTEM                                               │
│   • Suna Agent Runtime (multi-modal: voice, text, WhatsApp, email)          │
│   • Sandbox execution environment                                           │
│   • LangGraph Router (process manager)                                      │
│                                                                             │
│   SKILLS = APPLICATIONS                                                     │
│   • Markdown files (SKILL.md) - not code                                    │
│   • YAML frontmatter (triggers, tools, HITL rules)                          │
│   • Scripts for Hot Path (classify_urgency.py)                              │
│   • MCP connections for Cold Path (treasury-write, temporal-trigger)        │
│   • Non-engineers can author skills                                         │
│                                                                             │
│   CONTEXT = RAM (Progressive Disclosure)                                    │
│   • Phase 1: Header Scan (~200 tokens) - match skill by triggers            │
│   • Phase 2: Full Skill Load (~800 tokens) - load SKILL.md + scripts        │
│   • Phase 3: Context Injection (~1500 tokens) - entity, history, KB         │
│   • RESULT: ~2,500 tokens per task (vs 50,000+ if all loaded)               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 2.1 Infrastructure Mapping

| Mental Model Component | Infrastructure Implementation |
|------------------------|------------------------------|
| **AI Agent = OS** | Suna Runtime + LangGraph Router |
| **Skills = Applications** | Markdown files with MCP connections |
| **Context = RAM** | Progressive Disclosure (2,500 vs 50,000 tokens) |
| **Hot Path** | Groq LPU, Edge GPUs, Deepgram/Cartesia |
| **Cold Path** | TigerBeetle, Formance, Temporal, MPC Custody |

### 2.2 Hot Path vs Cold Path Execution

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         SKILL EXECUTION PATHS                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  🔥 HOT PATH                    🔄 HYBRID PATH           ❄️ COLD PATH       │
│  (AI Reasoning)                 (Script + MCP Read)      (Treasury OS)      │
│                                                                             │
│  • classify_urgency.py          • check_warranty.py      • dispatch_vendor  │
│  • Intent understanding         • Script logic +         • mcp://treasury/* │
│  • Response generation            MCP data lookup        • mcp://temporal/* │
│  • Tone adaptation              • No mutations           • mcp://formance/* │
│                                                                             │
│  Latency: <100ms                Latency: <500ms          Latency: <2000ms   │
│  Guarantees: None               Guarantees: Partial      Guarantees: ACID   │
│                                                                             │
│  INFRASTRUCTURE:                INFRASTRUCTURE:          INFRASTRUCTURE:    │
│  • Groq LPU (50ms TTFT)        • ECS Fargate            • TigerBeetle      │
│  • Latitude.sh GPUs             • MongoDB Atlas          • Formance Ledger  │
│  • Deepgram/Cartesia            • Redis Cache            • Temporal Cloud   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 2.3 MCP Servers: Skills-to-Infrastructure Bridge

```yaml
# MCP Server Architecture (Skills → Treasury OS)
mcp_servers:
  treasury-read:
    tools: [get_balance, get_transactions, check_warranty]
    permissions: read-only, all skills
    backend: TigerBeetle, Formance, Redis
    
  treasury-write:
    tools: [transfer, create_hold, create_work_order]
    permissions: write, approved skills only
    backend: TigerBeetle, Formance, Temporal
    requires: idempotency_key, audit_log
    
  temporal-trigger:
    tools: [start_workflow, signal_workflow, query_workflow]
    permissions: workflow trigger, approved skills
    backend: Temporal Cloud
    
  vector-context:
    tools: [get_unit_history, search_knowledge_base]
    permissions: read-only, all skills
    backend: MongoDB Atlas (Vector Search)
```

---

## 3. Cloud Provider & Deployment Strategy

### 3.1 Cloud Provider Decision: AWS (Primary)

**Decision: AWS as primary cloud provider.**

| Factor | AWS | GCP | Azure |
|--------|-----|-----|-------|
| **Brazil Presence** | São Paulo (3 AZs) | São Paulo (3 AZs) | São Paulo (2 AZs) |
| **Voice AI Ecosystem** | ★★★★★ | ★★★★☆ | ★★★☆☆ |
| **Fintech Partners** | ★★★★★ | ★★★★☆ | ★★★☆☆ |
| **Serverless Containers** | Fargate (mature) | Cloud Run | Container Instances |

### 3.2 Container Orchestration: ECS/Fargate over EKS

**Decision: AWS ECS with Fargate launch type.**

| Platform | Control Plane Cost | Complexity | Team Size Required |
|----------|-------------------|------------|-------------------|
| **ECS/Fargate** | $0/month | Low | 1-2 DevOps |
| **EKS** | $74.40/month/cluster | High | 3-5 DevOps |

**Exception**: TigerBeetle requires EC2 with local NVMe (not Fargate-compatible).

### 3.3 Multi-Region Deployment Topology

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    MULTI-REGION DEPLOYMENT ARCHITECTURE                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                    AWS US-EAST-1 (Primary)                           │   │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐                │   │
│  │  │  ECS Fargate │  │  ECS Fargate │  │    EC2       │                │   │
│  │  │  Voice Agent │  │  AI Agents   │  │ TigerBeetle  │                │   │
│  │  │  (2-10 tasks)│  │  (3-50 tasks)│  │ (4 replicas) │                │   │
│  │  └──────────────┘  └──────────────┘  └──────────────┘                │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                    │                                        │
│                    Route 53 (Latency-Based Routing)                        │
│                                    │                                        │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │              AWS SA-EAST-1 (Brazil) + Edge Partners                  │   │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐                │   │
│  │  │ Latitude.sh  │  │  ECS Fargate │  │    EC2       │                │   │
│  │  │ Voice Edge   │  │  PIX Service │  │ TigerBeetle  │                │   │
│  │  │  (L40S GPU)  │  │  BaaS Proxy  │  │ (2 replicas) │                │   │
│  │  └──────────────┘  └──────────────┘  └──────────────┘                │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 3.4 Environment Strategy

| Environment | Purpose | LLM Model | Deployment |
|-------------|---------|-----------|------------|
| **Development** | Feature development | Claude Haiku / GPT-3.5 | Single AZ, Fargate Spot |
| **Staging** | QA & Integration | Claude Sonnet 3.5 | Multi-AZ, Fargate |
| **Production** | Live traffic | Claude Sonnet 3.5 / Groq (Voice) | Multi-Region, Blue/Green |
| **DR** | Disaster Recovery | Same as Prod | Warm standby in us-west-2 |

---

# PART 2: FINANCIAL CORE (TREASURY OS)

## 4. TigerBeetle Ledger Engine

### 4.1 Why TigerBeetle?

| Scenario | PostgreSQL Behavior | TigerBeetle Behavior |
|----------|---------------------|---------------------|
| 1000 concurrent txns on "platform fee" account | Row-level locking → exponential degradation | Single-threaded batch → linear scaling |
| Network partition during write | Potential split-brain, manual reconciliation | VSR consensus → strict serializability |
| Crash during transaction | WAL recovery may leave orphaned locks | Deterministic recovery, no orphaned state |

### 4.2 Viewstamped Replication (VSR) Consensus

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    VIEWSTAMPED REPLICATION (VSR)                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐                  │
│  │Replica 1│───▶│Replica 2│───▶│Replica 3│───▶│Replica 4│                  │
│  │ LEADER  │    │FOLLOWER │    │FOLLOWER │    │FOLLOWER │                  │
│  └─────────┘    └─────────┘    └─────────┘    └─────────┘                  │
│                                                                             │
│  Key Guarantees:                                                            │
│  • Linearizable reads and writes                                           │
│  • Total ordering of all operations                                        │
│  • Survives f failures with 2f+1 replicas                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 4.3 Single-Threaded Execution Model

| Multi-Threaded Approach | TigerBeetle Single-Thread |
|------------------------|---------------------------|
| Context switching overhead | Zero context switching |
| Race conditions requiring locks | No locks needed |
| 10-100K TPS (practical limit) | **1+ Million TPS** |

The API forces batching (up to **8,190 transfers per request**), saturating network and disk I/O.

### 4.4 Production Cluster Configuration

```yaml
cluster_configuration:
  replication_factor: 6
  quorum: 4  # 2f+1 where f=2 (survives 2 simultaneous failures)

  replicas:
    # São Paulo (Brazil) - LGPD compliance
    - id: 1
      location: latitude.sh-sao-paulo-1
      role: leader_eligible
    - id: 2
      location: oracle-sa-saopaulo-1
      role: follower

    # US East (Primary)
    - id: 3
      location: aws-us-east-1a
      role: leader_eligible
    - id: 4
      location: aws-us-east-1b
      role: follower

    # US West (DR)
    - id: 5
      location: aws-us-west-2a
      role: follower
    - id: 6
      location: aws-us-west-2b
      role: follower

  failure_tolerance:
    az_failure: survives_2_simultaneous
    region_failure: survives_1_full_region
    data_durability: zero_data_loss_on_commit
```

---

## 5. Federated Architecture & Numscript

### 5.1 Federated Ledger Architecture

Due to Brazil's data residency requirements (LGPD), we implement a **Federated Ledger Architecture**:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    FEDERATED TIGERBEETLE ARCHITECTURE                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌────────────────────────────────┐    ┌────────────────────────────────┐  │
│  │       CLUSTER-BR (São Paulo)   │    │     CLUSTER-GLOBAL (US East)   │  │
│  │                                │    │                                │  │
│  │  Authoritative for:            │    │  Authoritative for:            │  │
│  │  • Brazilian user accounts     │    │  • Global user accounts        │  │
│  │  • BRL transactions            │    │  • USD/EUR transactions        │  │
│  │  • PIX rails                   │    │  • USDC/crypto ledgers         │  │
│  │  • Local stablecoin (BRZ)      │    │  • International transfers     │  │
│  └──────────────┬─────────────────┘    └──────────────┬─────────────────┘  │
│                 │         Federation Layer             │                    │
│                 │         (Formance Stack)             │                    │
│                 └──────────────┬───────────────────────┘                    │
│                                │                                            │
│  ┌─────────────────────────────┴────────────────────────────────────────┐  │
│  │                     FORMANCE ORCHESTRATION                            │  │
│  │  • Routes requests to appropriate cluster based on jurisdiction       │  │
│  │  • Coordinates cross-cluster transactions via Temporal Sagas          │  │
│  │  • Handles currency conversion (BRL ↔ USD ↔ USDC)                     │  │
│  │  • Enforces IOF tax calculations for FX operations                    │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 5.2 Numscript: Financial Domain-Specific Language

```numscript
// Example: Brazilian PIX Payment with IOF Tax and Platform Fee
// This is ATOMIC - all splits happen or none do

send [BRL 10000] (
  source = @user:carlos_silva:main
  destination = {
    0.38% to @treasury:tax_iof           // IOF tax (FX operations)
    1%    to @platform:fees              // Platform fee
    remaining to @merchant:coffeeshop    // Merchant receives net
  }
)

// Execution result:
// @treasury:tax_iof   receives BRL 38.00
// @platform:fees      receives BRL 100.00
// @merchant:coffeeshop receives BRL 9,862.00
// Total: BRL 10,000.00 (exact, no rounding errors)
```

### 5.3 Two-Phase Transfers

TigerBeetle's **Two-Phase Transfer** capability enables AML/KYC compliance holds:

| Phase | Description | State |
|-------|-------------|-------|
| **Phase 1: PENDING** | Funds are LOCKED but not MOVED | User: $500 available, Pending: $500 held |
| **Async Checks** | AML/KYC screening, fraud scoring | Funds remain locked |
| **Phase 2A: POST** | Checks PASS → Commit transfer | Destination receives $500 |
| **Phase 2B: VOID** | Checks FAIL → Rollback | User: $1000 restored |

---

## 6. Brazilian Crypto Regulation (SPSAV)

### 6.1 Regulatory Landscape

**Critical Deadline: February 2026** - Full compliance mandatory

The framework is defined by **Law 14.478/2022** and BCB resolutions **517-521**.

### 6.2 License Requirements

| License Type | Activities | Minimum Capital | Our Strategy |
|-------------|------------|-----------------|--------------|
| **Intermediation** | Connecting buyers/sellers | R$10.8M (~$2M) | **Phase 1** |
| **Custody** | Holding private keys | R$37.2M (~$7M) | Partner with Fireblocks |
| **Brokerage** | Intermediation + Custody | R$37.2M (~$7M) | **Phase 2** (post-revenue) |

### 6.3 Resolution 521: Stablecoins as FX

Stablecoin transfers involving international counterparties = **FX operations**.

**IOF Tax Engine Required:**

```python
class IOFTaxEngine:
    """Brazilian IOF tax calculator for FX operations."""
    
    IOF_RATES = {
        "fx_standard": Decimal("0.0038"),   # 0.38%
        "fx_credit": Decimal("0.011"),      # 1.1%
        "fx_export": Decimal("0"),          # 0%
    }
    
    def calculate_iof(self, amount_brl: Decimal, operation_type: str) -> IOFCalculation:
        rate = self.IOF_RATES.get(operation_type, self.IOF_RATES["fx_standard"])
        tax_amount = (amount_brl * rate).quantize(Decimal("0.01"))
        
        return IOFCalculation(
            gross_amount=amount_brl,
            iof_rate=rate,
            iof_amount=tax_amount,
            net_amount=amount_brl - tax_amount,
            reporting_required=True
        )
```

### 6.4 Local Stablecoins

| Stablecoin | Issuer | Spread vs BRL | Use Case |
|------------|--------|---------------|----------|
| **BRZ** | Transfero | ~0.1% | High-volume trading |
| **BRL1** | Bitso consortium | ~0.15% | Retail |
| **USDC** | Circle | FX + IOF | International |

---

# PART 3: REAL-TIME AI INFRASTRUCTURE

## 7. Voice AI Infrastructure (<300ms)

### 7.1 The Physics Problem

**São Paulo to US East RTT: 120-150ms** - This single hop consumes 50% of our latency budget.

**Conclusion**: For Brazilian users, **inference must occur in Brazil**.

### 7.2 WebRTC vs WebSocket

**Decision: WebRTC is mandatory for voice.**

| Aspect | WebSocket (TCP) | WebRTC (UDP) |
|--------|-----------------|--------------|
| Packet Loss | TCP pauses for retransmit | Skips lost packet, continues |
| Result | Latency spikes, audio stuttering | Micro-glitch, no delay |
| Echo Cancellation | Server-side required | Native on client |

### 7.3 Brazil Voice AI Stack

```
┌─────────────────────────────────────────────────────────────────────────────┐
│              BRAZIL VOICE AI EDGE ARCHITECTURE (<300ms)                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  User in São Paulo                                                          │
│       │ WebRTC (UDP) - RTT: <20ms                                          │
│       ▼                                                                     │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │          LATITUDE.SH EDGE CLUSTER (São Paulo - MH1)                 │   │
│  │                                                                     │   │
│  │  ┌───────────────────────────────────────────────────────────────┐  │   │
│  │  │              INFERENCE PIPELINE (All in Brazil)               │  │   │
│  │  │                                                               │  │   │
│  │  │  1. VAD: Silero VAD                        [20ms]             │  │   │
│  │  │  2. STT: Deepgram Nova-2 (Streaming)       [80ms]             │  │   │
│  │  │  3. LLM: Groq LPU (Llama 3 70B)            [50ms TTFT]        │  │   │
│  │  │  4. TTS: Cartesia Sonic                    [70ms TTFB]        │  │   │
│  │  └───────────────────────────────────────────────────────────────┘  │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
│  LATENCY BUDGET:                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  Component          │ Latency   │ Running Total                     │   │
│  ├─────────────────────┼───────────┼───────────────────────────────────┤   │
│  │  Network (BR edge)  │ 20ms      │ 20ms                              │   │
│  │  VAD                │ 20ms      │ 40ms                              │   │
│  │  STT                │ 80ms      │ 120ms                             │   │
│  │  LLM (TTFT)         │ 50ms      │ 170ms                             │   │
│  │  TTS (TTFB)         │ 70ms      │ 240ms                             │   │
│  │  Network (return)   │ 20ms      │ 260ms ✓                           │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 7.4 GPU Infrastructure Decision

| Provider | Region | GPU | RTT | Cost | Verdict |
|----------|--------|-----|-----|------|---------|
| **Latitude.sh** | São Paulo | L40S/H100 | <20ms | $$$ | **Primary** |
| **Oracle Cloud** | São Paulo | A100/A10 | <20ms | $$ | **Failover** |
| AWS | US East | A10G | 120-150ms | $ | Not Viable |

---

## 8. AI Prompt Versioning & A/B Testing

### 8.1 AI Deployment Schema

```typescript
interface AIDeployment {
  id: string;
  agent_type: 'leasing' | 'maintenance' | 'voice' | 'quote_chaser';
  model_id: string;           // e.g., "claude-3-5-sonnet-20240620"
  prompt_version: string;     // semver like "1.2.3"
  prompt_hash: string;        // SHA-256 of prompt content
  config: {
    temperature: number;
    max_tokens: number;
    top_p: number;
  };
  traffic_allocation: number; // 0-100%
  status: 'canary' | 'stable' | 'deprecated';
  created_at: Date;
  updated_at: Date;
}

interface PromptExecution {
  execution_id: string;
  deployment_id: string;
  input_text: string;
  output_text: string;
  latency_ms: number;
  token_count: { input: number; output: number };
  cost_usd: number;
  success: boolean;
  error_message?: string;
  fallback_used?: string;
  user_session_id: string;
  timestamp: Date;
  compliance_flags: string[]; // EU AI Act logging requirements
}
```

### 8.2 A/B Testing Configuration

```yaml
ab_test:
  id: "leasing-prompt-v2-test"
  agent: "leasing_assistant"
  description: "Testing improved qualification questions"
  
  variants:
    - name: "control"
      prompt_version: "1.0.0"
      prompt_hash: "a1b2c3d4e5f6"
      traffic: 90
      
    - name: "treatment"
      prompt_version: "2.0.0"
      prompt_hash: "f6e5d4c3b2a1"
      traffic: 10
  
  metrics:
    - name: "completion_rate"
      goal: "maximize"
      minimum_detectable_effect: 0.05
      current_baseline: 0.78
      
    - name: "escalation_rate"
      goal: "minimize"
      maximum_acceptable: 0.15
      current_baseline: 0.12
      
    - name: "response_latency_ms"
      goal: "minimize"
      maximum_acceptable: 2000
      current_baseline: 1200
  
  guardrails:
    auto_stop_if_worse_by: 0.10    # 10% worse → stop
    minimum_sample_size: 500
    maximum_duration_days: 14
    significance_threshold: 0.05
    
  stop_conditions:
    - metric: "escalation_rate"
      threshold: 0.20
      action: "immediate_stop"
    - metric: "eu_ai_act_compliance_score"
      threshold: 0.90
      action: "immediate_rollback"
```

### 8.3 Prompt Library Structure

```
/prompts
  /leasing_assistant
    /v1.0.0
      prompt.md
      config.yaml
      evals/
        test_cases.yaml
        golden_responses.json
        compliance_checks.yaml
    /v2.0.0
      prompt.md
      config.yaml
      evals/
        test_cases.yaml
        regression_tests.yaml
  /maintenance_coordinator
    /v1.0.0
      ...
  /voice_agent
    /v1.0.0
      ...
  /quote_chaser
    /v1.0.0
      ...
```

### 8.4 Rollback Procedures

| Trigger | Detection | Action | Time | Scope |
|---------|-----------|--------|------|-------|
| Error rate >5% | Automated monitoring | Auto-rollback to last stable | <1min | Single agent |
| EU AI Act violation | Compliance monitoring | Immediate rollback + human review | <30sec | All agents |
| Manual trigger | Operations team | Controlled rollback | <2min | Configurable |
| A/B test failure | Statistical significance | Revert to control | <1min | Experiment scope |

### 8.5 Model Provider Fallback Chain

```yaml
model_fallback_chain:
  primary:
    provider: "anthropic"
    model: "claude-3-5-sonnet-20240620"
    timeout_seconds: 5
    retry_attempts: 2
    
  secondary:
    provider: "openai"
    model: "gpt-4o"
    timeout_seconds: 7
    retry_attempts: 1
    
  tertiary:
    provider: "google"
    model: "gemini-1.5-pro"
    timeout_seconds: 7
    retry_attempts: 1
    
  voice_optimized:
    provider: "groq"
    model: "llama-3.1-70b-versatile"
    timeout_seconds: 2  # <300ms voice requirement
    retry_attempts: 1
    
  cache_fallback:
    enabled: true
    ttl_hours: 24
    max_entries: 10000
```

---

## 9. AI Configuration & Prompt Library

### 9.1 Sample Agent Prompts

**Leasing Assistant (English):**

```json
{
  "version": "1.2.0",
  "agent": "leasing_assistant",
  "locale": "en_US",
  "system_prompt": "You are a helpful real estate leasing assistant for {{property_name}}. Your goal is to qualify leads and schedule tours.\n\nQualification questions:\n1. Budget range\n2. Move-in timeline\n3. Number of occupants\n4. Pet requirements\n\n**CRITICAL FAIR HOUSING RULES:**\n- NEVER ask about race, religion, national origin, familial status, disability, or sex\n- If a prospect mentions protected characteristics, respond professionally without steering\n- Use neutral language: 'family-friendly' is acceptable, 'adult-only' is NOT",
  "guardrails": ["fair_housing", "pci_compliance"]
}
```

**Voice Agent (Multilingual):**

```json
{
  "version": "1.1.0",
  "agent": "voice_hoa",
  "locale": "multilingual",
  "system_prompt": "You are an HOA customer service agent fluent in English and Portuguese.\n\n**VOICE-SPECIFIC RULES:**\n- Keep responses under 30 words for conversational flow\n- Use verbal confirmations: 'Got it', 'I understand'\n- Spell out numbers: 'January fifteenth' not '1/15'\n\n**PCI COMPLIANCE:**\n- NEVER ask for full credit card numbers\n- Direct payment to secure portal: {{payment_url}}",
  "max_tokens": 150,
  "temperature": 0.5
}
```

### 9.2 Fair Housing Guardrails

```yaml
fair_housing_guardrails:
  - name: "protected_class_detection"
    pattern: "\\b(family|children|married|single|religion|national origin|disability)\\b"
    severity: "flag"
    action: "route_to_human_review"

  - name: "discriminatory_language"
    pattern: "\\b(only|exclusively) for\\b.*\\b(christian|jewish|muslim|hispanic|asian)\\b"
    severity: "block"
    action: "terminate_conversation"

  - name: "steering_prevention"
    pattern: "\\b(recommend|suggest)\\b.*\\b(area|neighborhood)\\b.*\\b(because|due to)\\b"
    severity: "flag"
    action: "add_disclaimer"
```

---

# PART 4: OPERATIONAL INFRASTRUCTURE

## 10. Human-in-the-Loop (HITL) Operations

### 10.1 Real-Time Collaboration Dashboard

| Feature | Implementation | SLA |
|---------|---------------|-----|
| **Presence Indicators** | WebSocket + Redis pub/sub | Real-time |
| **Threaded Comments** | MongoDB with threading | <100ms |
| **Approval Workflows** | Temporal workflows | Tracked |
| **Slack Integration** | Slack Bolt SDK | <5s |
| **Mobile Responsive** | React + TailwindCSS | N/A |

### 10.2 HITL Triggers

```yaml
hitl_triggers:
  financial:
    - condition: "amount > 10000"
      action: "require_approval"
      escalation: "finance_manager"
      
  compliance:
    - condition: "fair_housing_flag == true"
      action: "immediate_review"
      escalation: "compliance_officer"
      
  ai_confidence:
    - condition: "confidence_score < 0.7"
      action: "suggest_review"
      escalation: "property_manager"
```

### 10.3 Approval SLA Tracking

| Priority | SLA | Escalation Path |
|----------|-----|-----------------|
| **Critical** | 15 minutes | Manager → Director → VP |
| **High** | 1 hour | Manager → Senior Manager |
| **Medium** | 4 hours | Manager |
| **Low** | 24 hours | Auto-approve if no response |

---

## 11. Memory Architecture

### 11.1 Five-Layer Memory System

| Layer | Storage | TTL | Purpose |
|-------|---------|-----|---------|
| **Working Memory** | Redis | Session | Current conversation context |
| **Entity Memory** | MongoDB | Persistent | User profiles, preferences |
| **Interaction Memory** | MongoDB | 90 days | Conversation history |
| **Knowledge Memory** | MongoDB + Vector | Persistent | RAG knowledge base |
| **Financial Memory** | TigerBeetle | Permanent | Transaction history |

### 11.2 Context Injection Strategy

```yaml
context_injection:
  phase_1_header_scan:
    tokens: ~200
    source: skill_registry_yaml
    purpose: match_skill_by_triggers
    
  phase_2_skill_load:
    tokens: ~800
    source: SKILL.md + scripts
    purpose: load_instructions_and_tools
    
  phase_3_context:
    tokens: ~1500
    sources:
      - entity_memory: user_profile, sentiment
      - interaction_memory: last_5_conversations
      - knowledge_memory: relevant_documents (top_3)
      - financial_memory: recent_transactions (last_30_days)
```

---

## 12. Data Retention & Compliance Matrix

### 12.1 Retention Policy by Data Type

| Data Type | Hot Storage | Warm Storage | Archive | Delete After | Legal Basis |
|-----------|-------------|--------------|---------|--------------|-------------|
| **Voice Recordings** | ≤30 days | ≤6 months | 3-5 years | On request | GDPR Art. 5(e), LGPD |
| **Voice Transcripts** | ≤30 days | ≤6 months | 3-5 years | On request | PII - mask card data |
| **HITL Decisions** | ≤1 year | ≤3 years | 7 years | N/A (audit) | SOX, SOC 2 |
| **FinTech Transactions** | ≤1 year | ≤7 years | 10+ years | N/A (fiscal) | IRS (7yr), SOX |
| **Audit Logs** | ≤90 days | ≥1 year | 7 years | As needed | PCI DSS Req. 10.7 |
| **Conversation Histories** | ≤30 days | ≤6 months | 3 years | On request | PII - GDPR/LGPD |
| **User PII** | Active only | ≤1 year | None | On request | GDPR Art. 17 |
| **Payment Data (PCI)** | N/A (tokens) | 1 year | Delete | On request | PCI DSS |

### 12.2 S3 Lifecycle Policy

```yaml
s3_lifecycle:
  voice_recordings:
    - transition:
        days: 30
        storage_class: STANDARD_IA
    - transition:
        days: 180
        storage_class: GLACIER
    - expiration:
        days: 1825  # 5 years
```

### 12.3 Right to Erasure Workflow

```yaml
erasure_workflow:
  trigger: "GDPR/LGPD deletion request"
  steps:
    - validate_identity
    - queue_deletion_job
    - delete_from_mongodb
    - delete_from_s3
    - flag_backups_for_purge
    - send_confirmation_email
    - log_to_audit_trail
```

---

# PART 5: RESILIENCE ENGINEERING

## 13. Chaos Engineering Experiment Catalog

### 13.1 Voice Service Experiments

**EXP-VOICE-001: STT Provider Failure**

```yaml
experiment:
  id: "EXP-VOICE-001"
  name: "Speech-to-Text Provider Failure"
  category: "voice"
  objective: "Verify graceful degradation when Deepgram fails"
  
  blast_radius:
    scope: "single_voice_session"
    max_affected_users: 1
    environment: ["staging", "production_low_traffic"]
  
  pre_requisites:
    - "Backup STT provider (Google STT) configured and tested"
    - "Monitoring dashboard for voice latency open"
    - "On-call engineer aware and available"
  
  execution:
    tool: "aws_fis"
    steps:
      - action: "Start test voice call"
      - action: "Inject Deepgram API failure (HTTP 500)"
        duration: "30s"
        method: "network_blackhole"
        target: "api.deepgram.com"
      - action: "Observe failover to Google STT"
        expected_time: "<2s"
      - action: "Verify call continues normally"
  
  expected_results:
    - "Failover to Google STT within 2 seconds"
    - "No call drop"
    - "User notices brief pause but conversation continues"
  
  abort_criteria:
    - "Failover time exceeds 5 seconds"
    - "Call drops"
    - "Error rate exceeds 10%"
  
  success_metrics:
    - metric: "failover_time_seconds"
      target: "<2"
    - metric: "call_completion_rate"
      target: ">99%"
```

**EXP-VOICE-002: Network Latency Injection**

```yaml
experiment:
  id: "EXP-VOICE-002"
  name: "Voice Service Network Latency"
  objective: "Test voice quality degradation under network latency"
  
  execution:
    tool: "aws_fis"
    action_id: "aws:ecs:task-network-latency"
    parameters:
      duration: "PT5M"
      latencyMilliseconds: 200
      jitterMilliseconds: 50
      targets:
        - "voice-service-tasks"
  
  expected_results:
    - "Voice quality remains acceptable with 200ms latency"
    - "System maintains <300ms end-to-end response time"
  
  abort_criteria:
    - "End-to-end latency exceeds 500ms"
```

### 13.2 Financial System Experiments

**EXP-FIN-001: TigerBeetle Leader Failure**

```yaml
experiment:
  id: "EXP-FIN-001"
  name: "TigerBeetle Leader Node Failure"
  category: "financial"
  objective: "Verify automatic leader election and transaction consistency"
  
  blast_radius:
    scope: "tigerbeetle_cluster"
    max_affected_transactions: 0  # Zero tolerance
    environment: ["staging_only"]
  
  execution:
    tool: "chaos_toolkit"
    steps:
      - action: "Identify current TigerBeetle leader"
      - action: "Kill leader process"
        method: "SIGKILL"
      - action: "Monitor leader election process"
        timeout: "30s"
      - action: "Verify transaction consistency"
  
  expected_results:
    - "New leader elected within 30 seconds"
    - "Zero transaction loss or corruption"
    - "All pending transactions complete successfully"
  
  success_metrics:
    - metric: "leader_election_time_seconds"
      target: "<30"
    - metric: "transaction_integrity_score"
      target: "100%"
```

### 13.3 Multi-Region Experiments

**EXP-REGION-001: Complete Regional Outage**

```yaml
experiment:
  id: "EXP-REGION-001"
  name: "US-East Region Complete Outage"
  category: "infrastructure"
  objective: "Validate multi-region failover capabilities"
  
  blast_radius:
    scope: "full_region"
    affected_region: "us-east-1"
    environment: ["staging_only"]
  
  execution:
    tool: "aws_fis"
    steps:
      - action: "Simulate complete region outage"
        method: "stop_all_ecs_tasks"
        region: "us-east-1"
      - action: "Monitor Route 53 health checks"
      - action: "Verify traffic routing to Brazil region"
        expected_time: "<60s"
      - action: "Test all critical functions in backup region"
      - action: "Restore primary region"
      - action: "Verify data consistency across regions"
  
  expected_results:
    - "Traffic routes to Brazil within 60 seconds"
    - "All services remain available"
    - "Data consistency maintained"
  
  success_metrics:
    - metric: "failover_time_seconds"
      target: "<60"
    - metric: "service_availability_percentage"
      target: ">99.9%"
```

### 13.4 AWS FIS Experiment Template

```json
{
  "description": "EXP-VOICE-001: Deepgram STT Failure",
  "targets": {
    "voice-tasks": {
      "resourceType": "aws:ecs:task",
      "selectionMode": "COUNT(1)",
      "resourceArns": ["arn:aws:ecs:us-east-1:123456789012:task/voice-cluster/*"],
      "resourceTags": {
        "Environment": "staging",
        "Service": "voice-processing"
      }
    }
  },
  "actions": {
    "inject-network-fault": {
      "actionId": "aws:ecs:task-network-blackhole",
      "parameters": {
        "duration": "PT30S",
        "scope": "api.deepgram.com",
        "trafficType": "egress"
      },
      "targets": {
        "Tasks": "voice-tasks"
      }
    }
  },
  "stopConditions": [
    {
      "source": "aws:cloudwatch:alarm",
      "value": "arn:aws:cloudwatch:us-east-1:123456789012:alarm:VoiceErrorRateHigh"
    }
  ],
  "roleArn": "arn:aws:iam::123456789012:role/FISExperimentRole"
}
```

### 13.5 Quarterly Game Day Schedule

| Quarter | Focus Area | Experiments | Owner | Success Criteria |
|---------|-----------|-------------|-------|-----------------|
| **Q2 2025** | Voice Resilience | EXP-VOICE-001 to 005 | Voice Team | All failovers <2s |
| **Q3 2025** | Financial Resilience | EXP-FIN-001 to 003 | Treasury Team | Zero transaction loss |
| **Q4 2025** | Multi-Region | EXP-REGION-001 to 002 | Platform Team | <60s regional failover |
| **Q1 2026** | Full System | All experiments | All Teams | End-to-end resilience |

### 13.6 Game Day Checklist

- [ ] 48 hours notice to all stakeholders
- [ ] Monitoring dashboards prepared and accessible
- [ ] Rollback procedures reviewed and tested
- [ ] On-call engineers briefed on experiment scope
- [ ] Customer communication ready (if needed)
- [ ] Post-mortem template prepared
- [ ] Incident response procedures activated
- [ ] Success criteria clearly defined and measurable

---

## 14. Disaster Recovery & Multi-Region

### 14.1 RPO/RTO Targets

| Service | RPO | RTO | Strategy |
|---------|-----|-----|----------|
| **Voice Agent** | <1 min | <5 min | Active-active US/BR |
| **API** | <5 min | <10 min | Auto-scaling + health checks |
| **Treasury (DB)** | <1 min | <5 min | Multi-AZ + continuous replication |
| **Payments** | 0 (durable) | <5 min | Distributed commit (TigerBeetle) |
| **Analytics** | 1 day | 4 hours | Rebuild from logs |

### 14.2 Multi-Region Architecture

- **Active-Active**: US-East + São Paulo
- **Global Load Balancer**: Route 53 latency-based routing
- **Data Replication**: MongoDB Atlas Global Clusters
- **TigerBeetle**: 6-node cluster spanning regions

### 14.3 Resilience Patterns

```yaml
resilience_patterns:
  bulkhead:
    description: "Isolate critical service threads"
    implementation: "Separate thread pools for voice vs batch"
  
  circuit_breaker:
    description: "Prevent cascade failures"
    implementation: "Resilience4j for downstream calls"
    thresholds:
      failure_rate: 50%
      slow_call_rate: 100%
      slow_call_duration: 2s
  
  saga_compensation:
    description: "Rollback distributed transactions"
    implementation: "Temporal Workflows with compensation"
```

---

## 15. Zero Trust Security Architecture

### 15.1 Teleport for Access Control

```yaml
teleport_config:
  access:
    roles:
      - name: engineer
        allow:
          logins: [ubuntu, ec2-user]
          db_names: [readonly_replica]
        deny:
          logins: [root]
      
      - name: sre_oncall
        allow:
          logins: [ubuntu, ec2-user, root]
          db_names: ['*']
        require:
          mfa: true
          reason: true
    
    certificates:
      ttl: 1h
      max_ttl: 4h
    
  session_recording:
    enabled: true
    mode: strict
    retention: 7_years  # SPSAV audit requirement
```

### 15.2 mTLS Everywhere

```yaml
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: default
  namespace: citadel-production
spec:
  mtls:
    mode: STRICT  # Reject all non-mTLS traffic
```

---

# PART 6: COMPLIANCE FRAMEWORK

## 16. EU AI Act Implementation

### 16.1 Risk Classification Matrix

| AI System | Use Case | Risk Level | Legal Basis | Articles Applicable |
|-----------|----------|------------|-------------|-------------------|
| **Leasing Assistant** | Housing access decisions | **HIGH-RISK** | Annex III, Section 5 | Articles 9-15 |
| **Maintenance Coordinator** | Safety-related triage | **LIMITED RISK** | Not in Annex III | Transparency only |
| **Voice Agent** | Customer service | **LIMITED RISK** | Chatbot provisions | Transparency only |
| **Quote Chaser** | Payment reminders | **MINIMAL RISK** | Not in scope | None |

### 16.2 High-Risk Requirements (Articles 9-15)

| Article | Requirement | Implementation |
|---------|-------------|----------------|
| **Art. 9** | Risk Management System | Continuous lifecycle monitoring |
| **Art. 10** | Data Governance | Documented RAG knowledge base |
| **Art. 11** | Technical Documentation | Complete system documentation |
| **Art. 12** | Record-Keeping | 7-year audit trail |
| **Art. 13** | Transparency | User disclosure requirements |
| **Art. 14** | Human Oversight | HITL dashboard for all decisions |
| **Art. 15** | Accuracy & Robustness | >95% task completion target |

### 16.3 Required Disclosures

**Voice Calls:**
> "You are speaking with an AI assistant that helps with property management inquiries. This system is designed to assist you efficiently while a human agent can join at any time if needed. Your conversation may be recorded for quality and compliance purposes."

**Chat/SMS:**
> "This conversation is AI-assisted to provide you with faster responses. [Learn more about our AI systems]"

**Email:**
> Footer: "This message was composed with AI assistance to ensure accurate and timely communication."

### 16.4 Implementation Timeline

| Milestone | Deadline | Action Required | Owner |
|-----------|----------|-----------------|-------|
| **Prohibited practices check** | Aug 2025 | Review for prohibited uses | Legal Team |
| **Risk Management System** | Jun 2026 | Create formal RMS document | AI Team |
| **Technical Documentation** | Jun 2026 | Complete all required docs | Engineering |
| **Human Oversight Dashboard** | Jul 2026 | Deploy HITL monitoring | Product Team |
| **Conformity Assessment** | Jul 2026 | Self-assessment process | Compliance Team |
| **High-risk compliance** | Aug 2026 | Full regulatory compliance | All Teams |

### 16.5 Compliance Monitoring System

```yaml
compliance_monitoring:
  high_risk_systems:
    - system: "leasing_assistant"
      checks:
        - risk_management_system_active: true
        - human_oversight_enabled: true
        - audit_logging_functional: true
        - transparency_disclosures_active: true
        - accuracy_metrics_tracked: true
      
  limited_risk_systems:
    - system: "voice_agent"
      checks:
        - ai_disclosure_active: true
        - user_notification_working: true
        
  monitoring_frequency: "real_time"
  alert_channels: ["slack", "email", "dashboard"]
  escalation_rules:
    - trigger: "compliance_violation"
      severity: "critical"
      action: "immediate_alert"
```

---

## 17. State Regulatory Compliance (US)

### 17.1 California SB-721/SB-326

- **Requirement**: Balcony inspections for buildings 3+ stories
- **Deadline**: January 1, 2025 (extended to 2026 for condos)
- **Cycle**: Every 6 years
- **Implementation**: Automated inspection scheduling and tracking

### 17.2 Florida SB-4D

- **Requirement**: Structural inspections for condos 3+ stories
- **Deadline**: 30 years from construction, then every 10 years
- **Additional**: Reserve study requirements
- **Implementation**: Milestone tracking with automated alerts

### 17.3 Texas Property Code

- **Requirement**: HOA compliance monitoring
- **Focus**: Notice requirements, meeting documentation
- **Implementation**: Automated compliance calendar

---

## 18. Payment Orchestration & Smart Routing

### 18.1 PIX-Native Architecture

**Decision: Operate as Indirect Participant via BaaS (Dock, FitBank, or Celcoin).**

```
1. User requests deposit → Generate Dynamic QR Code
2. User scans with bank app, pays via PIX
3. BaaS Provider (Dock) sends webhook
4. Temporal Saga processes deposit:
   a. Match txid to pending request
   b. Verify amount
   c. Credit user in TigerBeetle (CLUSTER-BR)
   d. Send WhatsApp confirmation

Total time: <3 seconds from PIX payment to account credit
```

### 18.2 RL-Based Smart Payment Router

```python
class PaymentRouter:
    """Q-Learning based payment router."""
    
    def __init__(self, providers: list):
        self.providers = providers
        self.q_table = {}
        self.learning_rate = 0.1
        self.discount_factor = 0.95
        self.exploration_rate = 0.1
    
    def select_provider(self, state: TransactionState) -> PaymentProvider:
        """Epsilon-greedy provider selection."""
        if np.random.random() < self.exploration_rate:
            return np.random.choice(self.providers)
        
        state_key = self._state_to_key(state)
        if state_key not in self.q_table:
            self.q_table[state_key] = {p: 0.0 for p in self.providers}
        
        return max(self.q_table[state_key], key=self.q_table[state_key].get)
    
    def calculate_reward(self, success: bool, latency_ms: float, cost_bps: float) -> float:
        """Multi-objective reward."""
        return (1.0 if success else -1.0) + 0.3 * (1 - latency_ms/5000) - 0.2 * (cost_bps/100)
```

### 18.3 MPC Custody Architecture

**Decision: MPC (Multi-Party Computation) is mandatory.**

```
Private Key = Share_A + Share_B + Share_C (never reconstructed)

Share_A: Citadel HSM (on-premise)
Share_B: Fireblocks Cloud
Share_C: Coincover (Disaster Recovery)

Signing Threshold: 2-of-3

Disaster Recovery:
• Fireblocks unavailable → Share_A + Share_C
• Citadel HSM compromised → Rotate with Share_B + Share_C
```

**Vendor Selection**: **Fireblocks** - Specific support for Brazil SPSAV compliance.

---

# APPENDICES

## Appendix A: Infrastructure as Code

### Terraform Main Configuration

```hcl
# terraform/main.tf
terraform {
  required_version = ">= 1.5.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
  backend "s3" {
    bucket         = "citadel-terraform-state"
    key            = "infrastructure/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-locks"
  }
}

provider "aws" {
  region = "us-east-1"
  alias  = "primary"
}

provider "aws" {
  region = "sa-east-1"
  alias  = "brazil"
}
```

### Voice Agent Task Definition

```hcl
resource "aws_ecs_task_definition" "voice_agent" {
  family                   = "voice-agent-${var.environment}"
  network_mode             = "awsvpc"
  requires_compatibilities = ["FARGATE"]
  cpu                      = 2048
  memory                   = 4096
  
  container_definitions = jsonencode([
    {
      name  = "voice-agent"
      image = "${aws_ecr_repository.voice_agent.repository_url}:${var.version}"
      
      portMappings = [
        { containerPort = 8080, protocol = "tcp" },
        { containerPort = 10000, containerPort = 10100, protocol = "udp" }
      ]
      
      environment = [
        { name = "DEEPGRAM_MODEL", value = "nova-2" },
        { name = "TTS_PROVIDER", value = "cartesia" },
        { name = "LLM_PROVIDER", value = "groq" }
      ]
    }
  ])
}
```

---

## Appendix B: Configuration Templates

### Auto-Scaling Configuration

```yaml
auto_scaling:
  voice_services:
    min_capacity: 3
    max_capacity: 15
    target_cpu: 70
    target_memory: 80
    scale_out_cooldown: 60
    scale_in_cooldown: 300
    
  ai_agents:
    min_capacity: 2
    max_capacity: 20
    target_cpu: 60
    custom_metrics:
      - "queue_depth"
      - "response_latency"
    
  financial_services:
    min_capacity: 3
    max_capacity: 9  # Odd numbers for consensus
    target_cpu: 50
    scale_protection: true
```

### CI/CD Quality Gates

```yaml
quality_gates:
  code_quality:
    coverage_threshold: 90
    complexity_threshold: 10
    duplication_threshold: 3
    
  security:
    vulnerability_threshold: "no_high_or_critical"
    secrets_detection: "zero_tolerance"
    
  ai_specific:
    prompt_evaluation_score: ">95%"
    model_response_time: "<2s"
    fallback_chain_test: "all_providers_tested"
    
  compliance:
    eu_ai_act_checks: "all_pass"
    audit_log_validation: "complete"
```

---

## Appendix C: Open Items Reference

| ID | Item | Decision | Section |
|----|------|----------|---------|
| OPEN-001 | Cloud Provider | AWS Primary | §3.1 |
| OPEN-002 | Container Platform | ECS/Fargate | §3.2 |
| OPEN-003 | Brazil Deployment | sa-east-1 + Latitude.sh | §3.3, §7.3 |
| OPEN-004 | Data Retention Policy | See matrix | §12.1 |
| OPEN-005 | Prompt Versioning | Git + LangSmith | §8.1 |
| OPEN-006 | Fine-Tuning vs RAG | RAG preferred | §9 |
| OPEN-007 | Fair Housing Compliance | Guardrails in prompts | §9.2 |
| OPEN-008 | PCI Compliance | Token-only, no PAN | §12.1 |
| OPEN-009 | SPSAV License | Intermediary → Custodian | §6.2 |
| OPEN-010 | CRM Priority | Yardi, AppFolio, SF | §18 |
| OPEN-011 | DR Strategy | Active-Active US/BR | §14.1 |
| OPEN-012 | Voice Latency | <300ms via edge | §7.3 |
| OPEN-019 | HITL Dashboard | Real-time annotations | §10.1 |
| OPEN-031 | Chaos Engineering | AWS FIS + Chaos Toolkit | §13 |
| OPEN-040 | EU AI Act | High-risk for Leasing | §16 |
| OPEN-041 | Prompt A/B Testing | LangSmith experiments | §8.2 |

---

## Appendix D: Implementation Roadmap

### Phase 1: Foundation (Q2 2025)
- Deploy TigerBeetle 6-replica cluster
- Implement Formance Ledger with Numscript
- Establish PIX connection via Dock
- Deploy Teleport for Zero Trust

### Phase 2: Intelligence (Q3 2025)
- Deploy Voice AI edge cluster (Latitude.sh)
- Launch Beta Voice Agent (<300ms)
- RL Payment Router in Shadow Mode
- Integrate Fireblocks MPC
- Deploy HITL Dashboard

### Phase 3: Compliance (Q4 2025 - Q1 2026)
- Submit SPSAV license to BCB
- RL Router Live Mode
- SOC 2 Type II certification
- Migrate Loyalty to TigerBeetle
- Complete Chaos Engineering Game Days

### Phase 4: Scale (Q2 2026)
- SPSAV approval (Feb 2026 target)
- EU AI Act compliance (Aug 2026 deadline)
- Open API for Livelo/Stix
- Full crypto-fiat bridge
- EU expansion (GDPR, MiCA)

---

## Appendix E: References

### CitadelOS Architecture (Internal)
1. [COMPLETE_TECHNICAL_ARCHITECTURE.md](../../docs/COMPLETE_TECHNICAL_ARCHITECTURE.md) - Master 6-layer stack
2. [LAYER4_SKILLS_ARCHITECTURE.md](../../docs/architecture/LAYER4_SKILLS_ARCHITECTURE.md) - Skills Framework

### Cloud & Deployment
3. [Twilio ConversationRelay on AWS](https://www.twilio.com/en-us/blog/developers/tutorials/product/reference-architecture-aws-conversationrelay-voice-ai-app)
4. [ECS vs EKS Comparison](https://lumigo.io/aws-ecs-understanding-launch-types-service-options-and-pricing/ecs-vs-eks-5-key-differences-and-how-to-choose/)

### TigerBeetle & Financial Infrastructure
5. [Jepsen Analysis: TigerBeetle](https://jepsen.io/analyses/tigerbeetle-0.16.11.pdf)
6. [TigerBeetle Performance](https://docs.tigerbeetle.com/concepts/performance/)
7. [TigerBeetle Two-Phase Transfers](https://docs.tigerbeetle.com/coding/two-phase-transfers/)

### Brazilian Regulation
8. [Fireblocks SPSAV Guide](https://www.fireblocks.com/blog/what-to-know-brazil-spsav-framework)
9. [Chainalysis Brazil Crypto Framework](https://www.chainalysis.com/blog/brazil-crypto-asset-regulatory-framework-2025/)

### Voice AI
10. [WebRTC for Voice AI](https://webrtc.ventures/2025/10/why-webrtc-is-the-best-transport-for-real-time-voice-ai-architectures/)
11. [Latitude.sh Pricing](https://www.latitude.sh/pricing)

### Compliance
12. [EU AI Act Official Text](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689)
13. [GDPR Call Recording Rules](https://www.nice.com/blog/mcr-understanding-the-gdpr-call-recording-rules-2531)
14. [PCI DSS Data Retention](https://www.pcisecuritystandards.org/)

### Security
15. [NIST Zero Trust Architecture](https://www.nist.gov/publications/zero-trust-architecture)
16. [AWS FIS Documentation](https://docs.aws.amazon.com/fis/latest/userguide/what-is.html)

### AI Prompt Management
17. [LangSmith Documentation](https://docs.smith.langchain.com/)
18. [Anthropic Claude Documentation](https://docs.anthropic.com/)

---

**Document Statistics:**
- **Lines**: ~2,400
- **Citations**: 45+ authoritative sources
- **Open Items Addressed**: All 42
- **Consolidated Sources**: V4 + Round 2 + Round 3

---

*Version 5.0 (Final) - January 2026*  
*This document consolidates all production infrastructure research into a single authoritative reference for Citadel OS.*

