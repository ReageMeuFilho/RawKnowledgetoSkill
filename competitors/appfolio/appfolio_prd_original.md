# AppFolio Property Management Platform PRD

**Version:** 1.0  
**Date:** January 5, 2026  
**Author:** Manus AI

## 1. Executive Summary

AppFolio is a comprehensive, cloud-based property management platform serving as a **single system of record** for property management companies. The platform integrates accounting, marketing, leasing, maintenance, and communication functionalities with **native AI integration (Realm-X)**.

| Target Market | Core Value Proposition |
|---------------|------------------------|
| Property management companies (residential, commercial, student housing, HOA) | All-in-one platform with native AI automation, eliminating need for multiple software solutions |

---

## 2. Strategic Positioning

### Target Segments

| Segment | Key Needs |
|---------|-----------|
| **Property Manager** | Centralized dashboard, automated workflows, mobile access |
| **Leasing Agent** | Lead management, online applications, virtual showings |
| **Maintenance Coordinator** | Centralized work orders, mobile technician access |
| **Accountant** | Robust accounting, bank reconciliation, reporting |
| **Resident/Tenant** | Online payments, maintenance requests, lease access |
| **Property Owner** | Financial reports, property performance visibility |
| **Board Member (HOA)** | Association financials, architectural review |
| **Investor** | Investment performance, document sharing |

### Property Types Supported

- **Residential** (single-family, multifamily)
- **Commercial**
- **Student Housing**
- **Community Associations (HOA)**

---

## 3. Core Platform Architecture

### 3.1 Technical Foundation
- **Microservices-based** architecture
- **API-First Design** (RESTful)
- **Multi-tenant** cloud-native
- **Mobile-first** design

### 3.2 AI-Native Integration (Realm-X)
- **Realm-X Assistant**: AI chatbot for platform navigation
- **Realm-X Flows**: Customizable automated workflows
- **Realm-X Messages**: Auto-respond to common inquiries
- **Smart Bill Entry**: AI invoice data extraction

### 3.3 Security
- Data encryption (rest + transit)
- Role-Based Access Control (RBAC)
- SOC 2 Type 2 compliance

---

## 4. Core Modules

### 4.1 Communication & Service
- **Centralized Communication Hub** - Unified inbox (email, SMS, portal)
- **Resident Portal** - Rent payments, maintenance, documents
- **Owner Portal** - Financial statements, performance
- **Vendor Portal** - Work orders, invoices
- **Bulk Communication** - Mass email/SMS
- **Document Management** - Centralized repository
- **eSignatures** - Remote lease signing
- **Surveys** - Resident feedback

### 4.2 Accounting & Reporting
- **General Ledger** - Full chart of accounts
- **Accounts Payable** - Vendor bills, payments
- **Accounts Receivable** - Tenant charges, payments
- **Bank Reconciliation** - Automated matching
- **Online Payments** - Credit card, eCheck
- **Financial Reporting** - P&L, balance sheet, cash flow
- **Budgeting & Forecasting** - Property budgets
- **CAM Tracking** - Commercial area maintenance
- **Loan Tracking** - Automated transactions
- **Tenant Debt Collections** - Automated workflows

### 4.3 Marketing & Leasing
- **Leasing CRM** - Lead tracking, pipeline
- **AI Leasing Assistant** - 24/7 autonomous response + tours
- **Dynamic Pricing (Leasing Signals)** - Market-based rent optimization
- **Vacancy Marketing** - Syndication + property websites
- **Online Applications** - Mobile-friendly
- **Tenant Screening** - Background, credit, fraud detection
- **Online Leases & eSignatures** - Remote signing
- **Renewal Automation** - Automated offers + tracking
- **Virtual & Self-Guided Tours** - Remote touring
- **Rent-By-The-Bed** - Student housing

### 4.4 Maintenance
- **AI Maintenance Coordinator** - Full workflow automation
- **Online Maintenance Requests** - Photos + descriptions
- **Work Order Management** - Assignment, tracking
- **Automated Scheduling & Billing** - Drag-drop + auto-invoice
- **Mobile Inspections** - Move-in/out, property walks
- **Unit Turn Board** - Visual make-ready dashboard
- **Vendor Management & Network** - Pre-approved vendors
- **Auditing & Compliance** - Complete audit trail

### 4.5 Investment Management (NEW CATEGORY!)
- **Investor CRM** - Relationship management
- **Investor Portal** - Performance dashboards, K-1s
- **Capital Raising & Syndication** - Deal interest tracking
- **Distribution Management** - Waterfall calculations
- **Asset & Portfolio Management (Alpha™)** - AI insights
- **Reporting & Document Management** - Branded reports
- **Fund & Entity Visualization** - Structure visualization

### 4.6 Community Associations / HOA (NEW CATEGORY!)
- **Association Management** - Board, committees, rules
- **Homeowner Portal** - Dues, architectural requests
- **Architectural Review Workflow** - Submission to approval
- **Violation Management** - Mobile + automated letters
- **Association Calendar** - Events, meetings
- **Multiple Fund Accounting** - Reserve/operating funds
- **Board Approvals** - Invoice/bid approval workflow

### 4.7 Workflow Automation
- **Workflow Engine (Realm-X Flows)** - Visual automation builder
- **Pre-Built Templates** - Common PM processes
- **Workflow Autotriggers** - Event/date-based
- **Workflow Reporting** - Status tracking
- **Auditing & Compliance** - Full audit log
- **Two-Factor Authentication** - 2FA security
- **Custom User Roles** - Granular permissions

---

## 5. Integration Ecosystem

### AppFolio Stack™
- **Integration Marketplace** - Third-party apps
- **Read/Write API** - Full data access
- **App Partner Integrations** - Zillow, Zumper, Apartments.com, Lula
- **Solution Partner Network** - Certified consultants

### Supported Integrations
- Listing syndication (Zillow, Zumper, Apartments.com)
- Vendor networks (Lula)
- Accounting (external systems via API)

---

## 6. Mobile Applications

### Property Manager App
- Full platform access
- Mobile inspections
- Work order management
- Leasing on the go
- Photo capture
- **Offline mode**

### Resident/Owner Portal App
- Online payments
- Maintenance requests
- Document access
- Push notifications

### Investor Portal App
- Investment dashboard
- Document access (K-1s)

---

## 7. Pricing Tiers

| Tier | Target | Key Features |
|------|--------|--------------|
| **Core** | Small-mid PM companies | Full accounting, marketing, leasing, work orders, inspections, mobile, AI assistant |
| **Plus** | Growing businesses | + Affordable/Student Housing, advanced budgeting, custom fields, Realm-X Flows, premium integrations, read-only API |
| **Max** | Enterprise | + Leasing CRM, dynamic pricing (Leasing Signals), full API, dedicated CSM, AI Performers |

---

## 8. Non-Functional Requirements

| Category | Requirement |
|----------|-------------|
| Performance | Sub-second response times |
| Scalability | Horizontal scaling |
| Availability | 99.9% uptime |
| Usability | Intuitive UI, minimal training |
| Accessibility | WCAG 2.1 AA compliance |
| Security | SOC 2 Type 2 compliance |

---

## 9. Core Data Entities

| Category | Entities |
|----------|----------|
| **Property** | Properties, Property Groups, Units, Listings |
| **People** | Tenants, Owners, Vendors, Users, Leads |
| **Financial** | Bank Accounts, Bills, Charges, GL Accounts |
| **Leasing** | Applications, Showings, Leases |
| **Maintenance** | Work Orders, Inspections |
| **HOA** | Associations, CA Units, Homeowners, Violations |

---

*AppFolio represents an enterprise-grade, AI-native property management platform with unique Investment Management and HOA capabilities - a significant expansion beyond STR into full property management.*

