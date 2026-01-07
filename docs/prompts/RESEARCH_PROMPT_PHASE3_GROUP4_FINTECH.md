# Research Prompt: Phase 3 Group 4 - Advanced Fintech & Crypto

> **Target Agent**: AI Research Analyst
> **Output Location**: `knowledge/fintech/KD-PHASE3-G4-advanced-fintech.md`
> **Skills to Research**: SKILL-158 through SKILL-167 (10 skills)
> **Priority**: P3 (Advanced)
> **Estimated Research Time**: 8-10 hours

---

## 🎯 RESEARCH OBJECTIVE

Research and document comprehensive engineering specifications for **Advanced Fintech & Crypto** capabilities that enable property managers and residents to leverage blockchain technology, stablecoins, DeFi protocols, and advanced treasury management for real estate operations.

**Note**: This is a highly specialized domain requiring deep knowledge of both traditional finance AND blockchain/crypto. This represents a key competitive moat for Citadel OS.

---

## 📋 SKILLS TO SPECIFY

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-158** | Stablecoin Rent Collection | Fintech | Accept USDC/USDT rent payments |
| **SKILL-159** | On-Chain Credit Scoring | Fintech | DeFi credit history integration |
| **SKILL-160** | Yield Optimization | Fintech | Idle fund investment automation |
| **SKILL-161** | International Wire Management | Fintech | Cross-border payment optimization |
| **SKILL-162** | Security Deposit DeFi | Fintech | Deposit in yield-bearing protocols |
| **SKILL-163** | Invoice Factoring | Fintech | Rent receivable financing |
| **SKILL-164** | Insurance Escrow | Fintech | Automated insurance premium collection |
| **SKILL-165** | Property Tokenization | Fintech | Fractional ownership tokens |
| **SKILL-166** | Multi-Currency Accounting | Fintech | Full multi-currency ledger |
| **SKILL-167** | Tax Withholding Automation | Fintech | Automated 1099/W-9 management |

---

## 🔍 RESEARCH QUESTIONS BY SKILL

### SKILL-158: Stablecoin Rent Collection

**Core Questions**:
1. What stablecoins are best suited for rent payments (USDC, USDT, DAI)?
2. How do crypto payment processors work (Circle, BitPay, Coinbase Commerce)?
3. What's the typical flow for stablecoin → fiat conversion?
4. How to handle gas fees (who pays, how to optimize)?
5. What wallet infrastructure is needed (custodial vs. non-custodial)?
6. How to generate payment requests (QR codes, payment links)?
7. What's the settlement time for stablecoin payments?
8. How to handle partial payments and overpayments?
9. What compliance requirements exist (KYC/AML for crypto)?

**Technical Requirements**:
- Multi-chain support (Ethereum, Polygon, Solana)
- Payment request generation
- Real-time balance checking
- Automatic fiat conversion option
- Transaction reconciliation
- Tax reporting for crypto receipts

**Regulatory Considerations**:
- FinCEN guidance on virtual currency
- State money transmitter licenses
- IRS reporting (Form 1099-K)
- SPSAV compliance (Brazil)

### SKILL-159: On-Chain Credit Scoring

**Core Questions**:
1. What on-chain data can indicate creditworthiness?
   - Wallet age and activity
   - DeFi loan repayment history
   - NFT holdings (proof of assets)
   - DAO participation
   - Transaction patterns
2. How do platforms like Spectral, Credora, and Masa work?
3. What's the correlation between on-chain behavior and credit risk?
4. How to combine on-chain + traditional credit data?
5. How to handle wallet address verification (proof of ownership)?
6. What privacy-preserving techniques exist (ZK proofs)?
7. How to prevent Sybil attacks (fake wallets)?

**Technical Requirements**:
- Multi-chain wallet analysis (EVM, Solana)
- DeFi protocol history aggregation
- Wallet ownership verification (signature challenge)
- Score calculation model
- Privacy-preserving data handling
- Integration with traditional screening

### SKILL-160: Yield Optimization

**Core Questions**:
1. What yield sources are appropriate for property management funds?
   - Money market funds (Sweep accounts)
   - Treasury bills
   - High-yield savings accounts
   - DeFi protocols (if risk-appropriate)
2. How do treasury management platforms (Ramp, Brex Treasury) optimize yield?
3. What DeFi yield protocols exist?
   - Aave, Compound (lending)
   - Curve, Uniswap (LP)
   - Yearn, Beefy (aggregators)
4. How to balance yield vs. liquidity requirements?
5. What risk controls are needed for DeFi exposure?
6. How to handle yield accounting (accrual, recognition)?
7. What regulatory considerations exist for investing customer funds?

**Technical Requirements**:
- Multi-protocol integration
- Risk scoring for yield sources
- Liquidity forecasting
- Automatic rebalancing
- Yield tracking and reporting
- Compliance with fiduciary duties

### SKILL-161: International Wire Management

**Core Questions**:
1. What are the main international wire networks (SWIFT, SEPA, ACH Global)?
2. How do platforms like Wise, OFX, and Airwallex optimize cross-border payments?
3. What are typical FX spreads and how to minimize them?
4. How to handle currency hedging for recurring payments?
5. What compliance requirements exist (OFAC, sanctions)?
6. How to optimize for speed vs. cost?
7. What documentation is needed for international transfers?
8. How to handle IOF tax (Brazil) and other country-specific taxes?

**Technical Requirements**:
- Multi-corridor support
- FX rate comparison engine
- Payment routing optimization
- Compliance screening (sanctions, AML)
- Currency hedging tools
- Beneficiary management

### SKILL-162: Security Deposit DeFi

**Core Questions**:
1. What are the legal requirements for security deposit handling by state?
2. How can security deposits earn yield for tenants?
3. What DeFi protocols are safe enough for security deposits?
   - Overcollateralized stablecoin deposits
   - Tokenized T-bills (Ondo, Backed)
4. How to handle interest allocation (landlord vs. tenant)?
5. What smart contract architecture ensures deposit return?
6. How to handle deposit disputes in a DeFi context?
7. What insurance/protection exists for DeFi deposits?

**Technical Requirements**:
- Smart contract for deposit custody
- Yield integration with low-risk protocols
- Interest calculation and distribution
- Withdrawal/return automation
- Dispute handling workflow
- Audit trail for regulatory compliance

### SKILL-163: Invoice Factoring

**Core Questions**:
1. How does invoice factoring/AR financing work?
2. What platforms offer rent receivable financing (Fundbox, BlueVine)?
3. What's the typical advance rate (80-90% of invoice)?
4. How are fees structured (discount rate, factor fee)?
5. What underwriting criteria apply to rent receivables?
6. How to handle non-payment and collections?
7. What's the difference between factoring and invoice financing?
8. How to integrate with existing payment collection?

**Technical Requirements**:
- Receivable eligibility analysis
- Factoring partner integration
- Advance disbursement workflow
- Fee calculation and tracking
- Collection status synchronization
- Reconciliation with payments

### SKILL-164: Insurance Escrow

**Core Questions**:
1. How do insurance escrow accounts work in property management?
2. What insurance types are typically escrowed (liability, property, renters)?
3. How to automate premium collection and payment?
4. What compliance requirements exist for escrow accounts?
5. How to handle policy renewals and changes?
6. What integration with insurance providers is needed?
7. How to track proof of insurance?

**Technical Requirements**:
- Escrow account management
- Premium calculation and collection
- Payment disbursement to insurers
- Policy tracking and renewal alerts
- Proof of insurance verification
- Reconciliation and reporting

### SKILL-165: Property Tokenization

**Core Questions**:
1. What is real estate tokenization?
2. How do platforms like RealT, Lofty, and Securitize work?
3. What legal structures enable tokenization (REITs, LLCs, SPVs)?
4. What blockchain standards apply (ERC-20, ERC-1404, ERC-3643)?
5. How are dividends/distributions handled on-chain?
6. What secondary market liquidity exists?
7. What accreditation requirements apply (Reg D, Reg A+)?
8. How to handle voting rights for tokenholders?

**Technical Requirements**:
- Token issuance platform
- Investor accreditation verification
- Dividend distribution smart contracts
- Transfer restriction logic (compliance)
- Cap table management
- Secondary market integration
- Regulatory reporting

### SKILL-166: Multi-Currency Accounting

**Core Questions**:
1. How to handle multi-currency in double-entry accounting?
2. What are functional currency vs. reporting currency?
3. How to handle FX gains/losses (realized vs. unrealized)?
4. What exchange rate sources are reliable (ECB, XE, OANDA)?
5. How to handle crypto as a currency/asset?
6. What's the treatment of stablecoins in accounting?
7. How to consolidate multi-currency entities?
8. What regulatory reporting requires currency translation?

**Technical Requirements**:
- Multi-currency chart of accounts
- Real-time FX rate integration
- Transaction date vs. settlement date handling
- FX gain/loss calculation
- Currency revaluation workflows
- Consolidated reporting
- Crypto asset accounting (FASB guidelines)

### SKILL-167: Tax Withholding Automation

**Core Questions**:
1. What tax forms are needed for property management?
   - 1099-MISC (rent payments to owners)
   - 1099-NEC (vendor payments)
   - 1099-K (payment processing)
   - W-9 collection
2. How to determine withholding requirements?
3. How to handle backup withholding?
4. What TIN verification is required?
5. How to automate 1099 generation and filing?
6. What state-specific requirements exist?
7. How to handle international payees (W-8BEN)?
8. What e-filing requirements apply?

**Technical Requirements**:
- TIN validation (IRS TIN Matching)
- W-9/W-8 collection workflow
- Threshold tracking for 1099 generation
- 1099 generation and e-filing
- Backup withholding calculation
- State 1099 filing
- Audit trail and compliance reporting

---

## 🏢 COMPETITOR RESEARCH

### Primary Competitors to Analyze

| Company | Product | Strengths to Study |
|---------|---------|-------------------|
| **Circle** | USDC, payments | Stablecoin infrastructure |
| **Coinbase Commerce** | Crypto payments | Payment processing |
| **Spectral Finance** | On-chain credit | Credit scoring |
| **Ramp Treasury** | Yield optimization | Corporate treasury |
| **Wise Business** | International payments | FX optimization |
| **RealT** | Real estate tokens | Property tokenization |
| **Securitize** | Security tokens | Compliance framework |
| **Fundbox** | Invoice factoring | AR financing |
| **Ondo Finance** | Tokenized treasuries | DeFi yield |
| **Fireblocks** | Custody | MPC wallets |

### Key Research Sources

1. **Circle/USDC**
   - https://www.circle.com/
   - USDC documentation
   - Payment APIs

2. **Spectral Finance**
   - https://www.spectral.finance/
   - MACRO Score methodology
   - On-chain credit scoring

3. **RealT**
   - https://realt.co/
   - Tokenization structure
   - Secondary market

4. **Ondo Finance**
   - https://ondo.finance/
   - Tokenized T-bills
   - Institutional DeFi

5. **Regulatory Guidance**
   - SEC guidance on digital assets
   - FinCEN virtual currency guidance
   - IRS cryptocurrency tax guidance
   - Brazil SPSAV framework

---

## 🏗️ ARCHITECTURE ALIGNMENT

### Citadel OS Layer Mapping

| Component | Layer | Implementation |
|-----------|-------|----------------|
| Fintech Dashboards | Layer 6: Applications | React + TypeScript |
| Fintech Bundle | Layer 5: Domain Bundles | Fintech domain |
| Fintech Skills | Layer 4: Skills Layer | SKILL.md files |
| Crypto APIs | Layer 3: Hot Path | FastAPI |
| Financial Calculations | Layer 2: Cold Path | TigerBeetle + Formance |
| Data Storage | Layer 1: Infrastructure | PostgreSQL + TigerBeetle |

### Required MCP Servers

```yaml
mcp_servers:
  # Core Treasury
  - mcp://treasury-read              # Financial data
  - mcp://treasury-write             # Transactions
  
  # Crypto
  - mcp://crypto/custody             # Fireblocks custody
  - mcp://crypto/payments            # Stablecoin payments
  - mcp://crypto/yield               # DeFi yield protocols
  
  # International
  - mcp://fx/rates                   # Exchange rates
  - mcp://fx/transfers               # Wire transfers
  
  # Tokenization
  - mcp://tokenization/issue         # Token issuance
  - mcp://tokenization/distributions # Dividend distribution
  
  # Tax
  - mcp://tax/withholding            # 1099 processing
  - mcp://tax/reporting              # Tax reporting
```

### Technology Stack Constraints

- **Backend**: Python 3.12+ (FastAPI), Rust (TigerBeetle)
- **Blockchain**: ethers.js, web3.py, viem
- **Custody**: Fireblocks MPC (already selected)
- **Database**: TigerBeetle (financial), PostgreSQL (metadata)
- **Smart Contracts**: Solidity (EVM), Rust (Solana if needed)
- **Compliance**: Chainalysis, Elliptic for AML
- **Container**: AWS ECS/Fargate

### Existing Infrastructure to Leverage

**From Treasury OS (Already Built)**:
- TigerBeetle high-throughput ledger (1M+ TPS)
- Formance bank-grade accounting
- Temporal for workflow orchestration
- Fireblocks MPC custody (selected)

---

## 📊 OUTPUT FORMAT REQUIREMENTS

### Document Structure

```markdown
# Engineering Specification: Advanced Fintech & Crypto Platform

## 1. Executive Summary
## 2. Skills Overview
## 3. Technical Architecture
## 4. Detailed Skill Specifications
   - For each skill:
     - Purpose and business value
     - Technical implementation
     - Blockchain/protocol specifics
     - API endpoints
     - Smart contract architecture (where applicable)
     - Regulatory considerations
## 5. Database Schema
## 6. Security Requirements
## 7. Compliance Framework
## 8. Risk Management
## 9. Testing Strategy
## 10. Implementation Roadmap
```

### Code Example Format

```python
# Include working code examples for:
# - Stablecoin payment processing
# - On-chain credit score calculation
# - Multi-currency accounting entries
# - 1099 generation logic
```

```solidity
// Include smart contract examples for:
// - Security deposit escrow
// - Token distribution
```

---

## ✅ QUALITY CHECKLIST

Before submitting, verify:

- [ ] All 10 skills have detailed specifications
- [ ] Blockchain integration architecture defined
- [ ] Smart contract specifications (where needed)
- [ ] Custody and security model documented
- [ ] Regulatory compliance framework comprehensive
- [ ] Multi-chain support addressed
- [ ] Gas fee optimization strategies
- [ ] Integration with existing Treasury OS
- [ ] Risk management controls specified
- [ ] Tax reporting requirements covered

---

## 📚 ADDITIONAL RESEARCH AREAS

1. **Regulatory Landscape**
   - SEC digital asset framework
   - FinCEN virtual currency rules
   - State money transmitter requirements
   - Brazil SPSAV (Law 14.478/2022)
   - EU MiCA regulation

2. **Custody & Security**
   - MPC vs. multi-sig wallets
   - Insurance for digital assets
   - Cold storage requirements
   - Key management best practices

3. **DeFi Risks**
   - Smart contract risk
   - Protocol risk (hacks, exploits)
   - Liquidity risk
   - Regulatory risk

4. **Accounting Standards**
   - FASB ASC 350 (intangible assets for crypto)
   - Fair value measurement
   - Impairment testing

---

## ⚠️ COMPLIANCE CRITICAL

This domain has the MOST complex regulatory requirements:

1. **Money Transmission**
   - Federal requirements (FinCEN)
   - State-by-state licensing
   - BitLicense (New York)

2. **Securities Laws**
   - Token classification (Howey test)
   - Reg D, Reg A+, Reg S compliance
   - Accredited investor verification

3. **Tax Reporting**
   - Crypto as property (IRS)
   - Cost basis tracking
   - 1099-B requirements

4. **International**
   - FATF travel rule
   - Country-specific restrictions
   - Sanctions compliance (OFAC)

5. **Brazil Specific**
   - SPSAV (BCB resolutions 517-521)
   - IOF tax on FX operations
   - LGPD data protection

**All specifications must include comprehensive compliance controls.**

---

## 🔐 SECURITY CRITICAL

This domain handles high-value financial assets:

1. **Custody Security**
   - MPC wallet architecture
   - Key ceremony procedures
   - Insurance requirements

2. **Smart Contract Security**
   - Audit requirements
   - Upgrade patterns
   - Emergency pause mechanisms

3. **Access Control**
   - Multi-signature approvals
   - Time-locked transactions
   - Withdrawal limits

4. **Monitoring**
   - Real-time anomaly detection
   - Transaction monitoring
   - AML screening

---

**Expected Output**: A comprehensive engineering specification document of 2,500-3,500 lines covering all 10 advanced fintech skills with production-ready technical details, smart contract architecture, and comprehensive compliance framework.

