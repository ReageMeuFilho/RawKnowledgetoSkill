# Knowledge Document: Production Infrastructure Strategic Decisions (V3)

<details>
<summary>📋 Version 3 Enhancements: What Changed from V2</summary>

## Critical Additions in V3

Version 3 incorporates deep technical research on Treasury OS internals, Brazilian crypto regulation, and edge AI infrastructure that V2 lacked.

### Major New Sections

1. **TigerBeetle Deep Architecture**
   - Viewstamped Replication (VSR) consensus protocol details
   - Single-threaded execution model rationale
   - Batching mechanics (8,190 transfers per request)
   - 6-replica cluster for 99.999% availability
   - Federated Ledger Architecture (Brazil vs Global clusters)

2. **Two-Phase Transfers**
   - AML/KYC compliance holds
   - Atomic cross-ledger swaps (crypto-fiat)
   - Escrow for loyalty redemptions

3. **Brazilian Crypto Regulation (SPSAV)**
   - Law 14.478/2022 and BCB resolutions 517-521
   - Capital requirements (R$10.8M - R$37.2M)
   - February 2026 compliance deadline
   - Stablecoins as FX operations (IOF Tax Engine)

4. **Voice AI: WebRTC Mandate**
   - Why WebSocket (TCP) fails for real-time voice
   - WebRTC (UDP) for no head-of-line blocking
   - Native echo cancellation

5. **Brazil GPU Infrastructure**
   - Latitude.sh (L40S/H100) as primary
   - Oracle Cloud São Paulo (A100) as failover
   - Why US GPUs are not viable (<20ms vs 150ms RTT)

6. **Local LLM Inference**
   - Groq LPU for ~50ms TTFT (vs Claude API ~100ms)
   - Self-hosted Llama 3 for voice in Brazil

7. **Local Stablecoins**
   - BRZ (Transfero) and BRL1 (Bitso consortium)
   - OTC desks: Finchtrade, Bitso, Transfero via FIX API

8. **MPC Custody (Mandatory)**
   - Fireblocks or Copper integration
   - Disaster recovery architecture

9. **RL-Based Payment Router**
   - Q-Learning model for provider selection
   - Multi-objective reward function

10. **Zero Trust Security**
    - Teleport for engineer access
    - mTLS everywhere
    - SPSAV audit compliance

</details>

---

# Production Infrastructure Strategic Architecture: Citadel OS & Treasury OS

## Strategic Technical Roadmap & Compliance Framework (2025-2026)

---

## 1. Executive Strategic Overview

This document serves as the definitive architectural blueprint for Citadel OS, a next-generation financial operating system designed to facilitate high-velocity value exchange across fiat, crypto, and loyalty assets. The objective is to construct a platform capable of sustaining **$75-100M in Annual Recurring Revenue (ARR)** within a highly competitive and regulated global landscape, with a primary expansion focus on **Brazil**.

### Architectural Philosophy: Financial Correctness by Design

The governing doctrine moves beyond the traditional "buy vs. build" dichotomy toward **"Financial Correctness by Design"**—leveraging deterministic infrastructure to eliminate the reconciliation overhead that plagues legacy fintechs. This requires a fundamental departure from monolithic banking cores toward a composable, event-driven microservices architecture anchored by a **strictly serializable ledger**.

### The Core Engineering Challenge

Reconciling two opposing forces:
1. **Extreme Performance**: Sub-300ms latency for Voice AI and million-TPS throughput for the ledger
2. **Rigid Regulatory Constraints**: Brazilian LGPD, the evolving SPSAV framework (effective February 2026), and the PIX instant payment system

### Strategic Moat Through Infrastructure

By embedding compliance into code via programmable ledgers (Formance) and immutable audit trails (TigerBeetle), we transform regulatory burdens into **barriers to entry** for competitors. Our Voice AI architecture leverages edge-localized inference to deliver "mouth-to-ear" latency that creates a **UX moat** traditional banking apps cannot bridge.

---

## 2. Treasury OS: The Financial Core Architecture

The Treasury OS is the central nervous system of Citadel. In a modern fintech architecture, the ledger is not a passive database recording what *happened*—it is the **active enforcement layer** determining what *is allowed to happen*.

### 2.1. The Ledger Engine: TigerBeetle Implementation Strategy

The selection of **TigerBeetle** as the immutable system of record is derived from first-principles analysis of financial failure modes.

#### 2.1.1. Why Not Traditional Databases?

Traditional OLTP databases (PostgreSQL, MySQL) are designed for flexible query patterns (SQL), not for the **contention patterns** inherent in financial ledgers:

| Scenario | PostgreSQL Behavior | TigerBeetle Behavior |
|----------|---------------------|---------------------|
| 1000 concurrent transactions on "platform fee" account | Row-level locking causes exponential degradation | Single-threaded batch processing, linear scaling |
| Network partition during write | Potential split-brain, requires manual reconciliation | VSR consensus ensures strict serializability |
| Crash during transaction | WAL recovery may leave orphaned locks | Deterministic recovery, no orphaned state |

**Reference**: [Jepsen Analysis: TigerBeetle 0.16.11](https://jepsen.io/analyses/tigerbeetle-0.16.11.pdf) - Jepsen, 2024

#### 2.1.2. Viewstamped Replication (VSR) Consensus

TigerBeetle utilizes **Viewstamped Replication**, a consensus protocol that ensures **strict serializability**—the gold standard in distributed systems:

- **Strict Serializability**: Once a transaction is committed, it is visible immediately to all subsequent operations in a total global order
- **No Double-Spend Anomalies**: Prevents the "dirty reads" that occur in eventually consistent systems (Cassandra, DynamoDB)
- **Deterministic Recovery**: No manual intervention required after crash

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    VIEWSTAMPED REPLICATION (VSR)                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  Leader Election:                                                           │
│  ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐                  │
│  │Replica 1│───▶│Replica 2│───▶│Replica 3│───▶│Replica 4│                  │
│  │ LEADER  │    │FOLLOWER │    │FOLLOWER │    │FOLLOWER │                  │
│  └─────────┘    └─────────┘    └─────────┘    └─────────┘                  │
│       │                                                                     │
│       │ PrepareRequest(op, view, seq)                                      │
│       ├──────────────────────────────────────────────────▶                  │
│       │                                                                     │
│       │ PrepareOK(view, seq) from quorum (3 of 4)                          │
│       ◀──────────────────────────────────────────────────                  │
│       │                                                                     │
│       │ Commit(seq) - operation now globally visible                        │
│       ├──────────────────────────────────────────────────▶                  │
│                                                                             │
│  Key Guarantees:                                                            │
│  • Linearizable reads and writes                                           │
│  • Total ordering of all operations                                        │
│  • Survives f failures with 2f+1 replicas                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Reference**: [TigerBeetle Architecture Documentation](https://github.com/tigerbeetle/tigerbeetle/blob/main/docs/internals/ARCHITECTURE.md) - TigerBeetle, 2024

#### 2.1.3. Single-Threaded Execution Model

**Counterintuitive but critical**: TigerBeetle employs a single-threaded execution model for its state machine:

| Multi-Threaded Approach | TigerBeetle Single-Thread |
|------------------------|---------------------------|
| Context switching overhead | Zero context switching |
| Race conditions requiring locks | No locks needed |
| Complex lock contention under load | Linear performance |
| 10-100K TPS (practical limit) | **1+ Million TPS** |

The single-thread achieves massive throughput through **batching**. The API forces applications to send transfers in batches (up to **8,190 transfers per request**), saturating network and disk I/O bandwidth while amortizing consensus and syscall costs.

**Reference**: [TigerBeetle Performance](https://docs.tigerbeetle.com/concepts/performance/) - TigerBeetle Docs, 2024

#### 2.1.4. Production Cluster Configuration

To meet **99.999% availability** (5.26 minutes downtime/year), we deploy a **6-replica cluster** distributed across three geographically distinct zones:

```yaml
# TigerBeetle 6-Replica Production Cluster
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

**Reference**: [TigerBeetle Cluster Recommendations](https://docs.tigerbeetle.com/operating/cluster/) - TigerBeetle Docs, 2024

### 2.2. Federated Ledger Architecture (Brazil + Global)

Due to Brazil's data residency requirements (LGPD), we cannot run a single global cluster. We implement a **Federated Ledger Architecture**:

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
│  │                                │    │                                │  │
│  │  ┌──────┐ ┌──────┐ ┌──────┐   │    │  ┌──────┐ ┌──────┐ ┌──────┐   │  │
│  │  │ TB-1 │ │ TB-2 │ │ TB-3 │   │    │  │ TB-4 │ │ TB-5 │ │ TB-6 │   │  │
│  │  └──────┘ └──────┘ └──────┘   │    │  └──────┘ └──────┘ └──────┘   │  │
│  │                                │    │                                │  │
│  └──────────────┬─────────────────┘    └──────────────┬─────────────────┘  │
│                 │                                      │                    │
│                 │         Federation Layer             │                    │
│                 │         (Formance Stack)             │                    │
│                 └──────────────┬───────────────────────┘                    │
│                                │                                            │
│  ┌─────────────────────────────┴────────────────────────────────────────┐  │
│  │                     FORMANCE ORCHESTRATION                            │  │
│  │                                                                       │  │
│  │  • Routes requests to appropriate cluster based on jurisdiction       │  │
│  │  • Coordinates cross-cluster transactions via Temporal Sagas          │  │
│  │  • Handles currency conversion (BRL ↔ USD ↔ USDC)                     │  │
│  │  • Enforces IOF tax calculations for FX operations                    │  │
│  │                                                                       │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│  CROSS-CLUSTER TRANSACTION EXAMPLE:                                        │
│  Brazilian user sends R$1000 to US user                                    │
│                                                                             │
│  1. Temporal Saga initiates                                                │
│  2. CLUSTER-BR: Debit user's BRL account (pending)                        │
│  3. IOF Tax Engine: Calculate and withhold 0.38% (R$3.80)                  │
│  4. FX Service: Convert R$996.20 → USD at market rate                     │
│  5. CLUSTER-GLOBAL: Credit recipient's USD account (pending)              │
│  6. Both clusters: Commit (atomic across federation)                       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 2.3. Two-Phase Transfers: The Compliance Mechanism

TigerBeetle's **Two-Phase Transfer** capability is critical for regulatory compliance:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      TWO-PHASE TRANSFER LIFECYCLE                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  PHASE 1: PENDING (Reserve)                                                │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                                                                     │   │
│  │  User Account: $1000                   Pending Account: $0          │   │
│  │       │                                      │                      │   │
│  │       │  create_transfer(pending=true)       │                      │   │
│  │       │  amount=$500                         │                      │   │
│  │       └──────────────────────────────────────▶                      │   │
│  │                                              │                      │   │
│  │  User Account: $500 (available)        Pending Account: $500 (held) │   │
│  │                                                                     │   │
│  │  STATE: Funds are LOCKED but not MOVED                              │   │
│  │  The $500 cannot be spent elsewhere                                 │   │
│  │                                                                     │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
│  ASYNC CHECKS (while funds are locked):                                    │
│  • AML/KYC screening (Chainalysis, Elliptic)                               │
│  • Fraud scoring model                                                      │
│  • External banking API confirmation                                        │
│  • Regulatory holds (if required)                                          │
│                                                                             │
│  PHASE 2A: POST (Commit) - If checks PASS                                  │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                                                                     │   │
│  │  post_pending_transfer(transfer_id)                                 │   │
│  │                                                                     │   │
│  │  Pending Account: $500 ───────────────────▶ Destination: $500       │   │
│  │                                                                     │   │
│  │  STATE: Funds are COMMITTED, transaction complete                   │   │
│  │                                                                     │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
│  PHASE 2B: VOID (Rollback) - If checks FAIL or TIMEOUT                     │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                                                                     │   │
│  │  void_pending_transfer(transfer_id)                                 │   │
│  │                                                                     │   │
│  │  Pending Account: $500 ───────────────────▶ User Account: $500      │   │
│  │                                                                     │   │
│  │  STATE: Funds RETURNED to user, no orphaned locks                   │   │
│  │                                                                     │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Use Cases for Two-Phase Transfers:**

| Use Case | Pending Phase | Commit/Void Trigger |
|----------|---------------|---------------------|
| **AML/KYC Compliance** | Lock funds when tx initiated | Commit after compliance check passes |
| **Atomic Crypto-Fiat Swap** | Lock USDC AND lock BRL | Commit both only when both confirmed |
| **Loyalty Escrow** | Lock points on service request | Commit on proof of completion |
| **Payment Authorization** | Lock amount on card auth | Commit on capture, void on timeout |

**Reference**: [TigerBeetle Two-Phase Transfers](https://docs.tigerbeetle.com/coding/two-phase-transfers/) - TigerBeetle Docs, 2024

### 2.4. Numscript: The Financial Domain-Specific Language

**Formance's Numscript** allows us to decouple financial policy from application code:

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

**Why Numscript Matters:**

1. **Atomic Execution**: Either all splits happen or none—no partial failure states
2. **Deterministic Rounding**: Uses integer math, never loses fractional cents
3. **Audit Trail**: Every Numscript execution is immutably logged
4. **Policy as Code**: Tax rates, fee structures are versioned in Git, not hardcoded

**Reference**: [What is Numscript and Why is it Awesome?](https://www.formance.com/blog/engineering/numscript) - Formance, 2024

### 2.5. Temporal: Durable Execution for Financial Workflows

Financial operations are inherently distributed and asynchronous. **Temporal** provides "Durable Execution" that solves the distributed transaction problem:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│           TEMPORAL SAGA: CRYPTO-TO-FIAT WITHDRAWAL (Brazil)                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  User requests: Withdraw 1000 USDC to PIX (BRL)                            │
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ STEP 1: Lock Crypto (Compensable)                                   │   │
│  │                                                                     │   │
│  │   Activity: lock_user_crypto(user_id, amount=1000, asset="USDC")    │   │
│  │   Compensation: unlock_user_crypto(user_id, amount=1000)            │   │
│  │                                                                     │   │
│  │   → Creates pending transfer in TigerBeetle                         │   │
│  │   → Funds locked, user cannot spend elsewhere                       │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                            │                                                │
│                            ▼                                                │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ STEP 2: Get OTC Quote (Compensable)                                 │   │
│  │                                                                     │   │
│  │   Activity: request_otc_quote(                                      │   │
│  │     desks=["bitso", "finchtrade", "transfero"],                     │   │
│  │     from="USDC", to="BRL", amount=1000                              │   │
│  │   )                                                                 │   │
│  │   Compensation: cancel_otc_quote(quote_id)                          │   │
│  │                                                                     │   │
│  │   → Smart router selects best price (e.g., Bitso: R$5.12/USDC)      │   │
│  │   → Quote locked for 30 seconds                                     │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                            │                                                │
│                            ▼                                                │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ STEP 3: Calculate IOF Tax (Non-Compensable)                         │   │
│  │                                                                     │   │
│  │   Activity: calculate_iof_tax(amount_brl=5120, type="fx_outbound")  │   │
│  │                                                                     │   │
│  │   → IOF rate: 1.1% for FX operations                                │   │
│  │   → Tax: R$56.32                                                    │   │
│  │   → Net to user: R$5,063.68                                         │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                            │                                                │
│                            ▼                                                │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ STEP 4: Initiate PIX Transfer (Compensable)                         │   │
│  │                                                                     │   │
│  │   Activity: initiate_pix_transfer(                                  │   │
│  │     baas_provider="dock",                                           │   │
│  │     recipient_pix_key="carlos@email.com",                           │   │
│  │     amount_brl=5063.68                                              │   │
│  │   )                                                                 │   │
│  │   Compensation: request_pix_refund(transfer_id)                     │   │
│  │                                                                     │   │
│  │   → PIX instant transfer initiated                                  │   │
│  │   → Awaiting confirmation webhook                                   │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                            │                                                │
│                            ▼                                                │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ STEP 5: Await PIX Confirmation (Signal)                             │   │
│  │                                                                     │   │
│  │   Signal: pix_confirmation_received(transfer_id, status)            │   │
│  │   Timeout: 5 minutes                                                │   │
│  │                                                                     │   │
│  │   → On SUCCESS: Proceed to Step 6                                   │   │
│  │   → On FAILURE/TIMEOUT: Execute compensations (Steps 4→3→2→1)       │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                            │                                                │
│                            ▼                                                │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ STEP 6: Commit Crypto Transfer (Final)                              │   │
│  │                                                                     │   │
│  │   Activity: commit_crypto_transfer(                                 │   │
│  │     pending_transfer_id,                                            │   │
│  │     destination="otc_desk:bitso"                                    │   │
│  │   )                                                                 │   │
│  │                                                                     │   │
│  │   → Posts pending transfer in TigerBeetle                           │   │
│  │   → USDC moved to OTC desk settlement account                       │   │
│  │   → Transaction COMPLETE                                            │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
│  DURABILITY GUARANTEES:                                                     │
│  • If worker crashes at ANY step, Temporal resumes on new worker           │
│  • Compensation chain executes automatically on failure                     │
│  • No orphaned funds, no double-spend, no lost transactions                │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Reference**: [Designing High-Performance Financial Ledgers with Temporal](https://temporal.io/blog/designing-high-performance-financial-ledgers-with-temporal) - Temporal, 2024

---

## 3. Brazilian Crypto Regulation: SPSAV Framework (2025-2026)

### 3.1. Regulatory Landscape

The regulatory framework is defined by **Law 14.478/2022** and subsequent Central Bank (BCB) resolutions **517, 519, 520, and 521**, establishing the licensing regime for Virtual Asset Service Providers (VASPs), locally known as **SPSAV** (*Sociedade Prestadora de Serviços de Ativos Virtuais*).

**Critical Deadline: February 2026** - Full compliance mandatory

**Reference**: [Brazil's Central Bank Unveils New Regulatory Framework for Cryptoassets](https://international.anbima.com.br/news/brazil-s-central-bank-unveils-new-regulatory-framework-for-cryptoassets) - ANBIMA, 2024

### 3.2. SPSAV License Requirements

| License Type | Activities | Minimum Capital | Strategic Implication |
|-------------|------------|-----------------|----------------------|
| **Intermediation** | Connecting buyers and sellers | R$10.8M (~$2M USD) | Lower capital, partner for custody |
| **Custody** | Holding private keys for users | R$37.2M (~$7M USD) | Higher capital, full control |
| **Brokerage** | Intermediation + Custody | R$37.2M (~$7M USD) | Complete service offering |

**Strategic Decision**: Launch as **Intermediary** initially (partnering with Fireblocks for custody) to lower capital intensity, then upgrade to **Custodian** license after establishing revenue base.

**Reference**: [Inside Brazil's New Digital Asset Rules: What Institutions Need to Know](https://www.fireblocks.com/blog/what-to-know-brazil-spsav-framework) - Fireblocks, 2024

### 3.3. Resolution 521: Stablecoins as FX Operations

**Game-changer**: Resolution 521 classifies stablecoin transfers involving international counterparties as **Foreign Exchange (FX)** operations.

**Implications:**
- Every Brazilian user buying USDC triggers FX reporting obligations
- **IOF (Imposto sobre Operações Financeiras)** tax applies:
  - 0.38% for standard FX operations
  - 1.1% for FX operations involving credit

**Mandatory Architecture Update**: The Payment Orchestrator must include an **IOF Tax Engine**:

```python
# IOF Tax Engine Implementation
class IOFTaxEngine:
    """
    Brazilian IOF tax calculator for FX operations.
    Required for SPSAV compliance.
    """

    IOF_RATES = {
        "fx_standard": 0.0038,      # 0.38% - standard FX
        "fx_credit": 0.011,         # 1.1% - FX with credit
        "fx_export": 0.0,           # 0% - export operations
        "fx_import_services": 0.0038,
    }

    def calculate_iof(
        self,
        amount_brl: Decimal,
        operation_type: str,
        is_credit: bool = False
    ) -> IOFCalculation:
        """
        Calculate IOF tax for FX operation.

        Args:
            amount_brl: Transaction amount in BRL
            operation_type: Type of FX operation
            is_credit: Whether operation involves credit

        Returns:
            IOFCalculation with tax amount and net amount
        """
        rate_key = "fx_credit" if is_credit else operation_type
        rate = self.IOF_RATES.get(rate_key, self.IOF_RATES["fx_standard"])

        tax_amount = (amount_brl * Decimal(str(rate))).quantize(
            Decimal("0.01"), rounding=ROUND_HALF_UP
        )

        return IOFCalculation(
            gross_amount=amount_brl,
            iof_rate=rate,
            iof_amount=tax_amount,
            net_amount=amount_brl - tax_amount,
            reporting_required=True,
            receita_federal_code=self._get_rf_code(operation_type)
        )

    def queue_for_remittance(self, calculation: IOFCalculation):
        """Queue IOF tax for remittance to Receita Federal."""
        # Tax must be remitted within 3 business days
        self.tax_queue.enqueue({
            "amount": calculation.iof_amount,
            "due_date": self._next_business_day(days=3),
            "rf_code": calculation.receita_federal_code
        })
```

**Reference**: [Breaking Down Brazil's New Crypto Framework](https://www.chainalysis.com/blog/brazil-crypto-asset-regulatory-framework-2025/) - Chainalysis, 2024

### 3.4. Asset Segregation Requirements

BCB Resolution 520 mandates **segregation of client assets** from platform proprietary assets:

```yaml
# TigerBeetle Ledger Segregation for SPSAV Compliance
ledger_configuration:
  ledgers:
    - id: 1
      name: "client_omnibus_brl"
      type: client_funds
      currency: BRL
      description: "Segregated client BRL holdings"

    - id: 2
      name: "client_omnibus_usdc"
      type: client_funds
      currency: USDC
      description: "Segregated client USDC holdings"

    - id: 3
      name: "corporate_treasury"
      type: proprietary
      currency: BRL
      description: "Platform operational funds"

    - id: 4
      name: "fee_collection"
      type: proprietary
      currency: BRL
      description: "Collected platform fees"

  segregation_rules:
    - rule: "no_commingling"
      description: "Client funds (ledger 1,2) can never mix with proprietary (3,4)"
      enforcement: "database_level"

    - rule: "audit_trail"
      description: "All movements between ledgers require compliance approval"
      enforcement: "temporal_workflow"
```

**On-Chain Segregation**: Separate wallet addresses for client omnibus vs corporate treasury, enforced by MPC custody policies.

---

## 4. Voice AI Infrastructure: Achieving <300ms Latency

### 4.1. The Physics Problem

The requirement is **<300ms voice-to-voice latency**. This is a hard constraint dictated by human cognitive processing—delays above 300-500ms cause users to talk over the bot, breaking the interaction.

**The São Paulo to US East Problem:**
- Round-trip time (RTT) from São Paulo to Virginia: **120-150ms**
- This single hop consumes **50% of our latency budget**

**Conclusion**: For Brazilian users, **inference must occur in Brazil**. We cannot rely on US-based GPUs.

**Reference**: [GCE Latency Discussion - São Paulo](https://groups.google.com/g/gce-discussion/c/hlKY_9cHD38) - Google Groups, 2024

### 4.2. WebRTC vs WebSocket: Transport Decision

**Decision: WebRTC is mandatory for voice.**

| Aspect | WebSocket (TCP) | WebRTC (UDP) |
|--------|-----------------|--------------|
| **Packet Loss** | TCP pauses for retransmit (Head-of-Line blocking) | Skips lost packet, continues |
| **Result** | Latency spikes, audio stuttering | Micro-glitch, no delay |
| **Echo Cancellation** | Must implement server-side | Native on client device |
| **NAT Traversal** | Requires additional infrastructure | Built-in (STUN/TURN) |

**Reference**: [Why WebRTC Is the Best Transport for Real-Time Voice AI Architectures](https://webrtc.ventures/2025/10/why-webrtc-is-the-best-transport-for-real-time-voice-ai-architectures/) - WebRTC.ventures, 2025

### 4.3. The Brazil Voice AI Stack

```
┌─────────────────────────────────────────────────────────────────────────────┐
│              BRAZIL VOICE AI EDGE ARCHITECTURE (<300ms)                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  User in São Paulo                                                          │
│       │                                                                     │
│       │ WebRTC (UDP)                                                        │
│       │ RTT: <20ms to edge                                                  │
│       ▼                                                                     │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │          LATITUDE.SH EDGE CLUSTER (São Paulo - MH1)                 │   │
│  │                                                                     │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                 │   │
│  │  │   L40S GPU  │  │   L40S GPU  │  │   L40S GPU  │                 │   │
│  │  │  (Primary)  │  │  (Primary)  │  │  (Failover) │                 │   │
│  │  └──────┬──────┘  └──────┬──────┘  └─────────────┘                 │   │
│  │         │                │                                          │   │
│  │         └────────────────┼──────────────────────────────────────┐   │   │
│  │                          │                                      │   │   │
│  │  ┌───────────────────────┴───────────────────────────────────┐  │   │   │
│  │  │              INFERENCE PIPELINE (All in Brazil)           │  │   │   │
│  │  │                                                           │  │   │   │
│  │  │  1. VAD: Silero VAD                        [20ms]         │  │   │   │
│  │  │     • Semantic end-of-turn detection                      │  │   │   │
│  │  │     • Distinguishes pause vs finished                     │  │   │   │
│  │  │                                                           │  │   │   │
│  │  │  2. STT: Deepgram Nova-2 (Streaming)       [80ms]         │  │   │   │
│  │  │     • Interim transcripts for speculative execution       │  │   │   │
│  │  │     • Portuguese (pt-BR) model                            │  │   │   │
│  │  │                                                           │  │   │   │
│  │  │  3. LLM: Groq LPU (Llama 3 70B)            [50ms TTFT]    │  │   │   │
│  │  │     • Deterministic hardware, 500+ tokens/sec             │  │   │   │
│  │  │     • OR: Self-hosted Llama 3 8B on L40S                  │  │   │   │
│  │  │                                                           │  │   │   │
│  │  │  4. TTS: Cartesia Sonic / ElevenLabs Turbo [70ms TTFB]    │  │   │   │
│  │  │     • Stream audio chunks immediately                     │  │   │   │
│  │  │     • Portuguese voice models                             │  │   │   │
│  │  │                                                           │  │   │   │
│  │  └───────────────────────────────────────────────────────────┘  │   │   │
│  │                                                                  │   │   │
│  └──────────────────────────────────────────────────────────────────┘   │   │
│                                                                             │
│  LATENCY BUDGET:                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  Component          │ Technology           │ Latency   │ Running   │   │
│  ├─────────────────────┼──────────────────────┼───────────┼───────────┤   │
│  │  Network (BR edge)  │ WebRTC (UDP)         │ 20ms      │ 20ms      │   │
│  │  VAD                │ Silero VAD           │ 20ms      │ 40ms      │   │
│  │  STT                │ Deepgram Nova-2      │ 80ms      │ 120ms     │   │
│  │  LLM (TTFT)         │ Groq LPU             │ 50ms      │ 170ms     │   │
│  │  TTS (TTFB)         │ Cartesia Sonic       │ 70ms      │ 240ms     │   │
│  │  Network (return)   │ WebRTC (UDP)         │ 20ms      │ 260ms     │   │
│  ├─────────────────────┼──────────────────────┼───────────┼───────────┤   │
│  │  TOTAL              │                      │           │ ~260ms ✓  │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 4.4. GPU Infrastructure Decision Matrix

| Provider | Region | GPU Model | RTT to BR User | Cost | Verdict |
|----------|--------|-----------|---------------|------|---------|
| **Latitude.sh** | São Paulo (MH1) | NVIDIA L40S / H100 | **<20ms** | $$$ | **Primary Choice** |
| **Oracle Cloud** | São Paulo (GRU) | NVIDIA A100 / A10 | **<20ms** | $$ | **Failover/Scale** |
| **AWS** | US East (Virginia) | NVIDIA A10G | 120-150ms | $ | **Not Viable** |
| **Fly.io** | US (ORD/IAD) | NVIDIA A100 | 140ms | $ | **Not Viable** |

**Strategic Decision**: Deploy Voice AI Edge Cluster on **Latitude.sh São Paulo** using L40S GPUs. Use **Oracle Cloud São Paulo** as failover/burst capacity.

**Reference**: [Latitude.sh Pricing - GPU VMs](https://www.latitude.sh/pricing?computeTab=gpu-vms) - Latitude.sh, 2024

### 4.5. Groq LPU: The LLM Latency Breakthrough

For voice applications, the LLM is typically the bottleneck. **Groq's Language Processing Unit (LPU)** provides deterministic, ultra-low latency inference:

| Metric | Claude API (US) | GPT-4 API (US) | Groq LPU (Llama 3 70B) |
|--------|-----------------|----------------|------------------------|
| **Time to First Token (TTFT)** | 100-200ms | 150-300ms | **~50ms** |
| **Tokens/Second** | 50-100 | 30-80 | **500+** |
| **Latency Variability** | High (shared infra) | High | **Low (deterministic)** |

**Trade-off**: Groq uses Llama models (not Claude). For voice, this is acceptable—responses are short, and the speed advantage outweighs the capability difference.

**Fallback**: For complex reasoning tasks that require Claude, route to US-based Claude API and accept higher latency (use for non-real-time features).

**Reference**: [Voice AI Infrastructure: Building Real-Time Speech Agents](https://introl.com/blog/voice-ai-infrastructure-real-time-speech-agents-asr-tts-guide-2025) - Introl, 2025

---

## 5. Payment Orchestration & Smart Routing

### 5.1. PIX-Native Architecture

PIX is the undisputed rail for Brazilian liquidity (150M+ users). Our architecture treats PIX as a **native protocol**, not an external plugin.

**Decision**: Operate as **Indirect Participant** via BaaS provider (Dock, FitBank, or Celcoin).

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       PIX INTEGRATION ARCHITECTURE                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  USER DEPOSIT FLOW:                                                         │
│                                                                             │
│  1. User requests deposit                                                   │
│     │                                                                       │
│     ▼                                                                       │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  CITADEL: Generate Dynamic QR Code                                  │   │
│  │                                                                     │   │
│  │  {                                                                  │   │
│  │    "qrcode_type": "dynamic",                                        │   │
│  │    "amount": 10000,  // R$100.00                                    │   │
│  │    "txid": "citadel_deposit_abc123",  // Unique identifier          │   │
│  │    "merchant": "CITADEL SERVICOS FINANCEIROS",                      │   │
│  │    "expiration": "2024-01-15T15:30:00Z"                             │   │
│  │  }                                                                  │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│     │                                                                       │
│     │ QR Code displayed in app                                             │
│     ▼                                                                       │
│  2. User scans with bank app, pays via PIX                                 │
│     │                                                                       │
│     ▼                                                                       │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  BAAS PROVIDER (Dock): Webhook notification                         │   │
│  │                                                                     │   │
│  │  POST /webhooks/pix                                                 │   │
│  │  {                                                                  │   │
│  │    "event": "pix.received",                                         │   │
│  │    "txid": "citadel_deposit_abc123",                                │   │
│  │    "amount": 10000,                                                 │   │
│  │    "payer": {                                                       │   │
│  │      "cpf": "***.***.***-**",  // Masked                            │   │
│  │      "name": "CARLOS DA SILVA"                                      │   │
│  │    },                                                               │   │
│  │    "end_to_end_id": "E12345678901234567890123456789012"             │   │
│  │  }                                                                  │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│     │                                                                       │
│     ▼                                                                       │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  TEMPORAL SAGA: Process PIX Deposit                                 │   │
│  │                                                                     │   │
│  │  1. Match txid to pending deposit request                           │   │
│  │  2. Verify amount matches expected                                  │   │
│  │  3. Credit user account in TigerBeetle (CLUSTER-BR)                 │   │
│  │  4. Send confirmation via WhatsApp                                  │   │
│  │  5. Update user balance in app (real-time)                          │   │
│  │                                                                     │   │
│  │  Total time: <3 seconds from PIX payment to account credit          │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Reference**: [PIX Integration through EBANX Direct API](https://docs.ebanx.com/docs/payments/guides/accept-payments/api/brazil/pix/) - EBANX, 2024

### 5.2. Local Stablecoins: BRZ and BRL1

To mitigate FX friction, we integrate **local stablecoins** with tighter BRL spreads:

| Stablecoin | Issuer | Backing | Spread vs BRL | Use Case |
|------------|--------|---------|---------------|----------|
| **BRZ** | Transfero | 1:1 BRL reserves | ~0.1% | High-volume trading |
| **BRL1** | Bitso consortium | 1:1 BRL reserves | ~0.15% | Retail transactions |
| **USDC** | Circle | 1:1 USD reserves | FX spread + IOF | International |

**Liquidity Aggregation**: Connect to OTC desks via FIX API:
- **Finchtrade** - Crypto OTC specialist
- **Bitso** - Latin America's largest exchange
- **Transfero** - BRZ issuer, direct liquidity

**Reference**: [BRZ Stablecoin - RWA.xyz](https://app.rwa.xyz/assets/BRZ) - RWA.xyz, 2024

### 5.3. RL-Based Smart Payment Router

We deploy a **Reinforcement Learning** model for dynamic provider selection:

```python
# Q-Learning Payment Router
import numpy as np
from dataclasses import dataclass
from enum import Enum

class PaymentProvider(Enum):
    DOCK = "dock"
    FITBANK = "fitbank"
    CELCOIN = "celcoin"

@dataclass
class TransactionState:
    time_of_day: int          # 0-23
    transaction_size: float   # BRL amount
    destination_bank: str     # ISPB code
    recent_failure_rate: float

class PaymentRouter:
    """
    Q-Learning based payment router.
    Learns optimal provider for each transaction type.
    """

    def __init__(self, providers: list[PaymentProvider]):
        self.providers = providers
        self.q_table = {}  # State -> Action -> Q-value
        self.learning_rate = 0.1
        self.discount_factor = 0.95
        self.exploration_rate = 0.1

        # Reward weights
        self.w_success = 1.0
        self.w_latency = 0.3
        self.w_cost = 0.2

    def select_provider(self, state: TransactionState) -> PaymentProvider:
        """Select best provider using epsilon-greedy strategy."""
        state_key = self._state_to_key(state)

        if np.random.random() < self.exploration_rate:
            # Explore: random provider
            return np.random.choice(self.providers)

        # Exploit: best known provider
        if state_key not in self.q_table:
            self.q_table[state_key] = {p: 0.0 for p in self.providers}

        return max(self.q_table[state_key], key=self.q_table[state_key].get)

    def calculate_reward(
        self,
        success: bool,
        latency_ms: float,
        cost_bps: float
    ) -> float:
        """
        Multi-objective reward function.

        R = w1 * I(Success) + w2 * (1 - Latency/MaxLatency) - w3 * Cost
        """
        success_reward = self.w_success if success else -1.0
        latency_reward = self.w_latency * (1 - min(latency_ms / 5000, 1.0))
        cost_penalty = self.w_cost * (cost_bps / 100)

        return success_reward + latency_reward - cost_penalty

    def update(
        self,
        state: TransactionState,
        provider: PaymentProvider,
        reward: float,
        next_state: TransactionState
    ):
        """Update Q-table using Bellman equation."""
        state_key = self._state_to_key(state)
        next_state_key = self._state_to_key(next_state)

        if state_key not in self.q_table:
            self.q_table[state_key] = {p: 0.0 for p in self.providers}
        if next_state_key not in self.q_table:
            self.q_table[next_state_key] = {p: 0.0 for p in self.providers}

        current_q = self.q_table[state_key][provider]
        max_next_q = max(self.q_table[next_state_key].values())

        # Bellman update
        new_q = current_q + self.learning_rate * (
            reward + self.discount_factor * max_next_q - current_q
        )
        self.q_table[state_key][provider] = new_q
```

**Training Strategy**:
1. **Shadow Mode** (Q3 2025): Log routing decisions but use default provider
2. **A/B Testing** (Q4 2025): Route 10% of traffic via RL model
3. **Live Mode** (Q1 2026): Full RL routing with human oversight

**Reference**: [Reinforcement Learning in Payment Gateways](https://www.researchgate.net/publication/392979625_Reinforcement_Learning_in_Payment_Gateways_Optimizing_Transaction_Routing_for_Minimal_Latency) - ResearchGate, 2024

---

## 6. MPC Custody: Mandatory for Institutional Security

### 6.1. Why MPC Over HSM

**Decision: MPC (Multi-Party Computation) is mandatory.**

| Aspect | HSM (Hardware Security Module) | MPC (Multi-Party Computation) |
|--------|-------------------------------|-------------------------------|
| **Key Storage** | Full key in single device | Key split into shares across parties |
| **Single Point of Failure** | YES - device compromise = total loss | NO - need multiple parties to sign |
| **Disaster Recovery** | Complex, requires physical access | Distributed shares can be recovered |
| **Regulatory Compliance** | Traditional, well-understood | Modern, BCB-accepted for SPSAV |

**Reference**: [Custody Technology with MPC & HSM Security](https://komainu.com/expertise/custody-technology/) - Komainu, 2024

### 6.2. MPC Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    MPC CUSTODY ARCHITECTURE (Fireblocks)                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  KEY GENERATION (Initial Setup):                                            │
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  Private Key = Share_A + Share_B + Share_C (never reconstructed)   │   │
│  │                                                                     │   │
│  │  Share_A: Citadel HSM (on-premise)                                 │   │
│  │  Share_B: Fireblocks Cloud                                         │   │
│  │  Share_C: Coincover (Disaster Recovery)                            │   │
│  │                                                                     │   │
│  │  Signing Threshold: 2-of-3                                          │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
│  TRANSACTION SIGNING FLOW:                                                  │
│                                                                             │
│  1. Citadel initiates transaction                                          │
│     │                                                                       │
│     ▼                                                                       │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  POLICY ENGINE (Fireblocks)                                         │   │
│  │                                                                     │   │
│  │  Rules:                                                             │   │
│  │  • Amount > $10,000 → Requires 2 human approvers                   │   │
│  │  • New address → 24-hour delay                                     │   │
│  │  • Withdrawal to exchange → Compliance officer approval            │   │
│  │                                                                     │   │
│  │  IF rules pass:                                                     │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│     │                                                                       │
│     ▼                                                                       │
│  2. MPC Signing Ceremony (2-of-3)                                          │
│     │                                                                       │
│     │  ┌─────────┐      ┌─────────┐                                        │
│     │  │Share_A  │ ──── │Share_B  │                                        │
│     │  │(Citadel)│      │(Fireblks│                                        │
│     │  └─────────┘      └─────────┘                                        │
│     │       │                │                                             │
│     │       └────────┬───────┘                                             │
│     │                │                                                     │
│     │                ▼                                                     │
│     │       Partial Signature A                                            │
│     │       Partial Signature B                                            │
│     │                │                                                     │
│     │                ▼                                                     │
│     │       AGGREGATE → Full Signature                                     │
│     │       (Key never reconstructed)                                      │
│     │                                                                       │
│     ▼                                                                       │
│  3. Broadcast signed transaction to blockchain                             │
│                                                                             │
│  DISASTER RECOVERY:                                                         │
│  • If Fireblocks is unavailable: Use Share_A + Share_C (Coincover)         │
│  • If Citadel HSM is compromised: Rotate to new key, Share_B + Share_C     │
│  • Funds are NEVER at risk of total loss                                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Vendor Selection**: **Fireblocks** (primary) - Has specific support for Brazil SPSAV compliance.

**Reference**: [Finding End-to-End Security in Crypto Custody](https://learn.anchorage.com/Finding-End-to-End-Security-in-Crypto-Custody.pdf) - Anchorage Digital, 2024

---

## 7. Zero Trust Security Architecture

### 7.1. Identity-Aware Access (Teleport)

**SSH keys are banned.** All engineer access to production infrastructure is mediated by **Teleport**:

```yaml
# Teleport Configuration for SPSAV Compliance
teleport_config:
  auth_service:
    authentication:
      type: oidc
      connector_name: okta  # SSO integration

  access:
    roles:
      - name: engineer
        allow:
          logins: [ubuntu, ec2-user]
          kubernetes_groups: [developers]
          db_names: [readonly_replica]
        deny:
          logins: [root]
          kubernetes_groups: [admins]

      - name: sre_oncall
        allow:
          logins: [ubuntu, ec2-user, root]  # Root only for SRE
          kubernetes_groups: [admins]
          db_names: ['*']
        require:
          roles: [engineer]  # Must also be engineer
          mfa: true
          reason: true  # Must provide justification

    certificates:
      ttl: 1h  # Short-lived certificates (SPSAV requirement)
      max_ttl: 4h

  session_recording:
    enabled: true
    mode: strict  # All keystrokes logged
    storage: s3://citadel-audit-logs/teleport/
    retention: 7_years  # SPSAV audit requirement
```

**Why This Matters for SPSAV**: The Brazilian Central Bank requires complete audit trails of all access to financial systems. Teleport's session recording satisfies this requirement.

**Reference**: [Zero Trust Architecture](https://www.nist.gov/publications/zero-trust-architecture) - NIST SP 800-207, 2024

### 7.2. mTLS Everywhere

All microservice-to-microservice communication uses **mutual TLS**:

```yaml
# Istio mTLS Configuration
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: default
  namespace: citadel-production
spec:
  mtls:
    mode: STRICT  # Reject all non-mTLS traffic
---
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
  name: treasury-os-access
  namespace: citadel-production
spec:
  selector:
    matchLabels:
      app: treasury-os
  rules:
    - from:
        - source:
            principals:
              - "cluster.local/ns/citadel-production/sa/payment-service"
              - "cluster.local/ns/citadel-production/sa/voice-agent"
      to:
        - operation:
            methods: ["POST"]
            paths: ["/api/v1/transfers/*"]
```

---

## 8. Compliance Matrix (Brazil 2026)

| Requirement | Regulation | Implementation | Status |
|-------------|------------|----------------|--------|
| **SPSAV License** | Law 14.478 / BCB 519 | Apply for Intermediary → Custodian path | **In Progress** |
| **Capital Requirements** | BCB 520 | R$10.8M initial, scale to R$37.2M | **Funded** |
| **Data Residency** | LGPD | Federated K8s (BR & US), PII in sa-east-1 | **Architected** |
| **Asset Segregation** | BCB 520 | TigerBeetle Multi-Ledger + MPC wallets | **Native Support** |
| **Stablecoin FX Reporting** | BCB 521 | IOF Tax Engine in Payment Router | **Dev Required** |
| **Audit Trails** | SPSAV Rules | TigerBeetle immutable log + Teleport recording | **Native Support** |
| **MPC Custody** | BCB Mandate | Fireblocks integration with 2-of-3 signing | **In Progress** |
| **AML/KYC** | Law 9.613/1998 | Chainalysis + manual review for high-risk | **Standard** |

---

## 9. Implementation Roadmap

### Phase 1: Foundation (Q2 2025)
- Deploy TigerBeetle 6-replica cluster (São Paulo + US East)
- Implement Formance Ledger with Numscript for PIX flows
- Establish Indirect Participant PIX connection via Dock
- Deploy Teleport for Zero Trust access

### Phase 2: Intelligence (Q3 2025)
- Deploy Voice AI edge cluster on Latitude.sh (L40S GPUs)
- Launch Beta Voice Agent with <300ms latency
- Implement RL Payment Router in Shadow Mode
- Integrate Fireblocks MPC custody

### Phase 3: Expansion & Compliance (Q4 2025 - Q1 2026)
- Submit SPSAV license application to BCB
- Activate Live Mode for RL Payment Router
- Migrate Loyalty ledger to TigerBeetle
- Complete SOC 2 Type II certification

### Phase 4: Scale (Q2 2026)
- SPSAV license approval (target: Feb 2026)
- Open API for Livelo/Stix loyalty partners
- Launch full crypto-fiat bridge (USDC ↔ BRL)
- EU expansion preparation (GDPR, MiCA)

---

## 10. References

### TigerBeetle & Financial Infrastructure
1. [Jepsen Analysis: TigerBeetle 0.16.11](https://jepsen.io/analyses/tigerbeetle-0.16.11.pdf) - Jepsen, 2024
2. [TigerBeetle Architecture Documentation](https://github.com/tigerbeetle/tigerbeetle/blob/main/docs/internals/ARCHITECTURE.md) - GitHub, 2024
3. [TigerBeetle Performance](https://docs.tigerbeetle.com/concepts/performance/) - TigerBeetle Docs, 2024
4. [Two-Phase Transfers](https://docs.tigerbeetle.com/coding/two-phase-transfers/) - TigerBeetle Docs, 2024
5. [Cluster Recommendations](https://docs.tigerbeetle.com/operating/cluster/) - TigerBeetle Docs, 2024
6. [Why TigerBeetle Is The Most Interesting Database](https://www.amplifypartners.com/blog-posts/why-tigerbeetle-is-the-most-interesting-database-in-the-world) - Amplify Partners, 2024

### Formance & Numscript
7. [What is Numscript and Why is it Awesome?](https://www.formance.com/blog/engineering/numscript) - Formance, 2024
8. [Numscript Introduction](https://docs.formance.com/modules/numscript/introduction) - Formance Docs, 2024
9. [Formance Ledger](https://www.formance.com/modules/ledger) - Formance, 2024

### Temporal & Durable Execution
10. [Designing High-Performance Financial Ledgers with Temporal](https://temporal.io/blog/designing-high-performance-financial-ledgers-with-temporal) - Temporal, 2024
11. [Mastering Saga Patterns for Distributed Transactions](https://temporal.io/blog/mastering-saga-patterns-for-distributed-transactions-in-microservices) - Temporal, 2024
12. [Saga Pattern Made Easy](https://temporal.io/blog/saga-pattern-made-easy) - Temporal, 2024

### Brazilian Crypto Regulation
13. [Brazil's Central Bank Unveils New Regulatory Framework](https://international.anbima.com.br/news/brazil-s-central-bank-unveils-new-regulatory-framework-for-cryptoassets) - ANBIMA, 2024
14. [Brazil Extends Financial Sector Regulations to Crypto](https://www.theblock.co/post/378295/brazil-crypto-new-rules) - The Block, 2024
15. [New Regulatory Framework for VASPs in Brazil](https://chambers.com/articles/new-regulatory-framework-for-virtual-asset-service-providers-in-brazil) - Chambers, 2024
16. [What Institutions Need to Know for SPSAV Readiness](https://www.fireblocks.com/blog/what-to-know-brazil-spsav-framework) - Fireblocks, 2024
17. [Breaking Down Brazil's New Crypto Framework](https://www.chainalysis.com/blog/brazil-crypto-asset-regulatory-framework-2025/) - Chainalysis, 2024

### PIX & Brazilian Payments
18. [PIX Integration through EBANX API](https://docs.ebanx.com/docs/payments/guides/accept-payments/api/brazil/pix/) - EBANX, 2024
19. [BRZ Stablecoin](https://app.rwa.xyz/assets/BRZ) - RWA.xyz, 2024
20. [Finchtrade OTC Desk](https://finchtrade.com/) - Finchtrade, 2024

### Voice AI & Latency
21. [WebRTC vs WebSocket for Real-Time Audio](https://medium.com/@inssa1102/websocket-vs-webrtc-for-real-time-audio-communication-d3b05edb5f41) - Medium, 2024
22. [Why WebRTC Is Best for Voice AI](https://webrtc.ventures/2025/10/why-webrtc-is-the-best-transport-for-real-time-voice-ai-architectures/) - WebRTC.ventures, 2025
23. [Solving Voice AI Latency](https://medium.com/@reveorai/solving-voice-ai-latency-from-5-seconds-to-sub-1-second-responses-d0065e520799) - Medium, 2024
24. [Voice AI Infrastructure Guide 2025](https://introl.com/blog/voice-ai-infrastructure-real-time-speech-agents-asr-tts-guide-2025) - Introl, 2025
25. [How to Optimize Latency for Conversational AI](https://elevenlabs.io/blog/how-do-you-optimize-latency-for-conversational-ai) - ElevenLabs, 2024

### GPU Infrastructure
26. [GCE Latency - São Paulo Region](https://groups.google.com/g/gce-discussion/c/hlKY_9cHD38) - Google Groups, 2024
27. [Oracle Cloud GPU Infrastructure](https://www.oracle.com/cloud/compute/gpu/) - Oracle, 2024
28. [Latitude.sh Pricing](https://www.latitude.sh/pricing) - Latitude.sh, 2024
29. [AI on Bare Metal in Brazil](https://www.melbicom.net/blog/dedicated/brazil-ai-bare-metal-latency/) - Melbicom, 2024

### MPC Custody
30. [Custody Technology with MPC & HSM](https://komainu.com/expertise/custody-technology/) - Komainu, 2024
31. [MPC vs HSM Wallets](https://www.youtube.com/watch?v=5NLAmEM8igo) - YouTube, 2024
32. [Finding End-to-End Security in Crypto Custody](https://learn.anchorage.com/Finding-End-to-End-Security-in-Crypto-Custody.pdf) - Anchorage, 2024
33. [Institutional Crypto Wallet Security](https://www.cobo.com/post/is-your-crypto-custody-institution-ready-a-security-benchmark) - Cobo, 2024

### Loyalty & Partners
34. [Livelo Innovates with Axway](https://blog.axway.com/life-axway/customer-experience/livelo-innovates-with-axway) - Axway, 2024
35. [Stix Creates Loyalty Ecosystem with Oracle Cloud](https://www.oracle.com/tw/customers/stix-fidelidade/) - Oracle, 2024

### Payment Routing & RL
36. [RL in Payment Gateways: Optimizing Transaction Routing](https://www.researchgate.net/publication/392979625_Reinforcement_Learning_in_Payment_Gateways_Optimizing_Transaction_Routing_for_Minimal_Latency) - ResearchGate, 2024
37. [Reinforcement Learning for Network Routing](https://ir.library.oregonstate.edu/downloads/gh93gz52t) - Oregon State, 2024

### Security & Compliance
38. [Zero Trust Architecture](https://www.nist.gov/publications/zero-trust-architecture) - NIST SP 800-207, 2024
39. [What is Zero Trust Security?](https://www.cloudflare.com/learning/security/glossary/what-is-zero-trust/) - Cloudflare, 2024
40. [Zero Trust Architecture - Palo Alto](https://www.paloaltonetworks.com/cyberpedia/what-is-a-zero-trust-architecture) - Palo Alto Networks, 2024

### Data Residency & LGPD
41. [EU Draft Adequacy Decision for Brazil - LGPD](https://www.mayerbrown.com/en/insights/publications/2025/12/european-data-protection-board-opinion-eu-draft-adequacy-decision-for-brazil-lgpd) - Mayer Brown, 2025
42. [Data Residency in Fintech](https://www.index.dev/blog/data-residency-in-fintech) - Index.dev, 2024

---

**Document Statistics:**
- **Lines**: ~1,650
- **Citations**: 42+ authoritative sources with URLs
- **Open Items Addressed**: 25/25
- **New Topics from Research**: 12 major additions
- **Strategic Decisions**: CTO-level with regulatory compliance

---

*This document represents Version 3 of the Production Infrastructure Strategic Decisions, incorporating deep technical research on Treasury OS internals, Brazilian crypto regulation (SPSAV), and edge AI infrastructure. It provides the definitive architectural blueprint for Citadel OS's $75-100M ARR platform.*

