# Engineering Specification: Advanced Fintech & Crypto Platform

## Document Control
| Field | Value |
|-------|-------|
| Spec ID | SPEC-FINTECH-P3G4 |
| Skills Covered | SKILL-158, SKILL-159, SKILL-160, SKILL-161, SKILL-162, SKILL-163, SKILL-164, SKILL-165, SKILL-166, SKILL-167 |
| Phase | Phase 3 |
| Group | Group 4 - Advanced Fintech & Crypto |
| Status | SPECIFIED |
| Created | 2026-01-07 |
| Author | Citadel OS Engineering |

---

## 1. Executive Summary

This specification defines the engineering implementation for the **Advanced Fintech & Crypto Platform**, a comprehensive blockchain-enabled financial infrastructure supporting multi-chain stablecoin payments, on-chain credit scoring, automated yield optimization, and regulatory-compliant tax automation for property management operations.

### 1.1 Skills Coverage

| Skill ID | Skill Name | Priority | Complexity |
|----------|------------|----------|------------|
| SKILL-158 | Multi-Chain Stablecoin Rent Collection | P0 | High |
| SKILL-159 | Blockchain-Based Credit Scoring | P1 | High |
| SKILL-160 | Automated Yield Generation | P1 | High |
| SKILL-161 | International Wire Management | P1 | Medium |
| SKILL-162 | Yield-Bearing Security Deposits | P2 | Medium |
| SKILL-163 | Rent Receivable Financing | P2 | High |
| SKILL-164 | Automated Insurance Management | P2 | Medium |
| SKILL-165 | Fractional Property Ownership | P3 | Very High |
| SKILL-166 | Global Currency Management | P1 | High |
| SKILL-167 | Automated Tax Compliance | P0 | High |

### 1.2 Key Differentiators

1. **Multi-Chain Gas Optimization**: Intelligent chain selection (Ethereum, Polygon, Solana, Base) minimizing transaction costs
2. **On-Chain Credit Scoring**: Spectral Finance MACRO Score integration for under-collateralized lending
3. **Institutional-Grade Custody**: Fireblocks MPC with 2-of-3 threshold signing
4. **TigerBeetle Integration**: 1M+ TPS financial ledger with strict serializability
5. **Regulatory-First Design**: Embedded AML/KYC, OFAC screening, and automated tax reporting

---

## 2. Technology Stack

### 2.1 Backend Services

```yaml
languages:
  primary: Python 3.12+
  secondary: Rust (TigerBeetle client)
  smart_contracts: Solidity 0.8+

frameworks:
  api: FastAPI 0.104+
  async: asyncio, aiohttp
  data: pandas 2.1+, numpy 1.24+
  
blockchain:
  - Circle SDK (Enterprise stablecoin APIs)
  - Web3.py 6.0+ (Ethereum)
  - Solana SDK (Solana network)
  - Ethers.js (TypeScript blockchain)
  
financial:
  - TigerBeetle Client Libraries
  - python-accounting
  - forex-python
  - QuantLib (derivatives)
```

### 2.2 Frontend

```yaml
web:
  framework: React 19.0+
  language: TypeScript 5.3+
  styling: TailwindCSS 4.1+
  state: Zustand 4.4+
  
mobile:
  framework: React Native 0.73+
  language: TypeScript
  wallet_connect: WalletConnect v2
```

### 2.3 Data Layer

```yaml
databases:
  financial_ledger:
    engine: TigerBeetle 0.16+
    replicas: 6
    consensus: Viewstamped Replication
    throughput: 1M+ TPS
    
  metadata:
    engine: PostgreSQL 16+
    extensions:
      - uuid-ossp
      - pgcrypto
      - pg_cron
    
  caching:
    engine: Redis 7.2+
    mode: Cluster
    persistence: AOF + RDB
    
  document_storage:
    service: AWS S3
    encryption: AES-256
```

### 2.4 Infrastructure

```yaml
cloud: AWS
container_orchestration: ECS Fargate
regions:
  primary: us-east-1
  dr: us-west-2
  brazil: sa-east-1
  
workflow_orchestration: Temporal 1.22+
message_streaming: Redpanda 23.3+
```

### 2.5 Third-Party Integrations

```yaml
blockchain_payments:
  - Circle Enterprise APIs (USDC/EURC)
  - BVNK Enterprise Payments
  
defi_protocols:
  - Ondo Finance (USDY/OUSG - tokenized T-bills)
  - Aave Protocol (lending/borrowing)
  
credit_scoring:
  - Spectral Finance MACRO Score API
  
custody:
  - Fireblocks MPC Platform
  - Fireblocks Trust Company (regulated custody)
  
compliance:
  - Chainalysis AML Screening
  - Elliptic (backup AML)
  - OFAC Sanctions Database
  
international_payments:
  - Wise Business API
  - Finastra Global PAYplus
  
fx_rates:
  - OANDA Real-time FX
  - XE Currency Data
  - ECB Reference Rates
```

---

## 3. System Architecture

### 3.1 Service Decomposition

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        API Gateway (Rust/Axum)                          │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐         │
│  │    Payment      │  │    Treasury     │  │    Custody      │         │
│  │  Orchestrator   │  │     Engine      │  │    Service      │         │
│  │   (SKILL-158)   │  │   (SKILL-160)   │  │  (Cross-cutting)│         │
│  └────────┬────────┘  └────────┬────────┘  └────────┬────────┘         │
│           │                    │                    │                   │
│  ┌────────┴────────┐  ┌────────┴────────┐  ┌────────┴────────┐         │
│  │   Compliance    │  │  Credit Scoring │  │  Multi-Currency │         │
│  │     Engine      │  │    Service      │  │   Accounting    │         │
│  │   (SKILL-167)   │  │   (SKILL-159)   │  │   (SKILL-166)   │         │
│  └────────┬────────┘  └────────┬────────┘  └────────┬────────┘         │
│           │                    │                    │                   │
│  ┌────────┴────────┐  ┌────────┴────────┐  ┌────────┴────────┐         │
│  │  International  │  │Security Deposit │  │   Tokenization  │         │
│  │  Wire Manager   │  │   Yield Service │  │    Service      │         │
│  │   (SKILL-161)   │  │   (SKILL-162)   │  │   (SKILL-165)   │         │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘         │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                    Temporal Workflow Orchestration                       │
├─────────────────────────────────────────────────────────────────────────┤
│                         TigerBeetle Cluster                             │
│              (6 replicas, Viewstamped Replication)                      │
└─────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Service Responsibilities

| Service | Domain | Key Responsibilities |
|---------|--------|---------------------|
| Payment Orchestrator | Stablecoin Processing | Multi-chain routing, gas optimization, settlement |
| Treasury Engine | Yield Management | Risk-adjusted allocation, DeFi protocol integration |
| Custody Service | Asset Security | MPC wallet management, transaction signing |
| Compliance Engine | Regulatory | AML/KYC screening, tax automation, OFAC |
| Credit Scoring | Risk Assessment | MACRO Score calculation, lending terms |
| Multi-Currency Accounting | Global Operations | FX revaluation, IFRS/FASB compliance |

---

## 4. Skill Specifications

### 4.1 SKILL-158: Multi-Chain Stablecoin Rent Collection

#### 4.1.1 Overview
Enable tenants to pay rent using stablecoins (USDC, USDT, EURC) across multiple blockchain networks with intelligent gas optimization.

#### 4.1.2 Core Components

```python
@dataclass
class StablecoinPaymentRequest:
    payment_id: UUID
    property_id: UUID
    guest_id: UUID
    amount_usd: Decimal
    stablecoin: str  # "USDC", "USDT", "EURC"
    preferred_chains: List[str]  # ["polygon", "solana", "base"]
    auto_convert_fiat: bool
    payment_deadline: datetime

@dataclass
class GasOptimizationResult:
    selected_chain: str
    estimated_gas_usd: Decimal
    savings_vs_ethereum: Decimal
    confirmation_time_seconds: int


class GasOptimizer:
    """Select optimal blockchain network based on gas costs"""
    
    CHAIN_GAS_ESTIMATES = {
        BlockchainNetwork.ETHEREUM: Decimal("25.00"),
        BlockchainNetwork.POLYGON: Decimal("0.15"),
        BlockchainNetwork.SOLANA: Decimal("0.0003"),
        BlockchainNetwork.BASE: Decimal("0.05")
    }
    
    def select_optimal_chain(self, 
                           amount: Decimal, 
                           chains: List[BlockchainNetwork]) -> GasOptimizationResult:
        """Select chain with lowest total cost"""
        
        # Filter to supported chains
        available_chains = [c for c in chains if c in self.CHAIN_GAS_ESTIMATES]
        
        if not available_chains:
            raise NoSupportedChainError("No supported chains in request")
        
        # Select minimum cost chain
        selected = min(available_chains, 
                      key=lambda c: self.CHAIN_GAS_ESTIMATES[c])
        
        eth_cost = self.CHAIN_GAS_ESTIMATES[BlockchainNetwork.ETHEREUM]
        selected_cost = self.CHAIN_GAS_ESTIMATES[selected]
        
        return GasOptimizationResult(
            selected_chain=selected.value,
            estimated_gas_usd=selected_cost,
            savings_vs_ethereum=eth_cost - selected_cost,
            confirmation_time_seconds=self.get_confirmation_time(selected)
        )
```

#### 4.1.3 Circle API Integration

```python
class CirclePaymentProcessor:
    """Enterprise-grade Circle API integration"""
    
    def __init__(self, api_key: str, environment: str = "production"):
        self.client = CircleClient(
            api_key=api_key,
            base_url="https://api.circle.com" if environment == "production"
                     else "https://api-sandbox.circle.com"
        )
    
    async def create_payment_request(self,
                                   request: StablecoinPaymentRequest) -> PaymentLink:
        """Create multi-chain payment request with QR code"""
        
        # Optimize chain selection
        gas_result = self.gas_optimizer.select_optimal_chain(
            amount=request.amount_usd,
            chains=request.preferred_chains
        )
        
        # Create Circle payment intent
        response = await self.client.create_payment_intent({
            "idempotencyKey": str(request.payment_id),
            "amount": {
                "amount": str(request.amount_usd),
                "currency": "USD"
            },
            "settlementCurrency": "USD",
            "paymentMethods": [{
                "type": "blockchain",
                "chain": gas_result.selected_chain
            }],
            "metadata": {
                "property_id": str(request.property_id),
                "guest_id": str(request.guest_id),
                "payment_type": "rent"
            }
        })
        
        return PaymentLink(
            payment_id=response["data"]["id"],
            payment_url=response["data"]["checkoutUrl"],
            qr_code=self.generate_eip681_qr(response["data"]),
            expires_at=datetime.utcnow() + timedelta(hours=24),
            selected_chain=gas_result.selected_chain,
            gas_estimate=gas_result.estimated_gas_usd
        )
    
    async def handle_webhook(self, webhook_data: Dict) -> None:
        """Process Circle webhook notifications"""
        event_type = webhook_data.get("type")
        
        if event_type == "payment.confirmed":
            await self.process_confirmation(webhook_data["data"])
        elif event_type == "payment.failed":
            await self.process_failure(webhook_data["data"])
        elif event_type == "payment.settled":
            await self.process_settlement(webhook_data["data"])
```

#### 4.1.4 TigerBeetle Recording

```python
async def record_stablecoin_payment(self, payment: StablecoinPayment) -> str:
    """Record payment in TigerBeetle ledger"""
    
    # Determine ledger based on currency
    ledger_id = self.CURRENCY_LEDGERS[payment.currency]
    
    transfer = Transfer(
        id=self.generate_transfer_id(),
        debit_account_id=self.get_tenant_account(payment.tenant_id),
        credit_account_id=self.get_property_account(payment.property_id),
        amount=int(payment.amount * 100),  # Convert to cents
        ledger=ledger_id,
        code=1001,  # Rent payment code
        user_data_128=payment.payment_id.bytes,
        user_data_64=int(payment.timestamp.timestamp()),
        user_data_32=payment.chain.encode()[:4]
    )
    
    result = await self.tigerbeetle_client.create_transfers([transfer])
    
    if result.errors:
        raise LedgerEntryError(f"Failed to record payment: {result.errors}")
    
    return str(result.transfer_ids[0])
```

---

### 4.2 SKILL-159: Blockchain-Based Credit Scoring

#### 4.2.1 Overview
Leverage Spectral Finance MACRO Score for on-chain creditworthiness assessment, enabling risk-based pricing and under-collateralized lending.

#### 4.2.2 MACRO Score Integration

```python
@dataclass
class MACROScoreRequest:
    wallet_addresses: List[str]
    verification_signatures: List[str]
    assessment_type: str  # "individual", "bundled"
    privacy_level: str  # "standard", "zero_knowledge"

@dataclass
class MACROScoreResult:
    score: int  # 300-850 range
    confidence_level: Decimal
    contributing_factors: Dict[str, Decimal]
    lending_terms: LendingTerms
    validity_period: timedelta


class CreditScoringEngine:
    """On-chain credit assessment using Spectral MACRO Score"""
    
    # Score component weights (matching FICO methodology)
    SCORE_WEIGHTS = {
        "payment_history": 0.30,      # DeFi loan repayments
        "liquidation_history": 0.25,   # Liquidation events
        "amounts_owed_repaid": 0.25,   # Debt utilization
        "credit_mix": 0.15,            # Protocol diversity
        "credit_history_length": 0.05  # Wallet age
    }
    
    async def calculate_macro_score(self, 
                                  request: MACROScoreRequest) -> MACROScoreResult:
        """Calculate MACRO score with privacy preservation"""
        
        # Verify wallet ownership
        ownership_verified = await self.verify_wallet_signatures(
            addresses=request.wallet_addresses,
            signatures=request.verification_signatures
        )
        
        if not ownership_verified:
            raise WalletVerificationError("Unable to verify wallet ownership")
        
        # Aggregate on-chain transaction history
        transaction_data = await self.aggregate_wallet_history(
            addresses=request.wallet_addresses,
            lookback_months=24
        )
        
        # Feature engineering (100+ features)
        features = self.engineer_credit_features(transaction_data)
        
        # Calculate component scores
        score_components = {
            "payment_history": self.analyze_payment_history(features),
            "liquidation_history": self.analyze_liquidations(features),
            "amounts_owed_repaid": self.analyze_debt_ratios(features),
            "credit_mix": self.analyze_protocol_diversity(features),
            "credit_history_length": self.analyze_wallet_age(features)
        }
        
        # Weighted composite score
        final_score = sum(
            component * self.SCORE_WEIGHTS[name]
            for name, component in score_components.items()
        )
        
        # Map to 300-850 range
        normalized_score = int(300 + (final_score * 550))
        
        return MACROScoreResult(
            score=normalized_score,
            confidence_level=self.calculate_confidence(transaction_data),
            contributing_factors=score_components,
            lending_terms=self.calculate_lending_terms(normalized_score),
            validity_period=timedelta(days=7)
        )
    
    def calculate_lending_terms(self, macro_score: int) -> LendingTerms:
        """Risk-based lending terms from MACRO score"""
        
        if macro_score >= 750:  # Excellent
            return LendingTerms(
                max_ltv=Decimal("0.90"),
                interest_rate=Decimal("0.08"),
                collateral_requirement=Decimal("1.10")
            )
        elif macro_score >= 650:  # Good
            return LendingTerms(
                max_ltv=Decimal("0.75"),
                interest_rate=Decimal("0.12"),
                collateral_requirement=Decimal("1.25")
            )
        else:  # Fair
            return LendingTerms(
                max_ltv=Decimal("0.60"),
                interest_rate=Decimal("0.18"),
                collateral_requirement=Decimal("1.50")
            )
```

#### 4.2.3 Anti-Sybil Controls

```python
class AntiSybilValidator:
    """Prevent MACRO score manipulation"""
    
    MINIMUM_WALLET_AGE_MONTHS = 6
    MINIMUM_TRANSACTION_COUNT = 10
    
    async def validate_wallet_authenticity(self, 
                                         addresses: List[str]) -> ValidationResult:
        """Detect artificial wallet activity"""
        
        checks = []
        
        for address in addresses:
            # Check wallet age
            wallet_age = await self.get_wallet_age(address)
            if wallet_age < self.MINIMUM_WALLET_AGE_MONTHS:
                checks.append(ValidationCheck(
                    check="wallet_age",
                    passed=False,
                    reason=f"Wallet age {wallet_age} months < minimum"
                ))
            
            # Check transaction count
            tx_count = await self.get_transaction_count(address)
            if tx_count < self.MINIMUM_TRANSACTION_COUNT:
                checks.append(ValidationCheck(
                    check="transaction_count",
                    passed=False,
                    reason=f"Transaction count {tx_count} < minimum"
                ))
            
            # Check for wash trading patterns
            wash_trading = await self.detect_wash_trading(address)
            if wash_trading.detected:
                checks.append(ValidationCheck(
                    check="wash_trading",
                    passed=False,
                    reason=wash_trading.pattern_description
                ))
            
            # Cross-wallet correlation check
            related_wallets = await self.find_related_wallets(address)
            if len(related_wallets) > 5:
                checks.append(ValidationCheck(
                    check="wallet_clustering",
                    passed=False,
                    reason=f"Found {len(related_wallets)} related wallets"
                ))
        
        return ValidationResult(
            passed=all(c.passed for c in checks),
            checks=checks
        )
```

---

### 4.3 SKILL-160: Automated Yield Generation

#### 4.3.1 Overview
Optimize idle operating capital through automated allocation across traditional and DeFi yield sources with institutional-grade risk management.

#### 4.3.2 Treasury Optimization Engine

```python
@dataclass
class TreasuryAllocation:
    protocol: str
    allocation_pct: Decimal
    current_apy: Decimal
    risk_score: int
    liquidity_hours: int

class TreasuryOptimizer:
    """Risk-adjusted yield optimization"""
    
    # Risk profile allocations
    ALLOCATION_PROFILES = {
        "conservative": {
            "treasury_bills": Decimal("0.90"),
            "ondo_usdy": Decimal("0.10"),
            "defi_protocols": Decimal("0.00")
        },
        "moderate": {
            "treasury_bills": Decimal("0.70"),
            "ondo_usdy": Decimal("0.20"),
            "defi_protocols": Decimal("0.10")
        },
        "aggressive": {
            "treasury_bills": Decimal("0.50"),
            "ondo_usdy": Decimal("0.30"),
            "defi_protocols": Decimal("0.20")
        }
    }
    
    async def optimize_allocation(self, 
                                portfolio: Portfolio,
                                risk_profile: str) -> List[TreasuryAllocation]:
        """Calculate optimal allocation based on risk profile"""
        
        # Get target allocation percentages
        targets = self.ALLOCATION_PROFILES[risk_profile]
        
        # Fetch current yields
        yield_sources = await self.fetch_yield_sources()
        
        allocations = []
        
        # Treasury Bills (traditional, lowest risk)
        if targets["treasury_bills"] > 0:
            allocations.append(TreasuryAllocation(
                protocol="US Treasury Bills",
                allocation_pct=targets["treasury_bills"],
                current_apy=yield_sources["tbills"]["apy"],
                risk_score=5,  # Very low risk
                liquidity_hours=24
            ))
        
        # Ondo USDY (tokenized T-bills)
        if targets["ondo_usdy"] > 0:
            allocations.append(TreasuryAllocation(
                protocol="Ondo USDY",
                allocation_pct=targets["ondo_usdy"],
                current_apy=yield_sources["usdy"]["apy"],  # ~4.25%
                risk_score=15,  # Low risk
                liquidity_hours=1
            ))
        
        # DeFi protocols (highest yield, higher risk)
        if targets["defi_protocols"] > 0:
            best_defi = self.select_best_defi_protocol(yield_sources)
            allocations.append(TreasuryAllocation(
                protocol=best_defi["name"],
                allocation_pct=targets["defi_protocols"],
                current_apy=best_defi["apy"],
                risk_score=best_defi["risk_score"],
                liquidity_hours=best_defi["withdrawal_hours"]
            ))
        
        return allocations
    
    async def execute_rebalancing(self, 
                                allocations: List[TreasuryAllocation]) -> RebalancingResult:
        """Execute portfolio rebalancing via Temporal workflow"""
        
        workflow_id = f"rebalance_{uuid.uuid4()}"
        
        result = await self.temporal_client.start_workflow(
            YieldOptimizationWorkflow.run,
            PortfolioAnalysis(allocations=allocations),
            id=workflow_id,
            task_queue="treasury-operations"
        )
        
        return result
```

#### 4.3.3 Ondo Finance Integration

```python
class OndoFinanceIntegration:
    """Integration with Ondo USDY/OUSG yield protocols"""
    
    USDY_CONTRACT = "0x96F6eF951840721AdBF46Ac996b59E0235CB985C"
    
    async def deposit_for_yield(self, 
                               amount_usdc: Decimal,
                               custody_wallet: str) -> YieldDepositResult:
        """Convert USDC to USDY for yield generation"""
        
        # Step 1: Approve USDC spending via Fireblocks
        approve_tx = await self.fireblocks.create_transaction(
            asset_id="USDC",
            source_id=custody_wallet,
            destination_address=self.USDY_CONTRACT,
            amount=str(amount_usdc),
            operation="APPROVE"
        )
        
        # Step 2: Deposit USDC for USDY
        deposit_tx = await self.fireblocks.create_transaction(
            asset_id="USDC",
            source_id=custody_wallet,
            destination_address=self.USDY_CONTRACT,
            amount=str(amount_usdc),
            operation="CONTRACT_CALL",
            extra_parameters={
                "contractCallData": self.encode_deposit_call(amount_usdc)
            }
        )
        
        # Step 3: Start yield tracking
        yield_tracking = await self.start_yield_tracking(
            deposit_amount=amount_usdc,
            deposit_tx_hash=deposit_tx["id"],
            expected_apy=Decimal("4.25")
        )
        
        return YieldDepositResult(
            deposit_tx_hash=deposit_tx["id"],
            usdy_amount=amount_usdc,
            expected_annual_yield=amount_usdc * Decimal("0.0425"),
            yield_tracking_id=yield_tracking.tracking_id
        )
    
    async def calculate_accrued_yield(self, 
                                    deposit_amount: Decimal,
                                    days_held: int) -> Decimal:
        """Calculate accrued yield based on USDY APY"""
        current_apy = await self.get_current_usdy_apy()
        daily_rate = current_apy / Decimal("365")
        return deposit_amount * daily_rate * Decimal(str(days_held))
```

---

### 4.4 SKILL-166: Global Currency Management

#### 4.4.1 Multi-Currency Ledger Design

```python
@dataclass
class MultiCurrencyTransaction:
    transaction_id: UUID
    functional_currency: str  # USD for US operations
    transaction_currency: str  # EUR, BRL, USDC
    amount_transaction: Decimal
    amount_functional: Decimal
    fx_rate: Decimal
    fx_rate_source: str
    transaction_date: datetime
    settlement_date: datetime


class MultiCurrencyLedger:
    """Multi-currency accounting with TigerBeetle"""
    
    # Currency to TigerBeetle ledger mapping
    CURRENCY_LEDGERS = {
        "USD": 700,
        "USDC": 701,
        "EUR": 702,
        "BRL": 703,
        "GBP": 704,
        "CAD": 705,
        "USDY": 706
    }
    
    async def record_transaction(self, 
                               txn: MultiCurrencyTransaction) -> str:
        """Record multi-currency transaction in TigerBeetle"""
        
        transfers = []
        
        # Calculate FX gain/loss if settlement differs
        fx_gain_loss = self.calculate_fx_variance(txn)
        
        # Primary transaction entry
        transfers.append(Transfer(
            id=self.generate_transfer_id(),
            debit_account_id=self.get_account_id(txn.debit_account),
            credit_account_id=self.get_account_id(txn.credit_account),
            amount=int(txn.amount_functional * 100),
            ledger=self.CURRENCY_LEDGERS[txn.functional_currency],
            code=self.get_transaction_code(txn),
            user_data_128=txn.transaction_id.bytes
        ))
        
        # FX gain/loss entry if applicable
        if fx_gain_loss != 0:
            transfers.append(Transfer(
                id=self.generate_transfer_id(),
                debit_account_id=self.get_fx_account(fx_gain_loss > 0),
                credit_account_id=self.get_fx_account(fx_gain_loss < 0),
                amount=abs(int(fx_gain_loss * 100)),
                ledger=self.CURRENCY_LEDGERS[txn.functional_currency],
                code=988,  # IRC Section 988 FX code
                user_data_128=f"fx_{txn.transaction_id}".encode()
            ))
        
        # Execute atomic batch
        result = await self.tigerbeetle_client.create_transfers(transfers)
        return str(result.transfer_ids[0])
    
    async def monthly_fx_revaluation(self) -> List[Transfer]:
        """Perform monthly FX revaluation per IFRS ASC 830"""
        
        open_positions = await self.get_open_fx_positions()
        revaluation_entries = []
        
        for position in open_positions:
            current_rate = await self.fx_service.get_current_rate(
                from_currency=position.currency,
                to_currency="USD"
            )
            
            unrealized_gain_loss = (
                position.amount * current_rate -
                position.amount * position.original_rate
            )
            
            if abs(unrealized_gain_loss) > Decimal("1.00"):
                revaluation_entries.append(Transfer(
                    id=self.generate_transfer_id(),
                    debit_account_id=self.get_oci_account(),
                    credit_account_id=self.get_fx_revaluation_account(),
                    amount=int(abs(unrealized_gain_loss) * 100),
                    ledger=700,  # USD ledger
                    code=830,  # IFRS ASC 830 code
                    user_data_128=f"reval_{position.id}".encode()
                ))
        
        return await self.tigerbeetle_client.create_transfers(revaluation_entries)
```

---

### 4.5 SKILL-167: Automated Tax Compliance

#### 4.5.1 Tax Automation Engine

```python
class TaxAutomationService:
    """Automated tax reporting and compliance"""
    
    FORM_1099_THRESHOLD = Decimal("600.00")
    BACKUP_WITHHOLDING_RATE = Decimal("0.24")
    
    async def generate_1099_forms(self, tax_year: int) -> List[Tax1099Form]:
        """Generate 1099 forms for all qualifying vendors"""
        
        # Query annual payment totals from TigerBeetle
        vendor_payments = await self.tigerbeetle_client.query_annual_payments(
            tax_year=tax_year,
            minimum_threshold=self.FORM_1099_THRESHOLD
        )
        
        forms = []
        
        for vendor_id, total_amount in vendor_payments.items():
            # Validate W-9 on file
            w9_status = await self.validate_w9_status(vendor_id)
            
            if not w9_status.valid:
                # Apply 24% backup withholding
                withholding = total_amount * self.BACKUP_WITHHOLDING_RATE
                await self.apply_backup_withholding(vendor_id, withholding)
            
            # Determine 1099 form type
            form_type = self.determine_1099_type(vendor_id, total_amount)
            
            form = Tax1099Form(
                form_id=uuid.uuid4(),
                tax_year=tax_year,
                form_type=form_type,
                payee_tin=w9_status.tin,
                payee_name=w9_status.legal_name,
                total_amount=total_amount,
                backup_withholding=withholding if not w9_status.valid else Decimal("0"),
                state_filing_required=self.requires_state_filing(vendor_id)
            )
            
            forms.append(form)
        
        return forms
    
    async def efile_with_irs(self, forms: List[Tax1099Form]) -> FilingResult:
        """Submit forms to IRS e-filing system"""
        
        # Convert to IRS XML schema
        xml_payload = self.convert_to_irs_xml(forms)
        
        # Submit to IRS FIRE system
        filing_result = await self.irs_client.submit_efile(
            xml_data=xml_payload,
            filing_type="ORIGINAL",
            payer_tin=self.company_tin
        )
        
        # Record filing in database
        await self.record_filing(forms, filing_result)
        
        return filing_result
```

#### 4.5.2 AML/KYC Compliance Engine

```python
@dataclass
class ComplianceScreeningResult:
    screening_id: str
    aml_status: str  # "cleared", "flagged", "blocked"
    ofac_status: str
    risk_score: int  # 0-100
    required_actions: List[str]
    expiry_timestamp: datetime


class ComplianceProcessor:
    """Real-time AML/KYC compliance screening"""
    
    async def screen_transaction(self, 
                               wallet_address: str,
                               amount: Decimal,
                               jurisdiction: str) -> ComplianceScreeningResult:
        """Perform real-time AML/KYC screening"""
        
        # OFAC sanctions screening
        ofac_result = await self.chainalysis_client.screen_address(
            address=wallet_address,
            amount=amount
        )
        
        # AML risk assessment
        aml_result = await self.chainalysis_client.assess_risk(
            address=wallet_address,
            transaction_history_days=90
        )
        
        # Combine results
        combined_risk = self.calculate_combined_risk(ofac_result, aml_result)
        
        # Determine required actions
        actions = []
        if combined_risk.score > 70:
            actions.append("enhanced_due_diligence")
        if combined_risk.score > 85:
            actions.append("manual_review")
        if ofac_result.status == "flagged":
            actions.append("block_transaction")
        
        return ComplianceScreeningResult(
            screening_id=f"cs_{uuid.uuid4()}",
            aml_status=self.determine_aml_status(combined_risk),
            ofac_status=ofac_result.status,
            risk_score=combined_risk.score,
            required_actions=actions,
            expiry_timestamp=datetime.utcnow() + timedelta(hours=24)
        )
```

---

## 5. Security Architecture

### 5.1 Fireblocks MPC Custody

```python
@dataclass
class MPCWalletConfig:
    wallet_name: str
    asset_types: List[str]
    threshold_signatures: int  # 2-of-3
    key_share_distribution: List[str]
    policy_template: str
    emergency_controls: bool


class FireblocksCustodyService:
    """Institutional-grade MPC wallet management"""
    
    async def create_mpc_wallet(self, config: MPCWalletConfig) -> MPCWallet:
        """Create MPC wallet with distributed key shares"""
        
        # Initiate key generation ceremony
        key_ceremony = await self.initiate_key_generation(
            participants=config.key_share_distribution,
            threshold=config.threshold_signatures
        )
        
        # Distribute key shares to secure enclaves
        key_shares = await self.distribute_key_shares(
            ceremony=key_ceremony,
            hardware_enclaves=self.get_sgx_enclaves()
        )
        
        # Configure transaction policies
        policies = await self.configure_policies(
            template=config.policy_template,
            approval_threshold=config.threshold_signatures,
            emergency_controls=config.emergency_controls
        )
        
        return MPCWallet(
            wallet_id=key_ceremony.wallet_id,
            public_address=key_ceremony.public_address,
            key_shares=key_shares,
            policies=policies
        )
    
    async def sign_transaction(self,
                             transaction: BlockchainTransaction,
                             required_approvals: List[str]) -> TransactionSignature:
        """Execute MPC signing with threshold approval"""
        
        # Validate transaction against policies
        policy_check = await self.validate_transaction_policy(
            transaction=transaction,
            approvers=required_approvals
        )
        
        if not policy_check.approved:
            raise PolicyViolationError(policy_check.reason)
        
        # Initiate distributed signing
        signing_session = await self.initiate_signing_session(
            transaction_hash=transaction.hash,
            required_participants=required_approvals
        )
        
        # Collect signature shares
        signature_shares = []
        for participant in required_approvals:
            share = await self.request_signature_share(
                participant_id=participant,
                transaction_hash=transaction.hash,
                signing_session_id=signing_session.session_id
            )
            signature_shares.append(share)
        
        # Combine shares into final signature
        final_signature = self.combine_signature_shares(signature_shares)
        
        return TransactionSignature(
            signature=final_signature,
            signing_session_id=signing_session.session_id,
            participants=required_approvals,
            timestamp=datetime.utcnow()
        )
```

### 5.2 Security Controls

| Layer | Control | Implementation |
|-------|---------|----------------|
| Hardware | Intel SGX Enclaves | Key shares stored in secure hardware |
| Policy | Maker/Checker | Multi-signature approval workflows |
| Network | DDoS Protection | Cloudflare + WAF |
| Data | Encryption | AES-256 at rest, TLS 1.3 in transit |
| Access | Zero Trust | mTLS, short-lived tokens |
| Audit | Immutable Logs | TigerBeetle event sourcing |

---

## 6. Database Schema

### 6.1 PostgreSQL Schema

```sql
-- Stablecoin Payments
CREATE TABLE stablecoin_payments (
    payment_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    property_id UUID NOT NULL REFERENCES properties(property_id),
    guest_id UUID NOT NULL REFERENCES guests(guest_id),
    amount_usd NUMERIC(12,2) NOT NULL,
    stablecoin_currency VARCHAR(10) NOT NULL,
    blockchain_network VARCHAR(20) NOT NULL,
    transaction_hash VARCHAR(100),
    settlement_status VARCHAR(20) DEFAULT 'pending',
    tigerbeetle_transfer_id BIGINT,
    gas_fee_usd NUMERIC(10,4),
    created_at TIMESTAMPTZ DEFAULT NOW(),
    settled_at TIMESTAMPTZ
) PARTITION BY RANGE (created_at);

-- Multi-Currency Transactions
CREATE TABLE multi_currency_transactions (
    transaction_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tigerbeetle_transfer_id BIGINT NOT NULL UNIQUE,
    functional_currency CHAR(3) NOT NULL,
    transaction_currency CHAR(3) NOT NULL,
    amount_transaction NUMERIC(20,8) NOT NULL,
    amount_functional NUMERIC(20,8) NOT NULL,
    fx_rate NUMERIC(12,8) NOT NULL,
    fx_rate_source VARCHAR(50) NOT NULL,
    transaction_date TIMESTAMPTZ NOT NULL,
    settlement_date TIMESTAMPTZ,
    realized_fx_gain_loss NUMERIC(20,8) DEFAULT 0,
    created_at TIMESTAMPTZ DEFAULT NOW()
) PARTITION BY RANGE (transaction_date);

-- Treasury Yield Positions
CREATE TABLE yield_positions (
    position_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    protocol_name VARCHAR(50) NOT NULL,
    asset_type VARCHAR(20) NOT NULL,
    principal_amount NUMERIC(16,2) NOT NULL,
    current_apy NUMERIC(6,4) NOT NULL,
    entry_date DATE NOT NULL,
    maturity_date DATE,
    accrued_yield NUMERIC(16,2) DEFAULT 0,
    risk_score INTEGER CHECK (risk_score BETWEEN 0 AND 100),
    fireblocks_vault_id VARCHAR(50),
    status VARCHAR(20) DEFAULT 'active'
);

-- Compliance Screenings
CREATE TABLE compliance_screenings (
    screening_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    entity_type VARCHAR(20) NOT NULL,
    entity_id UUID NOT NULL,
    screening_type VARCHAR(30) NOT NULL,
    risk_score INTEGER CHECK (risk_score BETWEEN 0 AND 100),
    screening_result VARCHAR(20) NOT NULL,
    screening_provider VARCHAR(50) NOT NULL,
    flagged_reasons TEXT[],
    expiry_timestamp TIMESTAMPTZ NOT NULL,
    created_at TIMESTAMPTZ DEFAULT NOW()
) PARTITION BY RANGE (created_at);

-- Tax Forms
CREATE TABLE tax_forms (
    form_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tax_year INTEGER NOT NULL,
    form_type VARCHAR(10) NOT NULL,
    payee_tin VARCHAR(20) NOT NULL,
    payee_name VARCHAR(200) NOT NULL,
    total_amount_usd NUMERIC(12,2) NOT NULL,
    backup_withholding_applied BOOLEAN DEFAULT FALSE,
    withholding_amount_usd NUMERIC(12,2) DEFAULT 0,
    irs_filing_status VARCHAR(20) DEFAULT 'pending',
    filed_at TIMESTAMPTZ,
    tigerbeetle_payment_refs BIGINT[]
);
```

### 6.2 TigerBeetle Ledger Configuration

```yaml
tigerbeetle_cluster:
  replica_count: 6
  consensus_protocol: viewstamped_replication
  availability_zones:
    us-east-1a: 2
    us-east-1b: 2
    us-east-1c: 2
  performance_target: "1M+ TPS"
  durability: fsync_on_commit
  
ledgers:
  700: "USD - Functional Currency"
  701: "USDC - Stablecoin Operations"
  702: "EUR - European Operations"
  703: "BRL - Brazil Operations (SPSAV)"
  704: "GBP - UK Operations"
  705: "CAD - Canada Operations"
  706: "USDY - Yield-Bearing Deposits"
  999: "Event Log Ledger"
```

---

## 7. Temporal Workflows

### 7.1 Stablecoin Payment Workflow

```python
@workflow.defn
class StablecoinPaymentWorkflow:
    """Multi-step stablecoin payment with guaranteed execution"""
    
    @workflow.run
    async def run(self, request: StablecoinPaymentRequest) -> PaymentResult:
        
        # Step 1: Gas optimization
        gas_analysis = await workflow.execute_activity(
            optimize_gas_fees,
            request,
            start_to_close_timeout=timedelta(seconds=30)
        )
        
        # Step 2: Compliance screening
        compliance = await workflow.execute_activity(
            screen_transaction,
            request,
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        if compliance.status == "blocked":
            raise ComplianceRejectionError(compliance.reason)
        
        # Step 3: Generate payment request
        payment_link = await workflow.execute_activity(
            generate_payment_request,
            gas_analysis,
            start_to_close_timeout=timedelta(seconds=10)
        )
        
        # Step 4: Wait for blockchain confirmation
        confirmation = await workflow.execute_activity(
            wait_for_confirmation,
            payment_link,
            start_to_close_timeout=timedelta(minutes=10),
            retry_policy=RetryPolicy(
                initial_interval=timedelta(seconds=30),
                maximum_interval=timedelta(minutes=2),
                maximum_attempts=5
            )
        )
        
        # Step 5: Fiat conversion (if requested)
        if request.auto_convert_fiat:
            await workflow.execute_activity(
                convert_to_fiat,
                confirmation,
                start_to_close_timeout=timedelta(minutes=5)
            )
        
        # Step 6: Record in TigerBeetle
        ledger_entry = await workflow.execute_activity(
            record_accounting_entry,
            confirmation,
            start_to_close_timeout=timedelta(seconds=30)
        )
        
        # Step 7: Tax reporting check
        await workflow.execute_activity(
            check_tax_reporting_requirements,
            ledger_entry,
            start_to_close_timeout=timedelta(seconds=10)
        )
        
        return PaymentResult(
            payment_id=confirmation.payment_id,
            settlement_time=confirmation.timestamp,
            final_amount_usd=ledger_entry.amount_usd,
            transaction_hash=confirmation.transaction_hash
        )
```

### 7.2 Yield Optimization Workflow

```python
@workflow.defn
class YieldOptimizationWorkflow:
    """Daily yield optimization with risk management"""
    
    @workflow.run
    async def run(self, portfolio: PortfolioAnalysis) -> OptimizationResult:
        
        # Step 1: Risk assessment
        risk_metrics = await workflow.execute_activity(
            assess_portfolio_risk,
            portfolio,
            start_to_close_timeout=timedelta(minutes=5)
        )
        
        # Step 2: Yield opportunity analysis
        opportunities = await workflow.execute_activity(
            analyze_yield_opportunities,
            risk_metrics,
            start_to_close_timeout=timedelta(minutes=10)
        )
        
        # Step 3: Allocation decision
        allocation = await workflow.execute_activity(
            calculate_optimal_allocation,
            opportunities,
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        # Step 4: Execute rebalancing if needed
        if allocation.rebalancing_required:
            await workflow.execute_activity(
                execute_rebalancing,
                allocation,
                start_to_close_timeout=timedelta(minutes=30),
                retry_policy=RetryPolicy(
                    initial_interval=timedelta(seconds=60),
                    maximum_attempts=3
                )
            )
        
        # Step 5: Update performance metrics
        await workflow.execute_activity(
            update_performance_metrics,
            allocation,
            start_to_close_timeout=timedelta(seconds=30)
        )
        
        return OptimizationResult(
            allocation_executed=allocation,
            expected_apy=allocation.projected_yield,
            risk_score=risk_metrics.composite_score,
            next_rebalance_date=datetime.utcnow() + timedelta(days=30)
        )
```

---

## 8. Performance Specifications

### 8.1 Service SLAs

| Metric | Target | Critical Threshold |
|--------|--------|-------------------|
| Payment Processing Latency | < 5 seconds | 30 seconds |
| Stablecoin Settlement | < 10 minutes | 30 minutes |
| Compliance Screening | < 2 minutes | 5 minutes |
| MPC Signing Time | < 30 seconds | 60 seconds |
| API Response Time (P95) | < 200ms | 500ms |
| System Availability | 99.95% | 99.9% |

### 8.2 Scaling Configuration

| Service | Min Instances | Max Instances | Scale Trigger |
|---------|---------------|---------------|---------------|
| Payment Orchestrator | 2 | 20 | >70% CPU or >1000 req/min |
| Treasury Engine | 1 | 5 | >80% CPU or >50 rebalances/hr |
| Custody Service | 2 | 8 | >60% CPU or >100 signatures/min |
| Compliance Engine | 2 | 10 | >60% CPU or >5000 screens/min |

### 8.3 TigerBeetle Performance

```yaml
performance_targets:
  throughput: 1M+ TPS
  latency_p99: 10ms
  batch_size: 8000 transfers
  
optimization:
  use_ulids: true  # 10% higher throughput than random UUIDs
  batch_by_ledger: true
  fsync_on_commit: true
```

---

## 9. Monitoring & Observability

### 9.1 Financial Metrics Dashboard

```python
@dataclass
class FinancialMetrics:
    # Transaction Metrics
    transaction_success_rate: Decimal  # Target: >99.9%
    average_settlement_time: timedelta  # Target: <5 minutes
    gas_optimization_savings: Decimal
    
    # Treasury Metrics
    total_aum: Decimal
    current_yield_apy: Decimal  # Target: 4.5-5.5%
    liquidity_ratio: Decimal  # Target: >5%
    
    # Compliance Metrics
    aml_screening_time: timedelta  # Target: <2 minutes
    tax_form_accuracy: Decimal  # Target: >99.5%
    regulatory_violations: int  # Target: 0
    
    # Custody Metrics
    mpc_signing_time: timedelta  # Target: <30 seconds
    security_incidents: int  # Target: 0
```

### 9.2 Critical Alerts

| Alert | Threshold | Escalation |
|-------|-----------|------------|
| Payment Failure Rate | >1% | Immediate PagerDuty |
| Settlement Delay | >10 minutes | 15-min warning |
| Custody Security Event | Any | Immediate + pause |
| Compliance Violation | Any | Immediate + legal |
| Yield Deviation | >0.5% | 1-hour review |
| Liquidity Shortage | <3% | Immediate rebalance |

---

## 10. Architecture Alignment Notes

### 10.1 Layer Mapping (Citadel OS 6-Layer Stack)

| Component | Layer | Rationale |
|-----------|-------|-----------|
| Payment Orchestrator | Layer 4 (Skills) | Core business logic |
| Treasury Engine | Layer 4 (Skills) | Financial optimization |
| Custody Service | Layer 5 (Hot Path) | Security-critical operations |
| Compliance Engine | Layer 4 (Skills) | Regulatory logic |
| TigerBeetle | Layer 6 (Cold Path) | Financial guarantees |
| Circle/Fireblocks APIs | Layer 6 (Infrastructure) | External integrations |

### 10.2 Execution Path Classification

| Skill | Execution Path | Reasoning |
|-------|---------------|-----------|
| SKILL-158 (Stablecoin Payments) | Hybrid | AI for gas optimization, Cold for settlement |
| SKILL-159 (Credit Scoring) | Hot | ML-based scoring requires AI reasoning |
| SKILL-160 (Yield Generation) | Cold | Financial guarantees via TigerBeetle |
| SKILL-166 (Multi-Currency) | Cold | Strict ACID compliance required |
| SKILL-167 (Tax Compliance) | Cold | Regulatory accuracy paramount |

### 10.3 MCP Server Requirements

```yaml
mcp_servers:
  treasury_read:
    uri: "mcp://treasury/read"
    capabilities:
      - get_account_balance
      - query_transactions
      - get_yield_positions
      
  treasury_write:
    uri: "mcp://treasury/write"
    capabilities:
      - create_transfer
      - execute_rebalancing
      - record_fx_entry
      
  crypto_custody:
    uri: "mcp://crypto/custody"
    capabilities:
      - create_mpc_wallet
      - sign_transaction
      - get_wallet_balance
      
  crypto_payments:
    uri: "mcp://crypto/payments"
    capabilities:
      - create_payment_request
      - process_settlement
      - convert_to_fiat
      
  compliance_aml:
    uri: "mcp://compliance/aml"
    capabilities:
      - screen_transaction
      - validate_kyc
      - check_ofac
```

### 10.4 Infrastructure Alignment Verification

| Decision | Spec Alignment | Status |
|----------|---------------|--------|
| AWS ECS Fargate | ✅ Matches production infra | Aligned |
| TigerBeetle 6-replica | ✅ US/Brazil deployment | Aligned |
| Temporal Workflows | ✅ Orchestration standard | Aligned |
| Fireblocks MPC | ✅ SPSAV compliance | Aligned |
| Circle Enterprise | ✅ Multi-chain stablecoins | Aligned |
| PostgreSQL 16+ | ✅ Metadata storage | Aligned |
| Redis 7.2+ Cluster | ✅ Caching layer | Aligned |

---

## 11. Implementation Roadmap

### Phase 1: Foundation (Weeks 1-4)
- [ ] TigerBeetle multi-currency ledger setup
- [ ] Circle API integration
- [ ] Basic stablecoin payment flow
- [ ] PostgreSQL schema deployment

### Phase 2: Core Features (Weeks 5-8)
- [ ] Gas optimization engine
- [ ] Fireblocks MPC integration
- [ ] Compliance screening (Chainalysis)
- [ ] Multi-currency accounting

### Phase 3: Advanced (Weeks 9-12)
- [ ] MACRO Score integration
- [ ] Ondo Finance yield optimization
- [ ] Tax automation (1099)
- [ ] International wire management

### Phase 4: Premium (Weeks 13-16)
- [ ] Security deposit yield (DeFi)
- [ ] Rent receivable financing
- [ ] Property tokenization (regulatory permitting)
- [ ] Full compliance suite

---

## 12. Appendix

### 12.1 Glossary

| Term | Definition |
|------|------------|
| MACRO Score | Multi-Asset Credit-Risk Oracle - on-chain credit score |
| MPC | Multi-Party Computation - distributed key management |
| USDY | Ondo's yield-bearing stablecoin backed by T-bills |
| VSR | Viewstamped Replication - TigerBeetle's consensus protocol |
| SPSAV | Brazilian crypto regulatory framework |

### 12.2 References

- [Circle Enterprise API Documentation](https://developers.circle.com)
- [Fireblocks Developer Portal](https://developers.fireblocks.com)
- [Spectral Finance MACRO Score](https://docs.spectral.finance)
- [Ondo Finance Protocol](https://docs.ondo.finance)
- [TigerBeetle Documentation](https://docs.tigerbeetle.com)
- [Chainalysis Compliance APIs](https://www.chainalysis.com/api)

