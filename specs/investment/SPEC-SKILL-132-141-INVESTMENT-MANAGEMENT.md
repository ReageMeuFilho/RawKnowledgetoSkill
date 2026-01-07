# Engineering Specification: Investment Analysis & Portfolio Optimization System

> **Specification ID**: SPEC-SKILL-132-141
> **Version**: 1.0.0
> **Status**: FINAL
> **Created**: 2026-01-07
> **Phase**: 3, Group 1

---

## 📋 Document Control

| Field | Value |
|-------|-------|
| **Skills Covered** | SKILL-132 through SKILL-141 |
| **Category** | Investment Management |
| **Priority** | P3 |
| **Complexity** | High |
| **Research Source** | Research Phase 3 Group 1.txt |
| **Lines of Research** | ~7,660 lines |

---

## 🎯 Executive Summary

The Investment Analysis & Portfolio Optimization system provides institutional-grade financial modeling capabilities for real estate investment analysis. This specification covers 10 skills that enable property managers and individual investors to perform sophisticated DCF modeling, cap rate analysis, portfolio optimization using Modern Portfolio Theory, and waterfall distribution calculations for syndications.

### Skills Matrix

| Skill ID | Skill Name | Priority | Complexity | Treasury Value |
|----------|------------|----------|------------|----------------|
| **SKILL-132** | Property Valuation Model | Critical | High | 🟠 High |
| **SKILL-133** | Cap Rate Calculator | Critical | Low | 🟡 Medium |
| **SKILL-134** | Cash Flow Projector | Critical | High | 🔴 Critical |
| **SKILL-135** | ROI/IRR/CoC Analyzer | Critical | Medium | 🔴 Critical |
| **SKILL-136** | Market Comparison Analysis | High | Medium | 🟡 Medium |
| **SKILL-137** | Mortgage Calculator & Amortization | High | Medium | 🟡 Medium |
| **SKILL-138** | Deal Analyzer | High | Medium | 🟠 High |
| **SKILL-139** | Portfolio Performance Dashboard | Critical | Medium | 🟠 High |
| **SKILL-140** | Portfolio Optimizer | High | High | 🔴 Critical |
| **SKILL-141** | Investment Waterfall | Medium | High | 🔴 Critical |

---

## 🏗️ Architecture Alignment Notes

### Layer Mapping (Citadel OS 6-Layer Stack)

| Layer | Components | Implementation |
|-------|------------|----------------|
| **Layer 6: Applications** | Investment Dashboard, Investor Portal | React 19.1+, Next.js 15.4+ |
| **Layer 5: Domain Bundles** | `investment-analysis-bundle` | Property Valuation, Portfolio Management |
| **Layer 4: Skills Layer** | SKILL-132 to SKILL-141 | Hot Path (Calculations), Cold Path (Transactions) |
| **Layer 3: Hot Path** | Investment Analysis Engine | FastAPI 0.115+, NumPy, Pandas, SciPy |
| **Layer 2: Cold Path** | Financial Transactions | TigerBeetle, Temporal, Formance |
| **Layer 1: Infrastructure** | Data Storage | PostgreSQL 16+, Redis 7.4+, AWS S3 |

### Execution Path Classification

| Skill | Execution Path | Justification |
|-------|---------------|---------------|
| SKILL-132 | **Hybrid** | AI reasoning (DCF assumptions) + Financial guarantees (valuation records) |
| SKILL-133 | **Hot** | Pure mathematical calculation, sub-second response |
| SKILL-134 | **Hybrid** | AI projections + TigerBeetle transaction records |
| SKILL-135 | **Hot** | Mathematical calculations with caching |
| SKILL-136 | **Hot** | Market data retrieval + comparison logic |
| SKILL-137 | **Hot** | Mathematical amortization calculations |
| SKILL-138 | **Hybrid** | AI analysis + structured scoring |
| SKILL-139 | **Hot** | Real-time dashboard rendering |
| SKILL-140 | **Hybrid** | AI optimization + transaction execution |
| SKILL-141 | **Cold** | Financial waterfall requires TigerBeetle strict consistency |

### MCP Server Requirements

| Server | Protocol | Purpose |
|--------|----------|---------|
| `mcp://treasury-read` | MCP | Read investment account balances |
| `mcp://treasury-write` | MCP | Record investment transactions |
| `mcp://market-data` | MCP | Fetch real-time market data |
| `mcp://temporal-trigger` | MCP | Trigger cash flow projection workflows |
| `mcp://analytics-query` | MCP | Query portfolio performance data |

### Infrastructure Alignment Verification

| Decision | Architecture Requirement | Specification Compliance |
|----------|-------------------------|-------------------------|
| **Container Orchestration** | AWS ECS/Fargate | ✅ Aligned |
| **Primary Database** | PostgreSQL 16+ | ✅ Aligned |
| **Financial Ledger** | TigerBeetle | ✅ Aligned |
| **Cache Layer** | Redis 7.4+ | ✅ Aligned |
| **Workflow Orchestration** | Temporal | ✅ Aligned |
| **API Gateway** | Rust/Axum | ✅ FastAPI for calculations, Axum for gateway |
| **Cloud Provider** | AWS | ✅ Aligned |

---

## 📐 Technology Stack

### Backend Stack

| Component | Technology | Version | Justification |
|-----------|------------|---------|---------------|
| **Language** | Python | 3.12+ | Extensive financial libraries (NumPy, Pandas, SciPy) |
| **API Framework** | FastAPI | 0.115+ | High-performance async for financial calculations |
| **Validation** | Pydantic | 2.10+ | Type-safe financial data validation |
| **ORM** | SQLAlchemy | 2.0+ | Async PostgreSQL support |
| **Numerical** | NumPy | 2.1+ | Core mathematical operations |
| **Data Analysis** | Pandas | 2.2+ | Time series for cash flow projections |
| **Optimization** | SciPy | 1.14+ | Portfolio optimization algorithms |
| **Financial Engineering** | QuantLib-Python | 1.35+ | Bond pricing, yield curves |
| **Financial Ledger** | TigerBeetle-Python | 0.16+ | Mission-critical transactions |

### Frontend Stack

| Component | Technology | Version | Justification |
|-----------|------------|---------|---------------|
| **Language** | TypeScript | 5.8+ | Type safety for financial interfaces |
| **UI Library** | React | 19.1+ | Concurrent rendering for dashboards |
| **Framework** | Next.js | 15.4+ | SSR for investment reports |
| **Styling** | TailwindCSS | 4.1+ | Rapid responsive development |
| **Charts** | Recharts | 2.13+ | Financial visualizations |
| **Forms** | React Hook Form | 7.54+ | Complex investment forms |
| **Validation** | Zod | 3.24+ | Schema validation |

### Database Stack

| Component | Technology | Version | Purpose |
|-----------|------------|---------|---------|
| **Primary** | PostgreSQL | 16+ | Investment data, property records |
| **Financial Ledger** | TigerBeetle | 0.16+ | Double-entry bookkeeping, audit trails |
| **Cache** | Redis | 7.4+ | Market data cache (15-min TTL) |
| **Object Storage** | AWS S3 | - | Investment documents |

### External Services

| Service | Purpose | Integration Method |
|---------|---------|-------------------|
| **CoStar API** | Commercial real estate data | REST API with OAuth 2.0 |
| **MLS Systems** | Property listings | RETS/RESO Web API |
| **Zillow API** | Residential market data | REST API |
| **Auth0** | Authentication | OAuth 2.0/OIDC |

---

## 🔧 Skill Specifications

### SKILL-132: Property Valuation Model

**Description**: Comprehensive property valuation supporting DCF, Cap Rate, Market Comparison, and Cost Approach methodologies.

**Functional Requirements**:

| Req ID | Description | Acceptance Criteria | Priority |
|--------|-------------|---------------------|----------|
| F-132-001 | DCF Valuation Engine | 5-10 year cash flow projections with terminal value | Must-Have |
| F-132-002 | Market Approach Valuation | Automated comparable analysis with adjustments | Must-Have |
| F-132-003 | Cost Approach Valuation | Land value + construction - depreciation | Should-Have |
| F-132-004 | Valuation Report Generation | Professional PDF with charts and assumptions | Must-Have |

**API Contract**:

```python
# POST /api/v1/valuations/dcf
@router.post("/valuations/dcf")
async def calculate_dcf_valuation(
    property_id: UUID,
    request: DCFValuationRequest
) -> DCFValuationResponse:
    """
    Calculate Discounted Cash Flow valuation for a property.
    
    Args:
        property_id: UUID of the property
        request: DCFValuationRequest containing:
            - projection_years: int (5-10)
            - discount_rate: Decimal
            - terminal_cap_rate: Decimal
            - rent_growth_rate: Decimal
            - expense_growth_rate: Decimal
            - capex_schedule: List[CapExItem]
    
    Returns:
        DCFValuationResponse:
            - present_value: Decimal
            - terminal_value: Decimal
            - total_value: Decimal
            - year_by_year_cash_flows: List[CashFlowYear]
            - sensitivity_analysis: SensitivityMatrix
    """
```

**Data Model**:

```sql
CREATE TABLE valuations (
    valuation_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    property_id UUID NOT NULL REFERENCES properties(property_id),
    valuation_method valuation_method_enum NOT NULL,
    estimated_value DECIMAL(15,2) NOT NULL,
    cap_rate DECIMAL(5,4),
    noi DECIMAL(15,2),
    discount_rate DECIMAL(5,4),
    terminal_cap_rate DECIMAL(5,4),
    assumptions JSONB NOT NULL,
    created_by UUID NOT NULL REFERENCES users(user_id),
    valuation_date TIMESTAMP NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    CONSTRAINT valid_cap_rate CHECK (cap_rate > 0 AND cap_rate < 1),
    CONSTRAINT valid_discount_rate CHECK (discount_rate > 0 AND discount_rate < 1)
);

CREATE INDEX idx_valuations_property_date 
ON valuations (property_id, valuation_date DESC);
```

**Calculation Engine**:

```python
from decimal import Decimal
from typing import List
import numpy as np

class DCFCalculator:
    """Discounted Cash Flow valuation calculator."""
    
    def calculate_dcf(
        self,
        initial_noi: Decimal,
        projection_years: int,
        discount_rate: Decimal,
        terminal_cap_rate: Decimal,
        rent_growth_rate: Decimal,
        expense_growth_rate: Decimal,
        capex_schedule: List[Decimal]
    ) -> DCFResult:
        """
        Calculate DCF valuation.
        
        Formula: PV = Σ(CFt / (1+r)^t) + TV / (1+r)^n
        Where:
            CFt = Cash flow in year t
            r = Discount rate
            TV = Terminal Value = NOI(n+1) / Terminal Cap Rate
            n = Number of projection years
        """
        cash_flows = []
        current_noi = float(initial_noi)
        
        for year in range(1, projection_years + 1):
            # Apply growth rates
            current_noi *= (1 + float(rent_growth_rate))
            
            # Subtract CapEx
            capex = float(capex_schedule[year - 1]) if year <= len(capex_schedule) else 0
            net_cash_flow = current_noi - capex
            
            # Discount to present value
            discount_factor = (1 + float(discount_rate)) ** year
            present_value = net_cash_flow / discount_factor
            
            cash_flows.append(CashFlowYear(
                year=year,
                noi=Decimal(str(current_noi)),
                capex=Decimal(str(capex)),
                net_cash_flow=Decimal(str(net_cash_flow)),
                present_value=Decimal(str(present_value))
            ))
        
        # Calculate terminal value
        terminal_noi = current_noi * (1 + float(rent_growth_rate))
        terminal_value = terminal_noi / float(terminal_cap_rate)
        terminal_pv = terminal_value / ((1 + float(discount_rate)) ** projection_years)
        
        # Sum present values
        total_pv = sum(cf.present_value for cf in cash_flows) + Decimal(str(terminal_pv))
        
        return DCFResult(
            present_value=total_pv,
            terminal_value=Decimal(str(terminal_value)),
            terminal_pv=Decimal(str(terminal_pv)),
            year_by_year_cash_flows=cash_flows
        )
```

---

### SKILL-133: Cap Rate Calculator

**Description**: Real-time capitalization rate calculation using NOI / Property Value formula.

**Functional Requirements**:

| Req ID | Description | Acceptance Criteria | Priority |
|--------|-------------|---------------------|----------|
| F-133-001 | NOI Calculation | Automated NOI = Gross Income - Vacancy - OpEx | Must-Have |
| F-133-002 | Cap Rate Calculation | Cap Rate = NOI / Property Value with real-time updates | Must-Have |
| F-133-003 | Reverse Valuation | Property Value = NOI / Market Cap Rate | Must-Have |
| F-133-004 | Market Cap Rate Integration | Benchmark cap rates from market data | Should-Have |

**API Contract**:

```python
# POST /api/v1/calculations/cap-rate
@router.post("/calculations/cap-rate")
async def calculate_cap_rate(
    request: CapRateRequest
) -> CapRateResponse:
    """
    Calculate capitalization rate.
    
    Response time target: <1 second
    """

class CapRateRequest(BaseModel):
    gross_income: Decimal = Field(..., gt=0)
    vacancy_rate: Decimal = Field(..., ge=0, le=1)
    operating_expenses: Decimal = Field(..., ge=0)
    property_value: Decimal = Field(..., gt=0)

class CapRateResponse(BaseModel):
    noi: Decimal
    cap_rate: Decimal
    implied_value_at_market_cap: Optional[Decimal]
    market_cap_rate: Optional[Decimal]
    comparison_to_market: Optional[str]  # "Above", "Below", "At Market"
```

**Calculation Engine**:

```python
from decimal import Decimal, ROUND_HALF_UP

class CapRateCalculator:
    """Cap Rate calculation engine with market comparison."""
    
    def calculate(
        self,
        gross_income: Decimal,
        vacancy_rate: Decimal,
        operating_expenses: Decimal,
        property_value: Decimal,
        market_cap_rate: Optional[Decimal] = None
    ) -> CapRateResult:
        """
        Calculate Cap Rate: NOI / Property Value
        
        Cap Rate = (Gross Income × (1 - Vacancy Rate) - Operating Expenses) / Property Value
        """
        if property_value <= 0:
            raise ValueError("Property value must be greater than zero")
        
        # Calculate Effective Gross Income
        effective_gross = gross_income * (Decimal('1') - vacancy_rate)
        
        # Calculate NOI
        noi = effective_gross - operating_expenses
        
        if noi <= 0:
            raise ValueError("NOI must be positive for cap rate calculation")
        
        # Calculate Cap Rate
        cap_rate = (noi / property_value).quantize(
            Decimal('0.0001'), rounding=ROUND_HALF_UP
        )
        
        # Calculate implied value at market cap rate
        implied_value = None
        comparison = None
        if market_cap_rate and market_cap_rate > 0:
            implied_value = (noi / market_cap_rate).quantize(
                Decimal('1'), rounding=ROUND_HALF_UP
            )
            if cap_rate > market_cap_rate:
                comparison = "Above Market (Higher Risk/Return)"
            elif cap_rate < market_cap_rate:
                comparison = "Below Market (Lower Risk/Return)"
            else:
                comparison = "At Market"
        
        return CapRateResult(
            noi=noi,
            cap_rate=cap_rate,
            implied_value=implied_value,
            market_cap_rate=market_cap_rate,
            comparison=comparison
        )
    
    def reverse_valuation(
        self,
        noi: Decimal,
        target_cap_rate: Decimal
    ) -> Decimal:
        """
        Calculate property value from NOI and target cap rate.
        
        Property Value = NOI / Cap Rate
        """
        if target_cap_rate <= 0:
            raise ValueError("Cap rate must be greater than zero")
        
        return (noi / target_cap_rate).quantize(
            Decimal('1'), rounding=ROUND_HALF_UP
        )
```

---

### SKILL-134: Cash Flow Projector

**Description**: Detailed cash flow modeling at property and portfolio levels with multi-year projections.

**Functional Requirements**:

| Req ID | Description | Acceptance Criteria | Priority |
|--------|-------------|---------------------|----------|
| F-134-001 | Multi-Year Projections | 5-10 year projections with growth assumptions | Must-Have |
| F-134-002 | Scenario Modeling | Base, upside, downside scenarios | Must-Have |
| F-134-003 | Lease-by-Lease Modeling | Individual lease analysis with rollovers | Should-Have |
| F-134-004 | CapEx Planning | CapEx scheduling with cash flow impact | Must-Have |

**Data Model**:

```sql
CREATE TABLE cash_flows (
    cash_flow_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    property_id UUID NOT NULL REFERENCES properties(property_id),
    scenario_type scenario_enum DEFAULT 'base',
    projection_year INTEGER NOT NULL,
    gross_potential_rent DECIMAL(15,2),
    vacancy_loss DECIMAL(15,2),
    effective_gross_income DECIMAL(15,2),
    operating_expenses DECIMAL(15,2),
    net_operating_income DECIMAL(15,2),
    capital_expenditures DECIMAL(15,2),
    debt_service DECIMAL(15,2),
    net_cash_flow DECIMAL(15,2),
    assumptions JSONB,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    CONSTRAINT unique_property_year_scenario 
        UNIQUE (property_id, projection_year, scenario_type)
) PARTITION BY RANGE (projection_year);

-- Create yearly partitions
CREATE TABLE cash_flows_2026 PARTITION OF cash_flows
    FOR VALUES FROM (2026) TO (2027);
CREATE TABLE cash_flows_2027 PARTITION OF cash_flows
    FOR VALUES FROM (2027) TO (2028);
```

**Projection Engine**:

```python
from dataclasses import dataclass
from typing import List, Optional
from decimal import Decimal
from enum import Enum

class ScenarioType(Enum):
    BASE = "base"
    UPSIDE = "upside"
    DOWNSIDE = "downside"

@dataclass
class ProjectionAssumptions:
    rent_growth_rate: Decimal
    expense_growth_rate: Decimal
    vacancy_rate: Decimal
    capex_reserve_pct: Decimal
    inflation_rate: Decimal

class CashFlowProjector:
    """Multi-year cash flow projection engine."""
    
    SCENARIO_ADJUSTMENTS = {
        ScenarioType.BASE: {
            'rent_multiplier': Decimal('1.0'),
            'vacancy_adjustment': Decimal('0.0'),
            'expense_multiplier': Decimal('1.0')
        },
        ScenarioType.UPSIDE: {
            'rent_multiplier': Decimal('1.15'),
            'vacancy_adjustment': Decimal('-0.02'),
            'expense_multiplier': Decimal('0.95')
        },
        ScenarioType.DOWNSIDE: {
            'rent_multiplier': Decimal('0.90'),
            'vacancy_adjustment': Decimal('0.05'),
            'expense_multiplier': Decimal('1.10')
        }
    }
    
    def project_cash_flows(
        self,
        property_id: UUID,
        base_year_financials: PropertyFinancials,
        assumptions: ProjectionAssumptions,
        projection_years: int = 10,
        scenario: ScenarioType = ScenarioType.BASE
    ) -> List[ProjectedCashFlow]:
        """
        Generate multi-year cash flow projections.
        
        Response time target: <5 seconds for 10-year projection
        """
        adjustments = self.SCENARIO_ADJUSTMENTS[scenario]
        projections = []
        
        current_rent = base_year_financials.gross_potential_rent
        current_expenses = base_year_financials.operating_expenses
        
        for year in range(1, projection_years + 1):
            # Apply growth rates with scenario adjustments
            rent_growth = (
                assumptions.rent_growth_rate * 
                adjustments['rent_multiplier']
            )
            current_rent *= (Decimal('1') + rent_growth)
            
            expense_growth = (
                assumptions.expense_growth_rate * 
                adjustments['expense_multiplier']
            )
            current_expenses *= (Decimal('1') + expense_growth)
            
            # Calculate vacancy with scenario adjustment
            effective_vacancy = (
                assumptions.vacancy_rate + 
                adjustments['vacancy_adjustment']
            )
            vacancy_loss = current_rent * effective_vacancy
            effective_gross = current_rent - vacancy_loss
            
            # Calculate NOI
            noi = effective_gross - current_expenses
            
            # CapEx reserve
            capex = current_rent * assumptions.capex_reserve_pct
            
            # Net Cash Flow
            net_cash_flow = noi - capex
            
            projections.append(ProjectedCashFlow(
                property_id=property_id,
                scenario_type=scenario,
                projection_year=year,
                gross_potential_rent=current_rent,
                vacancy_loss=vacancy_loss,
                effective_gross_income=effective_gross,
                operating_expenses=current_expenses,
                net_operating_income=noi,
                capital_expenditures=capex,
                net_cash_flow=net_cash_flow
            ))
        
        return projections
```

---

### SKILL-135: ROI/IRR/CoC Analyzer

**Description**: Comprehensive return metrics calculation including IRR, NPV, and Cash-on-Cash Return.

**Functional Requirements**:

| Req ID | Description | Acceptance Criteria | Priority |
|--------|-------------|---------------------|----------|
| F-135-001 | IRR Calculation | Time-weighted IRR with cash flow timing | Must-Have |
| F-135-002 | Cash-on-Cash Return | Annual cash flow / initial cash investment | Must-Have |
| F-135-003 | NPV Analysis | Present value with discount rate | Must-Have |
| F-135-004 | Equity Multiple | Total returns / initial equity over hold period | Should-Have |

**Calculation Engine**:

```python
import numpy as np
from numpy_financial import irr, npv
from decimal import Decimal
from typing import List

class InvestmentMetricsCalculator:
    """Investment return metrics calculator."""
    
    def calculate_irr(self, cash_flows: List[Decimal]) -> Decimal:
        """
        Calculate Internal Rate of Return.
        
        IRR is the discount rate that makes NPV = 0
        
        Args:
            cash_flows: List starting with negative initial investment
        
        Returns:
            IRR as a decimal (e.g., 0.12 for 12%)
        """
        np_cash_flows = np.array([float(cf) for cf in cash_flows])
        result = irr(np_cash_flows)
        
        if np.isnan(result):
            raise ValueError("IRR could not be calculated - check cash flow signs")
        
        return Decimal(str(result)).quantize(Decimal('0.0001'))
    
    def calculate_npv(
        self, 
        cash_flows: List[Decimal], 
        discount_rate: Decimal
    ) -> Decimal:
        """
        Calculate Net Present Value.
        
        NPV = Σ(CFt / (1+r)^t)
        """
        np_cash_flows = np.array([float(cf) for cf in cash_flows])
        result = npv(float(discount_rate), np_cash_flows)
        
        return Decimal(str(result)).quantize(Decimal('0.01'))
    
    def calculate_cash_on_cash(
        self,
        annual_cash_flow: Decimal,
        initial_cash_invested: Decimal
    ) -> Decimal:
        """
        Calculate Cash-on-Cash Return.
        
        CoC = Annual Cash Flow / Initial Cash Investment
        """
        if initial_cash_invested <= 0:
            raise ValueError("Initial cash investment must be positive")
        
        return (annual_cash_flow / initial_cash_invested).quantize(
            Decimal('0.0001')
        )
    
    def calculate_equity_multiple(
        self,
        total_distributions: Decimal,
        initial_equity: Decimal
    ) -> Decimal:
        """
        Calculate Equity Multiple.
        
        EM = Total Distributions / Initial Equity
        """
        if initial_equity <= 0:
            raise ValueError("Initial equity must be positive")
        
        return (total_distributions / initial_equity).quantize(
            Decimal('0.01')
        )
    
    def calculate_all_metrics(
        self,
        initial_investment: Decimal,
        annual_cash_flows: List[Decimal],
        sale_proceeds: Decimal,
        discount_rate: Decimal
    ) -> InvestmentMetricsResult:
        """
        Calculate all investment metrics for a deal.
        """
        # Construct full cash flow series
        all_cash_flows = [-initial_investment] + annual_cash_flows
        all_cash_flows[-1] += sale_proceeds  # Add sale to final year
        
        # Calculate metrics
        irr_value = self.calculate_irr(all_cash_flows)
        npv_value = self.calculate_npv(all_cash_flows, discount_rate)
        
        # Year 1 CoC
        coc = self.calculate_cash_on_cash(
            annual_cash_flows[0], 
            initial_investment
        )
        
        # Equity multiple
        total_distributions = sum(annual_cash_flows) + sale_proceeds
        equity_multiple = self.calculate_equity_multiple(
            total_distributions, 
            initial_investment
        )
        
        return InvestmentMetricsResult(
            irr=irr_value,
            npv=npv_value,
            cash_on_cash_year1=coc,
            equity_multiple=equity_multiple,
            average_annual_return=irr_value,  # Simplified
            payback_period=self._calculate_payback_period(
                initial_investment, annual_cash_flows
            )
        )
    
    def _calculate_payback_period(
        self,
        initial_investment: Decimal,
        cash_flows: List[Decimal]
    ) -> Optional[Decimal]:
        """Calculate simple payback period in years."""
        cumulative = Decimal('0')
        for i, cf in enumerate(cash_flows):
            cumulative += cf
            if cumulative >= initial_investment:
                # Linear interpolation for partial year
                prior_cumulative = cumulative - cf
                remaining = initial_investment - prior_cumulative
                partial_year = remaining / cf
                return Decimal(str(i)) + partial_year
        return None  # Not recovered
```

---

### SKILL-140: Portfolio Optimizer

**Description**: Asset allocation optimization using Modern Portfolio Theory and Black-Litterman model.

**Functional Requirements**:

| Req ID | Description | Acceptance Criteria | Priority |
|--------|-------------|---------------------|----------|
| F-140-001 | Asset Allocation Analysis | Optimal allocation across property types | Must-Have |
| F-140-002 | Efficient Frontier Calculation | Risk-return optimization using MPT | Should-Have |
| F-140-003 | Rebalancing Recommendations | Automated optimization suggestions | Should-Have |
| F-140-004 | Scenario Stress Testing | Portfolio performance under market conditions | Must-Have |

**Optimization Engine**:

```python
import numpy as np
from scipy.optimize import minimize
from typing import Dict, List, Tuple
from decimal import Decimal

class PortfolioOptimizer:
    """
    Portfolio optimization using Modern Portfolio Theory.
    
    Implements mean-variance optimization with optional
    Black-Litterman views integration.
    """
    
    def __init__(self, risk_free_rate: float = 0.04):
        self.risk_free_rate = risk_free_rate
    
    def calculate_efficient_frontier(
        self,
        returns: np.ndarray,
        cov_matrix: np.ndarray,
        num_portfolios: int = 100
    ) -> List[PortfolioPoint]:
        """
        Calculate the efficient frontier.
        
        Returns portfolios from minimum variance to maximum return.
        """
        n_assets = len(returns)
        
        # Find min variance portfolio
        min_var_weights = self._minimize_variance(cov_matrix)
        min_return = np.dot(min_var_weights, returns)
        
        # Find max return portfolio
        max_return = np.max(returns)
        
        # Generate target returns
        target_returns = np.linspace(min_return, max_return, num_portfolios)
        
        frontier = []
        for target in target_returns:
            weights = self._optimize_for_return(
                returns, cov_matrix, target
            )
            portfolio_return = np.dot(weights, returns)
            portfolio_risk = np.sqrt(
                np.dot(weights.T, np.dot(cov_matrix, weights))
            )
            sharpe = (portfolio_return - self.risk_free_rate) / portfolio_risk
            
            frontier.append(PortfolioPoint(
                weights=weights.tolist(),
                expected_return=portfolio_return,
                volatility=portfolio_risk,
                sharpe_ratio=sharpe
            ))
        
        return frontier
    
    def optimize_portfolio(
        self,
        returns: np.ndarray,
        cov_matrix: np.ndarray,
        constraints: Optional[PortfolioConstraints] = None
    ) -> OptimalPortfolio:
        """
        Find optimal portfolio maximizing Sharpe ratio.
        """
        n_assets = len(returns)
        
        def neg_sharpe(weights):
            port_return = np.dot(weights, returns)
            port_vol = np.sqrt(np.dot(weights.T, np.dot(cov_matrix, weights)))
            return -(port_return - self.risk_free_rate) / port_vol
        
        # Constraints
        constraint_list = [
            {'type': 'eq', 'fun': lambda w: np.sum(w) - 1}  # Weights sum to 1
        ]
        
        if constraints:
            if constraints.max_single_asset:
                for i in range(n_assets):
                    constraint_list.append({
                        'type': 'ineq',
                        'fun': lambda w, i=i: constraints.max_single_asset - w[i]
                    })
        
        # Bounds (0 to 1 for each asset, no shorting)
        bounds = tuple((0, 1) for _ in range(n_assets))
        
        # Initial guess (equal weights)
        init_weights = np.array([1/n_assets] * n_assets)
        
        result = minimize(
            neg_sharpe,
            init_weights,
            method='SLSQP',
            bounds=bounds,
            constraints=constraint_list
        )
        
        optimal_weights = result.x
        port_return = np.dot(optimal_weights, returns)
        port_vol = np.sqrt(
            np.dot(optimal_weights.T, np.dot(cov_matrix, optimal_weights))
        )
        
        return OptimalPortfolio(
            weights={
                f"asset_{i}": Decimal(str(w)).quantize(Decimal('0.0001'))
                for i, w in enumerate(optimal_weights)
            },
            expected_return=Decimal(str(port_return)).quantize(Decimal('0.0001')),
            expected_volatility=Decimal(str(port_vol)).quantize(Decimal('0.0001')),
            sharpe_ratio=Decimal(str(-result.fun)).quantize(Decimal('0.0001'))
        )
    
    def generate_rebalancing_recommendations(
        self,
        current_allocation: Dict[str, Decimal],
        optimal_allocation: Dict[str, Decimal],
        threshold: Decimal = Decimal('0.05')
    ) -> List[RebalancingAction]:
        """
        Generate rebalancing recommendations based on drift from optimal.
        """
        actions = []
        
        for asset_id in set(current_allocation.keys()) | set(optimal_allocation.keys()):
            current = current_allocation.get(asset_id, Decimal('0'))
            optimal = optimal_allocation.get(asset_id, Decimal('0'))
            drift = current - optimal
            
            if abs(drift) > threshold:
                action_type = 'SELL' if drift > 0 else 'BUY'
                actions.append(RebalancingAction(
                    asset_id=asset_id,
                    action=action_type,
                    current_weight=current,
                    target_weight=optimal,
                    adjustment_amount=abs(drift)
                ))
        
        return sorted(actions, key=lambda x: x.adjustment_amount, reverse=True)
```

---

### SKILL-141: Investment Waterfall

**Description**: Sophisticated profit-sharing calculations for syndications and fund structures.

**Functional Requirements**:

| Req ID | Description | Acceptance Criteria | Priority |
|--------|-------------|---------------------|----------|
| F-141-001 | Preferred Return Calculation | LP preferred return (6-10%) before GP promote | Must-Have |
| F-141-002 | Catch-up Distribution | GP catch-up calculation after pref | Must-Have |
| F-141-003 | Promote Tiers | Multiple promote tiers (20/80, 30/70, etc.) | Must-Have |
| F-141-004 | Capital Account Tracking | LP/GP capital balance maintenance | Must-Have |

**Waterfall Engine**:

```python
from decimal import Decimal, ROUND_HALF_UP
from typing import List, Dict
from dataclasses import dataclass

@dataclass
class WaterfallTier:
    irr_threshold: Decimal
    lp_split: Decimal
    gp_split: Decimal
    description: str

@dataclass
class WaterfallDistribution:
    tier: str
    irr_threshold: Decimal
    amount: Decimal
    lp_amount: Decimal
    gp_amount: Decimal

class InvestmentWaterfallEngine:
    """
    Investment waterfall distribution calculator.
    
    Supports multi-tier promote structures with:
    - Preferred return
    - Return of capital
    - GP catch-up
    - Tiered promotes based on IRR hurdles
    """
    
    def __init__(
        self,
        preferred_return: Decimal = Decimal('0.08'),  # 8% pref
        catch_up_split: Decimal = Decimal('0.50'),     # 50% GP catch-up
        tiers: Optional[List[WaterfallTier]] = None
    ):
        self.preferred_return = preferred_return
        self.catch_up_split = catch_up_split
        
        # Default tier structure
        self.tiers = tiers or [
            WaterfallTier(
                irr_threshold=Decimal('0.12'),
                lp_split=Decimal('0.80'),
                gp_split=Decimal('0.20'),
                description="Tier 1: 12-15% IRR"
            ),
            WaterfallTier(
                irr_threshold=Decimal('0.15'),
                lp_split=Decimal('0.70'),
                gp_split=Decimal('0.30'),
                description="Tier 2: 15-20% IRR"
            ),
            WaterfallTier(
                irr_threshold=Decimal('0.20'),
                lp_split=Decimal('0.60'),
                gp_split=Decimal('0.40'),
                description="Tier 3: 20%+ IRR"
            )
        ]
    
    def calculate_waterfall(
        self,
        lp_capital: Decimal,
        total_distributions: Decimal,
        holding_period_years: Decimal
    ) -> WaterfallResult:
        """
        Calculate waterfall distribution.
        
        Order of distribution:
        1. Return of LP capital
        2. LP preferred return
        3. GP catch-up
        4. Tiered profit splits
        """
        distributions: List[WaterfallDistribution] = []
        remaining = total_distributions
        lp_total = Decimal('0')
        gp_total = Decimal('0')
        
        # Step 1: Return of Capital
        roc_amount = min(remaining, lp_capital)
        distributions.append(WaterfallDistribution(
            tier="Return of Capital",
            irr_threshold=Decimal('0'),
            amount=roc_amount,
            lp_amount=roc_amount,
            gp_amount=Decimal('0')
        ))
        lp_total += roc_amount
        remaining -= roc_amount
        
        if remaining <= 0:
            return self._build_result(distributions, lp_total, gp_total, lp_capital)
        
        # Step 2: Preferred Return (8% cumulative)
        pref_amount = lp_capital * self.preferred_return * holding_period_years
        pref_distributed = min(remaining, pref_amount)
        distributions.append(WaterfallDistribution(
            tier=f"Preferred Return ({self.preferred_return * 100}%)",
            irr_threshold=self.preferred_return,
            amount=pref_distributed,
            lp_amount=pref_distributed,
            gp_amount=Decimal('0')
        ))
        lp_total += pref_distributed
        remaining -= pref_distributed
        
        if remaining <= 0:
            return self._build_result(distributions, lp_total, gp_total, lp_capital)
        
        # Step 3: GP Catch-up (50% to GP until 20% of profits)
        total_profits = total_distributions - lp_capital
        gp_catch_up_target = total_profits * Decimal('0.20')  # 20/80 split
        gp_catch_up_needed = gp_catch_up_target - gp_total
        
        if gp_catch_up_needed > 0:
            catch_up_amount = min(remaining, gp_catch_up_needed / self.catch_up_split)
            gp_catch_up = catch_up_amount * self.catch_up_split
            lp_catch_up = catch_up_amount - gp_catch_up
            
            distributions.append(WaterfallDistribution(
                tier="GP Catch-up",
                irr_threshold=self.preferred_return,
                amount=catch_up_amount,
                lp_amount=lp_catch_up,
                gp_amount=gp_catch_up
            ))
            lp_total += lp_catch_up
            gp_total += gp_catch_up
            remaining -= catch_up_amount
        
        if remaining <= 0:
            return self._build_result(distributions, lp_total, gp_total, lp_capital)
        
        # Step 4: Tiered Profit Splits
        for tier in self.tiers:
            if remaining <= 0:
                break
            
            tier_amount = remaining  # All remaining goes to current tier
            lp_amount = tier_amount * tier.lp_split
            gp_amount = tier_amount * tier.gp_split
            
            distributions.append(WaterfallDistribution(
                tier=tier.description,
                irr_threshold=tier.irr_threshold,
                amount=tier_amount,
                lp_amount=lp_amount,
                gp_amount=gp_amount
            ))
            lp_total += lp_amount
            gp_total += gp_amount
            remaining -= tier_amount
        
        return self._build_result(distributions, lp_total, gp_total, lp_capital)
    
    def _build_result(
        self,
        distributions: List[WaterfallDistribution],
        lp_total: Decimal,
        gp_total: Decimal,
        lp_capital: Decimal
    ) -> WaterfallResult:
        total = lp_total + gp_total
        return WaterfallResult(
            distributions=distributions,
            lp_total=lp_total,
            gp_total=gp_total,
            total_distributed=total,
            lp_equity_multiple=(lp_total / lp_capital).quantize(Decimal('0.01')),
            lp_percentage=(lp_total / total * 100).quantize(Decimal('0.01')),
            gp_percentage=(gp_total / total * 100).quantize(Decimal('0.01'))
        )
```

**TigerBeetle Integration for Capital Tracking**:

```python
from tigerbeetle import Client, Account, Transfer

class WaterfallLedgerService:
    """TigerBeetle integration for waterfall capital tracking."""
    
    LEDGER_INVESTMENT = 100
    CODE_LP_CAPITAL = 1000
    CODE_GP_CAPITAL = 1001
    CODE_DISTRIBUTIONS = 2000
    
    def __init__(self, tigerbeetle_client: Client):
        self.client = tigerbeetle_client
    
    def create_investment_accounts(
        self,
        investment_id: int,
        lp_ids: List[int],
        gp_ids: List[int]
    ) -> None:
        """Create accounts for LP and GP capital tracking."""
        accounts = []
        
        for lp_id in lp_ids:
            accounts.append(Account(
                id=self._generate_account_id(investment_id, lp_id, 'LP'),
                ledger=self.LEDGER_INVESTMENT,
                code=self.CODE_LP_CAPITAL,
                flags=0,
                user_data_128=investment_id
            ))
        
        for gp_id in gp_ids:
            accounts.append(Account(
                id=self._generate_account_id(investment_id, gp_id, 'GP'),
                ledger=self.LEDGER_INVESTMENT,
                code=self.CODE_GP_CAPITAL,
                flags=0,
                user_data_128=investment_id
            ))
        
        errors = self.client.create_accounts(accounts)
        if errors:
            raise LedgerError(f"Failed to create accounts: {errors}")
    
    def record_distribution(
        self,
        investment_id: int,
        waterfall_result: WaterfallResult
    ) -> None:
        """Record waterfall distribution in TigerBeetle."""
        transfers = []
        
        for dist in waterfall_result.distributions:
            if dist.lp_amount > 0:
                transfers.append(Transfer(
                    id=self._generate_transfer_id(),
                    debit_account_id=self._get_holding_account(investment_id),
                    credit_account_id=self._get_lp_account(investment_id),
                    amount=int(dist.lp_amount * 100),  # Cents
                    ledger=self.LEDGER_INVESTMENT,
                    code=self.CODE_DISTRIBUTIONS
                ))
            
            if dist.gp_amount > 0:
                transfers.append(Transfer(
                    id=self._generate_transfer_id(),
                    debit_account_id=self._get_holding_account(investment_id),
                    credit_account_id=self._get_gp_account(investment_id),
                    amount=int(dist.gp_amount * 100),  # Cents
                    ledger=self.LEDGER_INVESTMENT,
                    code=self.CODE_DISTRIBUTIONS
                ))
        
        errors = self.client.create_transfers(transfers)
        if errors:
            raise LedgerError(f"Failed to record distributions: {errors}")
```

---

## 📊 Database Schema Summary

### PostgreSQL Tables

```sql
-- Core Tables
CREATE TABLE properties (
    property_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    address VARCHAR(255) NOT NULL,
    city VARCHAR(100) NOT NULL,
    state VARCHAR(2) NOT NULL,
    zip_code VARCHAR(10) NOT NULL,
    latitude DECIMAL(10,7),
    longitude DECIMAL(10,7),
    property_type property_type_enum NOT NULL,
    square_feet INTEGER,
    bedrooms INTEGER,
    bathrooms DECIMAL(3,1),
    year_built INTEGER,
    purchase_price DECIMAL(15,2),
    purchase_date DATE,
    owner_id UUID NOT NULL REFERENCES users(user_id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE portfolios (
    portfolio_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    portfolio_name VARCHAR(255) NOT NULL,
    description TEXT,
    manager_id UUID NOT NULL REFERENCES users(user_id),
    total_value DECIMAL(15,2) DEFAULT 0,
    target_allocation JSONB,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE portfolio_properties (
    portfolio_property_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    portfolio_id UUID NOT NULL REFERENCES portfolios(portfolio_id),
    property_id UUID NOT NULL REFERENCES properties(property_id),
    ownership_percentage DECIMAL(5,4) DEFAULT 1.0,
    acquisition_date DATE NOT NULL,
    acquisition_cost DECIMAL(15,2) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    CONSTRAINT unique_portfolio_property UNIQUE (portfolio_id, property_id)
);

CREATE TABLE market_comparables (
    comparable_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    subject_property_id UUID NOT NULL REFERENCES properties(property_id),
    comparable_address VARCHAR(255) NOT NULL,
    sale_price DECIMAL(15,2) NOT NULL,
    sale_date DATE NOT NULL,
    square_feet INTEGER,
    cap_rate DECIMAL(5,4),
    adjustments JSONB,
    adjusted_price DECIMAL(15,2),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Indexes
CREATE INDEX idx_properties_location ON properties (city, state, property_type);
CREATE INDEX idx_properties_price ON properties (purchase_price);
CREATE INDEX idx_valuations_property ON valuations (property_id, valuation_date DESC);
CREATE INDEX idx_cash_flows_property ON cash_flows (property_id, projection_year);
CREATE INDEX idx_portfolio_properties ON portfolio_properties (portfolio_id);
```

### TigerBeetle Account Structure

| Account Code | Type | Description |
|--------------|------|-------------|
| 1000 | Investment Capital | LP/GP contributions |
| 1001 | GP Capital | General Partner capital |
| 2000 | Property Assets | Real estate holdings |
| 3000 | Operating Income | Rental income, fees |
| 4000 | Operating Expenses | Management, maintenance |
| 5000 | Distributions | Payout tracking |

---

## 🔒 Security & Compliance

### Authentication & Authorization

| Component | Implementation | Compliance |
|-----------|---------------|------------|
| **User Auth** | Auth0 with MFA | SOC 2 Type II |
| **API Auth** | OAuth 2.0 + JWT | Industry Standard |
| **Service Auth** | mTLS Certificates | Zero Trust |
| **Data Encryption** | AES-256 at rest, TLS 1.3 in transit | GDPR |

### Role-Based Access Control

| Role | Property Data | Financials | Portfolio | Admin |
|------|---------------|------------|-----------|-------|
| Individual Investor | Read Own | Read/Write Own | Read/Write Own | - |
| Portfolio Manager | Read All | Read/Write Managed | Full | - |
| Limited Partner | Read Invested | Read Own | Read Invested | - |
| System Admin | Full | Read All | Full | Full |

### Audit Trail Requirements

- All financial calculations logged to TigerBeetle (immutable)
- User actions tracked with timestamp, user ID, IP address
- 7-year retention for SEC compliance
- Real-time compliance monitoring

---

## 📈 Performance Requirements

### Response Time SLAs

| Operation | Target | Warning | Critical |
|-----------|--------|---------|----------|
| Cap Rate Calculation | <500ms | >1s | >2s |
| DCF Valuation | <3s | >5s | >10s |
| Portfolio Optimization | <30s | >45s | >60s |
| Market Data Refresh | <15min | >20min | >30min |

### Throughput Targets

| Metric | Target | Measurement |
|--------|--------|-------------|
| Concurrent Users | 1,000 | Peak load |
| Calculations/Second | 100 | Standard operations |
| Transaction TPS | 1,000+ | TigerBeetle |
| API Requests/Min | 10,000 | Gateway |

---

## 🧪 Testing Strategy

### Test Coverage Requirements

| Component | Coverage Target | Critical Paths |
|-----------|----------------|----------------|
| Financial Calculations | 100% | All formulas |
| API Endpoints | 95% | CRUD, errors |
| Database Operations | 90% | Core CRUD |
| External Integrations | 85% | API calls |

### Financial Calculation Tests

```python
@pytest.mark.parametrize("noi,value,expected_cap", [
    (Decimal('100000'), Decimal('1250000'), Decimal('0.0800')),
    (Decimal('75000'), Decimal('1000000'), Decimal('0.0750')),
    (Decimal('150000'), Decimal('2000000'), Decimal('0.0750')),
])
def test_cap_rate_calculation(noi, value, expected_cap):
    """Test cap rate calculation accuracy."""
    calculator = CapRateCalculator()
    result = calculator.calculate(
        gross_income=noi / Decimal('0.95'),  # Assume 5% vacancy
        vacancy_rate=Decimal('0.05'),
        operating_expenses=Decimal('0'),
        property_value=value
    )
    assert result.cap_rate == expected_cap
```

---

## 🚀 Deployment Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        AWS Cloud                                 │
├─────────────────────────────────────────────────────────────────┤
│  ┌─────────────────┐    ┌─────────────────┐                    │
│  │   CloudFront    │    │   Route 53      │                    │
│  │   (CDN)         │    │   (DNS)         │                    │
│  └────────┬────────┘    └────────┬────────┘                    │
│           │                      │                              │
│  ┌────────┴──────────────────────┴────────┐                    │
│  │      Application Load Balancer          │                    │
│  └────────────────────┬───────────────────┘                    │
│                       │                                         │
│  ┌────────────────────┴───────────────────┐                    │
│  │           ECS Fargate Cluster           │                    │
│  │  ┌─────────────┐  ┌─────────────┐      │                    │
│  │  │ Investment  │  │  Portfolio  │      │                    │
│  │  │ Analysis    │  │  Management │      │                    │
│  │  │ Service     │  │  Service    │      │                    │
│  │  └─────────────┘  └─────────────┘      │                    │
│  │  ┌─────────────┐  ┌─────────────┐      │                    │
│  │  │ Market Data │  │  Reporting  │      │                    │
│  │  │ Service     │  │  Service    │      │                    │
│  │  └─────────────┘  └─────────────┘      │                    │
│  └────────────────────────────────────────┘                    │
│                       │                                         │
│  ┌────────────────────┴───────────────────┐                    │
│  │              Data Layer                 │                    │
│  │  ┌─────────────┐  ┌─────────────┐      │                    │
│  │  │ PostgreSQL  │  │ TigerBeetle │      │                    │
│  │  │ (RDS)       │  │ (EC2)       │      │                    │
│  │  └─────────────┘  └─────────────┘      │                    │
│  │  ┌─────────────┐  ┌─────────────┐      │                    │
│  │  │   Redis     │  │    S3       │      │                    │
│  │  │ (ElastiCache)│ │ (Documents) │      │                    │
│  │  └─────────────┘  └─────────────┘      │                    │
│  └────────────────────────────────────────┘                    │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📚 References

- **Research Source**: Research Phase 3 Group 1.txt (~7,660 lines)
- **Competitor Analysis**: ARGUS Enterprise, CoStar Analytics, RealPage
- **Financial Standards**: GAAP, SEC Rule 204-2, SOX Compliance
- **Architecture**: Citadel OS 6-Layer Stack, Treasury OS Integration

---

**Document Version**: 1.0.0
**Last Updated**: 2026-01-07
**Next Review**: After implementation kickoff

