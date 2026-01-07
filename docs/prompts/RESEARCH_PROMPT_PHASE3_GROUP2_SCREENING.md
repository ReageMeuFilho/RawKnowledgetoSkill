# Research Prompt: Phase 3 Group 2 - Tenant Screening & Lease Intelligence

> **Target Agent**: AI Research Analyst
> **Output Location**: `knowledge/screening/KD-PHASE3-G2-tenant-screening.md`
> **Skills to Research**: SKILL-142 through SKILL-149 (8 skills)
> **Priority**: P3 (Advanced)
> **Estimated Research Time**: 6-8 hours

---

## 🎯 RESEARCH OBJECTIVE

Research and document comprehensive engineering specifications for **Tenant Screening & Lease Intelligence** capabilities that enable property managers to make better tenant selection decisions, detect fraud, and intelligently manage lease lifecycles.

---

## 📋 SKILLS TO SPECIFY

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-142** | AI Tenant Scoring | Screening | ML-based tenant creditworthiness prediction |
| **SKILL-143** | Fraud Detection | Screening | Fake document and identity verification |
| **SKILL-144** | Lease Abstraction AI | Screening | Auto-extract terms from uploaded leases |
| **SKILL-145** | Renewal Prediction | Screening | Predict tenant renewal probability |
| **SKILL-146** | Rent Affordability Analysis | Screening | Income-to-rent ratio calculation |
| **SKILL-147** | Background Check Orchestration | Screening | Multi-vendor screening aggregation |
| **SKILL-148** | Eviction Risk Scoring | Screening | Predictive eviction risk assessment |
| **SKILL-149** | Reference Check Automation | Screening | AI-powered reference verification |

---

## 🔍 RESEARCH QUESTIONS BY SKILL

### SKILL-142: AI Tenant Scoring

**Core Questions**:
1. How do traditional tenant screening scores (FICO, VantageScore) work?
2. What alternative data can improve tenant scoring?
   - Rent payment history (through services like Experian RentBureau)
   - Utility payment history
   - Bank account cash flow analysis
   - Employment verification data
3. How do platforms like Naborly, Rentler, and SmartMove score tenants?
4. What ML models are used for credit risk scoring?
5. How to ensure Fair Housing Act compliance in scoring?
6. What's the correlation between credit score and rent payment behavior?
7. How to handle thin-file applicants (no credit history)?
8. What features are most predictive of tenant quality?

**Technical Requirements**:
- ML model selection (logistic regression, XGBoost, neural nets)
- Feature engineering for tenant data
- Model explainability (SHAP values)
- Fair lending compliance testing
- Score calibration and validation

### SKILL-143: Fraud Detection

**Core Questions**:
1. What types of rental application fraud exist?
   - Fake pay stubs (altered PDFs)
   - Synthetic identity fraud
   - Fake employment verification
   - Altered bank statements
   - Stolen identity
2. How do services like Snappt detect fake documents?
3. What image analysis techniques detect document tampering?
4. How to verify identity with government ID verification?
5. What are KYC (Know Your Customer) best practices?
6. How to detect synthetic identities?
7. What red flags indicate potential fraud?
8. What's the false positive rate for fraud detection?

**Technical Requirements**:
- Document analysis (OCR + metadata inspection)
- Image forensics (manipulation detection)
- Identity verification API integration (Plaid, Socure, Persona)
- Fraud scoring model
- Real-time verification workflow

### SKILL-144: Lease Abstraction AI

**Core Questions**:
1. What key terms need to be extracted from leases?
   - Lease dates (start, end, renewal)
   - Rent amount and escalations
   - Security deposit
   - Pet policies
   - Utilities included
   - Early termination clauses
   - Maintenance responsibilities
2. How do legal AI platforms (Kira, Luminance) perform lease abstraction?
3. What NLP techniques work best for legal documents?
4. How to handle non-standard lease formats?
5. What accuracy rates are achievable?
6. How to handle multi-page leases and addenda?
7. What's the human review workflow for extracted data?

**Technical Requirements**:
- Document classification (lease type identification)
- Named Entity Recognition (NER) for lease terms
- Table extraction (rent schedules)
- Confidence scoring for extracted fields
- Human-in-the-loop validation interface

### SKILL-145: Renewal Prediction

**Core Questions**:
1. What factors predict tenant renewal?
   - Payment history
   - Maintenance request patterns
   - Communication sentiment
   - Lease term length
   - Local market rent trends
   - Life events (job changes, family changes)
2. What ML models predict churn/renewal?
3. How early can renewal probability be predicted?
4. What's the typical baseline renewal rate by market?
5. How to incorporate tenant surveys/feedback?
6. What retention interventions work best?
7. How to prioritize renewal outreach?

**Technical Requirements**:
- Feature engineering from tenant behavior
- Time-series prediction model
- Probability calibration
- Actionable recommendations generation
- Integration with communication system for outreach

### SKILL-146: Rent Affordability Analysis

**Core Questions**:
1. What is the standard rent-to-income ratio (typically 30% gross)?
2. How do property managers verify income?
   - Pay stubs
   - Tax returns
   - Bank statements
   - Employment letters
3. How to handle variable income (self-employed, gig workers)?
4. What debt-to-income considerations apply?
5. How do housing subsidy programs (Section 8) affect calculations?
6. What alternative affordability metrics exist?
7. How to handle co-signers/guarantors?

**Technical Requirements**:
- Income verification API integration (Plaid, Argyle)
- Income calculation engine (annualize various pay periods)
- DTI calculation including known debts
- Affordability scoring with multiple thresholds
- Co-signer/guarantor handling logic

### SKILL-147: Background Check Orchestration

**Core Questions**:
1. What background check components are typically included?
   - Credit check
   - Criminal background
   - Eviction history
   - Employment verification
   - Rental history/reference check
2. What are the major screening providers?
   - TransUnion SmartMove
   - Experian RentBureau
   - CoreLogic/SafeRent
   - RentPrep
   - First Advantage
3. How to aggregate results from multiple vendors?
4. What FCRA compliance requirements exist?
5. How to handle adverse action notices?
6. What state-specific regulations affect screening?
7. How to optimize for speed vs. comprehensiveness?

**Technical Requirements**:
- Multi-vendor API integration
- Result normalization across providers
- FCRA-compliant workflows
- Adverse action letter generation
- State/local law compliance engine
- Cost optimization (which checks to run when)

### SKILL-148: Eviction Risk Scoring

**Core Questions**:
1. What factors predict eviction risk?
   - Prior evictions
   - Credit delinquencies
   - Criminal history patterns
   - Income stability
   - Employment history gaps
2. How do platforms like Naborly predict eviction likelihood?
3. What ML models work best for eviction prediction?
4. How to balance risk assessment with Fair Housing?
5. What early warning signals during tenancy indicate risk?
6. How to handle jurisdictions with eviction record restrictions?
7. What's the cost of eviction (legal, vacancy, turnover)?

**Technical Requirements**:
- Risk scoring model with historical eviction data
- Feature importance for explainability
- Early warning system during tenancy
- Integration with payment monitoring
- Intervention recommendation engine

### SKILL-149: Reference Check Automation

**Core Questions**:
1. What questions are asked in landlord reference checks?
   - Rent payment history
   - Lease violations
   - Property condition
   - Noise complaints
   - Would you rent to them again?
2. How to automate outreach to previous landlords?
3. What verification prevents fake references?
4. How to handle unresponsive references?
5. What employer verification is needed?
6. How to detect fraudulent reference phone numbers?
7. What's the typical reference check completion rate?

**Technical Requirements**:
- Automated email/SMS outreach
- Online reference submission portal
- Phone verification for reference numbers
- Sentiment analysis of reference responses
- Follow-up automation
- Reference fraud detection

---

## 🏢 COMPETITOR RESEARCH

### Primary Competitors to Analyze

| Company | Product | Strengths to Study |
|---------|---------|-------------------|
| **Naborly** | AI tenant screening | ML scoring, fraud detection |
| **Snappt** | Fraud detection | Document verification |
| **TransUnion SmartMove** | Background checks | Credit + criminal + eviction |
| **Plaid** | Income verification | Bank data, payroll |
| **Persona** | Identity verification | KYC, ID verification |
| **RentPrep** | Screening | FCRA compliance |
| **Findigs** | Modern screening | Applicant experience |
| **Kira Systems** | Lease abstraction | Legal AI |

### Key Research Sources

1. **Naborly**
   - https://www.naborly.com/
   - ML scoring methodology
   - Risk assessment approach

2. **Snappt**
   - https://www.snappt.com/
   - Document fraud detection
   - Income verification

3. **TransUnion SmartMove**
   - https://www.mysmartmove.com/
   - Credit report integration
   - Criminal/eviction databases

4. **Plaid**
   - https://plaid.com/
   - Income verification APIs
   - Bank data integration

5. **Industry Standards**
   - FCRA (Fair Credit Reporting Act)
   - Fair Housing Act
   - State screening laws (California, New York restrictions)

---

## 🏗️ ARCHITECTURE ALIGNMENT

### Citadel OS Layer Mapping

| Component | Layer | Implementation |
|-----------|-------|----------------|
| Screening Dashboards | Layer 6: Applications | React + TypeScript |
| Screening Bundle | Layer 5: Domain Bundles | Screening domain |
| Screening Skills | Layer 4: Skills Layer | SKILL.md files |
| ML Scoring | Layer 3: Hot Path | FastAPI + ML models |
| Document Analysis | Layer 2: Cold Path | Python + OCR |
| Data Storage | Layer 1: Infrastructure | PostgreSQL |

### Required MCP Servers

```yaml
mcp_servers:
  - mcp://screening/score           # Tenant scoring
  - mcp://screening/verify          # Identity verification
  - mcp://screening/fraud           # Fraud detection
  - mcp://ai/document-analysis      # Lease abstraction
  - mcp://integration/plaid         # Income verification
  - mcp://integration/transunion    # Credit reports
  - mcp://communication/orchestrate # Reference outreach
```

### Technology Stack Constraints

- **Backend**: Python 3.12+ (FastAPI, scikit-learn)
- **ML Models**: XGBoost, LightGBM for scoring
- **Document AI**: Tesseract OCR, spaCy NER
- **Identity**: Persona, Socure, or Jumio API
- **Income**: Plaid, Argyle API
- **Database**: PostgreSQL (encrypted PII)
- **Container**: AWS ECS/Fargate
- **Security**: AES-256 encryption, FCRA compliance

---

## 📊 OUTPUT FORMAT REQUIREMENTS

### Document Structure

```markdown
# Engineering Specification: Tenant Screening & Lease Intelligence

## 1. Executive Summary
## 2. Skills Overview
## 3. Technical Architecture
## 4. Detailed Skill Specifications
   - For each skill:
     - Purpose and business value
     - Technical implementation
     - ML model specifications (where applicable)
     - API endpoints
     - Data models
     - Compliance requirements
## 5. Database Schema
## 6. Security & Privacy Requirements
## 7. Compliance Framework (FCRA, Fair Housing)
## 8. Testing Strategy
## 9. Implementation Roadmap
```

### Code Example Format

```python
# Include working code examples for:
# - Tenant scoring model
# - Document fraud detection
# - Income verification workflow
# - Lease term extraction
```

---

## ✅ QUALITY CHECKLIST

Before submitting, verify:

- [ ] All 8 skills have detailed specifications
- [ ] ML model architecture documented for scoring
- [ ] FCRA compliance workflow specified
- [ ] Fair Housing compliance addressed
- [ ] Document fraud detection techniques detailed
- [ ] API integrations documented (Plaid, TransUnion, etc.)
- [ ] Data encryption and privacy requirements
- [ ] State-specific regulation handling
- [ ] Adverse action letter automation
- [ ] Human-in-the-loop workflows defined

---

## 📚 ADDITIONAL RESEARCH AREAS

1. **FCRA Compliance**: Permissible purpose, adverse action, dispute handling
2. **Fair Housing**: Disparate impact testing, protected class considerations
3. **State Laws**: Ban-the-box, eviction record restrictions, source-of-income protections
4. **Privacy**: CCPA, state privacy laws, data retention
5. **Fraud Trends**: Latest synthetic identity and document fraud techniques
6. **Alternative Data**: Non-traditional credit data sources

---

## ⚠️ COMPLIANCE CRITICAL

This domain has significant legal and regulatory requirements:

1. **FCRA (Fair Credit Reporting Act)**
   - Consumer rights disclosure
   - Adverse action procedures
   - Dispute resolution
   - Data accuracy obligations

2. **Fair Housing Act**
   - No discrimination based on protected classes
   - Consistent screening criteria
   - Reasonable accommodations

3. **State/Local Laws**
   - California: Credit report restrictions, ban-the-box
   - New York: Source of income protections
   - Seattle: First-in-time screening
   - Many cities: Criminal history restrictions

**All specifications must include compliance safeguards.**

---

**Expected Output**: A comprehensive engineering specification document of 2,000-3,000 lines covering all 8 tenant screening skills with production-ready technical details and full compliance framework.

