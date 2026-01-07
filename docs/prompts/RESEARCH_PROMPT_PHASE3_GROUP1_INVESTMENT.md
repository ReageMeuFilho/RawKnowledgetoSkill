# Research Prompt: Phase 3 Group 1 - Investment Management

> **Target Agent**: AI Research Analyst
> **Output Location**: `knowledge/investment/KD-PHASE3-G1-investment-management.md`
> **Skills to Research**: SKILL-132 through SKILL-141 (10 skills)
> **Priority**: P3 (Advanced)
> **Estimated Research Time**: 6-8 hours

---

## 🎯 RESEARCH OBJECTIVE

Research and document comprehensive engineering specifications for **Investment Management** capabilities that enable property investors, syndicators, and portfolio managers to analyze, track, and optimize real estate investments.

---

## 📋 SKILLS TO SPECIFY

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-132** | Property Valuation AI | Investment | Automated Comparative Market Analysis (CMA) |
| **SKILL-133** | Cap Rate Calculator | Investment | Real-time capitalization rate tracking |
| **SKILL-134** | Cash Flow Projections | Investment | AI-powered multi-year forecasting |
| **SKILL-135** | Portfolio Performance Dashboard | Investment | ROI, IRR, CoC return tracking |
| **SKILL-136** | Investment Waterfall | Investment | Profit sharing calculations for syndications |
| **SKILL-137** | 1031 Exchange Tracker | Investment | Tax-deferred exchange management |
| **SKILL-138** | Rent Roll Analysis | Investment | Automated rent roll generation |
| **SKILL-139** | Asset Disposition Planning | Investment | Optimal sell timing recommendations |
| **SKILL-140** | Investor Portal | Investment | LP investor communication and reporting |
| **SKILL-141** | Deal Analyzer | Investment | Acquisition due diligence automation |

---

## 🔍 RESEARCH QUESTIONS BY SKILL

### SKILL-132: Property Valuation AI

**Core Questions**:
1. How do leading valuation platforms (Zillow, Redfin, CoreLogic) calculate Automated Valuation Models (AVMs)?
2. What data sources are required for accurate CMA (Comparable Market Analysis)?
3. How to weight different comparison factors (sq ft, beds, baths, location, condition)?
4. What ML models work best for property valuation (gradient boosting, neural networks)?
5. How to handle properties with limited comparables?
6. What's the typical accuracy range for AVMs (median error percentage)?
7. How to incorporate income approach for investment properties?
8. What APIs provide comparable sales data (MLS, public records)?

**Technical Requirements**:
- Accuracy metrics (AVM confidence scores)
- Data freshness requirements
- Geographical coverage considerations
- Integration with MLS/public record systems

### SKILL-133: Cap Rate Calculator

**Core Questions**:
1. How is cap rate calculated (NOI / Property Value)?
2. What's included in NOI calculation (income - operating expenses)?
3. How do platforms like CoStar track market cap rates?
4. What's the relationship between cap rate and risk?
5. How to compare cap rates across different property types?
6. What data sources provide market cap rate benchmarks?
7. How to handle cap rate compression/expansion trends?

**Technical Requirements**:
- Real-time NOI calculation from property data
- Market cap rate data integration
- Historical trend analysis
- Cap rate by property type/market/vintage

### SKILL-134: Cash Flow Projections

**Core Questions**:
1. What inputs are required for multi-year cash flow projections?
2. How do platforms like ARGUS model cash flows?
3. What assumptions drive projections (rent growth, vacancy, expenses)?
4. How to model refinancing events and capital events?
5. What's the standard projection period (5, 7, 10 years)?
6. How to incorporate Monte Carlo simulation for sensitivity analysis?
7. What exit cap rate assumptions are typical?

**Technical Requirements**:
- Input parameter validation
- Scenario modeling (base, upside, downside)
- Sensitivity analysis (tornado charts)
- PDF/Excel export capabilities

### SKILL-135: Portfolio Performance Dashboard

**Core Questions**:
1. What are the key metrics for real estate investment performance?
   - IRR (Internal Rate of Return)
   - Cash-on-Cash Return (CoC)
   - Equity Multiple
   - Total Return
2. How do institutional investors benchmark performance?
3. What visualization patterns work best for portfolio dashboards?
4. How to handle multiple entities/funds in one view?
5. How to compare actual vs. projected performance?
6. What's the standard reporting frequency (monthly, quarterly)?

**Technical Requirements**:
- Time-weighted vs. money-weighted returns
- Benchmark comparison (NCREIF, public REITs)
- Drill-down from portfolio to property to unit level
- Export to LP reporting formats

### SKILL-136: Investment Waterfall

**Core Questions**:
1. What are common waterfall structures (American, European)?
2. How do preferred returns (pref) work?
3. What are typical promote structures (80/20, 70/30)?
4. How to handle catch-up provisions?
5. What are GP/LP split mechanics at different IRR hurdles?
6. How do platforms like Juniper Square model waterfalls?
7. How to handle multiple investor classes (Class A, B, C)?

**Technical Requirements**:
- Configurable waterfall tiers
- Multiple hurdle rates (8%, 12%, 15%, 20%)
- Capital account tracking
- Distribution calculations and forecasts
- Audit trail for distributions

### SKILL-137: 1031 Exchange Tracker

**Core Questions**:
1. What are the IRS rules for 1031 exchanges?
   - 45-day identification period
   - 180-day exchange period
   - Like-kind requirements
2. How do Qualified Intermediaries (QIs) work?
3. What documentation is required for compliance?
4. How to track multiple replacement properties?
5. What happens with boot (cash received)?
6. How do reverse exchanges work?
7. What deadlines need automated alerts?

**Technical Requirements**:
- Timeline tracking with countdown
- Compliance checklist automation
- Document management
- QI integration (if available)
- Tax basis carryover calculations

### SKILL-138: Rent Roll Analysis

**Core Questions**:
1. What data is included in a standard rent roll?
2. How to calculate effective rent vs. market rent?
3. What lease rollover analysis is needed?
4. How to identify below-market leases?
5. How to project revenue with lease expirations?
6. What OCR/AI techniques extract rent rolls from PDFs?
7. What's the standard rent roll format for due diligence?

**Technical Requirements**:
- Rent roll import (Excel, PDF extraction)
- Market rent comparison
- Lease expiration calendar
- Loss-to-lease analysis
- T-12 (trailing 12 months) generation

### SKILL-139: Asset Disposition Planning

**Core Questions**:
1. What factors determine optimal hold period?
2. How do depreciation recapture taxes affect timing?
3. What market signals indicate good sell timing?
4. How to model disposition scenarios?
5. What's the typical disposition timeline?
6. How to prepare properties for sale (value-add completion)?
7. What broker selection criteria exist?

**Technical Requirements**:
- Hold period optimization model
- Tax impact analysis
- Market timing indicators
- Disposition checklist workflow
- Broker RFP management

### SKILL-140: Investor Portal

**Core Questions**:
1. What information do LPs want in an investor portal?
2. How do platforms like Juniper Square and AppFolio Investment Management work?
3. What reporting formats are expected (K-1s, quarterly reports)?
4. How to handle capital calls and distributions?
5. What document sharing requirements exist?
6. How to manage investor communications?
7. What compliance/accreditation tracking is needed?

**Technical Requirements**:
- Secure document vault
- Capital account statements
- Distribution history
- K-1 delivery
- Investor accreditation tracking
- Commitment tracking

### SKILL-141: Deal Analyzer

**Core Questions**:
1. What due diligence is performed on acquisitions?
2. How to underwrite a deal quickly (back-of-envelope)?
3. What financial metrics are evaluated (purchase price per unit, per SF)?
4. How to compare multiple deals side-by-side?
5. What red flags should be automatically detected?
6. How to integrate with property data sources?
7. What's included in investment memos?

**Technical Requirements**:
- Quick deal screening inputs
- Side-by-side deal comparison
- Investment memo generation
- Pipeline tracking (LOI, DD, closing)
- Integration with valuation/projection tools

---

## 🏢 COMPETITOR RESEARCH

### Primary Competitors to Analyze

| Company | Product | Strengths to Study |
|---------|---------|-------------------|
| **AppFolio Investment Management** | Investment tracking | Portfolio dashboards, investor portal |
| **Juniper Square** | GP/LP platform | Waterfall modeling, capital tracking |
| **RealPage IMS** | Investment management | Portfolio analytics, benchmarking |
| **ARGUS Enterprise** | Valuation modeling | Cash flow projections, DCF |
| **CoStar** | Market data | Cap rates, valuations |
| **Stessa** | Portfolio tracking | Free portfolio dashboard |
| **DealMachine** | Deal finding | Deal analyzer, comparables |
| **RCM** | Back-office | Fund accounting, waterfalls |

### Key Research Sources

1. **AppFolio Investment Management**
   - https://www.appfolio.com/investment-management
   - Feature documentation
   - Investor portal demos

2. **Juniper Square**
   - https://www.junipersquare.com/
   - Waterfall documentation
   - GP/LP workflow guides

3. **ARGUS**
   - https://www.altus.com/argus/
   - DCF modeling best practices
   - Cash flow projection methodology

4. **Industry Standards**
   - NCREIF reporting standards
   - ILPA fee reporting template
   - INREV guidelines (Europe)

---

## 🏗️ ARCHITECTURE ALIGNMENT

### Citadel OS Layer Mapping

| Component | Layer | Implementation |
|-----------|-------|----------------|
| Investment Dashboards | Layer 6: Applications | React + TypeScript |
| Investment Bundle | Layer 5: Domain Bundles | Investment domain |
| Investment Skills | Layer 4: Skills Layer | SKILL.md files |
| Calculation Engines | Layer 3: Hot Path | FastAPI |
| Financial Calculations | Layer 2: Cold Path | Python + TigerBeetle |
| Data Storage | Layer 1: Infrastructure | PostgreSQL + TigerBeetle |

### Required MCP Servers

```yaml
mcp_servers:
  - mcp://investment/valuation      # Property valuation
  - mcp://investment/metrics        # IRR, CoC calculations
  - mcp://investment/waterfall      # Distribution modeling
  - mcp://treasury-read             # Financial data
  - mcp://treasury-write            # Investment transactions
  - mcp://integration/mls           # MLS data access
  - mcp://integration/costar        # Market data
```

### Technology Stack Constraints

- **Backend**: Python 3.12+ (FastAPI, NumPy, Pandas)
- **Financial Calculations**: TigerBeetle for ledger
- **ML Models**: scikit-learn, XGBoost for valuations
- **Frontend**: React 19 + TypeScript
- **Database**: PostgreSQL (investment data), TigerBeetle (transactions)
- **Caching**: Redis for market data
- **Container**: AWS ECS/Fargate

---

## 📊 OUTPUT FORMAT REQUIREMENTS

### Document Structure

```markdown
# Engineering Specification: Investment Management Platform

## 1. Executive Summary
## 2. Skills Overview
## 3. Technical Architecture
## 4. Detailed Skill Specifications
   - For each skill:
     - Purpose and business value
     - Technical implementation (code examples)
     - API endpoints
     - Data models
     - Integration requirements
## 5. Database Schema
## 6. Performance Requirements
## 7. Security Considerations
## 8. Testing Strategy
## 9. Implementation Roadmap
```

### Code Example Format

```python
# Include working code examples for:
# - IRR calculation
# - Waterfall distribution logic
# - Valuation model
# - Cash flow projection engine
```

---

## ✅ QUALITY CHECKLIST

Before submitting, verify:

- [ ] All 10 skills have detailed specifications
- [ ] Code examples provided for calculations (IRR, waterfall, valuation)
- [ ] Data models defined for all entities
- [ ] API endpoints documented
- [ ] Integration with TigerBeetle specified
- [ ] Security for investor data addressed
- [ ] Performance requirements stated
- [ ] UI/UX considerations for dashboards
- [ ] Export formats documented (PDF, Excel)
- [ ] Compliance requirements addressed (SEC, accreditation)

---

## 📚 ADDITIONAL RESEARCH AREAS

1. **SEC Compliance**: Regulation D, accredited investor verification
2. **Tax Considerations**: Depreciation schedules, capital gains, K-1 generation
3. **Benchmarking**: NCREIF, ODCE, public REIT comparisons
4. **International**: Different IRR standards, currency handling
5. **Integration**: QuickBooks, Yardi, property management sync

---

**Expected Output**: A comprehensive engineering specification document of 2,000-3,000 lines covering all 10 investment management skills with production-ready technical details.

