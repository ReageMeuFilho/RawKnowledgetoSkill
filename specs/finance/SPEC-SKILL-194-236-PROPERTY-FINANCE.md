# Engineering Specification: Advanced Property Finance Platform

## Document Control
| Field | Value |
|-------|-------|
| Spec ID | SPEC-FINANCE-P3G9 |
| Skills Covered | SKILL-194 to SKILL-236 (43 skills) |
| Phase | Phase 3 |
| Group | Group 9 - Property Finance |
| Status | SPECIFIED |
| Created | 2026-01-07 |
| Author | Citadel OS Engineering |

---

## 1. Executive Summary

This specification defines the engineering implementation for the **Advanced Property Finance Platform**, a comprehensive financial control plane for property management operations. The platform addresses the core business challenge of manual, error-prone financial processes that plague property management companies.

### 1.1 Business Impact

| Metric | Current State | Target State | Impact |
|--------|---------------|--------------|--------|
| Invoice Processing Time | 45 min/invoice | 5 min/invoice | 89% reduction |
| Reconciliation Accuracy | 85% first-pass | 98% first-pass | 15% improvement |
| Collections Cycle Time | 45 days | 25 days | 44% faster |
| Manual Processing | 100% | 25% | 75% automation |
| Trust Compliance | Manual | 100% automated | Zero violations |

### 1.2 Skills Coverage (43 Skills Across 7 Categories)

| Category | Skills | Skill IDs | Priority |
|----------|--------|-----------|----------|
| Control Plane Foundation | 9 | SKILL-194 to SKILL-202 | Foundation |
| Property Finance Core | 5 | SKILL-203 to SKILL-207 | Critical |
| Accounts Payable | 6 | SKILL-208 to SKILL-213 | High |
| Accounts Receivable | 6 | SKILL-214 to SKILL-219 | High |
| Trust/Reserves/Compliance | 6 | SKILL-220 to SKILL-225 | Critical |
| Owner Reporting | 5 | SKILL-226 to SKILL-230 | Medium |
| Treasury Operations | 6 | SKILL-231 to SKILL-236 | Critical |

---

## 2. Technology Stack

### 2.1 Backend Services

```yaml
languages:
  primary: Python 3.12+
  secondary: Rust (TigerBeetle client)
  supporting: Go (high-performance microservices)

frameworks:
  api: FastAPI 0.104+
  orm: SQLAlchemy 2.0+
  async: asyncio, aiohttp
  validation: Pydantic 2.5+
  
financial:
  - TigerBeetle (1M+ TPS ledger)
  - python-decimal (precise arithmetic)
  - pandas 2.1+ (data manipulation)
  - numpy 1.24+ (numerical computing)
  
ml_ai:
  - scikit-learn 1.3+ (transaction categorization)
  - XGBoost 2.0+ (classification models)
  - transformers 4.35+ (NLP)
  - PyTorch 2.1+ (deep learning)
```

### 2.2 Frontend

```yaml
web:
  framework: React 18+
  language: TypeScript 5.2+
  styling: TailwindCSS 3.3+
  state: Redux Toolkit
  charts: Recharts
  
mobile:
  cross_platform: React Native
  ios_native: Swift (financial integrations)
  android_native: Kotlin (financial integrations)
```

### 2.3 Data Layer

```yaml
databases:
  financial_ledger:
    engine: TigerBeetle
    performance: 1M+ TPS
    consensus: Viewstamped Replication
    replicas: 6
    
  metadata:
    engine: PostgreSQL 15+
    extensions:
      - TimescaleDB (time-series)
      - uuid-ossp
      - pgcrypto
    
  caching:
    engine: Redis 7+
    mode: Cluster
    use_cases: GL lookups, sessions
    
  document_storage:
    service: AWS S3
    encryption: SSE-S3 (AES-256)
    lifecycle: Glacier archival
```

### 2.4 Infrastructure

```yaml
cloud: AWS
container_orchestration: ECS Fargate (primary), EKS (optional)
regions:
  primary: us-east-1
  dr: us-west-2
  
workflow_orchestration: Temporal Cloud
message_streaming: Apache Kafka (Redpanda)
```

### 2.5 Third-Party Integrations

```yaml
banking:
  - Plaid (account connectivity)
  - MX (bank data aggregation)
  - Finicity (financial data)
  
payments:
  - Stripe (card payments)
  - NACHA ACH (batch payments)
  
ocr_ai:
  - Amazon Textract (invoice extraction)
  - Google Document AI (alternative)
  - AWS Comprehend (text analysis)
  
communication:
  - Amazon SES (email)
  - Twilio (SMS)
  - Firebase (push notifications)
  
monitoring:
  - DataDog (APM)
  - Sentry (error tracking)
  - Prometheus/Grafana (metrics)
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
│  │  Control Plane  │  │  Finance Core   │  │  AP Automation  │         │
│  │    Services     │  │    Services     │  │    Services     │         │
│  │ (SKILL-194-202) │  │ (SKILL-203-207) │  │ (SKILL-208-213) │         │
│  └────────┬────────┘  └────────┬────────┘  └────────┬────────┘         │
│           │                    │                    │                   │
│  ┌────────┴────────┐  ┌────────┴────────┐  ┌────────┴────────┐         │
│  │  AR/Collections │  │ Trust/Compliance│  │ Owner Reporting │         │
│  │    Services     │  │    Services     │  │    Services     │         │
│  │ (SKILL-214-219) │  │ (SKILL-220-225) │  │ (SKILL-226-230) │         │
│  └────────┬────────┘  └────────┬────────┘  └────────┬────────┘         │
│           │                    │                    │                   │
│  ┌────────┴───────────────────────────────────────────────────┐        │
│  │            Treasury Operations (SKILL-231-236)              │        │
│  └─────────────────────────────────────────────────────────────┘        │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                    Temporal Workflow Orchestration                       │
├─────────────────────────────────────────────────────────────────────────┤
│                         TigerBeetle Cluster                             │
│              (6 replicas, Viewstamped Replication)                      │
└─────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Data Flow Architecture

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  Bank APIs   │    │  Vendor      │    │  Tenant      │
│  (Plaid/MX)  │    │  Portals     │    │  Portals     │
└──────┬───────┘    └──────┬───────┘    └──────┬───────┘
       │                   │                   │
       ▼                   ▼                   ▼
┌─────────────────────────────────────────────────────┐
│              Data Ingestion Layer                    │
│  • Bank Feed Processing                              │
│  • Invoice OCR Extraction                            │
│  • Payment Gateway Integration                       │
└──────────────────────┬──────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────┐
│              Processing Engine                       │
│  • AI Transaction Categorization                     │
│  • Three-Way Reconciliation                          │
│  • Collections State Machine                         │
│  • Trust Compliance Monitoring                       │
└──────────────────────┬──────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────┐
│           TigerBeetle Financial Ledger               │
│  • Double-Entry Accounting                           │
│  • Real-Time Balance Validation                      │
│  • Trust Account Segregation                         │
└──────────────────────┬──────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────┐
│              Output Systems                          │
│  • Owner Statements                                  │
│  • ACH Payment Execution                             │
│  • Compliance Reporting                              │
└─────────────────────────────────────────────────────┘
```

---

## 4. Skill Specifications

### 4.1 Control Plane Foundation (SKILL-194 to SKILL-202)

#### SKILL-194: Policy & Permissioning

**Purpose**: Comprehensive RBAC for financial operations with segregation of duties.

```python
@dataclass
class FinancialRole:
    role_id: UUID
    name: str  # "property_manager", "bookkeeper", "owner", "approver", "auditor"
    permissions: List[Permission]
    entity_scope: List[UUID]  # Properties this role applies to
    amount_limits: Dict[str, Decimal]  # Transaction type → max amount

class PermissionType(Enum):
    VIEW_FINANCIALS = "view_financials"
    EDIT_TRANSACTIONS = "edit_transactions"
    APPROVE_PAYMENTS = "approve_payments"
    EXECUTE_PAYMENTS = "execute_payments"
    MANAGE_TRUST = "manage_trust"
    ACCESS_REPORTS = "access_reports"
    ADMIN_SETTINGS = "admin_settings"


class RBACService:
    """Hierarchical role-based access control"""
    
    async def check_permission(self, 
                              user_id: UUID,
                              permission: PermissionType,
                              entity_id: UUID,
                              amount: Optional[Decimal] = None) -> bool:
        """Validate user permission with amount threshold check"""
        
        # Get user roles for entity
        roles = await self.get_user_roles(user_id, entity_id)
        
        for role in roles:
            if permission in role.permissions:
                # Check amount limits if applicable
                if amount and permission in [PermissionType.APPROVE_PAYMENTS]:
                    if amount <= role.amount_limits.get(str(permission), Decimal("0")):
                        return True
                else:
                    return True
        
        return False
```

#### SKILL-195: Entity Hierarchy Management

**Purpose**: Manage complex property → unit → owner → tenant relationships.

```python
@dataclass
class PropertyEntity:
    entity_id: UUID
    entity_type: str  # "company", "property", "unit", "owner", "tenant"
    parent_id: Optional[UUID]
    name: str
    metadata: Dict[str, Any]
    financial_accounts: List[UUID]  # TigerBeetle account IDs


class EntityHierarchyService:
    """Graph-based entity relationship management"""
    
    async def get_entity_tree(self, root_id: UUID) -> EntityTree:
        """Retrieve full entity hierarchy from root"""
        
        query = """
        WITH RECURSIVE entity_tree AS (
            SELECT id, entity_type, parent_id, name, metadata, 0 as depth
            FROM entities WHERE id = $1
            
            UNION ALL
            
            SELECT e.id, e.entity_type, e.parent_id, e.name, e.metadata, et.depth + 1
            FROM entities e
            JOIN entity_tree et ON e.parent_id = et.id
            WHERE et.depth < 10
        )
        SELECT * FROM entity_tree ORDER BY depth, name;
        """
        
        results = await self.db.fetch_all(query, [root_id])
        return self.build_tree(results)
    
    async def get_financial_rollup(self, entity_id: UUID) -> FinancialSummary:
        """Calculate financial totals across entity hierarchy"""
        
        # Get all child entities
        children = await self.get_all_descendants(entity_id)
        entity_ids = [entity_id] + [c.entity_id for c in children]
        
        # Aggregate TigerBeetle balances
        balances = await self.tigerbeetle_client.get_account_balances(
            [e.financial_accounts for e in entity_ids]
        )
        
        return FinancialSummary(
            total_assets=sum(b.debits_posted for b in balances if b.account_type == "asset"),
            total_liabilities=sum(b.credits_posted for b in balances if b.account_type == "liability"),
            net_income=self.calculate_net_income(balances)
        )
```

#### SKILL-196: GL Account Configuration

**Purpose**: Real estate-specific chart of accounts with property mapping.

```python
GL_ACCOUNT_STRUCTURE = {
    # Assets (1000-1999)
    "1000": {"name": "Cash - Operating", "type": "asset", "normal": "debit"},
    "1100": {"name": "Cash - Trust", "type": "asset", "normal": "debit"},
    "1200": {"name": "Accounts Receivable", "type": "asset", "normal": "debit"},
    "1300": {"name": "Security Deposits - Asset", "type": "asset", "normal": "debit"},
    
    # Liabilities (2000-2999)
    "2000": {"name": "Accounts Payable", "type": "liability", "normal": "credit"},
    "2100": {"name": "Security Deposits - Liability", "type": "liability", "normal": "credit"},
    "2200": {"name": "Advance Rent", "type": "liability", "normal": "credit"},
    "2300": {"name": "HOA Reserve Liability", "type": "liability", "normal": "credit"},
    
    # Equity (3000-3999)
    "3000": {"name": "Owner Equity", "type": "equity", "normal": "credit"},
    "3100": {"name": "Retained Earnings", "type": "equity", "normal": "credit"},
    
    # Income (4000-4999)
    "4000": {"name": "Rental Income", "type": "income", "normal": "credit"},
    "4100": {"name": "Late Fee Income", "type": "income", "normal": "credit"},
    "4200": {"name": "Other Income", "type": "income", "normal": "credit"},
    
    # Expenses (5000-5999)
    "5100": {"name": "Maintenance & Repairs", "type": "expense", "normal": "debit"},
    "5200": {"name": "Utilities", "type": "expense", "normal": "debit"},
    "5300": {"name": "Property Management", "type": "expense", "normal": "debit"},
    "5400": {"name": "Insurance", "type": "expense", "normal": "debit"},
    "5500": {"name": "Professional Services", "type": "expense", "normal": "debit"},
    "5600": {"name": "Marketing", "type": "expense", "normal": "debit"},
}
```

#### SKILL-197 to SKILL-202: Additional Control Plane Skills

| Skill ID | Name | Key Implementation |
|----------|------|-------------------|
| SKILL-197 | Fund Type Definition | Operating, Trust, Reserve fund segregation |
| SKILL-198 | Fiscal Period Management | Accounting period open/close controls |
| SKILL-199 | Bank Account Configuration | Multi-bank integration with fund mapping |
| SKILL-200 | Audit Log & Decision Trace | Immutable event sourcing with TigerBeetle |
| SKILL-201 | Threshold & Limit Configuration | Amount-based approval triggers |
| SKILL-202 | Integration Credential Management | Encrypted credential storage (AWS KMS) |

---

### 4.2 Property Finance Core (SKILL-203 to SKILL-207)

#### SKILL-203: AI Transaction Categorization

**Purpose**: ML-powered transaction classification with 95%+ accuracy.

```python
@dataclass
class TransactionClassificationResult:
    transaction_id: UUID
    predicted_gl_code: str
    confidence_score: float  # 0.0-1.0
    alternative_codes: List[Tuple[str, float]]
    features_used: Dict[str, Any]
    requires_review: bool


class TransactionCategorizationEngine:
    """ML-powered transaction categorization"""
    
    # Feature weights for classification
    FEATURE_WEIGHTS = {
        "vendor_info": 0.35,
        "description": 0.30,
        "amount_patterns": 0.20,
        "historical_context": 0.15
    }
    
    CONFIDENCE_THRESHOLD = 0.85
    
    def __init__(self):
        self.xgboost_model = self.load_model("transaction_classifier_xgb.pkl")
        self.bert_model = self.load_model("transaction_nlp_bert")
        self.vendor_patterns = self.load_vendor_patterns()
    
    async def classify_transaction(self, 
                                  transaction: BankTransaction) -> TransactionClassificationResult:
        """Classify transaction using ensemble ML approach"""
        
        # Extract features
        features = await self.extract_features(transaction)
        
        # XGBoost prediction
        xgb_prediction = self.xgboost_model.predict_proba(features["numeric"])
        
        # BERT NLP prediction for description
        bert_prediction = self.bert_model.predict(features["text"])
        
        # Business rules override
        rules_prediction = self.apply_business_rules(transaction)
        
        # Ensemble voting
        final_prediction = self.ensemble_vote([
            (xgb_prediction, 0.4),
            (bert_prediction, 0.4),
            (rules_prediction, 0.2)
        ])
        
        return TransactionClassificationResult(
            transaction_id=transaction.id,
            predicted_gl_code=final_prediction["code"],
            confidence_score=final_prediction["confidence"],
            alternative_codes=final_prediction["alternatives"],
            features_used=features,
            requires_review=final_prediction["confidence"] < self.CONFIDENCE_THRESHOLD
        )
    
    async def extract_features(self, transaction: BankTransaction) -> Dict:
        """Extract ML features from transaction"""
        
        # Vendor pattern matching
        vendor_match = self.match_vendor_patterns(transaction.description)
        
        # Text embeddings
        text_embedding = self.bert_model.encode(transaction.description)
        
        # Amount patterns
        amount_features = {
            "amount_log": math.log(transaction.amount + 1),
            "is_round_number": transaction.amount % 100 == 0,
            "amount_bucket": self.get_amount_bucket(transaction.amount)
        }
        
        # Historical patterns
        historical = await self.get_historical_patterns(
            vendor_name=transaction.vendor_name,
            amount_range=(transaction.amount * 0.9, transaction.amount * 1.1)
        )
        
        return {
            "vendor": vendor_match,
            "text": text_embedding,
            "numeric": {**amount_features, **historical}
        }
```

#### SKILL-204: Three-Way Bank Reconciliation

**Purpose**: AppFolio-style reconciliation matching Bank Statement + Ledger + Trust Liability.

```python
@dataclass
class ReconciliationResult:
    reconciliation_id: UUID
    period_end: date
    bank_balance: Decimal
    ledger_balance: Decimal
    trust_liability_total: Decimal
    is_balanced: bool
    matched_transactions: List[MatchedTransaction]
    exceptions: List[ReconciliationException]
    

class ThreeWayReconciliationEngine:
    """AppFolio-style three-way reconciliation"""
    
    FUZZY_MATCH_THRESHOLD = 0.85
    AMOUNT_TOLERANCE = Decimal("0.01")
    DATE_TOLERANCE_DAYS = 3
    
    async def reconcile_account(self,
                              bank_account_id: UUID,
                              period_start: date,
                              period_end: date) -> ReconciliationResult:
        """Execute three-way reconciliation"""
        
        # Step 1: Get bank statement transactions
        bank_transactions = await self.get_bank_transactions(
            bank_account_id, period_start, period_end
        )
        
        # Step 2: Get ledger entries from TigerBeetle
        ledger_entries = await self.tigerbeetle_client.query_transfers(
            account_id=bank_account_id,
            start_date=period_start,
            end_date=period_end
        )
        
        # Step 3: Get trust liability balances
        trust_liabilities = await self.get_trust_liabilities(bank_account_id)
        
        # Step 4: Execute matching algorithm
        matches, exceptions = await self.match_transactions(
            bank_transactions, ledger_entries
        )
        
        # Step 5: Validate three-way balance
        bank_balance = sum(t.amount for t in bank_transactions)
        ledger_balance = self.calculate_ledger_balance(ledger_entries)
        trust_total = sum(tl.amount for tl in trust_liabilities)
        
        is_balanced = (
            abs(bank_balance - ledger_balance) < self.AMOUNT_TOLERANCE and
            abs(trust_total - bank_balance) < self.AMOUNT_TOLERANCE
        )
        
        return ReconciliationResult(
            reconciliation_id=uuid.uuid4(),
            period_end=period_end,
            bank_balance=bank_balance,
            ledger_balance=ledger_balance,
            trust_liability_total=trust_total,
            is_balanced=is_balanced,
            matched_transactions=matches,
            exceptions=exceptions
        )
    
    async def match_transactions(self,
                                bank_txns: List[BankTransaction],
                                ledger_entries: List[Transfer]) -> Tuple[List, List]:
        """Multi-pass matching algorithm"""
        
        matched = []
        exceptions = []
        
        unmatched_bank = list(bank_txns)
        unmatched_ledger = list(ledger_entries)
        
        # Pass 1: Exact match (amount + date)
        for bank_txn in unmatched_bank[:]:
            for ledger in unmatched_ledger[:]:
                if self.is_exact_match(bank_txn, ledger):
                    matched.append(MatchedTransaction(
                        bank_transaction=bank_txn,
                        ledger_entry=ledger,
                        match_type="exact",
                        confidence=1.0
                    ))
                    unmatched_bank.remove(bank_txn)
                    unmatched_ledger.remove(ledger)
                    break
        
        # Pass 2: Fuzzy match (description patterns)
        for bank_txn in unmatched_bank[:]:
            best_match = None
            best_score = 0
            
            for ledger in unmatched_ledger:
                score = self.fuzzy_match_score(bank_txn, ledger)
                if score > best_score and score >= self.FUZZY_MATCH_THRESHOLD:
                    best_score = score
                    best_match = ledger
            
            if best_match:
                matched.append(MatchedTransaction(
                    bank_transaction=bank_txn,
                    ledger_entry=best_match,
                    match_type="fuzzy",
                    confidence=best_score
                ))
                unmatched_bank.remove(bank_txn)
                unmatched_ledger.remove(best_match)
        
        # Pass 3: Create exceptions for unmatched
        for bank_txn in unmatched_bank:
            exceptions.append(ReconciliationException(
                exception_type="unmatched_bank",
                transaction=bank_txn,
                suggested_action="create_ledger_entry"
            ))
        
        for ledger in unmatched_ledger:
            exceptions.append(ReconciliationException(
                exception_type="unmatched_ledger",
                transaction=ledger,
                suggested_action="void_or_adjust"
            ))
        
        return matched, exceptions
```

#### SKILL-205: Reconciliation Exception Handler

```python
class ExceptionType(Enum):
    UNMATCHED_BANK = "unmatched_bank"
    UNMATCHED_LEDGER = "unmatched_ledger"
    AMOUNT_DISCREPANCY = "amount_discrepancy"
    TIMING_DIFFERENCE = "timing_difference"
    DUPLICATE_ENTRY = "duplicate_entry"


class ReconciliationExceptionHandler:
    """Handle reconciliation exceptions with SLAs"""
    
    EXCEPTION_SLAS = {
        ExceptionType.UNMATCHED_BANK: timedelta(hours=24),
        ExceptionType.UNMATCHED_LEDGER: timedelta(hours=4),
        ExceptionType.AMOUNT_DISCREPANCY: timedelta(hours=48),
        ExceptionType.TIMING_DIFFERENCE: timedelta(hours=72),
        ExceptionType.DUPLICATE_ENTRY: timedelta(hours=4),
    }
    
    async def process_exception(self, exception: ReconciliationException) -> ResolutionResult:
        """Process exception based on type"""
        
        if exception.exception_type == ExceptionType.UNMATCHED_BANK:
            return await self.handle_unmatched_bank(exception)
        elif exception.exception_type == ExceptionType.TIMING_DIFFERENCE:
            return await self.handle_timing_difference(exception)
        elif exception.exception_type == ExceptionType.DUPLICATE_ENTRY:
            return await self.handle_duplicate(exception)
        # ... other handlers
    
    async def handle_unmatched_bank(self, exception: ReconciliationException) -> ResolutionResult:
        """Create missing ledger entry for bank transaction"""
        
        bank_txn = exception.transaction
        
        # Attempt auto-categorization
        category = await self.categorization_service.classify_transaction(bank_txn)
        
        if category.confidence_score >= 0.90:
            # Auto-create ledger entry
            transfer = await self.create_ledger_entry(
                amount=bank_txn.amount,
                gl_code=category.predicted_gl_code,
                description=bank_txn.description,
                date=bank_txn.date
            )
            return ResolutionResult(
                status="auto_resolved",
                action_taken="created_ledger_entry",
                transfer_id=transfer.id
            )
        else:
            # Route to human review
            return ResolutionResult(
                status="pending_review",
                action_taken="queued_for_manual_review",
                suggested_gl_code=category.predicted_gl_code
            )
```

#### SKILL-206: Month-End Close Automation

```python
@workflow.defn
class MonthEndCloseWorkflow:
    """Automated month-end closing process"""
    
    @workflow.run
    async def run(self, period: AccountingPeriod) -> CloseResult:
        
        # Step 1: Validate all reconciliations complete
        reconciliation_status = await workflow.execute_activity(
            validate_reconciliations_complete,
            period,
            start_to_close_timeout=timedelta(minutes=5)
        )
        
        if not reconciliation_status.all_complete:
            raise MonthEndBlockerError(f"Incomplete reconciliations: {reconciliation_status.pending}")
        
        # Step 2: Process accruals and deferrals
        await workflow.execute_activity(
            process_accruals,
            period,
            start_to_close_timeout=timedelta(minutes=30)
        )
        
        # Step 3: Generate depreciation entries
        await workflow.execute_activity(
            post_depreciation_entries,
            period,
            start_to_close_timeout=timedelta(minutes=10)
        )
        
        # Step 4: Calculate owner distributions
        distributions = await workflow.execute_activity(
            calculate_owner_distributions,
            period,
            start_to_close_timeout=timedelta(minutes=30)
        )
        
        # Step 5: Generate financial statements
        statements = await workflow.execute_activity(
            generate_financial_statements,
            period,
            start_to_close_timeout=timedelta(minutes=15)
        )
        
        # Step 6: Lock accounting period
        await workflow.execute_activity(
            lock_accounting_period,
            period,
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        return CloseResult(
            period=period,
            distributions=distributions,
            statements=statements,
            closed_at=datetime.utcnow()
        )
```

#### SKILL-207: Year-End/Tax Preparation

```python
class TaxPreparationService:
    """Generate 1099s and tax documents"""
    
    FORM_1099_THRESHOLD = Decimal("600.00")
    
    async def generate_1099_forms(self, tax_year: int) -> List[Form1099]:
        """Generate 1099-MISC/NEC forms for qualifying vendors"""
        
        # Query vendor payments for year
        vendor_payments = await self.tigerbeetle_client.query_vendor_payments(
            tax_year=tax_year,
            minimum_amount=self.FORM_1099_THRESHOLD
        )
        
        forms = []
        for vendor_id, total_amount in vendor_payments.items():
            vendor = await self.get_vendor(vendor_id)
            
            # Validate W-9 on file
            w9_status = await self.validate_w9(vendor_id)
            
            form = Form1099(
                form_type="1099-NEC" if self.is_independent_contractor(vendor) else "1099-MISC",
                tax_year=tax_year,
                payer_tin=self.company_tin,
                payee_tin=vendor.tax_id,
                payee_name=vendor.legal_name,
                total_amount=total_amount,
                box_1_nonemployee_compensation=total_amount if form_type == "1099-NEC" else Decimal("0"),
                has_valid_w9=w9_status.valid
            )
            
            forms.append(form)
        
        return forms
    
    async def generate_irs_1099_file(self, forms: List[Form1099]) -> bytes:
        """Generate IRS-compliant 1099 e-file"""
        
        # IRS FIRE format generation
        fire_file = IRS1099FileGenerator(
            transmitter_tin=self.company_tin,
            tax_year=forms[0].tax_year
        )
        
        for form in forms:
            fire_file.add_payee_record(form)
        
        return fire_file.generate()
```

---

### 4.3 Accounts Payable Automation (SKILL-208 to SKILL-213)

#### SKILL-208: Invoice Data Extraction (OCR/AI)

```python
class InvoiceOCRService:
    """AI-powered invoice data extraction"""
    
    def __init__(self):
        self.textract_client = boto3.client('textract')
        self.document_ai_client = DocumentAI()
    
    async def extract_invoice_data(self, document: bytes) -> InvoiceExtraction:
        """Extract structured data from invoice PDF"""
        
        # Primary: Amazon Textract
        response = self.textract_client.analyze_expense(
            Document={'Bytes': document}
        )
        
        extraction = InvoiceExtraction(
            vendor_name=self.extract_field(response, "VENDOR_NAME"),
            vendor_address=self.extract_field(response, "VENDOR_ADDRESS"),
            invoice_number=self.extract_field(response, "INVOICE_NUMBER"),
            invoice_date=self.parse_date(self.extract_field(response, "INVOICE_DATE")),
            due_date=self.parse_date(self.extract_field(response, "DUE_DATE")),
            subtotal=self.parse_amount(self.extract_field(response, "SUBTOTAL")),
            tax_amount=self.parse_amount(self.extract_field(response, "TAX")),
            total_amount=self.parse_amount(self.extract_field(response, "TOTAL")),
            line_items=self.extract_line_items(response),
            confidence_scores=self.calculate_confidence(response)
        )
        
        # Validate extracted data
        validation = self.validate_extraction(extraction)
        extraction.validation_result = validation
        
        return extraction
    
    def extract_line_items(self, response: Dict) -> List[LineItem]:
        """Extract individual line items from invoice"""
        
        line_items = []
        
        for expense_doc in response.get('ExpenseDocuments', []):
            for line_group in expense_doc.get('LineItemGroups', []):
                for line in line_group.get('LineItems', []):
                    item = LineItem(
                        description=self.get_line_field(line, "ITEM"),
                        quantity=self.parse_number(self.get_line_field(line, "QUANTITY")),
                        unit_price=self.parse_amount(self.get_line_field(line, "UNIT_PRICE")),
                        amount=self.parse_amount(self.get_line_field(line, "PRICE"))
                    )
                    line_items.append(item)
        
        return line_items
```

#### SKILL-209: Invoice Triage & Coding

```python
class InvoiceTriageService:
    """Auto-route invoices based on content and rules"""
    
    async def triage_invoice(self, invoice: InvoiceExtraction) -> TriageResult:
        """Determine invoice routing and GL coding"""
        
        # Step 1: Vendor lookup
        vendor = await self.vendor_service.find_or_create_vendor(
            name=invoice.vendor_name,
            address=invoice.vendor_address
        )
        
        # Step 2: AI GL coding
        gl_suggestion = await self.categorization_engine.suggest_gl_codes(
            vendor=vendor,
            line_items=invoice.line_items,
            total_amount=invoice.total_amount
        )
        
        # Step 3: Property assignment
        property_assignment = await self.assign_property(
            vendor=vendor,
            invoice_description=invoice.description
        )
        
        # Step 4: Determine approval routing
        approval_route = await self.get_approval_route(
            amount=invoice.total_amount,
            property_id=property_assignment.property_id,
            vendor=vendor
        )
        
        return TriageResult(
            invoice_id=invoice.id,
            vendor=vendor,
            gl_coding=gl_suggestion,
            property_assignment=property_assignment,
            approval_route=approval_route,
            auto_approve=approval_route.amount < Decimal("500.00")
        )
```

#### SKILL-210: Approval Workflow Engine

```python
@workflow.defn
class InvoiceApprovalWorkflow:
    """Multi-level approval workflow with escalation"""
    
    APPROVAL_MATRIX = {
        (Decimal("0"), Decimal("500")): {"level": "auto", "timeout": None},
        (Decimal("500"), Decimal("2500")): {"level": "manager", "timeout": timedelta(hours=24)},
        (Decimal("2500"), Decimal("10000")): {"level": "senior_manager", "timeout": timedelta(hours=48)},
        (Decimal("10000"), None): {"level": "cfo", "timeout": timedelta(hours=72)}
    }
    
    @workflow.run
    async def run(self, invoice: Invoice) -> ApprovalResult:
        
        # Determine approval level
        approval_config = self.get_approval_config(invoice.total_amount)
        
        if approval_config["level"] == "auto":
            return ApprovalResult(
                invoice_id=invoice.id,
                status="approved",
                approver="system",
                approved_at=datetime.utcnow()
            )
        
        # Get approver(s)
        approvers = await workflow.execute_activity(
            get_approvers_for_level,
            ApproverRequest(
                level=approval_config["level"],
                property_id=invoice.property_id
            ),
            start_to_close_timeout=timedelta(minutes=1)
        )
        
        # Send approval request
        await workflow.execute_activity(
            send_approval_request,
            ApprovalRequestData(
                invoice=invoice,
                approvers=approvers
            ),
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        # Wait for approval with timeout
        try:
            approval_decision = await workflow.wait_condition(
                lambda: self.approval_received,
                timeout=approval_config["timeout"]
            )
        except workflow.TimeoutError:
            # Escalate to next level
            return await self.escalate(invoice, approval_config["level"])
        
        if approval_decision.approved:
            return ApprovalResult(
                invoice_id=invoice.id,
                status="approved",
                approver=approval_decision.approver_id,
                approved_at=approval_decision.timestamp
            )
        else:
            return ApprovalResult(
                invoice_id=invoice.id,
                status="rejected",
                approver=approval_decision.approver_id,
                rejection_reason=approval_decision.reason
            )
```

#### SKILL-211: Duplicate Invoice Detection

```python
class DuplicateInvoiceDetector:
    """Prevent duplicate invoice processing"""
    
    async def check_duplicate(self, invoice: InvoiceExtraction) -> DuplicateCheckResult:
        """Check if invoice is a duplicate"""
        
        # Exact match check
        exact_match = await self.find_exact_match(
            vendor_id=invoice.vendor_id,
            invoice_number=invoice.invoice_number,
            amount=invoice.total_amount
        )
        
        if exact_match:
            return DuplicateCheckResult(
                is_duplicate=True,
                confidence=1.0,
                matching_invoice_id=exact_match.id,
                match_type="exact"
            )
        
        # Fuzzy match check (same vendor, similar amount, date range)
        fuzzy_matches = await self.find_fuzzy_matches(
            vendor_id=invoice.vendor_id,
            amount=invoice.total_amount,
            amount_tolerance=Decimal("0.01"),
            date_range=(invoice.invoice_date - timedelta(days=30), 
                       invoice.invoice_date + timedelta(days=30))
        )
        
        for match in fuzzy_matches:
            similarity = self.calculate_similarity(invoice, match)
            if similarity > 0.90:
                return DuplicateCheckResult(
                    is_duplicate=True,
                    confidence=similarity,
                    matching_invoice_id=match.id,
                    match_type="fuzzy"
                )
        
        return DuplicateCheckResult(is_duplicate=False)
```

#### SKILL-212 & SKILL-213: Payment Optimization & 1099 Management

| Skill | Purpose | Key Features |
|-------|---------|--------------|
| SKILL-212 | Payment Method Optimization | ACH vs Check vs Virtual Card selection based on amount, vendor preference, rebates |
| SKILL-213 | 1099 Vendor Management | Track vendor payments, W-9 status, generate 1099 forms, backup withholding |

---

### 4.4 Accounts Receivable & Collections (SKILL-214 to SKILL-219)

#### SKILL-216: Collections Workflow Engine

```python
class CollectionState(Enum):
    CURRENT = "current"
    DAY_1_LATE = "day_1_late"
    DAY_5_LATE = "day_5_late"
    DAY_10_LATE = "day_10_late"
    DAY_15_LATE = "day_15_late"
    DAY_30_LATE = "day_30_late"
    LEGAL_ACTION = "legal_action"
    PAYMENT_PLAN = "payment_plan"
    EVICTION_FILED = "eviction_filed"


@workflow.defn
class CollectionsWorkflow:
    """State machine-driven collections process"""
    
    COLLECTION_ACTIONS = {
        CollectionState.DAY_1_LATE: "send_friendly_reminder",
        CollectionState.DAY_5_LATE: "send_late_notice",
        CollectionState.DAY_10_LATE: "send_demand_notice",
        CollectionState.DAY_15_LATE: "send_final_notice",
        CollectionState.DAY_30_LATE: "send_legal_warning",
        CollectionState.LEGAL_ACTION: "file_eviction"
    }
    
    @workflow.run
    async def run(self, tenant_account: TenantAccount) -> CollectionResult:
        
        current_state = CollectionState.CURRENT
        
        while current_state not in [CollectionState.CURRENT, CollectionState.EVICTION_FILED]:
            
            # Check for payment
            payment_received = await workflow.execute_activity(
                check_for_payment,
                tenant_account.id,
                start_to_close_timeout=timedelta(minutes=1)
            )
            
            if payment_received:
                # Return to current status
                await self.update_tenant_status(tenant_account.id, CollectionState.CURRENT)
                return CollectionResult(
                    status="resolved",
                    payment_received=True,
                    final_state=CollectionState.CURRENT
                )
            
            # Execute collection action for current state
            action = self.COLLECTION_ACTIONS.get(current_state)
            if action:
                await workflow.execute_activity(
                    execute_collection_action,
                    CollectionAction(
                        tenant_id=tenant_account.id,
                        action=action,
                        state=current_state
                    ),
                    start_to_close_timeout=timedelta(minutes=5)
                )
            
            # Wait for next state transition
            await workflow.sleep(self.get_wait_period(current_state))
            
            # Progress to next state
            current_state = self.get_next_state(current_state)
        
        return CollectionResult(
            status="legal_action",
            payment_received=False,
            final_state=current_state
        )
    
    def get_wait_period(self, state: CollectionState) -> timedelta:
        """Get wait period before next state"""
        periods = {
            CollectionState.DAY_1_LATE: timedelta(days=4),
            CollectionState.DAY_5_LATE: timedelta(days=5),
            CollectionState.DAY_10_LATE: timedelta(days=5),
            CollectionState.DAY_15_LATE: timedelta(days=15),
            CollectionState.DAY_30_LATE: timedelta(days=1),
        }
        return periods.get(state, timedelta(days=1))
```

#### SKILL-214, SKILL-215, SKILL-217-219

| Skill ID | Name | Purpose |
|----------|------|---------|
| SKILL-214 | Rent Roll Generation | Real-time occupancy, collection rates, variance analysis |
| SKILL-215 | Automated Late Fee Assessment | Policy-based fee calculation with state compliance |
| SKILL-217 | Tenant Ledger Management | Charge tracking, payment application, balance management |
| SKILL-218 | NSF/Bounced Payment Handler | ACH return processing, fee assessment, re-collection |
| SKILL-219 | Payment Plan Management | Create/track/monitor payment arrangements |

---

### 4.5 Trust/Reserves/Compliance (SKILL-220 to SKILL-225)

#### SKILL-220: Trust Account Compliance Monitor

```python
class TrustComplianceMonitor:
    """Real-time trust account compliance monitoring"""
    
    # State-specific rules
    STATE_RULES = {
        "CA": {
            "separate_account_required": True,
            "reconciliation_frequency": "monthly",
            "interest_required": False,
            "record_retention_years": 3,
            "commingling_prohibited": True
        },
        "TX": {
            "separate_account_required": True,
            "reconciliation_frequency": "monthly",
            "interest_required": True,
            "interest_threshold": Decimal("50.00"),
            "commingling_prohibited": True
        },
        "FL": {
            "separate_account_required": True,
            "reconciliation_frequency": "monthly",
            "interest_required": True,
            "interest_hold_period_months": 3,
            "commingling_prohibited": True
        },
        "NY": {
            "separate_account_required": True,
            "reconciliation_frequency": "monthly",
            "interest_required": True,
            "interest_frequency": "annual",
            "commingling_prohibited": True
        },
        "AZ": {
            "separate_account_required": False,
            "surety_bond_alternative": True,
            "reconciliation_frequency": "monthly",
            "interest_required": False
        }
    }
    
    async def monitor_trust_compliance(self, 
                                       trust_account_id: UUID,
                                       state: str) -> ComplianceStatus:
        """Continuous compliance monitoring"""
        
        rules = self.STATE_RULES[state]
        violations = []
        
        # Check commingling
        if rules["commingling_prohibited"]:
            commingling_check = await self.check_commingling(trust_account_id)
            if commingling_check.detected:
                violations.append(ComplianceViolation(
                    violation_type="commingling",
                    severity="critical",
                    description=f"Operating funds detected in trust account: ${commingling_check.amount}",
                    remediation="Immediately transfer operating funds to operating account"
                ))
        
        # Verify three-way balance
        balance_check = await self.verify_three_way_balance(trust_account_id)
        if not balance_check.balanced:
            violations.append(ComplianceViolation(
                violation_type="balance_mismatch",
                severity="high",
                description=f"Trust balance mismatch: Bank ${balance_check.bank_balance}, Liabilities ${balance_check.liability_total}",
                remediation="Complete reconciliation and identify discrepancy source"
            ))
        
        # Check reconciliation status
        reconciliation_status = await self.check_reconciliation_status(trust_account_id)
        if reconciliation_status.days_since_last > 30:
            violations.append(ComplianceViolation(
                violation_type="reconciliation_overdue",
                severity="high",
                description=f"Reconciliation overdue by {reconciliation_status.days_since_last - 30} days",
                remediation="Complete monthly reconciliation immediately"
            ))
        
        return ComplianceStatus(
            trust_account_id=trust_account_id,
            state=state,
            is_compliant=len(violations) == 0,
            violations=violations,
            last_checked=datetime.utcnow()
        )
    
    async def check_commingling(self, trust_account_id: UUID) -> ComminglingCheck:
        """Detect operating funds in trust account"""
        
        # Query recent deposits
        deposits = await self.tigerbeetle_client.query_transfers(
            account_id=trust_account_id,
            transfer_type="credit",
            days=30
        )
        
        # Verify each deposit is a valid trust deposit
        for deposit in deposits:
            if not await self.is_valid_trust_deposit(deposit):
                return ComminglingCheck(
                    detected=True,
                    amount=deposit.amount,
                    transaction_id=deposit.id
                )
        
        return ComminglingCheck(detected=False)
```

#### SKILL-221: Security Deposit Lifecycle Manager

```python
@dataclass
class SecurityDeposit:
    deposit_id: UUID
    tenant_id: UUID
    unit_id: UUID
    amount: Decimal
    deposit_date: date
    interest_rate: Optional[Decimal]
    accrued_interest: Decimal
    state: str
    status: str  # "held", "partial_refund", "full_refund", "applied"


class SecurityDepositManager:
    """Complete security deposit lifecycle management"""
    
    async def process_deposit(self, 
                             tenant_id: UUID,
                             unit_id: UUID,
                             amount: Decimal,
                             state: str) -> SecurityDeposit:
        """Record new security deposit"""
        
        # Create TigerBeetle entries
        transfer = await self.tigerbeetle_client.create_transfer(
            Transfer(
                debit_account_id=self.get_trust_cash_account(),
                credit_account_id=self.get_deposit_liability_account(tenant_id),
                amount=int(amount * 100),
                ledger=self.TRUST_LEDGER,
                code=2001,  # Security deposit code
                user_data_128=tenant_id.bytes
            )
        )
        
        # Calculate interest requirements
        interest_rate = self.get_state_interest_rate(state)
        
        deposit = SecurityDeposit(
            deposit_id=uuid.uuid4(),
            tenant_id=tenant_id,
            unit_id=unit_id,
            amount=amount,
            deposit_date=date.today(),
            interest_rate=interest_rate,
            accrued_interest=Decimal("0"),
            state=state,
            status="held"
        )
        
        await self.save_deposit(deposit)
        return deposit
    
    async def process_refund(self,
                            deposit_id: UUID,
                            deductions: List[Deduction]) -> RefundResult:
        """Process security deposit refund with deductions"""
        
        deposit = await self.get_deposit(deposit_id)
        
        # Calculate refund amount
        total_deductions = sum(d.amount for d in deductions)
        refund_amount = deposit.amount + deposit.accrued_interest - total_deductions
        
        # Validate state-specific deadlines
        state_rules = self.get_state_rules(deposit.state)
        deadline = deposit.move_out_date + timedelta(days=state_rules["refund_deadline_days"])
        
        if date.today() > deadline:
            # Potential penalty - some states require full refund if deadline missed
            if state_rules["penalty_for_late_refund"]:
                refund_amount = deposit.amount + deposit.accrued_interest
                deductions = []
        
        # Create refund entries in TigerBeetle
        transfers = []
        
        # Main refund
        if refund_amount > 0:
            transfers.append(Transfer(
                debit_account_id=self.get_deposit_liability_account(deposit.tenant_id),
                credit_account_id=self.get_trust_cash_account(),
                amount=int(refund_amount * 100),
                code=2002  # Deposit refund
            ))
        
        # Deduction entries
        for deduction in deductions:
            transfers.append(Transfer(
                debit_account_id=self.get_deposit_liability_account(deposit.tenant_id),
                credit_account_id=self.get_property_income_account(deposit.unit_id, deduction.category),
                amount=int(deduction.amount * 100),
                code=2003  # Deposit deduction
            ))
        
        await self.tigerbeetle_client.create_transfers(transfers)
        
        # Generate itemized statement
        statement = self.generate_itemized_statement(deposit, deductions, refund_amount)
        
        return RefundResult(
            deposit_id=deposit_id,
            refund_amount=refund_amount,
            deductions=deductions,
            statement=statement,
            processed_at=datetime.utcnow()
        )
```

---

### 4.6 Treasury Operations (SKILL-231 to SKILL-236)

#### SKILL-231: Owner Payout Calculation

```python
class OwnerPayoutCalculator:
    """Calculate owner distributions with reserve policies"""
    
    async def calculate_payout(self,
                              property_id: UUID,
                              period: AccountingPeriod) -> OwnerPayoutCalculation:
        """Calculate owner payout for period"""
        
        # Get property financials from TigerBeetle
        income = await self.get_period_income(property_id, period)
        expenses = await self.get_period_expenses(property_id, period)
        
        # Calculate net operating income
        noi = income.total - expenses.total
        
        # Apply reserve policy
        reserve_policy = await self.get_reserve_policy(property_id)
        reserve_contribution = self.calculate_reserve(noi, reserve_policy)
        
        # Calculate management fee
        management_fee = await self.calculate_management_fee(property_id, income.total)
        
        # Calculate net distribution
        net_distribution = noi - reserve_contribution - management_fee
        
        # Handle negative balance
        if net_distribution < 0:
            return OwnerPayoutCalculation(
                property_id=property_id,
                period=period,
                gross_income=income.total,
                total_expenses=expenses.total,
                noi=noi,
                reserve_contribution=Decimal("0"),
                management_fee=Decimal("0"),
                net_distribution=Decimal("0"),
                owner_contribution_required=abs(net_distribution),
                status="owner_contribution_required"
            )
        
        # Allocate to owners by ownership percentage
        owners = await self.get_property_owners(property_id)
        owner_distributions = []
        
        for owner in owners:
            owner_amount = net_distribution * owner.ownership_percentage
            owner_distributions.append(OwnerDistribution(
                owner_id=owner.id,
                amount=owner_amount,
                ownership_percentage=owner.ownership_percentage
            ))
        
        return OwnerPayoutCalculation(
            property_id=property_id,
            period=period,
            gross_income=income.total,
            total_expenses=expenses.total,
            noi=noi,
            reserve_contribution=reserve_contribution,
            management_fee=management_fee,
            net_distribution=net_distribution,
            owner_distributions=owner_distributions,
            status="ready_for_approval"
        )
```

#### SKILL-235: ACH Payment Execution

```python
class ACHPaymentProcessor:
    """NACHA-compliant ACH payment processing"""
    
    def __init__(self):
        self.nacha_generator = NACHAFileGenerator(
            immediate_destination=os.environ["BANK_ROUTING_NUMBER"],
            immediate_origin=os.environ["COMPANY_TIN"],
            company_name=os.environ["COMPANY_NAME"]
        )
    
    async def process_payment_batch(self,
                                   payments: List[PaymentInstruction]) -> ACHBatchResult:
        """Generate and submit NACHA ACH file"""
        
        # Validate all payment instructions
        validation_results = await asyncio.gather(*[
            self.validate_payment(p) for p in payments
        ])
        
        valid_payments = [p for p, v in zip(payments, validation_results) if v.valid]
        invalid_payments = [p for p, v in zip(payments, validation_results) if not v.valid]
        
        # Generate NACHA file
        nacha_file = self.nacha_generator.create_batch(
            batch_type="PPD",  # Prearranged Payment and Deposit
            effective_date=self.calculate_effective_date(),
            entries=[self.create_entry(p) for p in valid_payments]
        )
        
        # Submit to bank
        submission_result = await self.submit_to_bank(nacha_file)
        
        # Record in TigerBeetle
        for payment in valid_payments:
            await self.record_payment_pending(payment, submission_result.batch_id)
        
        return ACHBatchResult(
            batch_id=submission_result.batch_id,
            total_amount=sum(p.amount for p in valid_payments),
            payment_count=len(valid_payments),
            effective_date=nacha_file.effective_date,
            submitted_at=datetime.utcnow(),
            invalid_payments=invalid_payments
        )
    
    def create_entry(self, payment: PaymentInstruction) -> NACHAEntry:
        """Create NACHA entry detail record"""
        
        return NACHAEntry(
            transaction_code=self.get_transaction_code(payment),
            rdfi_id=payment.bank_routing[:8],
            check_digit=payment.bank_routing[8],
            dfi_account=payment.bank_account,
            amount=int(payment.amount * 100),
            individual_id=payment.recipient_id[:15],
            individual_name=payment.recipient_name[:22],
            trace_number=self.generate_trace_number()
        )
    
    async def process_ach_returns(self, return_file: bytes) -> List[ACHReturn]:
        """Process ACH return notifications"""
        
        returns = self.parse_return_file(return_file)
        
        for ach_return in returns:
            # Find original payment
            original = await self.find_payment_by_trace(ach_return.trace_number)
            
            if original:
                # Reverse TigerBeetle entry
                await self.reverse_payment(original, ach_return.return_code)
                
                # Trigger collection workflow for NSF
                if ach_return.return_code in ["R01", "R09"]:  # NSF codes
                    await self.trigger_nsf_workflow(original)
        
        return returns
```

#### SKILL-236: Payment Reconciliation

```python
class PaymentReconciliationService:
    """Reconcile payments with bank settlements"""
    
    async def reconcile_ach_batch(self, batch_id: str) -> BatchReconciliationResult:
        """Reconcile ACH batch with bank settlement"""
        
        # Get batch details
        batch = await self.get_batch(batch_id)
        
        # Get settlement report from bank
        settlement = await self.get_settlement_report(batch_id)
        
        # Match payments to settlements
        matched = []
        unmatched = []
        
        for payment in batch.payments:
            settlement_entry = self.find_settlement_entry(settlement, payment.trace_number)
            
            if settlement_entry:
                if settlement_entry.status == "settled":
                    # Update TigerBeetle - mark as cleared
                    await self.mark_payment_cleared(payment.id)
                    matched.append(PaymentMatch(
                        payment_id=payment.id,
                        settlement_date=settlement_entry.settlement_date,
                        status="cleared"
                    ))
                elif settlement_entry.status == "returned":
                    # Process return
                    await self.process_return(payment, settlement_entry.return_code)
                    matched.append(PaymentMatch(
                        payment_id=payment.id,
                        status="returned",
                        return_code=settlement_entry.return_code
                    ))
            else:
                unmatched.append(payment)
        
        return BatchReconciliationResult(
            batch_id=batch_id,
            total_payments=len(batch.payments),
            matched_count=len(matched),
            unmatched_count=len(unmatched),
            matched=matched,
            unmatched=unmatched
        )
```

---

## 5. Database Schema

### 5.1 TigerBeetle Account Types

```python
TIGERBEETLE_ACCOUNTS = {
    # Assets (1000-1999)
    1001: {"name": "Cash - Operating", "type": "asset", "normal": "debit"},
    1101: {"name": "Cash - Trust", "type": "asset", "normal": "debit"},
    1201: {"name": "Accounts Receivable", "type": "asset", "normal": "debit"},
    
    # Liabilities (2000-2999)
    2001: {"name": "Accounts Payable", "type": "liability", "normal": "credit"},
    2101: {"name": "Security Deposits Held", "type": "liability", "normal": "credit"},
    2201: {"name": "Advance Rent", "type": "liability", "normal": "credit"},
    
    # Equity (3000-3999)
    3001: {"name": "Owner Equity", "type": "equity", "normal": "credit"},
    
    # Income (4000-4999)
    4001: {"name": "Rental Income", "type": "income", "normal": "credit"},
    4101: {"name": "Late Fee Income", "type": "income", "normal": "credit"},
    
    # Expenses (5000-5999)
    5101: {"name": "Maintenance & Repairs", "type": "expense", "normal": "debit"},
    5201: {"name": "Utilities", "type": "expense", "normal": "debit"},
    5301: {"name": "Property Management Fee", "type": "expense", "normal": "debit"},
}
```

### 5.2 PostgreSQL Schema

```sql
-- Companies table
CREATE TABLE companies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    license_number VARCHAR(100),
    settings JSONB DEFAULT '{}',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Properties table
CREATE TABLE properties (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    name VARCHAR(255) NOT NULL,
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    city VARCHAR(100),
    state CHAR(2),
    zip_code VARCHAR(10),
    property_type VARCHAR(50), -- residential, commercial, hoa
    metadata JSONB DEFAULT '{}',
    tigerbeetle_ledger_id INTEGER,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Trust accounts table
CREATE TABLE trust_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    bank_name VARCHAR(255) NOT NULL,
    account_number_encrypted BYTEA NOT NULL,
    routing_number VARCHAR(9) NOT NULL,
    account_type VARCHAR(50), -- trust, operating
    state CHAR(2) NOT NULL,
    compliance_rules JSONB DEFAULT '{}',
    tigerbeetle_account_id BIGINT NOT NULL,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Invoices table
CREATE TABLE invoices (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    property_id UUID REFERENCES properties(id),
    vendor_id UUID NOT NULL REFERENCES vendors(id),
    invoice_number VARCHAR(100),
    invoice_date DATE NOT NULL,
    due_date DATE,
    subtotal NUMERIC(12,2),
    tax_amount NUMERIC(12,2) DEFAULT 0,
    total_amount NUMERIC(12,2) NOT NULL,
    status VARCHAR(50) DEFAULT 'pending', -- pending, approved, paid, rejected
    ocr_confidence NUMERIC(5,2),
    gl_coding JSONB DEFAULT '[]',
    approval_workflow_id VARCHAR(100),
    tigerbeetle_transfer_id BIGINT,
    document_url VARCHAR(500),
    created_at TIMESTAMPTZ DEFAULT NOW()
) PARTITION BY RANGE (invoice_date);

-- Create monthly partitions for invoices
CREATE TABLE invoices_2026_01 PARTITION OF invoices
    FOR VALUES FROM ('2026-01-01') TO ('2026-02-01');

-- Collections workflow table
CREATE TABLE collection_workflows (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL REFERENCES tenants(id),
    unit_id UUID NOT NULL REFERENCES units(id),
    current_state VARCHAR(50) NOT NULL,
    balance_due NUMERIC(12,2) NOT NULL,
    days_past_due INTEGER DEFAULT 0,
    workflow_instance_id VARCHAR(100),
    last_action_at TIMESTAMPTZ,
    next_action_at TIMESTAMPTZ,
    legal_case_id VARCHAR(100),
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Security deposits table
CREATE TABLE security_deposits (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL REFERENCES tenants(id),
    unit_id UUID NOT NULL REFERENCES units(id),
    amount NUMERIC(12,2) NOT NULL,
    deposit_date DATE NOT NULL,
    interest_rate NUMERIC(5,4),
    accrued_interest NUMERIC(12,2) DEFAULT 0,
    state CHAR(2) NOT NULL,
    status VARCHAR(50) DEFAULT 'held',
    refund_date DATE,
    refund_amount NUMERIC(12,2),
    deductions JSONB DEFAULT '[]',
    tigerbeetle_account_id BIGINT NOT NULL,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- ACH payment batches table
CREATE TABLE ach_batches (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID NOT NULL REFERENCES companies(id),
    batch_type VARCHAR(10) NOT NULL, -- PPD, CCD
    effective_date DATE NOT NULL,
    total_amount NUMERIC(14,2) NOT NULL,
    payment_count INTEGER NOT NULL,
    nacha_file_id VARCHAR(100),
    submission_status VARCHAR(50) DEFAULT 'pending',
    submitted_at TIMESTAMPTZ,
    settlement_status VARCHAR(50),
    settled_at TIMESTAMPTZ,
    created_at TIMESTAMPTZ DEFAULT NOW()
);
```

---

## 6. Performance Specifications

### 6.1 Service SLAs

| Component | Response Time | Throughput | Availability |
|-----------|---------------|------------|--------------|
| Financial Ledger | <50ms | 1M+ TPS | 99.99% |
| AI Categorization | <5 seconds | 1,000/min | 99.5% |
| Reconciliation | <5 min (10K txns) | 2,000/min | 99.9% |
| Payment Processing | <30 sec batch | 100K/batch | 99.99% |
| Document OCR | <30 seconds | 500/hour | 99.5% |
| API Gateway | <100ms | 10,000 req/sec | 99.95% |

### 6.2 Scaling Configuration

| Service | Min Instances | Max Instances | Scale Trigger |
|---------|---------------|---------------|---------------|
| Financial Ledger | 3 | 50 | >70% CPU or >1000 TPS |
| AI Categorization | 2 | 20 | >80% CPU or >500 req/min |
| Collections Engine | 2 | 10 | Queue depth > 1000 |
| Payment Processor | 2 | 20 | >60% CPU or batch queued |
| OCR Service | 2 | 10 | >70% CPU or queue > 50 |

---

## 7. Architecture Alignment Notes

### 7.1 Layer Mapping (Citadel OS 6-Layer Stack)

| Component | Layer | Rationale |
|-----------|-------|-----------|
| Control Plane Services | Layer 4 (Skills) | Business logic, permission management |
| AI Categorization | Layer 5 (Hot Path) | ML reasoning for classification |
| Financial Ledger | Layer 6 (Cold Path) | TigerBeetle guarantees |
| Workflow Orchestration | Layer 4 (Skills) | Temporal coordination |
| Trust Compliance | Layer 4 (Skills) | Rules engine + monitoring |
| Payment Processing | Layer 6 (Cold Path) | Financial guarantees |

### 7.2 Execution Path Classification

| Skill Category | Execution Path | Reasoning |
|----------------|---------------|-----------|
| Control Plane (194-202) | Cold | Security-critical, audit requirements |
| Finance Core (203-207) | Hybrid | AI categorization (Hot) + Ledger (Cold) |
| AP Automation (208-213) | Hybrid | OCR/ML (Hot) + Payment (Cold) |
| AR/Collections (214-219) | Hybrid | Workflow (Hot) + Ledger (Cold) |
| Trust/Compliance (220-225) | Cold | Regulatory guarantees required |
| Treasury Operations (231-236) | Cold | Financial guarantees paramount |

### 7.3 MCP Server Requirements

```yaml
mcp_servers:
  treasury_read:
    uri: "mcp://treasury/read"
    capabilities:
      - get_account_balance
      - query_transactions
      - get_reconciliation_status
      
  treasury_write:
    uri: "mcp://treasury/write"
    capabilities:
      - create_transfer
      - execute_payment_batch
      - post_journal_entry
      
  ap_automation:
    uri: "mcp://ap/automation"
    capabilities:
      - extract_invoice_data
      - route_for_approval
      - execute_payment
      
  ar_collections:
    uri: "mcp://ar/collections"
    capabilities:
      - get_tenant_balance
      - trigger_collection_action
      - apply_payment
      
  compliance_monitor:
    uri: "mcp://compliance/trust"
    capabilities:
      - check_trust_balance
      - validate_commingling
      - get_state_rules
```

### 7.4 Infrastructure Alignment Verification

| Decision | Spec Alignment | Status |
|----------|---------------|--------|
| AWS ECS Fargate | ✅ Matches production infra | Aligned |
| TigerBeetle 6-replica | ✅ US/Brazil deployment | Aligned |
| Temporal Workflows | ✅ Orchestration standard | Aligned |
| PostgreSQL 15+ | ✅ Metadata storage | Aligned |
| Redis 7+ Cluster | ✅ Caching layer | Aligned |
| Amazon Textract | ✅ OCR standard | Aligned |
| Plaid/MX | ✅ Bank connectivity | Aligned |

---

## 8. Implementation Roadmap

### Phase 1: Foundation (Weeks 1-4)
- [ ] Control Plane services (SKILL-194-202)
- [ ] TigerBeetle ledger setup
- [ ] PostgreSQL schema deployment
- [ ] Basic RBAC implementation

### Phase 2: Core Finance (Weeks 5-8)
- [ ] AI Transaction Categorization (SKILL-203)
- [ ] Three-Way Reconciliation (SKILL-204-205)
- [ ] Month-End Close (SKILL-206)
- [ ] Bank feed integration (Plaid)

### Phase 3: AP/AR (Weeks 9-12)
- [ ] Invoice OCR (SKILL-208)
- [ ] Approval Workflows (SKILL-210)
- [ ] Collections Engine (SKILL-216)
- [ ] Tenant Ledger Management (SKILL-217)

### Phase 4: Trust & Treasury (Weeks 13-16)
- [ ] Trust Compliance Monitor (SKILL-220)
- [ ] Security Deposit Manager (SKILL-221)
- [ ] Owner Payout Calculator (SKILL-231)
- [ ] ACH Payment Processing (SKILL-235)

---

## 9. Appendix

### 9.1 Glossary

| Term | Definition |
|------|------------|
| Three-Way Reconciliation | Matching Bank Statement + Ledger + Trust Liabilities |
| Trust Account | Segregated account holding tenant funds (security deposits, advance rent) |
| Commingling | Illegal mixing of trust and operating funds |
| NACHA | National Automated Clearing House Association (ACH standards) |
| Third-Party Sender | Property manager acting as payment processor on ACH network |
| GL Code | General Ledger account code for transaction categorization |

### 9.2 References

- [TigerBeetle Documentation](https://docs.tigerbeetle.com)
- [NACHA Operating Rules](https://www.nacha.org)
- [AppFolio Three-Way Reconciliation](https://www.appfolio.com)
- [State Trust Account Regulations](https://www.nar.realtor)
- [Amazon Textract API](https://docs.aws.amazon.com/textract)
- [Temporal Workflow Documentation](https://docs.temporal.io)

