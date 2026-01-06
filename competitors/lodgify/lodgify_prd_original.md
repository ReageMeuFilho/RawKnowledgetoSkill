# PRODUCT REQUIREMENTS DOCUMENT: LODGIFY (v2.0)

**Document Version:** 2.0    
**Last Updated:** January 5, 2026    
**Platform:** Lodgify Vacation Rental Website & PMS    
**Target Users:** Solo hosts, small property managers, direct-booking–focused operators  

---

## 1. EXECUTIVE SUMMARY

Lodgify is a website-first vacation rental platform that combines a drag-and-drop website builder, integrated booking engine, and basic PMS/channel management for small to mid-sized portfolios.  

**Key Positioning (v2 updates):**    
- Purpose-built **direct booking website** and booking engine as primary value, with PMS and channel manager as supporting components.    
- Affordable entry pricing starting around **$16/month** for 1 property on Starter, with a 1.9% booking fee, and higher plans removing booking fees.    
- Ideal for 1–50 property operators prioritizing branding, direct bookings, and ease of use over deep accounting or complex owner structures.  

**Core Value Proposition (v2 focus):**    
- **Professional Website in Days:** Drag-and-drop builder with templates, SSL, widgets, and booking engine.    
- **Multi-Channel Distribution:** Centralized calendar and channel manager to sync Airbnb, Vrbo, Booking.com, and others.    
- **All-in-One Starter Stack:** Basic PMS tools (reservations, payments, basic accounting, owner statements), automations, and analytics within one interface.    
- **Cost-Effective Growth:** Tiered plans for Starter, Professional, and Ultimate with per-property scaling and optional dynamic pricing add-on.  

---

## 2. MARKET POSITIONING & COMPETITIVE CONTEXT

### Target Segments

1. **Direct-Booking–Focused Solo Hosts**    
   - 1–5 properties needing a professional website and basic PMS.  

2. **Small Property Managers**    
   - 5–50 properties, multiple channels, and basic owner reporting needs.  

3. **New STR Businesses**    
   - Early-stage operators seeking a simple, affordable all-in-one tool before upgrading to more complex PM systems.  

### Competitive Positioning (v2)

#### vs. OwnerRez  
- **Advantage:**    
  - Easier onboarding and website creation; more modern drag-and-drop site builder out-of-the-box.    
- **Disadvantage:**    
  - Weaker accounting, trust accounting, and QuickBooks integrations; less suitable for accounting-heavy PMCs.    
- **Sweet Spot:**    
  - Hosts who care more about brand presence and simplicity than advanced financial control.  

#### vs. Hospitable  
- **Advantage:**    
  - Stronger website builder and branding; more flexible site templates and widgets.    
- **Disadvantage:**    
  - Less sophisticated AI messaging and smart-device orchestration.    
- **Sweet Spot:**    
  - Hosts who want a polished direct booking site and are fine with basic automations.  

#### vs. Hostaway  
- **Advantage:**    
  - Much lower entry price and simpler UX for small portfolios.    
- **Disadvantage:**    
  - Not designed for 100+ unit enterprise complexity; weaker advanced PM and accounting modules.    
- **Sweet Spot:**    
  - Small operators who don't need enterprise-grade tooling.  

### Unique Positioning Elements (v2)

1. **Website-First Design:**    
   - Platform built initially as a website builder with PMS layered on top, not the other way around.  

2. **No-Dev Direct Booking:**    
   - Drag-and-drop editor, templates, and widgets for non-technical users.  

3. **Google Vacation Rentals Integration (Higher Plans):**    
   - Higher tiers integrate direct sites into Google Vacation Rentals for extra exposure.  

### Market Risks

- **Limited Accounting Depth:** Basic financial tools may not satisfy PMCs with complex owner and trust needs.    
- **Scaling Plateau:** Portfolios above 50–100 units may outgrow Lodgify and require migration to more advanced PMS.    
- **Starter Booking Fee:** 1.9% booking fee on Starter plan reduces margin unless upgrading.  

---

## 3. CORE FEATURE ARCHITECTURE (v2)

### 3.1 Website Builder & Booking Engine

#### Website Builder

- **Drag-and-Drop Editor:** Visual builder to add sections, images, text, contact forms, and booking widgets without code.    
- **Templates:** Industry-specific templates optimized for vacation rentals, mobile responsive and SEO-ready.    
- **Branding:** Custom colors, fonts, logos, and custom domains with SSL included.  

#### Booking Engine

- **Integrated Checkout:** Guests can search, select dates, see pricing, and pay directly on site.    
- **Multi-Property Search:** Search by date, property, and basic filters across portfolio.    
- **Coupons & Promotions:** Create discount codes, seasonal promotions, and direct-booking incentives.  

### 3.2 PMS & Reservation Management

#### Reservations & Calendar

- **Multi-Calendar:** Unified calendar across properties showing all bookings and availability.    
- **Reservation Management:** View, modify, cancel, and add manual bookings (phone/OTAs).    
- **Seasonal & Rate Management:** Set seasons, length-of-stay rules, and nightly/weekly rates in PMS.  

#### Booking Rules & Fees

- **Minimum Stay, Turnover Days:** Configure per season or globally.    
- **Fees & Taxes:** Cleaning fees, extra guest fees, and tax rules applied per booking.  

### 3.3 Channel Manager

- **Channel Coverage:** Airbnb, Vrbo, Booking.com, and other channels via robust sync.    
- **Sync Types:** Two-way availability sync, rates, and often content (depending on channel).    
- **Double-Booking Prevention:** Real-time updates across connected channels when bookings occur.  

### 3.4 Communication & Automations

- **Guest Messaging:** Built-in messaging, templates, and basic auto-responses triggered by booking events.    
- **Review Requests:** Automated or manual post-stay review request messages.    
- **Multi-Language Support:** Automatic response languages and templates per language (v2 update).  

### 3.5 Owner & Team Management

- **Owner Statements:** Generate statements summarizing bookings, revenue, fees, and expenses over a period.    
- **Owner Emails:** Export or email statements directly to owners or stakeholders.    
- **Team Tasks (2025 Enhancements):**    
  - Create tasks manually or from templates.    
  - Assign tasks to team members.    
  - Set start/end times and approve completed work via desktop or mobile.  

---

## 4. REPORTING & ANALYTICS

### 4.1 Operational & Financial Reports

- **Booking Reports:** Overview of bookings by property, channel, and period.    
- **Revenue & Occupancy:** Track income and occupancy rates for different properties.    
- **Owner Statements:** Configurable statements with fees, taxes, and expenses.  

### 4.2 Performance Analytics

- **Channel Performance:** Identify which channels drive most revenue and occupancy.    
- **Direct vs OTA Mix:** Compare direct bookings to OTAs to optimize channel strategy.  

### 4.3 Exports

- **Data Export:** Export reports and statements for tax prep or use in external accounting tools like Excel or basic accounting software.  

---

## 5. INTEGRATIONS & API ECOSYSTEM

### 5.1 OTAs & Distribution

- **Major Channels:** Airbnb, Vrbo, Booking.com and 60+ channels via integrations.    
- **iCal Support:** Additional channels via calendar feeds to ensure broad coverage.  

### 5.2 Payments

- **Gateways:** Stripe, PayPal, 2Checkout, Braintree, and others for secure payments.    
- **Payment Features:** Deposits, split payments (with limits), and refunds managed from dashboard.  

### 5.3 Dynamic Pricing (Add-On)

- **Dynamic Pricing Tool:** Optional add-on (~0.8% per booking) to adjust rates based on demand and occupancy.  

### 5.4 API & Widgets

- **Widgets:** External booking widgets to embed booking engine into an existing site.    
- **API:** Available to higher-tier customers or via partner integrations for custom workflows (limited vs enterprise PMS APIs).  

---

## 6. PRICING & COMMERCIAL MODEL (v2)

### 6.1 Plans & Structure

- **Starter:**    
  - From **$16/month** (annual billing) for 1 property; scales by property count.    
  - **1.9% booking fee** on direct bookings.    
  - Includes bookable website, channel manager, email support, guest messaging.  

- **Professional:**    
  - Around **$40/month** for 1 property; no booking fees.    
  - Supports more properties (e.g., 1–10) with higher base; includes better support options and manual payment options.  

- **Ultimate:**    
  - Around **$59/month** for 1 property; no booking fees.    
  - Includes all Professional features plus more advanced automation and support; recommended for larger portfolios.  

### 6.2 Scaling Examples (Annual Billing Benchmarks)

- **1 Property:** Starter $16, Pro $40, Ultimate $59/month.    
- **5 Properties:** Starter $36 + 1.9% fee, Pro $110, Ultimate $147/month.    
- **10 Properties:** Starter $52 + 1.9% fee, Pro $155, Ultimate $206/month.    
- **100 Properties:** Starter $102 + 1.9% fee, Pro $813, Ultimate $1148/month.  

### 6.3 Commercial Terms

- **Free Trial:** Time-limited free trial available; no credit card required initially in many cases.    
- **Billing Options:** Monthly or annual; discounts for annual billing.  

---

## 7. CUSTOMER SUPPORT & SUCCESS

### 7.1 Support

- **Email Support:** Included across plans, with response SLAs varying by tier.    
- **Phone & Priority Support:** Available on Professional/Ultimate plans.    
- **Help Center:** In-depth documentation, tutorials, and video demos.  

### 7.2 Onboarding

- **Self-Service:** Guided onboarding flows and tutorials for website setup and channel connections.    
- **Webinars & Demos:** Live demos showing PMS modules, pricing setup, and owner statements.  

### 7.3 Reputation

- **Reviews:** Praised for ease of website creation and value; cons mention limitations in advanced PMS/accounting and occasional customer support delays.  

---

## 8. MOBILE & WEB APPLICATIONS

### 8.1 Web App

- **Main Dashboard:** Central hub for bookings, calendar, rates, and website management.    
- **Navigation:** Separate tabs for website builder, rentals, rates, PM modules, and widgets.  

### 8.2 Mobile

- **Mobile Access:** Responsive interface for managing bookings, calendar, and tasks on the go.    
- **Tasks on the Go (2025):** Create/assign/approve tasks via mobile layouts.  

---

## 9. ADVANCED FEATURES & SCALABILITY

### 9.1 Property Management Modules

- **Owner Statements & Strategies:**    
  - Create statement "strategies" defining which fees/taxes apply and how to split revenue.    
  - Generate monthly/quarterly statements with booking breakdowns and expenses.    
  - Export or email statements to owners or other stakeholders.  

- **Task Management:**    
  - Templates and manual creation of tasks; assign, track, and approve.  

### 9.2 AI & Product Enhancements (2025)

- **AI-Powered Features:**    
  - New features to reduce admin and support dynamic content, such as improved auto-response languages and potentially AI-assisted messaging (roadmap/early features).  

### 9.3 Scalability Considerations

- **Best Range:** 1–50 properties with moderate complexity.    
- **Beyond 100 Properties:** Custom pricing and increasing operational friction; comparison guides often recommend migrating to Guesty/Hostaway at larger scales.  

---

## 10. TECHNOLOGY, SECURITY & COMPLIANCE

### 10.1 Architecture

- **Cloud-Based SaaS:** Multi-tenant, browser-based solution.  

### 10.2 Security & Payments

- **SSL:** All Lodgify sites ship with SSL certificates.    
- **PCI Compliance:** Payments processed by PCI-compliant gateways like Stripe/PayPal.  

### 10.3 Compliance

- **GDPR-Aware:** Data-handling practices aligned to EU norms, though details may rely on third-party payment/data processors.  

---

## 11. KNOWN LIMITATIONS & CONSIDERATIONS (v2)

### 11.1 Accounting & PM Gaps

- **Trust Accounting:** No NC-compliant trust accounting like enterprise PMS (e.g., Guesty Pro).    
- **Deep Accounting:** Limited compared to OwnerRez/Hostaway; many PMCs still export data into external accounting.  

### 11.2 Automation & AI

- **Automation Depth:** Automations and messaging are improving but still considered "basic" vs AI-first tools like Hospitable.  

### 11.3 Growth Constraints

- **Large Portfolios:** 20+ units may start hitting functional limits (e.g., advanced workflows, owner structures), leading some operators to switch platforms.  

---

## 12. COMPETITIVE POSITIONING MATRIX (v2)

| Dimension / Feature       | Lodgify                                   | OwnerRez                                   | Hospitable                                   | Hostaway                                  |  
|---------------------------|-------------------------------------------|--------------------------------------------|----------------------------------------------|-------------------------------------------|  
| **Core Strength**         | Website & direct booking | Accounting & PM                   | AI automation & devices     | Enterprise PMS & channels|  
| **Best Portfolio Range**  | 1–50                             | 5–150                                      | 1–50                                         | 20–1000+                                  |  
| **Pricing Model**         | Tiered + booking fee on Starter   | Per-property + modules            | Tiered per listing          | Custom quote                              |  
| **Website Builder**       | Advanced drag-and-drop  | Solid but secondary                         | Simple sites                        | Basic                                     |  
| **Dynamic Pricing**       | Add-on ~0.8%/booking               | Partner tools                               | Partner tools + AI guidance | Partner tools                             |  
| **Accounting Depth**      | Basic                   | Deep QuickBooks-centric           | Light                      | Strong enterprise                         |  
| **AI Messaging**          | Emerging/basic                   | None                                       | Advanced AI               | Limited                                   |  
| **Ease of Use**           | Easy                    | Moderate/hard                      | Very easy                    | Hard                                      |

---

## 13. IDEAL CUSTOMER PROFILES (v2)

### Primary ICP: Direct-Booking–First Solo Host

- **Portfolio:** 1–5 properties.    
- **Needs:** Polished direct booking site, simple channel sync, basic automations.  

### Secondary ICP: Small PM with Branding Focus

- **Portfolio:** 5–30 properties.    
- **Needs:** Multi-property website, basic owner statements, and moderate PMS features.  

### Avoid / Low-Fit

- **Accounting-Heavy PMCs:** Deep trust/accounting better served by OwnerRez/Hostaway.    
- **Large Multi-Brand Enterprises:** Scaling beyond ~100 properties better on enterprise PMS.  

---

## 14. IMPLEMENTATION ROADMAP (TYPICAL)

### Phase 1: Website & Branding (Week 1)

- Select template and configure branding (logo, colors, fonts).    
- Set up pages (Home, Properties, About, Contact, Policies).  

### Phase 2: PMS & Rates (Weeks 1–2)

- Add properties, photos, and descriptions.    
- Configure rates, seasons, taxes, and fees.  

### Phase 3: Channels & Payments (Weeks 2–3)

- Connect Airbnb/Vrbo/Booking.com channels and sync calendars.    
- Connect payment gateways and run test transactions.  

### Phase 4: Automations & Owner Statements (Weeks 3–5)

- Set up messaging templates and auto-responses.    
- Configure owner statement strategies and run first statements.  

---

## 15. OUTCOME EXPECTATIONS

- **Time to Launch:** Professional direct-booking site and basic PMS in 1–2 weeks for small portfolios.    
- **ROI Drivers:** Increased direct bookings (lower OTA commission), improved brand presence, and reduced admin via centralized operations.    
- **Upgrade Paths:** As portfolios or complexity grow, users may either expand Lodgify (Ultimate + add-ons) or migrate to more advanced PMS.  


