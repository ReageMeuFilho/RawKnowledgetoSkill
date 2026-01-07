# Hostfully Research

## 1. Company Overview

Hostfully is a cloud-based, all-in-one property management platform for short-term rentals. They provide a suite of tools to automate and streamline operations for property managers. Their target market is vacation rental businesses of all sizes.

**Products:**
* Property Management Platform (PMP)
* Digital Guidebooks

**Verticals:**
* Short-Term Rentals (STR)

**Market Position:**
Hostfully positions itself as a leading PMS in the vacation rental industry, with a strong emphasis on integrations and automation. They are a preferred or premium partner with major booking channels like Airbnb, Vrbo, and Booking.com.

**Strengths:**
* Extensive integrations with over 100 partners
* Open API for custom solutions
* Strong focus on automation and streamlining workflows
* Comprehensive feature set covering all aspects of property management

**Limitations:**
* Primarily focused on STR, may not be suitable for other property types.
* Lacks native features for some accounting functions like bank reconciliation and trust accounting, relying on third-party integrations.

## 2. Workflow Deep Dives

### 1. Owner Statements / Owner Payouts

Hostfully allows property managers to generate and share booking reports with property owners through the Owner Portal. The process is as follows:

**Steps:**

1.  **Create a booking report:** From the 'Reports' page, select the owner and date range for the report.
2.  **Generate a booking statement:** This creates a statement with three sections: Booking Report, Owner Adjustments Report, and Financial Report.
3.  **Publish the statement:** The statement can be published to the owner's account, and the owner is notified by email.

**Inputs:**

*   Owner selection
*   Date range

**Outputs:**

*   Booking Report (PDF or Excel)
*   Owner Statement (published to Owner Portal)

**Roles/Permissions:**

*   Property Manager: Generates and publishes reports.
*   Owner: Views reports in the Owner Portal.

**Edge Cases/Exception Handling:**

*   White-labeled sites: Owners must log in through the white-labeled URL to view statements.

**Common Failure Modes:**

*   Owners being unable to access statements if they don't use the correct URL.

### 2. Bank Reconciliation

Hostfully does not have a built-in bank reconciliation feature. Instead, it integrates with third-party accounting software like Clearing to provide this functionality. The integration with Clearing allows for automated bookkeeping, reconciliation, and efficient payout processes.

**Steps (with Clearing integration):**

1.  **Turn on the integration:** Enable the Clearing integration in Hostfully's settings.
2.  **Configure properties:** Toggle on the properties to be synced with Clearing.
3.  **Initialize in Clearing:** Connect to Hostfully from the Clearing dashboard using the Hostfully Agency UID.
4.  **Confirm and configure assets:** Properties are automatically pulled into Clearing, where they can be named and grouped.

**Inputs:**

*   Hostfully property and booking data
*   Bank account transactions

**Outputs:**

*   Detailed records for each line item within a transaction
*   Streamlined trust accounting setup

**Roles/Permissions:**

*   Property Manager: Sets up and manages the integration.

**Edge Cases/Exception Handling:**

*   Properties not showing up in Clearing can be refreshed.

**Common Failure Modes:**

*   Incorrect Agency UID entered during setup.

### 3. AP: invoice intake → coding → approvals → payments

Hostfully does not have a native AP workflow. Instead, it integrates with third-party applications like EZcare to manage maintenance work orders and invoicing. With the EZcare integration, users can:

**Steps (with EZcare integration):**

1.  **Auto-assign maintenance work orders:** Track time and parts used for each job.
2.  **Invoice from the mobile app:** Instantly create timesheet and invoice reports.
3.  **Export to accounting:** Roll up and export invoice data to accounting software.

**Inputs:**

*   Maintenance work orders
*   Time and parts data

**Outputs:**

*   Invoices
*   Timesheet reports

**Roles/Permissions:**

*   Field staff: Use the mobile app to track work and create invoices.
*   Property Manager: Manages the integration and accounting export.

**Edge Cases/Exception Handling:**

*   Misplaced receipts and late billing are minimized by using the mobile app.

**Common Failure Modes:**

*   Issues with the EZcare integration or data syncing.

### 4. AR: rent roll → collections → notices → adjustments

Hostfully allows for the management of rent and other charges through its 'Fees, Taxes and Policies' settings. This serves as a quasi-rent roll, allowing property managers to define and apply various charges to bookings.

**Steps:**

1.  **Set up fees and taxes:** Define various fees and taxes, such as cleaning fees, pet fees, and rental taxes.
2.  **Roll fee into rent:** Optionally, fees can be rolled into the rent, so they are not displayed as separate line items to the guest.
3.  **Apply to properties and channels:** Fees and taxes can be applied to all or selected properties, and can be mapped to specific booking channels.

**Inputs:**

*   Fee and tax definitions (name, value, scope, etc.)
*   Property and channel selections

**Outputs:**

*   A comprehensive breakdown of charges for each booking.

**Roles/Permissions:**

*   Property Manager: Sets up and manages fees, taxes, and policies.

**Edge Cases/Exception Handling:**

*   Channel-specific fee and tax mapping to ensure compliance with each platform's requirements.

**Common Failure Modes:**

*   Incorrectly configured fees or taxes leading to inaccurate charges.
*   Syncing delays between Hostfully and booking channels.

### 5. Trust/escrow/security deposit handling

Hostfully does not have a native trust accounting feature. It relies on third-party integrations with platforms like VRPlatform and Clearing to provide this functionality. The VRPlatform integration, for example, offers a standalone trust accounting platform called VRTrust.

**Steps (with VRPlatform integration):**

1.  **Sync data:** Reservation and fee details are synced from Hostfully and payment processors into VRTrust.
2.  **Real-time updates:** Accounting entries are updated in real-time when reservations change or are canceled.
3.  **Capture payouts:** Stripe and Airbnb payouts are captured with full fee-level detail.
4.  **Apply rules:** Revenue splits, taxes, and fees are applied according to property-specific rules.
5.  **Generate statements:** Custom owner statements are automatically created and published through a secure online portal.

**Inputs:**

*   Hostfully reservation and fee data
*   Payment processor data

**Outputs:**

*   Trust accounting records
*   Owner statements

**Roles/Permissions:**

*   Property Manager: Sets up and manages the integration.

**Edge Cases/Exception Handling:**

*   The integration handles changes and cancellations to reservations automatically.

**Common Failure Modes:**

*   Issues with the VRPlatform integration or data syncing.

### 6. Reserves (HOA/Condo): operating vs reserves management

Hostfully is primarily designed for short-term rentals and does not have specific features for managing HOA/Condo reserves.

### 7. Month-end close checklist + reporting pack

Hostfully does not have a dedicated month-end close checklist feature. However, it provides a range of financial reports that can be used for month-end closing, including:

*   Booking reports
*   Owner statements
*   Enhanced reporting with custom queries

These reports can be exported to CSV or HTML for further analysis and inclusion in a reporting pack.

## 3. Data Model and Artifacts

**Data Model Entities:**

*   Property
*   Unit
*   Owner
*   Guest
*   Vendor (via integrations)
*   GL Account (via integrations)
*   Fund (via integrations)
*   Bank Account (via integrations)

**Artifacts:**

*   Booking Reports (PDF, Excel)
*   Owner Statements (PDF, Excel)
*   Enhanced Reports (CSV, HTML)
*   Invoices (via integrations)

## 4. Skill Candidates

*   **CP-001:** Generate Owner Statements
*   **CP-002:** Process Owner Payouts
*   **FIN-001:** Reconcile Bank Accounts (via integration)
*   **AP-001:** Process Invoices (via integration)
*   **AR-001:** Manage Rent Roll
*   **TR-001:** Handle Security Deposits
*   **REP-001:** Generate Financial Reports
*   **TRE-001:** Capture Payouts

## 5. Treasury Capture Opportunities

*   **Payout Calculation:** The point where owner payouts are calculated and disbursed presents an opportunity for an AI agent to own the approval and execution of these payments.
*   **Fund Segregation:** In a trust accounting setup (via integration), an AI agent could manage the segregation of funds between operating and trust accounts.

## 6. Training Data Candidates

*   **Example Artifacts:** Sample booking reports, owner statements, and invoices can be used to train an AI to understand and process these documents.
*   **Edge Cases:** The handling of white-labeled sites for owner statements and channel-specific fee mapping provides valuable edge cases for training.
*   **Evaluation Scenarios:** Scenarios involving incorrect fee calculations, syncing delays, and integration failures can be used to evaluate the AI's ability to handle exceptions and resolve issues.
