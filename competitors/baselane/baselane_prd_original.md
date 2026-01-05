# Product Requirements Document: Baselane

**A Comprehensive Financial and Property Management Platform for Real Estate Investors**

**Author:** Manus AI  
**Date:** January 5, 2026  
**Version:** 1.0

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Product Overview](#2-product-overview)
3. [User Personas](#3-user-personas)
4. [Functional Requirements](#4-functional-requirements)
5. [Non-Functional Requirements](#5-non-functional-requirements)
6. [Glossary](#6-glossary)

---

## 1. Executive Summary

This Product Requirements Document (PRD) provides a comprehensive specification for building a financial and property management platform designed specifically for real estate investors and landlords. The platform consolidates banking, bookkeeping, rent collection, tenant management, and property management into a single, unified solution.

The platform addresses the fragmented nature of landlord financial management by providing integrated banking services with competitive interest rates, automated bookkeeping aligned with IRS Schedule E categories, streamlined rent collection with automated reminders and late fees, comprehensive tenant screening and lease management, and a robust partner ecosystem for insurance, loans, and professional services.

This document details every functional capability required to replicate the complete feature set, organized by module and user workflow. The focus is on functionality and user experience rather than technical implementation details.

---

## 2. Product Overview

The platform serves as an all-in-one financial operating system for landlords, combining the functionality of a bank, accounting software, property management system, and tenant portal into a single application.

### Core Value Propositions

The platform delivers value through several key mechanisms. First, it provides **unified financial management** by consolidating all property finances in one place, eliminating the need for multiple banking relationships and accounting tools. Second, it offers **automated bookkeeping** where transactions are automatically categorized to Schedule E tax categories and assigned to specific properties, dramatically reducing manual data entry. Third, **streamlined rent collection** enables landlords to collect rent via ACH or credit card with automated invoicing, reminders, and late fee assessment. Fourth, **competitive banking** offers high-yield savings accounts with up to 2.63% APY, no monthly fees, and no minimum balances. Finally, **integrated services** connect landlords with trusted partners for insurance, loans, legal services, and property maintenance.

### Target Market

The platform targets individual landlords managing one to fifty rental properties, real estate investors building rental portfolios, property managers overseeing multiple properties, and small LLCs and business entities holding real estate assets.

---

## 3. User Personas

### Primary Persona: The Independent Landlord

The independent landlord is an individual who owns between one and ten rental properties, either as a sole proprietor or through an LLC. They handle most property management tasks themselves, including tenant communication, maintenance coordination, and financial management. Their primary pain points include tracking income and expenses across multiple properties, preparing for tax season, and managing rent collection manually. They value simplicity, automation, and tools that save time.

### Secondary Persona: The Growing Investor

The growing investor is actively expanding their rental portfolio and may own between ten and fifty properties. They may work with property managers, accountants, or other team members. Their primary pain points include coordinating with team members, maintaining visibility across a larger portfolio, and accessing capital for new acquisitions. They value scalability, collaboration features, and access to financing.

### Tertiary Persona: The Property Manager

The property manager oversees properties on behalf of other owners. They need to track finances separately for each owner while maintaining their own business operations. Their primary pain points include managing multiple owner relationships, generating owner reports, and handling rent collection at scale. They value multi-entity support, reporting capabilities, and efficient workflows.

---

## 4. Functional Requirements

### 4.1 User Onboarding and Setup Guide

The onboarding experience is critical for user adoption and retention. The platform provides a structured setup guide that walks new users through all essential configuration steps.

#### 4.1.1 Setup Guide Structure

The setup guide presents as an expandable accordion interface with multiple sections, each containing specific setup tasks. Users can expand any section to view detailed instructions and action buttons. Progress is tracked visually, showing completed and pending tasks.

#### 4.1.2 Banking Setup Section

This section guides users through establishing their banking relationship with the platform.

| Task | Description | User Actions |
|------|-------------|--------------|
| Open a Banking Account | Initiate the bank account application process | Click "Open Account" to start application flow |
| Set Up Checking & Savings | Create additional accounts for organization | Click "Add Account" from banking dashboard |
| Fund Your Accounts | Transfer money into new accounts | Initiate transfer from external account |
| Assign Properties to Accounts | Link properties to specific accounts | Select property and assign to account |

The banking setup section emphasizes key benefits: unlimited checking and savings accounts, up to 2.63% APY, no monthly fees, and no minimum balances.

#### 4.1.3 Cash Flow Centralization Section

This section helps users consolidate their financial operations within the platform.

| Task | Description | User Actions |
|------|-------------|--------------|
| Collect Rental Payments | Set up rent collection for properties | Choose between monthly rent or short-term payouts |
| Add Vendors | Configure vendor relationships | Enter vendor details and payment preferences |
| Migrate Payments | Transfer existing payment setups | Import or manually configure existing arrangements |

For rent collection, users can choose between two paths: collecting monthly rent for traditional long-term rentals with automated reminders and late fees, or collecting short-term payouts for vacation rentals from platforms like Airbnb and Vrbo.

#### 4.1.4 Bookkeeping Automation Section

This section guides users through setting up automated financial tracking.

| Task | Description | User Actions |
|------|-------------|--------------|
| Import Bookkeeping Data | Bring in existing financial records | Upload CSV or connect existing accounts |
| Categorize Transactions | Tag transactions to categories | Review and categorize imported transactions |
| Automate Tracking | Set up automation rules | Configure rules for automatic categorization |

### 4.2 Banking Module

The banking module provides integrated banking services specifically designed for real estate investors.

#### 4.2.1 Account Types

The platform supports two primary account types to accommodate different business structures.

**Sole Proprietor Accounts** are designed for individual landlords operating without a formal business entity. The application process collects personal information including legal name, date of birth, address, and government-issued identification for verification.

**Business Accounts** are designed for LLCs, corporations, and other business entities. The application process collects business information including legal business name, EIN, entity type, state of incorporation, and control person information for regulatory compliance.

#### 4.2.2 Account Dashboard

The banking dashboard provides a comprehensive overview of all accounts and financial activity.

| Metric | Description | Display Format |
|--------|-------------|----------------|
| Total Balance | Aggregate balance across all accounts | Currency with cents |
| This Month | Net inflows and outflows for current month | Currency with direction indicator |
| Eligible APY | Current interest rate tier | Percentage |
| Lifetime Interest | Total interest earned since account opening | Currency |

#### 4.2.3 Interest Rate Structure

The platform offers tiered interest rates based on account balance, incentivizing users to maintain higher balances.

| Tier | APY Rate |
|------|----------|
| Base | 0.95% |
| Tier 2 | 1.30% |
| Tier 3 | 1.69% |
| Tier 4 | 2.03% |
| Tier 5 | 2.39% |
| Maximum | 2.63% |

### 4.3 Transfers and Payments

The transfers and payments module enables users to move money between accounts and make payments to vendors and other parties.

#### 4.3.1 Transfer Types

| Transfer Type | Description | Processing Time |
|---------------|-------------|-----------------|
| Internal Transfer | Between Baselane accounts | Instant |
| External Transfer (Outbound) | To external bank account | 1-3 business days |
| External Transfer (Inbound) | From external bank account | 1-3 business days |
| Scheduled Transfer | Recurring or future-dated transfer | As scheduled |

#### 4.3.2 Payment Capabilities

The platform supports various payment methods for different use cases.

| Payment Method | Use Case | Features |
|----------------|----------|----------|
| ACH Payment | Vendor payments, bill pay | Low cost, 1-3 day processing |
| Wire Transfer | Large or urgent payments | Same-day processing, higher fees |
| Debit Card | Point-of-sale purchases | Instant, spend controls available |

#### 4.3.3 Debit Card Features

Physical and virtual debit cards are available with the following capabilities:

| Feature | Description |
|---------|-------------|
| Physical Cards | Traditional debit cards for in-person use |
| Virtual Cards | Instant digital cards for online purchases |
| Spend Controls | Set spending limits and merchant restrictions |
| Account Linking | Cards linked to specific checking accounts |

### 4.4 External Account Integration

The external accounts module allows users to connect bank accounts and credit cards from other financial institutions.

#### 4.4.1 Supported Account Types

| Account Type | Capabilities |
|--------------|--------------|
| Bank Accounts | Collect rent, import transactions, fund Baselane accounts |
| Credit Cards | Import transactions for expense tracking |

#### 4.4.2 Connection Methods

Users can connect external accounts through two methods:

**Plaid Integration** provides automated, secure connection using bank credentials. This is the recommended method for most users, offering instant account verification and automatic transaction import.

**Manual Entry** allows users to enter account and routing numbers directly. This method is available for users who prefer not to use Plaid or whose financial institution is not supported.

### 4.5 Transaction Management

The transaction management module provides a comprehensive ledger for tracking all property-related financial activity.

#### 4.5.1 Transaction Categories

The category system is aligned with IRS Schedule E for rental property tax reporting, organized into hierarchical groups.

**Revenue Categories:**

| Category | Subcategories |
|----------|---------------|
| Fees & Other Revenue | Application fees, late fees, pet fees, etc. |
| Rents | Monthly rent, security deposits, etc. |

**Operating Expense Categories:**

| Category | Description |
|----------|-------------|
| Advertising | Marketing and advertising costs |
| Auto & Travel | Vehicle and travel expenses |
| Cleaning & Maintenance | Cleaning services and routine maintenance |
| Commissions | Agent and broker commissions |
| Depreciation | Asset depreciation |
| Insurance | Property and liability insurance |
| Legal & Professional Fees | Attorney, accountant, and consultant fees |
| Management Fees | Property management costs |
| Other Operating Expenses | Miscellaneous operating costs |
| Repairs | Property repairs |
| Supplies | Maintenance and office supplies |
| Taxes | Property taxes and other taxes |
| Utilities | Water, electric, gas, trash, etc. |

### 4.6 Reporting and Analytics

The reporting module provides financial insights and reports for portfolio analysis and decision-making.

#### 4.6.1 Available Reports

| Report Type | Description | Filters Available |
|-------------|-------------|-------------------|
| Net Cash Flow | Income minus expenses over time | Date range, property, category |
| Income Statement | Detailed revenue and expense breakdown | Date range, property |
| Expense Report | Categorized expense analysis | Date range, property, category |
| Property Performance | Per-property financial metrics | Date range, property |

### 4.7 Tax Center

The tax center provides tools and resources for tax preparation and compliance.

#### 4.7.1 Tax Package Generation

| Document | Description |
|----------|-------------|
| Schedule E Summary | Pre-filled Schedule E data from categorized transactions |
| 1099 Forms | Generated 1099s for contractors paid through platform |
| Year-End Summary | Comprehensive annual financial summary |

#### 4.7.2 Tax Preparation Support

| Feature | Description |
|---------|-------------|
| Category Mapping | All categories aligned with Schedule E line items |
| Accountant Access | Share reports with tax professional |
| Audit Trail | Complete transaction history with receipts |

### 4.8 Property Management

The property management module provides a centralized database for all rental properties.

#### 4.8.1 Property Information

| Field | Required | Description |
|-------|----------|-------------|
| Property Name | Yes | Nickname for easy identification |
| Address | Yes | Full street address |
| City | Yes | City name |
| State | Yes | State abbreviation |
| Zip Code | Yes | Postal code |
| Property Type | Yes | Single-family, multi-family, condo, etc. |
| Number of Units | Yes | Total units in property |

#### 4.8.2 Property-Account Association

Each property can be linked to specific bank accounts for automatic transaction categorization and cash flow tracking.

| Association | Purpose |
|-------------|---------|
| Operating Account | Primary account for rent deposits and expenses |
| Security Deposit Account | Separate account for tenant deposits |
| Reserve Account | Savings account for capital expenditures |

### 4.9 Tenant Screening

The tenant screening module provides comprehensive background checks for prospective tenants.

#### 4.9.1 Screening Reports

| Report Type | Contents |
|-------------|----------|
| Credit Report | Credit score, payment history, outstanding debts |
| Criminal Background | Criminal history search |
| Eviction History | Prior eviction records |
| Income Verification | Employment and income confirmation |

#### 4.9.2 Screening Provider

The platform partners with TransUnion SmartMove for screening services, providing industry-standard reports with nationwide coverage.

### 4.10 Lease Agreements

The lease agreements module provides tools for creating, managing, and executing rental agreements.

#### 4.10.1 Lease Creation Options

| Option | Description |
|--------|-------------|
| Draft & E-Sign | Create new lease using platform templates |
| Upload Existing | Upload previously created lease document |

#### 4.10.2 E-Signature

| Feature | Description |
|---------|-------------|
| Digital Signatures | Legally binding electronic signatures |
| Signature Tracking | Monitor who has signed |
| Automatic Reminders | Remind unsigned parties |
| Completed Document | Automatically distributed to all parties |

### 4.11 Rent Collection

The rent collection module automates the process of collecting rent from tenants.

#### 4.11.1 Payment Methods

| Method | Processing Time | Fees |
|--------|-----------------|------|
| ACH (Bank Transfer) | 5 business days (standard) or 2 days (Smart Plan) | $2 per transaction (waived for Baselane Banking) |
| Credit Card | 1-2 business days | Percentage of transaction |
| Debit Card | 1-2 business days | Flat fee per transaction |

#### 4.11.2 Automation Features

| Feature | Description |
|---------|-------------|
| Recurring Invoices | Automatically generate monthly invoices |
| Payment Reminders | Send reminders before due date |
| Late Fee Assessment | Automatically apply late fees after grace period |
| Receipt Generation | Send receipts upon payment |

### 4.12 Tenant Management

The tenant management module provides a centralized database for all tenant information.

#### 4.12.1 Tenant Portal

Tenants have access to a self-service portal with the following capabilities:

| Feature | Description |
|---------|-------------|
| Payment Portal | Make one-time or recurring payments |
| Payment History | View past payments and receipts |
| Lease Documents | Access signed lease agreements |
| Maintenance Requests | Submit and track maintenance issues |

### 4.13 Partner Integrations

The platform provides access to a curated network of partner services through an integrated marketplace.

#### 4.13.1 Partner Categories

| Category | Services |
|----------|----------|
| Insurance | Landlord insurance, liability coverage |
| Lending | Rental property loans, refinancing |
| Legal & Professional | LLC formation, legal document templates |
| Property Management | Contractor booking, maintenance services |
| Tax Preparation | CPA services, tax filing |
| Brokerage | Property acquisition, market analysis |

#### 4.13.2 Insurance Partners

The platform partners with insurance providers to offer landlord-specific coverage:

| Coverage Type | Description |
|---------------|-------------|
| Dwelling | Building structure coverage |
| Personal Property | Optional coverage for landlord belongings |
| Loss of Use | Coverage during property repairs |
| Loss of Rent | Income replacement during vacancy |
| Liability | Protection against lawsuits |
| Medical Payments | Guest injury coverage |

#### 4.13.3 Lending Partners

The platform connects landlords with lenders offering various loan products:

| Loan Type | Description |
|-----------|-------------|
| Conventional | Traditional mortgage financing |
| DSCR | Debt Service Coverage Ratio loans |
| Fix and Flip | Short-term renovation financing |
| BRRRR | Buy, Rehab, Rent, Refinance, Repeat strategy |
| New Construction | Ground-up development financing |
| Portfolio | Loans for multiple properties |

### 4.14 User Account and Settings

The account and settings module provides user profile management and platform configuration options.

#### 4.14.1 Workspace Settings

Workspace settings control organization-level configuration:

| Tab | Description |
|-----|-------------|
| Members | Team member management (Smart Plan) |
| Business Profile | Business information displayed to tenants |
| Rent Collection | ACH fee preferences |
| Transaction Categories | Custom category management (Smart Plan) |

**Members Tab (Smart Plan Feature):**

| Role | Permissions |
|------|-------------|
| Owner | Full access to all features |
| Business Partner | Configurable access levels |
| Bookkeeper | Financial data access |
| Property Manager | Property and tenant management |

#### 4.14.2 Connected Apps

| Integration | Description |
|-------------|-------------|
| QuickBooks | Sync transaction data with QuickBooks |
| BiggerPockets Pro | Unlock Smart subscription benefits |

### 4.15 Premium Subscription (Smart Plan)

The Smart Plan is a premium subscription tier offering advanced automation and collaboration features.

#### 4.15.1 Pricing

| Component | Details |
|-----------|---------|
| Trial Period | 30 days free |
| Monthly Price | $25/month |
| Cancellation | Cancel anytime |

#### 4.15.2 Smart Plan Features

| Feature | Description |
|---------|-------------|
| Advanced Tagging Rules | Auto-tag transactions based on recipient, amount, or account |
| Auto-tag Assistant | AI-powered category suggestions for every transaction |
| Auto-receipt Match | Automatic matching of uploaded receipts to transactions |
| Custom Categories | Create and customize category structures |
| Minimum Balance Transfers | Automatic account top-ups when balance is low |
| 2-day Rent | Fast-tracked rent deposits (2 days vs. 5 days) |
| Shared Access | Team collaboration with configurable permissions |
| Priority Support | Dedicated, fast support response |

---

## 5. Non-Functional Requirements

### 5.1 Security

| Requirement | Description |
|-------------|-------------|
| Encryption | 256-bit SSL encryption for all data transmission |
| Authentication | Multi-factor authentication support |
| Credential Isolation | Third-party credentials never stored |
| Compliance | SOC 2 Type II compliance |
| FDIC Insurance | Bank deposits insured up to $250,000 |

### 5.2 Performance

| Requirement | Target |
|-------------|--------|
| Page Load Time | Under 3 seconds |
| Transaction Processing | Real-time for internal transfers |
| Report Generation | Under 10 seconds for standard reports |
| Uptime | 99.9% availability |

---

## 6. Glossary

| Term | Definition |
|------|------------|
| ACH | Automated Clearing House, electronic bank-to-bank transfer |
| APY | Annual Percentage Yield, interest rate accounting for compounding |
| BRRRR | Buy, Rehab, Rent, Refinance, Repeat investment strategy |
| DBA | Doing Business As, trade name for a business |
| DSCR | Debt Service Coverage Ratio, loan qualification metric |
| EIN | Employer Identification Number, IRS-issued business identifier |
| KYC | Know Your Customer, identity verification process |
| LLC | Limited Liability Company, business entity type |
| LTV | Loan-to-Value ratio, loan amount relative to property value |
| Schedule E | IRS form for reporting rental property income and expenses |
| Smart Plan | Premium subscription tier with advanced features |

---

*This document provides a comprehensive specification for replicating the Baselane platform's functionality. Implementation teams should use this as a reference for feature development, ensuring all described capabilities are included in the final product.*

