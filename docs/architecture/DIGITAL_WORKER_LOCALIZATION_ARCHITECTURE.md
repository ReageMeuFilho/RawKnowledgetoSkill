# 🌍 Digital Worker Localization Architecture
## Multi-Dimensional Customization for Global Property Management

**Version**: 1.0
**Date**: January 2026
**Status**: Architecture Specification

---

## Executive Summary

The Digital Worker (AI Agent) must operate intelligently across multiple dimensions of variation:

| Dimension | Examples | Impact |
|-----------|----------|--------|
| **Geography** | Brazil, US, Italy, Spain | Laws, language, payment rails, culture |
| **Property Type** | STR, LTR, HOA/Condomínio, Commercial | Business rules, workflows, terminology |
| **User Role** | Property Manager, Landlord, Investor, HOA Board | Permissions, priorities, communication style |
| **Management Style** | DIY Landlord, Professional PM, Institutional | Automation level, approval workflows |

This document defines how skills, behaviors, and knowledge adapt automatically based on context.

---

## 1. The Multi-Dimensional Localization Matrix

### 1.1 Dimension Hierarchy

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                           DIGITAL WORKER LOCALIZATION MATRIX                                          │
├─────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                      │
│                              ┌──────────────────────────────────┐                                   │
│                              │     PLATFORM DEFAULTS            │                                   │
│                              │     (Base Skills Library)        │                                   │
│                              └────────────────┬─────────────────┘                                   │
│                                               │                                                      │
│                    ┌──────────────────────────┼──────────────────────────┐                          │
│                    ▼                          ▼                          ▼                          │
│   ┌────────────────────────┐  ┌────────────────────────┐  ┌────────────────────────┐               │
│   │  GEOGRAPHY LAYER       │  │  PROPERTY TYPE LAYER   │  │  USER ROLE LAYER       │               │
│   │  (Country/Region)      │  │  (Domain Vertical)     │  │  (Persona)             │               │
│   │                        │  │                        │  │                        │               │
│   │  🇧🇷 Brazil            │  │  🏠 STR (Short-Term)   │  │  👤 Property Manager   │               │
│   │  🇺🇸 United States     │  │  🏢 LTR (Long-Term)    │  │  🏠 DIY Landlord       │               │
│   │  🇮🇹 Italy             │  │  🏛️ HOA/Condomínio    │  │  💼 Investor           │               │
│   │  🇪🇸 Spain             │  │  🏗️ Commercial        │  │  📋 HOA Board Member   │               │
│   │  🇵🇹 Portugal          │  │  🏨 Hospitality       │  │  🔧 Maintenance Staff  │               │
│   │                        │  │                        │  │                        │               │
│   └────────────────────────┘  └────────────────────────┘  └────────────────────────┘               │
│                    │                          │                          │                          │
│                    └──────────────────────────┼──────────────────────────┘                          │
│                                               │                                                      │
│                                               ▼                                                      │
│                              ┌──────────────────────────────────┐                                   │
│                              │    INTERSECTION = CONTEXT        │                                   │
│                              │                                  │                                   │
│                              │  Example:                        │                                   │
│                              │  Brazil + HOA + Board Member     │                                   │
│                              │  = Brazilian Condomínio Síndico  │                                   │
│                              │                                  │                                   │
│                              │  Italy + STR + DIY Landlord      │                                   │
│                              │  = Italian Vacation Rental Owner │                                   │
│                              │                                  │                                   │
│                              └──────────────────────────────────┘                                   │
│                                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### 1.2 Context Resolution

When a Digital Worker activates for a task, the system resolves the context:

```python
# Context Resolution Example
class ContextResolver:
    """
    Resolves the full localization context for a Digital Worker task
    """
    
    def resolve(self, request: TaskRequest) -> LocalizationContext:
        # Step 1: Identify the property
        property = self.property_service.get(request.property_id)
        
        # Step 2: Build context from dimensions
        context = LocalizationContext(
            # Geography (from property address)
            country=property.country,           # "BR"
            region=property.region,             # "SP" (São Paulo)
            city=property.city,                 # "São Paulo"
            
            # Property Type (from property classification)
            domain=property.property_type,      # "hoa" | "str" | "ltr"
            sub_type=property.sub_type,         # "condominio_vertical"
            
            # User Role (from authenticated user)
            user_role=request.user.role,        # "sindico" | "owner" | "tenant"
            management_style=request.user.management_style,  # "professional" | "diy"
            
            # Organization context
            organization_id=request.user.org_id,
            organization_tier=request.user.org.tier,  # "enterprise" | "pro" | "starter"
        )
        
        return context
```

---

## 2. Skill Inheritance & Override System

### 2.1 Override Resolution Order

Skills are resolved using a cascade system where more specific configurations override less specific ones:

```
RESOLUTION ORDER (most specific wins):

1. Unit Override       → /config/properties/{id}/units/{unit_id}/skills/
2. Property Override   → /config/properties/{id}/skills/
3. Organization Override → /config/orgs/{org_id}/skills/
4. Domain × Country    → /localization/{country}/{domain}/skills/
5. Domain Global       → /domains/{domain}/skills/
6. Country Global      → /localization/{country}/skills/
7. Platform Default    → /global/skills/
```

### 2.2 Skill File Structure with Inheritance

```
citadel-skills/
│
├── /global/                                    # 🌍 PLATFORM DEFAULTS
│   ├── /communication/
│   │   └── /message-responder/SKILL.md        # Base message handling
│   ├── /finance/
│   │   └── /payment-processing/SKILL.md       # Base payment handling
│   └── /operations/
│       └── /maintenance-triage/SKILL.md       # Base maintenance
│
├── /domains/                                   # 🏢 PROPERTY TYPE OVERRIDES
│   │
│   ├── /str/                                   # Short-Term Rental
│   │   ├── /guest-communication/SKILL.md      # Guest (not tenant) messaging
│   │   ├── /dynamic-pricing/SKILL.md          # STR-specific pricing
│   │   └── /channel-sync/SKILL.md             # OTA management
│   │
│   ├── /ltr/                                   # Long-Term Rental
│   │   ├── /tenant-communication/SKILL.md     # Tenant messaging
│   │   ├── /lease-management/SKILL.md         # Lease lifecycle
│   │   └── /rent-collection/SKILL.md          # Monthly rent
│   │
│   └── /hoa/                                   # HOA/Condominium
│       ├── /resident-communication/SKILL.md   # Resident messaging
│       ├── /dues-collection/SKILL.md          # Monthly dues/taxas
│       ├── /violation-management/SKILL.md     # CC&R violations
│       └── /board-governance/SKILL.md         # Board voting/meetings
│
├── /localization/                              # 🌎 COUNTRY OVERRIDES
│   │
│   ├── /br/                                    # 🇧🇷 BRAZIL
│   │   │
│   │   ├── /payment-processing/SKILL.md       # PIX, Boleto, WhatsApp
│   │   ├── /communication/
│   │   │   └── /message-responder/SKILL.md    # pt-BR, informal tone
│   │   │
│   │   ├── /hoa/                              # 🇧🇷 Brazil + HOA = Condomínio
│   │   │   ├── /dues-collection/SKILL.md      # Taxa condominial, PIX
│   │   │   ├── /sindico-dashboard/SKILL.md    # Síndico-specific views
│   │   │   ├── /assembleia-management/SKILL.md # AGO/AGE rules
│   │   │   └── /portaria-integration/SKILL.md # Doorman/security integration
│   │   │
│   │   ├── /ltr/                              # 🇧🇷 Brazil + LTR = Aluguel
│   │   │   ├── /rent-collection/SKILL.md      # Lei do Inquilinato rules
│   │   │   ├── /iptu-management/SKILL.md      # IPTU tax handling
│   │   │   └── /caution-money/SKILL.md        # Caução (3 months)
│   │   │
│   │   └── /str/                              # 🇧🇷 Brazil + STR = Temporada
│   │       ├── /booking-management/SKILL.md   # Airbnb BR, Booking.com
│   │       └── /tax-nota-fiscal/SKILL.md      # Nota fiscal generation
│   │
│   ├── /us/                                    # 🇺🇸 UNITED STATES
│   │   │
│   │   ├── /payment-processing/SKILL.md       # ACH, Wire, Check
│   │   │
│   │   ├── /hoa/                              # 🇺🇸 US + HOA
│   │   │   ├── /dues-collection/SKILL.md      # Monthly HOA dues
│   │   │   ├── /cc-r-enforcement/SKILL.md     # CC&R violations
│   │   │   └── /arc-review/SKILL.md           # Architectural review
│   │   │
│   │   └── /ltr/                              # 🇺🇸 US + LTR
│   │       ├── /rent-collection/SKILL.md      # State-specific rules
│   │       ├── /security-deposit/SKILL.md     # State deposit limits
│   │       └── /eviction-process/SKILL.md     # State eviction laws
│   │
│   └── /it/                                    # 🇮🇹 ITALY
│       │
│       ├── /payment-processing/SKILL.md       # SEPA, Bonifico
│       │
│       ├── /str/                              # 🇮🇹 Italy + STR = Affitto Breve
│       │   ├── /cedolare-secca/SKILL.md       # 21% flat tax regime
│       │   ├── /questura-reporting/SKILL.md   # Police registration (Alloggiati Web)
│       │   └── /tourist-tax/SKILL.md          # Tassa di soggiorno
│       │
│       └── /ltr/                              # 🇮🇹 Italy + LTR
│           ├── /contratto-locazione/SKILL.md  # 4+4 contract rules
│           └── /imu-management/SKILL.md       # IMU property tax
│
└── /roles/                                     # 👤 USER ROLE OVERRIDES
    │
    ├── /sindico/                               # Brazilian HOA Manager (Síndico)
    │   └── /dashboard/SKILL.md                # Síndico-specific dashboard
    │
    ├── /diy-landlord/                          # Self-managing property owner
    │   └── /simplified-workflows/SKILL.md     # Streamlined processes
    │
    ├── /investor/                              # Portfolio-focused user
    │   └── /roi-dashboard/SKILL.md            # Investment metrics focus
    │
    └── /professional-pm/                       # Professional property manager
        └── /bulk-operations/SKILL.md          # Multi-property management
```

### 2.3 Skill Override Example: Rent Collection

**Base Skill** (`/global/finance/payment-processing/SKILL.md`):
```yaml
---
name: payment-processing
description: Process payments using configured rails
version: 1.0.0
---

# Payment Processing

## Supported Rails
- Credit Card (3% fee)
- Bank Transfer
- Wire Transfer

## Standard SLA
- Processing: 1-3 business days
- Notification: Email confirmation
```

**Brazil Override** (`/localization/br/payment-processing/SKILL.md`):
```yaml
---
name: payment-processing
description: Process payments using Brazilian rails (PIX primary)
extends: global/finance/payment-processing
version: 1.0.0-br
overrides:
  - supported_rails
  - notification_channel
  - sla
---

# Payment Processing (Brazil)

## Supported Rails (Priority Order)
1. **PIX** (instant, free) - PRIMARY
   - Generate QR code for amounts < R$5,000
   - Request key type: CPF, email, phone, random
   - Instant confirmation
2. **Boleto** (3-day settlement)
   - Generate for recurring monthly payments
   - Auto-send 5 days before due date
3. **Credit Card** (2.5% fee)
   - Fallback option only

## Communication
- Primary: WhatsApp (95% open rate in Brazil)
- Fallback: SMS
- Tone: Informal, emoji-friendly
- Language: pt-BR

## SLA
- PIX: Instant confirmation
- Boleto: 3 business days
- Notification: WhatsApp → SMS → Email
```

**Brazil + HOA Override** (`/localization/br/hoa/dues-collection/SKILL.md`):
```yaml
---
name: dues-collection
description: Collect monthly taxa condominial (HOA dues) in Brazil
extends: localization/br/payment-processing
version: 1.0.0-br-hoa
overrides:
  - terminology
  - default_amount_source
  - late_fee_rules
  - legal_references
---

# Taxa Condominial Collection (Brazil HOA)

## Terminology Mapping
| Global Term | Brazilian Term | Portuguese |
|-------------|----------------|------------|
| HOA Dues | Taxa Condominial | Taxa de condomínio |
| HOA | Condomínio | Condomínio |
| HOA Board | Conselho Deliberativo | Conselho |
| HOA Manager | Síndico | Síndico(a) |
| Monthly Assessment | Cota Condominial | Cota mensal |
| Special Assessment | Rateio Extra | Rateio extraordinário |
| Reserve Fund | Fundo de Reserva | Fundo de reserva |

## Amount Determination
- Source: Convenção do Condomínio (CC&R equivalent)
- Calculation: Fração ideal × Monthly budget
- Updates: Requires Assembleia approval

## Late Fee Rules (Art. 1.336 Código Civil)
- Grace period: 10 days after vencimento
- Late fee (multa): Maximum 2%
- Interest (juros): Maximum 1% per month
- Monetary correction: IGPM or IPCA index

## Default Communication Flow

### 5 Days Before Due Date
```
Olá {name}! 👋

Sua taxa condominial do mês de {month} vence em 5 dias:

💰 Valor: R$ {amount}
📅 Vencimento: {due_date}

Para pagar via PIX, use a chave:
🔑 {pix_key}

Ou escaneie o QR Code:
[QR_CODE]

Qualquer dúvida, estou aqui! 😊
```

### Due Date Reminder
```
Oi {name}! 

Hoje é o dia do vencimento da sua taxa condominial:

💰 R$ {amount}
📅 Vencimento: HOJE

Pague via PIX para confirmação instantânea!
🔑 {pix_key}

Lembrando: após 10 dias, incide multa de 2% + juros de 1% ao mês.
```

### 15 Days Past Due (First Collection)
```
{name}, tudo bem?

Identificamos que a taxa condominial de {month} está em aberto:

💰 Valor original: R$ {original_amount}
📅 Vencimento: {due_date}
⚠️ Multa (2%): R$ {late_fee}
📈 Juros: R$ {interest}
💵 Total atualizado: R$ {total_amount}

Podemos parcelar em até 3x sem juros adicionais!

Quer que eu gere um boleto ou PIX atualizado?
```

## Legal References
- Código Civil: Arts. 1.331 a 1.358
- Lei 4.591/1964 (Condomínios)
- Convenção do Condomínio específica

## Integration Points
- mcp://treasury/dues-collection (TigerBeetle ledger)
- mcp://whatsapp/send (Communication)
- mcp://pix/generate-qrcode (Payment)
- mcp://boleto/generate (Payment fallback)
```

---

## 3. Domain-Specific Configurations

### 3.1 Brazil HOA (Condomínio)

```yaml
# /config/domains/br/hoa/domain.yaml
---
domain_id: br-hoa
display_name: "Condomínio Brasileiro"
description: "Gestão de condomínios verticais e horizontais no Brasil"

# Terminology Override
terminology:
  property: "Unidade"
  owner: "Condômino"
  tenant: "Inquilino/Locatário"
  manager: "Síndico(a)"
  board: "Conselho Deliberativo"
  meeting: "Assembleia"
  annual_meeting: "AGO (Assembleia Geral Ordinária)"
  special_meeting: "AGE (Assembleia Geral Extraordinária)"
  dues: "Taxa Condominial"
  reserve_fund: "Fundo de Reserva"
  cc_r: "Convenção do Condomínio"
  rules: "Regimento Interno"
  violation: "Infração"
  fine: "Multa"

# Roles & Permissions
roles:
  sindico:
    display_name: "Síndico(a)"
    permissions:
      - manage_finances
      - approve_expenses_under_limit
      - manage_staff
      - manage_vendors
      - send_communications
      - view_all_units
      - manage_violations
    expense_approval_limit: 5000.00  # Above this needs Conselho approval
    
  conselheiro:
    display_name: "Conselheiro"
    permissions:
      - view_finances
      - approve_expenses
      - vote_on_budgets
      - audit_accounts
    
  condomino:
    display_name: "Condômino"
    permissions:
      - view_own_finances
      - pay_dues
      - submit_requests
      - vote_in_assembleia
      - view_common_areas
    
  inquilino:
    display_name: "Inquilino"
    permissions:
      - pay_dues  # If delegated
      - submit_maintenance
      - view_common_areas
      - access_portaria

# Financial Structure
financial:
  account_structure:
    - name: "Conta Corrente"
      type: operating
      required: true
    - name: "Fundo de Reserva"
      type: reserve
      required: true
      minimum_balance_months: 6
    - name: "Fundo de Obras"
      type: capital_improvement
      required: false
      
  payment_rails:
    primary: pix
    secondary: boleto
    fallback: credit_card
    
  late_fee_rules:
    grace_period_days: 10
    penalty_rate: 0.02  # 2% max by law
    interest_rate_monthly: 0.01  # 1% max by law
    monetary_correction: "IGPM"  # Or IPCA

# Compliance Requirements
compliance:
  required_meetings:
    - type: AGO
      frequency: annual
      quorum: 0.50  # First call
      quorum_second_call: 0.25  # Any number if less
      agenda_required:
        - "Aprovação de Contas"
        - "Previsão Orçamentária"
        - "Eleição de Síndico/Conselho"  # If applicable
        
  document_retention:
    financial_records: 5  # years
    meeting_minutes: permanent
    contracts: 10  # years after expiration
    
  required_insurance:
    - type: "Seguro Obrigatório"
      coverage: building_structure
      required: true

# Skill Mappings
enabled_skills:
  - dues-collection
  - assembleia-management
  - sindico-dashboard
  - violation-management
  - common-area-booking
  - portaria-integration
  - maintenance-triage
  - vendor-management
  - financial-reporting

disabled_skills:
  - dynamic-pricing  # Not applicable
  - guest-checkin    # Not applicable
  - channel-sync     # Not applicable
```

### 3.2 US Landlord (Self-Managing)

```yaml
# /config/domains/us/ltr/diy-landlord/domain.yaml
---
domain_id: us-ltr-diy
display_name: "US Self-Managing Landlord"
description: "Individual landlords managing their own properties in the US"

# Management Style
management_style: diy
automation_level: high  # Automate as much as possible
approval_workflows: minimal  # Owner approves most things directly

# Terminology
terminology:
  property: "Unit"
  owner: "Landlord"
  tenant: "Tenant"
  lease: "Lease Agreement"
  deposit: "Security Deposit"
  dues: "Rent"
  violation: "Lease Violation"
  eviction: "Eviction"

# Simplified Role (DIY = Owner does everything)
roles:
  owner:
    display_name: "Property Owner"
    permissions:
      - full_access
    expense_approval_limit: unlimited

# Financial Structure
financial:
  account_structure:
    - name: "Operating Account"
      type: operating
      required: true
    - name: "Security Deposit Trust"
      type: trust
      required: true  # Many states require separate account
      
  payment_rails:
    primary: ach
    secondary: credit_card
    fallback: check
    
  rent_collection:
    due_day: 1  # First of month
    grace_period_days: 5  # Varies by state
    late_fee_type: flat_or_percentage
    late_fee_max: state_specific  # CA: max 5-6%, NY: varies

# State-Specific Compliance (Example: California)
compliance:
  state: "CA"
  security_deposit:
    max_amount:
      unfurnished: 2  # months rent
      furnished: 3    # months rent
    return_deadline_days: 21
    itemized_deductions: required
    
  rent_increase:
    notice_days: 30  # <10% increase
    notice_days_large: 90  # >10% increase
    cap: 0.10  # 10% + CPI for rent control areas
    
  eviction:
    pay_or_quit_days: 3
    cure_or_quit_days: 3
    just_cause_required: true  # For rent-controlled

# DIY-Specific Features
diy_features:
  enabled:
    - auto_rent_reminders
    - auto_late_fee_calculation
    - tenant_screening_integration
    - maintenance_request_portal
    - expense_tracking
    - tax_report_generation
    - lease_template_library
    
  simplified_workflows:
    - one_click_rent_collection
    - auto_generate_1099
    - simple_expense_categorization
    
  learning_resources:
    - landlord_legal_guide
    - state_specific_forms
    - tax_deduction_tips

# Skill Mappings
enabled_skills:
  - rent-collection
  - security-deposit-management
  - tenant-screening
  - lease-management
  - maintenance-triage
  - expense-tracking
  - tax-reporting
  - tenant-communication
  - eviction-guidance

disabled_skills:
  - multi-property-dashboard  # Single property focus
  - staff-management          # No staff
  - bulk-operations           # Not needed
```

### 3.3 Italy STR (Affitto Breve)

```yaml
# /config/domains/it/str/domain.yaml
---
domain_id: it-str
display_name: "Affitto Breve (Italy STR)"
description: "Short-term vacation rental management in Italy"

# Terminology
terminology:
  property: "Immobile" / "Alloggio"
  owner: "Proprietario"
  guest: "Ospite"
  booking: "Prenotazione"
  check_in: "Check-in"
  check_out: "Check-out"
  deposit: "Caparra"
  cleaning_fee: "Spese di pulizia"
  tourist_tax: "Tassa di Soggiorno"

# Compliance Requirements (Critical for Italy)
compliance:
  police_registration:
    name: "Alloggiati Web"
    agency: "Questura"
    deadline_hours: 24  # Within 24 hours of check-in
    required_data:
      - document_type
      - document_number
      - nationality
      - date_of_birth
      - place_of_birth
      - citizenship
      - arrival_date
      - departure_date
    penalty_per_guest: 206.00  # EUR
    
  tourist_tax:
    name: "Tassa di Soggiorno"
    varies_by: municipality
    collection: at_checkout
    reporting: monthly
    example_rates:
      rome: 3.50  # EUR per night per person
      florence: 5.00
      venice: 5.00
      milan: 3.00
    max_nights: 10  # Usually capped at 10 nights
    exempt:
      - children_under_10
      - residents
      - hospitalized
      
  tax_regime:
    cedolare_secca:
      rate: 0.21  # 21% flat tax
      applicable_duration_days_max: 30
      requirements:
        - individual_owner  # Not companies
        - residential_property
        - no_additional_services  # No hotel-like services
        
    regime_ordinario:
      rate: progressive  # Based on income bracket
      applies_when:
        - company_ownership
        - stays_over_30_days
        - hotel_services_provided

# CIN (Codice Identificativo Nazionale) - Required from 2024
cin_requirement:
  required: true
  display_on: all_listings
  penalty_range:
    min: 800
    max: 8000
  renewal: annual

# OTA Integration
ota_integration:
  supported_channels:
    - airbnb
    - booking_com
    - vrbo
    - tripadvisor
    - casevacanza_it  # Italian platform
    
  required_info_per_listing:
    - cin_code
    - tourist_tax_rate
    - check_in_time
    - house_rules
    - wifi_details
    - emergency_contacts

# Financial
financial:
  payment_rails:
    primary: sepa
    secondary: credit_card
    
  pricing:
    currency: EUR
    include_tourist_tax: separate  # Must be shown separately
    
  withholding:
    ota_withholding: 0.21  # Airbnb/Booking withhold 21% for tax

# Skills for Italy STR
enabled_skills:
  - questura-reporting
  - tourist-tax-collection
  - cedolare-secca-management
  - cin-management
  - dynamic-pricing
  - guest-communication
  - channel-sync
  - cleaning-coordination
  - keyless-entry
  - local-guide-creation

# Italian-Specific Skills
italy_specific_skills:
  - name: questura-reporting
    description: "Automatic Alloggiati Web police registration"
    automation_level: full
    integrations:
      - alloggiati_web_api
      
  - name: tourist-tax-collection
    description: "Collect and report tassa di soggiorno"
    municipality_rates: dynamic  # Load per municipality
    
  - name: cedolare-secca-management
    description: "Track 21% flat tax obligations"
    generates:
      - f24_payment_forms
      - redditi_pf_data
```

---

## 4. Investment Management Localization

### 4.1 Investment Philosophy by Market

Different markets have fundamentally different approaches to real estate investment:

```yaml
# /config/investment/market-philosophies.yaml
---
markets:
  brazil:
    investment_philosophy:
      name: "Brazilian Real Estate Investment"
      key_metrics:
        - cap_rate  # Called "Taxa de Capitalização"
        - rental_yield  # "Rentabilidade do Aluguel"
        - valuation_appreciation  # "Valorização"
        - inflation_protection  # "Proteção contra Inflação"
      
      valuation_methods:
        primary: comparative_sales  # "Avaliação por Comparação"
        secondary: income_capitalization
        
      unique_factors:
        - igpm_indexation  # Rents indexed to inflation
        - high_interest_rates  # CDI/SELIC as benchmark
        - currency_risk  # BRL volatility
        
      benchmark_returns:
        cdi: "Reference rate (currently ~13%)"
        real_estate_fund: "FIIs average 8-12% yield"
        direct_ownership: "Target 0.5-0.8% monthly rent/value"
        
      tax_considerations:
        - itbi  # Transfer tax: 2-3%
        - iptu  # Annual property tax
        - ir_rental  # Income tax on rent: progressive
        - ir_sale  # Capital gains: 15-22.5%
        
      typical_investor_profile:
        - high_net_worth_individuals
        - family_offices
        - real_estate_funds  # FIIs
        
  united_states:
    investment_philosophy:
      name: "US Real Estate Investment"
      key_metrics:
        - cap_rate
        - cash_on_cash_return
        - irr  # Internal Rate of Return
        - dscr  # Debt Service Coverage Ratio
        - noi  # Net Operating Income
        
      valuation_methods:
        primary: income_approach  # NOI / Cap Rate
        secondary: sales_comparison
        tertiary: cost_approach
        
      unique_factors:
        - 1031_exchange  # Tax-deferred exchanges
        - depreciation_shield  # 27.5 years residential
        - leverage_friendly  # Low rates, easy financing
        - reit_structure  # Pass-through taxation
        
      benchmark_returns:
        sp500: "Historical ~10% annually"
        reit_index: "Historical ~9-11%"
        direct_multifamily: "Target 8-12% CoC"
        
      tax_considerations:
        - depreciation: 27.5  # years for residential
        - capital_gains: 0.20  # Federal long-term
        - state_taxes: varies
        - 1031_exchange: defer_capital_gains
        
      typical_investor_profile:
        - individual_investors
        - syndicates
        - reits
        - family_offices
        - institutional
        
  italy:
    investment_philosophy:
      name: "Italian Real Estate Investment"
      key_metrics:
        - rental_yield  # "Rendimento Locativo"
        - capital_appreciation
        - tax_efficiency  # Cedolare secca impact
        
      valuation_methods:
        primary: comparative_market  # "Valore di Mercato"
        secondary: income_approach
        
      unique_factors:
        - cedolare_secca  # 21% flat tax option
        - high_transaction_costs  # ~10% total
        - rent_control_legacy  # Old contracts
        - tourist_rental_opportunity
        
      benchmark_returns:
        btp: "Italian government bonds ~4%"
        direct_residential: "Target 3-5% gross yield"
        tourist_rental: "Target 6-10% gross yield"
        
      tax_considerations:
        - imposta_registro  # 9% purchase tax (or 2% first home)
        - notary_fees  # 1-2.5%
        - imu  # Annual property tax
        - cedolare_secca: 0.21  # Flat rental income tax
        - capital_gains: exempt_after_5_years
        
      typical_investor_profile:
        - italian_families
        - foreign_buyers
        - small_investors
```

### 4.2 Investment Dashboard Localization

```yaml
# /skills/investor/dashboard/SKILL.md
---
name: roi-dashboard
description: Investment performance dashboard localized by market
version: 1.0.0
localizations:
  - br
  - us
  - it
---

# Investment Dashboard

## Metric Display by Market

### Brazil Dashboard
```
┌────────────────────────────────────────────────────────────────────┐
│  📊 PAINEL DE INVESTIMENTOS - BRASIL                               │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│  RENTABILIDADE                                                     │
│  ┌────────────────────┐  ┌────────────────────┐                   │
│  │ Rent Yield Mensal  │  │ CDI Comparativo    │                   │
│  │ 0.65% a.m.         │  │ CDI: 13.25% a.a.   │                   │
│  │ (7.8% a.a.)        │  │ vs Imóvel: 7.8%    │                   │
│  └────────────────────┘  └────────────────────┘                   │
│                                                                    │
│  VALORIZAÇÃO                                                       │
│  ┌────────────────────────────────────────────┐                   │
│  │ Valor de Compra:    R$ 500.000             │                   │
│  │ Valor Atual:        R$ 580.000 (+16%)      │                   │
│  │ Correção IGPM:      +12.5%                 │                   │
│  │ Valorização Real:   +3.5%                  │                   │
│  └────────────────────────────────────────────┘                   │
│                                                                    │
│  PRÓXIMO REAJUSTE: 15/03/2026 (IGPM)                              │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

### US Dashboard
```
┌────────────────────────────────────────────────────────────────────┐
│  📊 INVESTMENT DASHBOARD - US                                      │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│  KEY METRICS                                                       │
│  ┌────────────────────┐  ┌────────────────────┐                   │
│  │ Cash-on-Cash       │  │ Cap Rate           │                   │
│  │ 8.2%               │  │ 5.5%               │                   │
│  └────────────────────┘  └────────────────────┘                   │
│                                                                    │
│  ┌────────────────────┐  ┌────────────────────┐                   │
│  │ IRR (5-yr proj)    │  │ DSCR               │                   │
│  │ 14.5%              │  │ 1.35x              │                   │
│  └────────────────────┘  └────────────────────┘                   │
│                                                                    │
│  TAX BENEFITS                                                      │
│  ┌────────────────────────────────────────────┐                   │
│  │ Depreciation Deduction:    $18,182/yr      │                   │
│  │ Tax Savings (24% bracket): $4,364/yr       │                   │
│  │ 1031 Exchange Available:   Yes ✓           │                   │
│  └────────────────────────────────────────────┘                   │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

### Italy Dashboard
```
┌────────────────────────────────────────────────────────────────────┐
│  📊 PANNELLO INVESTIMENTI - ITALIA                                 │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│  RENDIMENTO                                                        │
│  ┌────────────────────┐  ┌────────────────────┐                   │
│  │ Rendimento Lordo   │  │ Rendimento Netto   │                   │
│  │ 5.2%               │  │ 4.1% (ced. secca)  │                   │
│  └────────────────────┘  └────────────────────┘                   │
│                                                                    │
│  REGIME FISCALE: Cedolare Secca (21%)                             │
│  ┌────────────────────────────────────────────┐                   │
│  │ Canone Annuo:       €12.000                │                   │
│  │ Cedolare Secca:     €2.520 (21%)           │                   │
│  │ Netto Proprietario: €9.480                 │                   │
│  └────────────────────────────────────────────┘                   │
│                                                                    │
│  AFFITTO BREVE (Tourist Rental)                                   │
│  ┌────────────────────────────────────────────┐                   │
│  │ Occupancy:          72%                    │                   │
│  │ ADR:                €120/notte             │                   │
│  │ RevPAR:             €86/notte              │                   │
│  │ Tassa Soggiorno:    €480 collected         │                   │
│  └────────────────────────────────────────────┘                   │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```
```

---

## 5. Skill Context Injection

### 5.1 How Context Flows to Skills

```python
# Context injection into skill execution
class SkillExecutor:
    """
    Executes skills with full localization context
    """
    
    async def execute_skill(
        self, 
        skill_id: str, 
        task: str, 
        context: LocalizationContext
    ) -> SkillResult:
        
        # Step 1: Resolve skill file (with inheritance)
        skill_path = self.skill_resolver.resolve(
            skill_id=skill_id,
            country=context.country,
            domain=context.domain,
            role=context.user_role
        )
        
        # Step 2: Load skill definition
        skill = self.skill_loader.load(skill_path)
        
        # Step 3: Inject localization context into prompt
        system_prompt = self.build_system_prompt(skill, context)
        
        # Step 4: Add localized knowledge
        knowledge = await self.knowledge_service.retrieve(
            query=task,
            filters={
                "country": context.country,
                "domain": context.domain,
                "property_id": context.property_id
            }
        )
        
        # Step 5: Execute with localized MCP servers
        mcp_servers = self.get_localized_mcp_servers(context)
        
        result = await self.agent_runtime.execute(
            system_prompt=system_prompt,
            user_message=task,
            knowledge_context=knowledge,
            tools=mcp_servers,
            model_config=self.get_model_config(context)
        )
        
        return result
    
    def build_system_prompt(
        self, 
        skill: Skill, 
        context: LocalizationContext
    ) -> str:
        """
        Build system prompt with all localization context
        """
        return f"""
You are a Digital Worker specialized in {context.domain} property management 
in {context.country_name}.

## Your Role
{self.get_role_description(context.user_role)}

## Terminology
{self.get_terminology_mapping(context)}

## Communication Style
- Language: {context.language}
- Tone: {context.communication_tone}
- Preferred Channel: {context.preferred_channel}

## Local Rules
{self.get_local_rules(context)}

## Skill Instructions
{skill.instructions}

## Current Context
- Property: {context.property_name}
- User: {context.user_name} ({context.user_role})
- Timezone: {context.timezone}
"""
```

### 5.2 MCP Server Localization

Different markets connect to different payment rails, compliance systems, etc:

```yaml
# /mcp-servers/config/server-mapping.yaml
---
mcp_server_mapping:
  
  # Payment Processing
  payment:
    global: mcp://treasury/payment
    overrides:
      br:
        primary: mcp://pix/payment
        secondary: mcp://boleto/payment
        tertiary: mcp://treasury/payment
      us:
        primary: mcp://ach/payment
        secondary: mcp://stripe/payment
      it:
        primary: mcp://sepa/payment
        secondary: mcp://stripe/payment
      
  # Compliance Reporting
  compliance:
    global: mcp://audit/log
    overrides:
      br:
        - mcp://receita-federal/reporting
        - mcp://sped/fiscal
      it:
        - mcp://questura/alloggiati
        - mcp://agenzia-entrate/reporting
      us:
        - mcp://irs/1099-reporting
        
  # Communication
  communication:
    global: mcp://email/send
    overrides:
      br:
        primary: mcp://whatsapp/send
        fallback: mcp://sms/send
      us:
        primary: mcp://email/send
        fallback: mcp://sms/send
      it:
        primary: mcp://email/send
        fallback: mcp://whatsapp/send
```

---

## 6. Implementation: Adding a New Market

### 6.1 Checklist for New Market Launch

```markdown
## New Market Launch Checklist: [COUNTRY]

### Phase 1: Legal & Compliance Research
- [ ] Identify property law framework
- [ ] Document landlord/tenant regulations
- [ ] Identify tax obligations (rental income, capital gains)
- [ ] Document compliance requirements (registrations, reporting)
- [ ] Identify local payment rails

### Phase 2: Configuration
- [ ] Create `/localization/{country}/` directory
- [ ] Define `domain.yaml` for each property type (LTR, STR, HOA)
- [ ] Map terminology (local language)
- [ ] Configure payment rails
- [ ] Set up compliance integrations

### Phase 3: Skill Localization
- [ ] Override `payment-processing` skill
- [ ] Override `communication` skills (language, tone)
- [ ] Create country-specific skills (e.g., tax reporting)
- [ ] Translate all skill instructions
- [ ] Create local knowledge base

### Phase 4: MCP Server Integration
- [ ] Integrate local payment provider
- [ ] Integrate compliance APIs
- [ ] Configure local messaging (WhatsApp, SMS, etc.)

### Phase 5: Testing
- [ ] Test full user journey in local language
- [ ] Validate payment processing
- [ ] Validate compliance reporting
- [ ] User acceptance testing with local property managers

### Phase 6: Launch
- [ ] Documentation in local language
- [ ] Local support team training
- [ ] Marketing localization
- [ ] Gradual rollout
```

### 6.2 Example: Adding Mexico

```yaml
# /localization/mx/domain.yaml
---
country_id: mx
display_name: "México"
language: es-MX
timezone: America/Mexico_City
currency: MXN

# Communication
communication:
  primary_channel: whatsapp
  tone: formal_friendly  # "Usted" form common
  
# Payment Rails
payment_rails:
  primary: spei  # Sistema de Pagos Electrónicos Interbancarios
  secondary: oxxo_pay  # Cash payments at OXXO stores
  tertiary: credit_card
  
# Property Types Available
property_types:
  - ltr  # Arrendamiento tradicional
  - str  # Airbnb México
  - hoa  # Condominio (similar to Brazil)

# Compliance
compliance:
  tax_authority: SAT  # Servicio de Administración Tributaria
  rental_income_tax: progressive  # ISR
  withholding_optional: true
  cfdi_required: true  # Digital invoice
  
# Terminology
terminology:
  property: "Inmueble" / "Propiedad"
  owner: "Propietario" / "Arrendador"
  tenant: "Inquilino" / "Arrendatario"
  lease: "Contrato de Arrendamiento"
  deposit: "Depósito"
  rent: "Renta"
  hoa: "Condominio"
  hoa_fees: "Cuota de Mantenimiento"
```

---

## 7. Architecture Summary

### 7.1 Key Design Principles

| Principle | Implementation |
|-----------|----------------|
| **Inheritance** | Skills cascade: Unit → Property → Org → Domain×Country → Domain → Country → Global |
| **Override** | More specific configs override less specific; explicit overrides always win |
| **Composition** | Market config = Country rules + Domain rules + Role rules |
| **Portability** | Core skills remain unchanged; only configs and overrides differ |
| **Extensibility** | Adding a market = adding config files, not changing code |

### 7.2 Benefits

| Benefit | Impact |
|---------|--------|
| **Time to New Market** | 2-4 weeks vs 3-6 months |
| **Code Reuse** | 70%+ of skills work across markets |
| **Local Compliance** | Built into config, not afterthought |
| **Language/Culture** | Native experience for every user |
| **Investment Logic** | Market-appropriate metrics and benchmarks |

---

## 8. Conclusion

The Digital Worker Localization Architecture enables Citadel OS to serve diverse markets with minimal incremental effort while providing a native experience for each user. The key innovation is treating localization as a **configuration concern** rather than a **code concern**, allowing rapid expansion while maintaining quality.

**Core Formula**:
```
Digital Worker Context = 
    Platform Defaults
    + Country Overrides
    + Domain Overrides
    + Role Overrides
    + Organization Customization
    + Property-Specific Rules
```

This creates a Digital Worker that "speaks" Brazilian Portuguese to a Síndico managing a condomínio, knows about PIX payments and Lei do Inquilinato, while the same platform "speaks" Italian to a vacation rental owner, knows about Alloggiati Web and Cedolare Secca, and "speaks" English to a US landlord, knows about 1031 exchanges and state-specific security deposit rules.

---

**Document Status**: Architecture Specification
**Next Steps**: 
1. Implement skill resolver with inheritance
2. Build configuration loader
3. Create first 3 market configs (BR, US, IT)
4. Test cross-market skill execution

