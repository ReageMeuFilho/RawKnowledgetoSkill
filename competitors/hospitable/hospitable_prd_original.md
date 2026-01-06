# PRODUCT REQUIREMENTS DOCUMENT: HOSPITABLE (v2.0)

**Document Version:** 2.0    
**Last Updated:** January 5, 2026    
**Platform:** Hospitable – "Super App" for Vacation Rental Hosts    
**Target Users:** Solo hosts, co-hosts, and small-to-mid property managers focused on automation  

---

## 1. EXECUTIVE SUMMARY

Hospitable is an automation-first vacation rental platform that centralizes guest communication, channel management, smart devices, and direct bookings with a deep emphasis on AI-driven messaging and operations.  

**Key Positioning (v2 updates):**    
- AI-native "super app" for 1–50 properties, with automation of up to **90% of guest messages** via rules plus AI.    
- Combines unified inbox, direct booking engine, smart lock and thermostat orchestration, and revenue optimization into one hub.    
- Designed for hosts who value time-saving automation and guest experience over deep accounting or enterprise PM modules.  

**Core Value Proposition (v2 focus):**    
- **AI Guest Experience:** Automatic, human-like replies, sentiment detection, and AI boosts for upsells and stay extensions.    
- **Smart Devices:** Native management of smart locks and thermostats that sync with bookings, reducing manual work and energy costs.    
- **Unified Hub:** One interface for Airbnb, Vrbo, Booking.com, and direct bookings, with calendar sync and messaging.    
- **Cost-Efficient Plans:** Fixed monthly pricing based on property count, with no revenue share or booking fees.  

---

## 2. MARKET POSITIONING & COMPETITIVE CONTEXT

### Target Segments

1. **Solo & Small Portfolio Hosts**    
   - 1–15 properties, highly time-constrained.    
   - Need fast setup and automation, not complex accounting or PM structures.  

2. **Co-Hosts & Micro-PMCs**    
   - 5–30 listings across multiple owners.    
   - Require scalable messaging, calendars, and basic team task coordination.  

3. **Automation-First Operators**    
   - Tech-forward hosts who want AI to handle messaging, upsells, and pricing advice.  

### Competitive Positioning (v2)

#### vs. OwnerRez  
- **Advantage:**    
  - Superior AI and automation; much easier UX; native smart devices.    
  - Faster time-to-value for smaller portfolios.    
- **Disadvantage:**    
  - Limited trust accounting and owner statement capabilities; less suited for complex PM accounting.    
- **Sweet Spot:**    
  - Hosts for whom communication and operational automation matter more than GL-level accounting.  

#### vs. Hostaway  
- **Advantage:**    
  - Lower entry cost; simpler UI; more consumerized AI feature set.    
- **Disadvantage:**    
  - Less enterprise-scale PM functionality, fewer advanced owner/financial features.    
- **Sweet Spot:**    
  - 1–50 listings where full enterprise overhead is overkill.  

#### vs. Lodgify  
- **Advantage:**    
  - Stronger AI messaging, smart devices, and operational automation; better unified inbox and guest workflows.    
- **Disadvantage:**    
  - Lodgify offers more advanced website design flexibility; Hospitable sites are simpler.    
- **Sweet Spot:**    
  - Operators prioritizing automation over rich website design.  

### Unique Positioning Elements (v2)

1. **AI Copilot & Knowledge Hub**    
   - AI that reads guidebooks and historical messages to auto-answer guest questions, summarize guests, and provide business insights.  

2. **Smart Devices Management**    
   - Native orchestration of locks and thermostats tied directly to reservations.  

3. **AI-Boosted Upsells & Orphan Nights**    
   - AI detects upsell opportunities (early/late check-in) and orphan nights and sends offers.  

4. **Direct Bookings With Google Vacation Rentals**    
   - Direct sites that can be listed on Google Vacation Rentals via Hospitable Direct.  

### Market Risks

- **Shallower Accounting:** Lacks advanced trust accounting and QuickBooks-depth integrations of OwnerRez/Hostaway.    
- **AI Dependence:** Hosts must trust AI decisions and monitor edge cases; misconfiguration can affect guest satisfaction.    
- **Scaling to 100+ Units:** May require layered tooling or migration to more enterprise PM solutions at very large scale.  

---

## 3. CORE FEATURE ARCHITECTURE (v2)

### 3.1 Unified Inbox & Guest Communication

#### Unified Inbox

- **Channels:** Airbnb, Vrbo, Booking.com, email, and direct messages in one inbox.    
- **Threading & Filters:** Conversation history by guest, listing, and channel; filters for open, pending, needs-review.  

#### Automated Guest Messaging

- **Rules Engine:** Triggered by events (pre-booking, booking confirmed, check-in/out, reviews) and time offsets.    
- **Templates:** Dynamic variables for guest name, property, dates, door codes, etc.    
- **90% Automation Target:** System designed so most conversations never need manual handling.  

#### AI Messaging Layer

- **AI-Drafted Responses:** Suggest with AI composes replies from guidebook, prior messages, and booking context.    
- **Auto Inbox:** Optional fully automated replies with host override when needed.    
- **AI Answers from Guidebook:** AI reads host guidebooks and knowledge hub to answer FAQs automatically.    
- **Sentiment Detection:** Detects guest frustration or issues and flags conversations for human escalation.  

### 3.2 Channel Management & Calendar

- **Multi-Channel Sync:** Connect to Airbnb, Vrbo, Booking.com with two-way synchronization of rates and availability.    
- **Calendar View:** Centralized multi-property calendar with blocking and simple rate adjustments.    
- **Double-Booking Prevention:** Real-time sync to reduce overlaps across channels.  

### 3.3 Direct Booking Platform

#### Direct Websites

- **Website Builder:** Hospitable-hosted direct booking website with simple templates and branding.    
- **Google Vacation Rentals:** Integration allowing direct site listings on Google Vacation Rentals.    
- **Guest Screening & Protection:** Tools for screening, deposits, and damage protection via partners.  

#### Booking Engine

- **Search & Booking:** Availability search, listing pages, and checkout with online payments.    
- **Upsells:** Early check-in, late check-out, and ancillary services offered during or after checkout.  

### 3.4 Smart Devices Management

- **Locks:** Syncs door codes to bookings; guests receive codes automatically at appropriate times.    
- **Thermostats:** Adjusts temperature based on occupancy; energy-saving modes when vacant.    
- **Central Orchestration:** Single interface to manage devices across listings; avoids juggling multiple apps.  

### 3.5 Task & Team Management

- **Task Generation:** Cleaning and maintenance tasks created automatically relative to check-in/out.    
- **Assignments:** Assign tasks to cleaners or team members and share access as needed.    
- **Notifications:** Email/app notifications when tasks are created or overdue.  

---

## 4. REPORTING & ANALYTICS

### 4.1 AI Copilot & Insights

- **Business Insights:** AI Copilot can answer questions about occupancy, underperforming listings, and trends.    
- **Performance Flags:** Highlights vacant nights, low-performing properties, and recurring issues in reviews.  

### 4.2 Operational & Guest Metrics

- **Response Times:** Reports on average reply times and automation coverage.    
- **Review Management:** Automated review suggestions and analysis of themes in guest feedback.  

### 4.3 Financial Overviews

- **Revenue Summaries:** Basic revenue and booking summaries by listing and channel.    
- **Export:** Data export for accounting tools; not a full accounting suite.  

---

## 5. INTEGRATIONS & API ECOSYSTEM

### 5.1 OTA Channels

- **Core Channels:** Airbnb, Vrbo, Booking.com with deep messaging integration and calendar sync.  

### 5.2 Dynamic Pricing

- **Tools:** Integrations with PriceLabs, Beyond, Wheelhouse, etc. for dynamic rates.    
- **AI Revenue Opportunities:** Hospitable's AI also suggests opportunities like discount tiers and orphan-night strategies.  

### 5.3 Payments & Protection

- **Payment Providers:** Stripe and similar gateways for direct booking payments.    
- **Damage Protection:** Integration with damage protection/insurance offerings.  

### 5.4 Smart Devices

- **Device Partners:** Smart locks (e.g., RemoteLock) and thermostat ecosystems with direct sync to bookings.  

---

## 6. PRICING & COMMERCIAL MODEL (v2)

### 6.1 Pricing Structure

- **Fixed Subscription:** No revenue share or booking commission; monthly price scales with property count.    
- **Three Core Plans:** Host, Professional, Mogul; each includes a base number of properties.  

### 6.2 Example Pricing (2024–2025 Benchmarks)

- **Host Plan:**    
  - ~$29/month for 1 property; ~$10/month per additional property.    
  - Designed for 1–3 listings.  

- **Professional Plan:**    
  - ~$59/month with 2 properties included; ~$15 per additional property.    
  - Includes smart lock automation at ~$5/device for extras.  

- **Mogul Plan:**    
  - ~$99/month with 3 properties included; ~$30 per additional property.    
  - Adds owner portals and enhanced branding options.  

- **Per-Listing Economics:**    
  - Typical per-listing fees around £9–£44, average ~£31/listing across user reports.  

### 6.3 Commercial Terms

- **14-Day Free Trial:** No setup fees, easy cancellation.    
- **Billing:** Monthly or annual with potential discounts; pay only for active properties/check-ins in some tiers.  

---

## 7. CUSTOMER SUPPORT & SUCCESS

### 7.1 Support Channels

- **Email & In-App Support:** Standard for all plans.    
- **Help Center & Community:** Documentation, webinars, and community resources.  

### 7.2 Onboarding

- **Self-Service Setup:** Guided workflows to connect channels and configure automations.    
- **Templates:** Pre-built message flows and AI configurations to speed up implementation.  

### 7.3 Reputation

- **Reviews:** Highly rated for ease of use and automation; some users wish for deeper PM and accounting features.  

---

## 8. MOBILE & WEB APPLICATIONS

### 8.1 Web App

- **Primary Interface:** Full feature set available in browser on desktop.    
- **Responsive UI:** Optimized for tablet and mobile browsers.  

### 8.2 Mobile Experience

- **Notifications:** Instant alerts for guest messages and urgent tasks via mobile.    
- **AI-Assisted Replies:** Ability to use AI suggestions on mobile to handle conversations quickly.  

---

## 9. ADVANCED FEATURES & SCALABILITY

### 9.1 AI Guest Experience Stack

- **Knowledge Hub:** Central repository of host rules, guidebooks, and policies used by AI.    
- **Guest Summaries:** AI-generated summaries of guest profiles before check-in.    
- **Pattern Detection:** Identifies recurring issues across reviews to guide improvements.  

### 9.2 Orchestration of Operations

- **Workflows:** Combined triggers across messaging, devices, and tasks (e.g., booking confirmed → send welcome → create cleaning task → program lock).    
- **Scaling to 50+ Units:** Handles messaging and tasks but may require additional layers for complex owner accounting or multi-brand structures.  

---

## 10. TECHNOLOGY, SECURITY & COMPLIANCE

### 10.1 Architecture

- **Cloud-Based SaaS:** Multi-tenant architecture designed for always-on access.  

### 10.2 Security

- **Encrypted Communications:** HTTPS for data in transit; payment data handled by PCI-compliant processors.    
- **Access Control:** Team-level access configurations for co-hosts and cleaners.  

### 10.3 Compliance

- **GDPR-Aware:** European users supported; data handling aligned with major privacy norms.  

---

## 11. KNOWN LIMITATIONS & CONSIDERATIONS (v2)

### 11.1 Feature Gaps

- **Accounting Depth:** No full trust accounting or QuickBooks-level double-entry modules.    
- **Owner Statements:** Owner reporting less sophisticated than OwnerRez/Hostaway.  

### 11.2 Operational Risks

- **AI Over-Reliance:** Mis-tuned AI or incomplete guidebooks can lead to suboptimal responses.    
- **Complex Portfolios:** Micro-PMCs with many owners and varying contracts may outgrow Hospitable's PM feature depth.  

### 11.3 Long-Term Scaling

- **100+ Property Portfolios:** May require combining Hospitable with separate accounting/PM tools or eventually migrating to enterprise PMS.  

---

## 12. COMPETITIVE POSITIONING MATRIX (v2)

| Dimension / Feature          | Hospitable                                   | OwnerRez                                 | Hostaway                                 | Lodgify                                 |  
|-----------------------------|-----------------------------------------------|-------------------------------------------|-------------------------------------------|------------------------------------------|  
| **Target**                  | Solo & small teams                           | Mid-market PMs                            | Enterprise & large PMCs                   | Solo & small PMs                         |  
| **Best Portfolio Range**    | 1–50                                         | 5–150                                     | 20–1000+                                  | 1–50                                     |  
| **Pricing Model**           | Tiered per property         | Per-property + modules          | Custom quote                              | Tiered/property + fees |  
| **AI Messaging**            | Extensive, guidebook-aware | Rules only, no AI                | Partial templates                         | Minimal                                  |  
| **Smart Devices**           | Native locks + thermostats   | Via partners                     | Via partners                              | Limited                                  |  
| **Direct Booking**          | Built-in sites + GVR       | Hosted sites + WP plugin         | Booking engine                            | Strong website builder|  
| **Accounting Depth**        | Light                                        | Deep QuickBooks-centric         | Strong enterprise                         | Basic                   |  
| **Ease of Use**             | Very easy                    | Moderate/hard           | Hard                                      | Easy                   |  
| **Best For**                | Automation-first hosts                       | Accounting-heavy PMCs                    | Enterprise portfolios                     | Direct booking–focused hosts             |

---

## 13. IDEAL CUSTOMER PROFILES (v2)

### Primary ICP: Automation-First Solo/Small Host

- **Portfolio:** 1–10 listings.    
- **Needs:** Offload guest communication, basic channel sync, simple direct bookings.  

### Secondary ICP: Co-Host / Micro-PMC

- **Portfolio:** 10–40 listings under management.    
- **Needs:** AI to scale guest comms, simple team/co-host flows, some owner-friendly reporting.  

### Avoid / Low-Fit

- **Accounting-Heavy PMCs:** Deep trust accounting needs better served by OwnerRez/Hostaway.    
- **Large Multi-Brand Enterprises:** Need complex workflows and enterprise governance beyond Hospitable's scope.  

---

## 14. IMPLEMENTATION ROADMAP (TYPICAL)

### Phase 1: Setup (Days 1–3)

- Connect Airbnb, Vrbo, Booking.com accounts.    
- Import listings and basic details.  

### Phase 2: Automation (Days 4–10)

- Configure message rules and AI Answer from guidebook.    
- Upload guidebooks and policies to Knowledge Hub.    
- Connect smart locks and thermostats.  

### Phase 3: Direct Bookings (Weeks 2–3)

- Launch direct booking site, connect payments, and optionally enable Google Vacation Rentals.  

### Phase 4: Optimization (Weeks 3–6)

- Monitor AI responses, refine prompts and templates.    
- Enable upsells and AI orphan-night offers.  

---

## 15. OUTCOME EXPECTATIONS

- **Time to Automation Value:** Within 1–2 weeks for messaging automation and device workflows.    
- **Time Savings:** Hosts report large reductions in manual guest messaging workload once AI is tuned.    
- **ROI Drivers:** Less time spent on messaging, more direct bookings, improved occupancy through AI-driven upsells and dynamic pricing partnerships.  


