# PRODUCT REQUIREMENTS DOCUMENT: OWNERREZ (v2.0)

**Document Version:** 2.0    
**Last Updated:** January 5, 2026    
**Platform:** OwnerRez Vacation Rental Management Software    
**Target Users:** Property management companies, multi-property operators, accounting-focused hosts  

---

## 1. EXECUTIVE SUMMARY

OwnerRez is a mature, mid-market property management platform designed for professional property managers and serious property operators who need robust channel management, advanced accounting workflows via QuickBooks, and scalable operations for 5–100+ property portfolios.  

**Key Positioning (v2 updates):**    
- Mid-market solution with stronger emphasis on **trust accounting workflows via QuickBooks Online** and owner statement automation.    
- Per-property, transparent pricing with modular add-ons for PM, QuickBooks, hosted sites, and advanced features.    
- Best fit for accounting-focused PMCs and serious operators who prioritize financial accuracy over ease-of-use.  

**Core Value Proposition (v2 focus):**    
- **Transparency:** Clear, modular per-property pricing; unlimited bookings; no setup or booking fees.    
- **Accounting Excellence:** Deep QuickBooks Online integration including deposit syncing, owner expenses, and to-the-penny reconciliation.    
- **Professional Operations:** Commission tracking, owner statements, task automation, and multi-channel distribution.    
- **Scalability:** Economical as unit count grows; cost per property drops significantly beyond 20–50 units.    
- **Ecosystem:** Extensive third-party integrations (dynamic pricing, smart locks, operations tools like Turno/Breezeway).  

---

## 2. MARKET POSITIONING & COMPETITIVE CONTEXT

### Target Segments

1. **Property Management Companies (PMCs)**    
   - Portfolios: 10–150 units (core sweet spot 10–60).    
   - High complexity around owner accounting, trust workflows, and tax reporting.  

2. **Professional Multi-Property Hosts**    
   - 5–20 units, moving from "host tools" to professional stack.    
   - Need stronger reporting, docs, and owner-ready financials.  

3. **Accounting-Focused Operators**    
   - Require accurate financial exports to QuickBooks Online and clear audit trails.  

4. **Tech-Forward STR Operators**    
   - Heavy reliance on automations, smart devices, and dynamic pricing tools.  

### Competitive Positioning (v2)

#### vs. Hostaway  
- **Advantage:**    
  - Lower entry price for smaller portfolios; transparent public pricing.    
  - Deeper QuickBooks Online integration emphasis; simpler API surface for mid-market use.    
- **Disadvantage:**    
  - Less enterprise onboarding, fewer "done-for-you" services, and smaller feature set for mega-portfolios.    
- **Sweet Spot:**    
  - PMCs that need strong accounting and trust workflows but do not require full enterprise implementation teams.  

#### vs. Hospitable  
- **Advantage:**    
  - Much deeper financial and owner management capabilities, including PM module and owner statements.    
  - Better for 10+ units and multi-owner structures.    
- **Disadvantage:**    
  - Less AI-native; messaging is template/automation-based rather than fully AI-driven.    
- **Sweet Spot:**    
  - Professional PMCs who can tolerate more complexity to gain accounting power.  

#### vs. Lodgify  
- **Advantage:**    
  - Stronger accounting, reporting, and channel management depth; more flexible automations.    
- **Disadvantage:**    
  - Steeper learning curve; UI less beginner-friendly, smaller website-design emphasis.    
- **Sweet Spot:**    
  - Operators outgrowing Lodgify's simple accounting and needing robust PM/owner tooling.  

### Unique Positioning Elements (v2)

1. **QuickBooks-First Accounting:**    
   - Designed to offload full accounting to QuickBooks Online while providing detailed sync rules and deposit syncing.  

2. **Modular Pricing Architecture:**    
   - Base PMS plus add-on modules (PM, QuickBooks, hosted sites, SMS) allowing granular control over cost structure.  

3. **Advanced Channel Rate Tools:**    
   - Rate comparison by channel, markup and testing tools for price optimization.  

4. **Power-User Automations:**    
   - Complex triggers for messaging, tasks, contracts, and fees with fine-grained conditions.  

### Market Risks

- **UI Complexity:** Reviews frequently mention a steeper learning curve and non-intuitive UX.    
- **Limited Native Mobile Depth:** Mobile experience mature but not as "mobile-first" as newer tools.    
- **No Native Double-Entry:** Depends on external accounting; some buyers prefer all-in-one accounting.  

---

## 3. CORE FEATURE ARCHITECTURE (v2)

### 3.1 Property Management System (PMS)

#### Unified Calendar Management

- **Real-Time Calendar Sync:** Centralized multi-property calendar across Airbnb, Vrbo, Booking.com, direct, and other OTAs.    
- **Views:** Month, timeline, and grid with color-coded sources and statuses.    
- **Bulk Editing:** Batch change rates, minimum stays, and availability across selected properties.    
- **Manual Blocks:** Seasonal blocks, maintenance windows, owner stays.  

#### Reservation Management

- **Booking Capture:** Consolidates reservations from all connected OTAs plus direct/phone bookings.    
- **Guest Profile:** CRM fields, contact info, repeat-guest history, notes, tags.    
- **Quote-to-Booking Flow:** Create quotes with taxes/fees, send to guests, and convert to bookings.  

##### Digital Documents & E-Signatures

- **Rental Agreements:** Custom agreements per property, channel, or use case; digital signature collection.    
- **Automation:** Auto-send contracts on booking creation; require signature before check-in.  

##### Security Deposits & Protection

- **Security Deposit Holds:** Pre-authorization holds with configurable amounts and timing.    
- **Refundable Damage Deposits:** Support for RDD workflows separate from holds.    
- **Damage Protection:** Integration with third-party insurance products.  

### 3.2 Channel Management

#### OTA Integrations (Native)

- **OTA Coverage:** Airbnb, Vrbo, Booking.com, plus iCal channels and niche partners.    
- **Two-Way Sync:** Availability, rates, restrictions, and content pushed from OwnerRez.    
- **Reservation Import:** Automatic import of future bookings; CSV workflows for legacy data if required.  

#### Channel Features

- **Channel-Specific Rate Markups:** Markup/markdown per channel to maintain parity and margin.    
- **Rate Comparison & Testing:** Tools to compare actual OTA listings vs expected nightly prices.    
- **Channel Fees & Taxes:** Configuration of guest fees, channel commissions, and tax logic.  

### 3.3 Direct Booking Platform

#### Website Options

- **Hosted Sites:** OwnerRez-hosted websites with templates and direct booking engine.    
- **WordPress Plugin:** Deep integration plugin to connect custom WP sites to OwnerRez inventory.    
- **Branding:** Logos, colors, pages, SEO metadata, and custom domains.  

#### Direct Booking Engine

- **Search & Filters:** Date, guest count, and basic amenity filters.    
- **Checkout Flow:** Guest details, pricing breakdown, taxes/fees, upsells, and payment capture.    
- **Coupons & Promotions:** Coupon codes, discounts by stay length, and seasonal promos.  

### 3.4 Financial Management & Accounting

#### Trust Accounting & PM (via QuickBooks)

- **OwnerRez Ledger:** Handles invoicing, payments, and expense tracking internally but delegates double-entry to QuickBooks.    
- **QuickBooks Sync:**    
  - Bookings, payments, and deposits auto-synced to QuickBooks Online.    
  - Deposit syncing for to-the-penny bank reconciliations.    
- **Limitations:**    
  - No full GL or multi-entity accounting inside OwnerRez; relies on QuickBooks for P&L, balance sheet, etc.  

#### Owner Statements & Payouts

- **Owner Statements:** Monthly statements with revenue, fees, and expenses by owner and property.    
- **Payout Rules:** Commission splits, PM fees, and owner net calculations.    
- **QuickBooks Payout Sync:** Pushes payout entries as checks to print or unpaid bills.  

#### Taxes

- **Tax Rules Engine:** Configure tax rules by jurisdiction, property, and channel.    
- **OTA Tax Sync:** Push certain tax configuration to channels where supported.    
- **Reporting:** Exportable tax summaries for filing and accountant use.  

### 3.5 Messaging & Guest Communication

#### Unified Inbox

- **Channels:** Email, SMS, Airbnb/Vrbo messaging consolidated.    
- **Threading & Search:** Conversation history by guest, property, or booking.  

#### Automations (Rules Engine)

- **Triggers:**    
  - Time-based (X days before/after check-in/out).    
  - Event-based (booking created, payment received, contract signed).    
- **Templates:** Dynamic fields for guest name, dates, property, access codes, etc.    
- **Limitations:** No native generative AI; rules are deterministic and template-based.  

### 3.6 Task Management & Operations

- **Tasks:** Cleaning, inspections, maintenance tasks tied to booking events.    
- **Rules:** Auto-create tasks on booking confirmation, mid-stay, departure, vacancy windows.    
- **Assignees:** Assign to cleaners, maintenance staff, or vendors; optional integrations for Turno/Breezeway.  

---

## 4. REPORTING & ANALYTICS

### 4.1 Business & Operational Reports

- **Occupancy & Revenue:** By property, owner, and channel over time.    
- **Booking Funnel:** Conversion metrics from quote to booking.    
- **Operations:** Task completion logs and staff performance where integrated.  

### 4.2 Financial Reports

- **Booking & Payment Reports:** Detailed breakdowns with export to CSV/Excel.    
- **Owner Statements:** Recurring statements as part of PM module.    
- **Tax Reports:** Tax line items aggregated by jurisdiction for a period.  

### 4.3 Custom & Export

- **Filters:** Date range, channel, property, owner, and tags.    
- **Export:** CSV and Excel exports to combine with external BI tools.  

---

## 5. INTEGRATIONS & API ECOSYSTEM

### 5.1 OTA Channels

- **Direct Integrations:** Airbnb, Vrbo, Booking.com, and others via official APIs.    
- **iCal Support:** For long tail channels without native API integrations.  

### 5.2 Accounting

- **QuickBooks Online:**    
  - One-way and two-way flows for invoices, payments, and deposits.    
  - No QuickBooks Desktop support in core integration.  

### 5.3 Payments

- **Payment Processors:** Ability to use own processor (Stripe and others) for flexibility and cost control.    
- **Security:** PCI-compliant processors recommended and documented.  

### 5.4 Operations & Devices

- **Smart Locks & IoT:** RemoteLock and similar tools for code generation and guest access.    
- **Housekeeping Platforms:** Turno, Breezeway and others for advanced task routing.  

---

## 6. PRICING & COMMERCIAL MODEL (v2)

### 6.1 Base Pricing

- **Per-Property Model:** Starts around **$40/month for 1 property**; price-per-property decreases as property count increases.    
- **Public Examples:**    
  - 2 properties: around $35/month (G2 small-user example).    
  - 5 properties: ~$56/month.    
  - 10 properties: ~$89/month.  

- **Scaling Discounts:**    
  - 20–49 properties: ~$6/property/month for base product.    
  - 50–99 properties: ~$4/property/month.  

### 6.2 Premium Modules & Add-Ons

- **Property Management Module (PM):** Adds owner statements and commissions at additional per-property pricing.    
- **QuickBooks Integration:** Premium feature, charged per property or account.    
- **Hosted Websites & WP Integration:** Additional per-property pricing for hosted sites and WP plugin usage.    
- **SMS Messaging:** Separate metered or add-on pricing.  

### 6.3 Commercial Terms

- **Unlimited Bookings:** No per-booking fees.    
- **No Contracts:** Month-to-month with 14-day free trial.    
- **Enterprise Deals:** Custom arrangements for very large portfolios or special use cases.  

---

## 7. CUSTOMER SUPPORT & SUCCESS

### 7.1 Support Channels

- **Email & Ticketing:** Standard channel for most users.    
- **Knowledge Base:** Extensive self-service documentation and community forum.  

### 7.2 Onboarding

- **Self-Service Setup:** Emphasis on documentation and videos over paid onboarding.    
- **Migration Guides:** Articles for moving from other PMS tools and importing historical data.  

### 7.3 Reputation & Retention

- **Reviews:** High ratings on Capterra/GetApp for features and value, with UI complexity as common con.    
- **Retention:** Strong loyalty among accounting-focused PMs.  

---

## 8. MOBILE & WEB APPLICATIONS

### 8.1 Web Application

- **Primary Experience:** Full-featured web dashboard optimized for desktop workflows.    
- **Responsive Design:** Usable on tablets and laptops for on-the-go management.  

### 8.2 Mobile Access

- **Mobile Web:** Responsive layouts for calendar, inbox, and basic controls.    
- **Third-Party Apps:** Many operational functions (cleaning, locks) handled via integrated partner apps.  

---

## 9. ADVANCED FEATURES & SCALABILITY

### 9.1 Multi-Owner Management

- **Owner Records:** Contact details, property assignments, payout settings.    
- **Owner Portals:** Either via reports or dedicated access depending on configuration.    
- **Owner Stays:** Special reservation status so owner stays appear in calendars and financials appropriately.  

### 9.2 Automation Rules Engine

- **Complex Conditions:** Channel, property, booking source, date ranges, and more.    
- **Use Cases:**    
  - Auto-send lock codes.    
  - Auto-create tasks relative to check-in/out.    
  - Auto-apply fees based on stay length or guest count.  

### 9.3 Scaling Considerations

- **Best Fit Portfolio Size:** 5–150 properties; above that, admins may require more enterprise-style governance.    
- **Performance:** Designed for high booking volumes and unlimited transactions under a single account.  

---

## 10. TECHNOLOGY, SECURITY & COMPLIANCE

### 10.1 Architecture

- **Cloud-Hosted Web App:** Multi-tenant SaaS model.    
- **API & Integrations:** REST API and secure integrations with major providers.  

### 10.2 Security

- **Data Protection:** Encrypted transport (HTTPS) and secure handling of payment data via PCI-compliant processors.    
- **Access Control:** Role-based user permissions internally and with some integrations.  

### 10.3 Compliance

- **Accounting Accuracy:** Designed to support compliant accounting when paired with QuickBooks Online.    
- **Privacy:** Aligns with standard SaaS data processing practices in US/EU markets.  

---

## 11. KNOWN LIMITATIONS & CONSIDERATIONS (v2)

### 11.1 Feature Gaps

- **No Native Double-Entry:** Must rely on QuickBooks or external GL for full accounting, including balance sheet and advanced reporting.    
- **Limited Native AI:** Messaging automation is rules-based, not LLM-driven.    
- **Thermostat & Device Depth:** Integrations primarily around locks and noise sensors; less native device orchestration than Hospitable.  

### 11.2 Usability & Onboarding

- **Steep Learning Curve:** Power-user orientation; can be overwhelming for non-technical operators.    
- **UI Legacy:** Some screens show legacy UX patterns vs modern competitors.  

### 11.3 Enterprise Fit

- **Large Multi-Brand PMCs:** Very large firms may require more granular org segmentation and enterprise support than OwnerRez offers.  

---

## 12. COMPETITIVE POSITIONING MATRIX (v2)

| Feature / Dimension           | OwnerRez                               | Hostaway                           | Hospitable                           | Lodgify                               |  
|------------------------------|----------------------------------------|------------------------------------|--------------------------------------|----------------------------------------|  
| **Target**                   | Mid-market PMs                         | Enterprise / upper mid             | Solo & small teams                   | Solo & budget mid-market              |  
| **Best Portfolio Range**     | 5–150                                  | 20–1000+                           | 1–20                                 | 1–50                                   |  
| **Pricing Model**            | Per-property + add-ons       | Custom quote                       | Tiered per-listing         | Tiered/property               |  
| **Base Cost (1 prop)**       | ~$40/mo              | $500+ /mo (typical)                | From ~$40–$65/mo  | From ~$16–$30/mo      |  
| **Dynamic Pricing**          | Via partners (e.g., PriceLabs)        | Via partners                       | Included add-on options    | Via partners                  |  
| **Smart Devices**            | Locks/IoT via partners        | Locks via partners                 | Native locks + thermostats  | Limited smart device support  |  
| **AI Messaging**             | No native AI                           | Partial templates                  | Extensive AI engine | Minimal / none              |  
| **Accounting Integration**   | Very strong QuickBooks Online focus | Strong but broader               | Basic reports only         | Basic accounting              |  
| **Trust Accounting**         | Strong via PM + QuickBooks workflows | Strong internal                  | Limited                              | Very limited                           |  
| **Team Features**            | Good roles & tasks            | Strong enterprise roles            | Basic team tools           | Basic roles                   |  
| **Onboarding**               | Self-service                           | Paid onboarding                    | Self-service                         | Self-service                           |  
| **Ease of Use**              | Moderate/Hard        | Hard                               | Very easy           | Easy                   |  
| **Website Builder**          | Solid, but secondary          | Basic pages                        | Simple direct booking pages  | Core strength        |

---

## 13. IDEAL CUSTOMER PROFILES (v2)

### Primary ICP: Accounting-Heavy PMC

- **Portfolio:** 15–80 properties.    
- **Team:** 3–10 staff, including a bookkeeper or accountant.    
- **Key Needs:**    
  - Trust-like workflows via QuickBooks; owner statements; tax exports.    
  - Flexible automations and integrations (locks, cleaners, pricing).  

### Secondary ICP: Advanced Multi-Property Operator

- **Portfolio:** 5–20 units, typically STR-heavy.    
- **Key Needs:**    
  - Strong channel management, direct booking, and decent accounting exports.    
  - Willing to learn a powerful system in exchange for control and cost-efficiency.  

### Avoid / Low-Fit

- **Brand-New Solo Hosts (1–2 listings):** May find complexity unnecessary; Hospitable or Lodgify often more appropriate.    
- **Mega-Enterprise PMCs (500+ units):** May prefer Hostaway/Guesty with enterprise success teams and custom SLAs.  

---

## 14. IMPLEMENTATION ROADMAP (TYPICAL)

### Phase 1: Discovery & Planning (Week 1)

- Inventory properties, channels, and current accounting setup.    
- Define owner payout rules and commission models.  

### Phase 2: Configuration (Weeks 2–3)

- Create properties and units in OwnerRez.    
- Configure taxes, fees, and rate structures.    
- Set up direct booking site or WordPress integration.  

### Phase 3: Integrations (Weeks 3–5)

- Connect Airbnb, Vrbo, Booking.com, and other channels.    
- Configure payment processors and test transactions.    
- Connect QuickBooks Online and validate mappings.  

### Phase 4: Operational Automation (Weeks 5–7)

- Build messaging templates and trigger rules.    
- Set up task rules, cleaning workflows, and IoT integrations.  

### Phase 5: Go-Live & Optimization (Weeks 8–12)

- Gradual migration of live bookings; close gaps in historical data.    
- Tune pricing rules, automations, and owner statements after first full accounting period.  

---

## 15. OUTCOME EXPECTATIONS

- **Time to Operational Fit:** 1–2 months for calendar and messaging stability.    
- **Time to Financial Accuracy:** 2–4 months for fully reconciled QuickBooks flows and owner statements.    
- **ROI Drivers:** Reduced manual accounting work, fewer channel errors, improved direct bookings, and better owner transparency.  


