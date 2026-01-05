Here is the comprehensive, implementation-ready **Product Requirements Document (PRD)** for the Short-Term Rental (STR) vertical.

This document synthesizes the best-in-class features from **Guesty (Operations), Cloudbeds (Distribution), Mews (Hospitality), BoomAI (Agentic Automation), and BestyAI (Revenue Ops)** into a single, unified architecture.

---

# **Product Requirements Document: The Host OS (STR Vertical)**

Product Name: NEXUS Host OS

Version: 5.0 (Final Release Candidate)

Date: January 4, 2026

Architecture: Agentic Skills Runtime \+ Event-Driven Core

---

## **1\. Executive Summary**

The **Host OS** is a specialized runtime environment designed for high-velocity, hourly-cycle hospitality management. It serves as the central nervous system for Airbnb hosts, boutique hotels, and serviced apartment operators.

**Core Philosophy:**

1. **Polymorphic Inventory:** Manage Beds, Rooms, Parking Spots, and Meeting Rooms in one system.  
2. **Agentic Workforce:** AI Agents handle 95% of guest comms, upselling, and review management autonomously.  
3. **Trust-Based Financials:** Automated splitting of every dollar between Owner, Manager, Vendor, and Tax Authority.

---

## **2\. Module I: Advanced Inventory & Distribution Engine**

*Derived from Cloudbeds & Mews*

**Goal:** Maximize distribution reach while strictly preventing double bookings via complex inventory logic.

### **2.1 Polymorphic Inventory Architecture**

* **Space Types:** System must support defined inventory classes:  
  * **Accommodation:** Entire Home, Private Room, Shared Bed (Dorm).  
  * **Ancillary:** Parking Spot, Meeting Room, Co-working Desk, Event Space.  
* **Parent/Child Dependency (Critical):**  
  * *Logic:* A "Villa" (Parent) consists of "Suite A" (Child) and "Suite B" (Child).  
  * *Rule 1:* Booking Parent blocks availability for Child A and Child B.  
  * *Rule 2:* Booking Child A blocks Parent, but leaves Child B available.  
* **Multi-Unit Clustering:**  
  * Ability to group 50 identical units under one "Inventory Type" (e.g., "Standard King") to optimize OTA placement.

### **2.2 The Channel Manager (Distribution)**

* **Connectivity:** Real-time 2-way API sync with:  
  * **Tier 1:** Airbnb, Vrbo, Booking.com, Expedia, Google Hotels.  
  * **Tier 2:** Agoda (Asia), TripAdvisor, Hopper.  
  * **Niche:** Marriott Homes & Villas, Plum Guide.  
* **Sync Requirements:**  
  * **Latency:** Availability updates \< 30 seconds. Rate updates \< 60 seconds.  
  * **Content API:** Push Photos, Amenities, and Policies from NEXUS to OTAs (Single Source of Truth).  
* **Multi-Rate Plans:**  
  * Support for "Derived Rates" (e.g., Non-Refundable \= Base Rate \- 10%).

---

## **3\. Module II: The Agentic AI Workforce**

*Derived from BoomAI, BestyAI, and Inntelo*

**Goal:** Deploy autonomous "Digital Employees" to handle specific domains of the business.

### **Skill A: The Guest Experience Agent (skill\_guest\_comms)**

* **Unified Inbox:** Aggregates Airbnb, Booking.com, Vrbo, SMS, WhatsApp, and Email.  
* **Intent Recognition:** Classifies inbound messages: *Inquiry, Booking Request, Check-in Help, Complaint, Review.*  
* **Knowledge Graph (RAG):**  
  * *Input:* Guest asks "How do I turn on the hot tub?"  
  * *Process:* Agent retrieves house\_manual.pdf for specific Unit ID.  
  * *Output:* "To turn on the hot tub, press the red button on the side panel. Here is a photo."  
* **Sentiment Guardrails:**  
  * If Sentiment Score \< 0.3 (Angry/Frustrated), **STOP** auto-reply and tag @HumanManager.

### **Skill B: The Revenue & Upsell Agent (skill\_revenue\_ops)**

* **Gap Night Logic (BestyAI):**  
  * *Trigger:* Calendar shows a 1 or 2-night "orphan" gap.  
  * *Action:* Agent messages the adjacent guests: *"Extend your stay by 1 night for 50% off?"*  
* **Attribute-Based Upselling:**  
  * *Trigger:* Guest books "Standard Room."  
  * *Action:* 72 hours pre-arrival, Agent emails: *"Upgrade to the Ocean View Suite for just $40/night? (It is currently vacant)."*  
* **Ancillary Sales:**  
  * Automated selling of Early Check-in / Late Check-out based on housekeeping schedule availability.

### **Skill C: The Review Management Agent (skill\_reputation)**

* **Review Solicitation:** Text guest 2 hours post-checkout: *"Safe travels\! We are leaving you a 5-star review."*  
* **Auto-Review Posting:** System posts a randomized 5-star review for the guest immediately to trigger the "Review Blind" on Airbnb.  
* **Bad Review Defense:** If a guest leaves \< 4 stars, AI drafts a professional, factual rebuttal for Manager approval.

---

## **4\. Module III: Operations, Housekeeping & Maintenance**

*Derived from Guesty, Amenitiz, and Breezeway*

**Goal:** Precision logistics execution between 11:00 AM (Checkout) and 3:00 PM (Check-in).

### **4.1 The "No-Login" Housekeeping App**

* **Access:** Cleaners receive a "Magic Link" via SMS (No username/password required).  
* **Workflow:**  
  1. **Clock In:** GPS Geofence validation.  
  2. **Checklist:** Interactive strip sheet (Linens, Towels, Coffee).  
  3. **Photo Gate:** Cleaner *cannot* mark "Ready" without uploading timestamped photos of Bed, Bathroom, and Kitchen.  
  4. **Damage Reporting:** "One-tap" upload for damages (e.g., stained carpet).  
  5. **Clock Out:** Triggers payment calculation.

### **4.2 Automated Maintenance Blocking**

* **OOO (Out of Order):** Hard block on calendar (Inventory \= 0).  
* **OOS (Out of Service):** Soft block (Inventory \= 0, but can be overridden).  
* **Logic:** If a "Critical" maintenance ticket (e.g., Broken AC) is created, AI checks for incoming guests.  
  * *If Guest Arriving:* Trigger "Emergency Relocation" protocol.  
  * *If Vacant:* Auto-create OOO block for estimated repair duration.

---

## **5\. Module IV: Financials, Trust Accounting & Folios**

*Derived from Guesty (Trust) and Mews (Folios)*

**Goal:** Enterprise-grade accounting for multi-stakeholder payouts.

### **5.1 The "Guest Folio" (Hotel-Style Tab)**

* **Capability:** Ability to add charges to a reservation *after* the initial booking.  
* **Use Cases:** Minibar consumption, Room Service, Spa, Damaged Towel fee.  
* **Payment Method:** "Card on File" tokenization via Stripe. Pre-authorization logic ($200 hold) released 24h post-checkout.

### **5.2 Advanced Trust Accounting Engine**

* **The Split Logic:** Upon receipt of $1,000 Booking:  
  * **Account A (Tax):** 12% Occupancy Tax auto-routed to segregated liability account.  
  * **Account B (Vendor):** $80 Cleaning Fee auto-routed to "Cleaning Reserve."  
  * **Account C (Manager):** 20% Commission auto-routed to "Operating Account."  
  * **Account D (Owner):** Remainder auto-routed to "Owner Wallet."  
* **Owner Statements:** Auto-generated PDF at month-end showing: Gross Revenue \- OTA Fees \- Mgmt Fees \- Repairs \= Net Payout.

---

## **6\. Module V: Compliance, Identity & IoT**

*Derived from CheKin, Minut, and CondoControl*

**Goal:** Legal compliance and asset protection.

### **6.1 Identity Verification (The "CheKin" Layer)**

* **Workflow:** Booking Confirmed $\rightarrow$ AI sends "Pre-Check-in Link".  
* **Process:** Guest scans Passport \+ Selfie. Biometric liveness check.  
* **Police Reporting:**  
  * *EU/Asia:* Auto-generation of police reports (e.g., *Schede Alloggiati* in Italy) and API submission to local authorities.  
* **Access Gate:** Smart Lock code is *only* revealed after ID verification is successful.

### **6.2 Party Prevention Grid**

* **Hardware Integration:** Minut / NoiseAware.  
* **Crowd Detection:** Monitor number of mobile devices via WiFi counting.  
* **Escalation Sequence:**  
  1. **Warning:** Noise \> 75dB for 10 mins $\rightarrow$ SMS to Guest.  
  2. **Intervention:** Noise continues $\rightarrow$ Automated Voice Call to Guest.  
  3. **Dispatch:** Noise continues $\rightarrow$ Alert Security Patrol / Owner.

---

## **7\. Module VI: Direct Brand Builder**

*Derived from Amenitiz*

**Goal:** Reduce OTA dependency by 30%.

### **7.1 No-Code Website Builder**

* **Templates:** "Luxury Villa," "Urban Loft," "Boutique Hotel."  
* **Booking Widget:** Embedded calendar with real-time availability.  
* **SEO Engine:** Auto-creates landing pages (e.g., "Vacation Rentals in Austin near Convention Center").

---

## **8\. Technical Specifications & Data Models**

### **8.1 Core Data Models (SQL)**

**Table: inventory\_units**

SQL

id: UUID  
property\_id: UUID  
parent\_unit\_id: UUID (Nullable, for split inventory)  
inventory\_type: Enum (Accommodation, Parking, Meeting)  
base\_rate: Decimal  
max\_occupancy: Integer  
smart\_lock\_id: String

**Table: reservations**

SQL

id: UUID  
guest\_id: UUID  
unit\_id: UUID  
channel\_source: Enum (Airbnb, Direct, Booking...)  
status: Enum (Pending, Confirmed, CheckedIn, CheckedOut)  
check\_in\_time: Timestamp  
check\_out\_time: Timestamp  
folio\_balance: Decimal  
id\_verified: Boolean

**Table: trust\_ledger\_entries**

SQL

id: UUID  
reservation\_id: UUID  
amount: Decimal  
recipient\_type: Enum (Owner, Manager, Vendor, TaxAuthority)  
status: Enum (Held, Paid, Refunded)

### **8.2 Required API Integrations**

1. **Plaid/Stripe Connect:** For split payouts and banking.  
2. **Twilio/SendGrid:** For the Universal Inbox.  
3. **OpenAI / Anthropic API:** For the Agent Skills runtime.  
4. **Seam / Igloohome:** For Smart Lock control.  
5. **Channex / Rentals United:** Middleware for OTA connectivity (Option to build direct vs buy middleware).

---

## **9\. Success Metrics (KPIs)**

| Metric | Target | Definition |
| :---- | :---- | :---- |
| **Automation Rate** | \> 90% | Percentage of guest threads requiring zero human replies. |
| **Sync Latency** | \< 30s | Time from Booking on Airbnb to Block on Vrbo. |
| **Direct Mix** | \> 20% | Percentage of bookings coming via Direct Website vs OTAs. |
| **Upsell Attach Rate** | \> 15% | Percentage of bookings adding Early Check-in or Gap Night. |
| **Turnover Compliance** | 100% | Percentage of cleanings with verified photos before Check-in. |



