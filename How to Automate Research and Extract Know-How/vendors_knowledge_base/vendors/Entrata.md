# Entrata Knowledge Document

## 1. Company Overview

Entrata is a comprehensive property management software provider that offers a unified platform for various property types, including multifamily, student, affordable, military, and commercial housing. Founded in 2003, the company aims to streamline property management operations, enhance the resident experience, and improve financial performance for its clients. Entrata's platform is built on an open-access, single-login system, providing a centralized solution for managing the entire property lifecycle.

| Feature | Description |
| :--- | :--- |
| **Products** | Entrata offers a suite of products covering property operations, AI and automation, resident experience, and analytics. |
| **Verticals** | The company serves a wide range of verticals, including multifamily, student housing, affordable housing, military housing, and commercial properties. |
| **Market Position** | Entrata is a leading provider in the property management software market, known for its all-in-one platform and focus on AI and automation. |
| **Strengths** | Key strengths include a comprehensive platform, a strong emphasis on innovation with AI, a user-friendly interface, and broad market coverage. |
| **Limitations** | While the platform is robust, the reliance on partnerships for certain features (e.g., Plaid for bank reconciliation, Finch for payroll) may introduce external dependencies. |

## 2. Workflow Deep Dives

### Accounts Payable: Invoice Intake, Coding, and Approvals

A detailed Standard Operating Procedure (SOP) for invoice entry in Entrata reveals a structured workflow. Property staff are responsible for entering invoice details and coding, while approvers (such as property managers) review and approve them. The corporate or AP supervisor oversees the entire process. The system includes features to prevent duplicate invoice entries and allows for the use of recurring invoice templates. Invoices can also be matched with purchase orders, which auto-fills some of the data.

### Accounts Receivable: Collections and Notices

Entrata provides a comprehensive collections workflow, as detailed in its user guide. The process begins with setting up collections parameters, including the threshold for sending an account to collections and the timing of pre-collection letters. The system allows for the creation of custom pre-collection letters and automates the sending of notifications. Once a resident's financial move-out is complete, they can be sent to collections, either individually or in bulk. The platform also allows for the integration of third-party collections vendors through the Entrata App Store.

## 3. Data Model and Artifacts

Entrata's data model is centered around the **property** entity, with various related entities that support the property management lifecycle. The API documentation provides insights into the key data entities, which include:

*   **Property:** The core entity, representing a physical property.
*   **Unit:** A rentable unit within a property.
*   **Tenant/Resident:** An individual or group renting a unit.
*   **Lease:** The rental agreement between a tenant and the property.
*   **Vendor:** A third-party provider of goods or services.
*   **Invoice:** A bill for goods or services rendered.
*   **Payment:** A financial transaction, typically from a tenant.

## 4. Skill Candidates

Based on the analysis of Entrata's workflows and data model, several skill candidates for an AI Digital Workforce Manager have been identified:

| Skill ID | Description |
| :--- | :--- |
| **AP-001** | **Invoice Data Extraction:** The detailed invoice entry SOP provides a clear basis for a skill that can extract data from invoices. |
| **AP-002** | **Invoice Approval Workflow:** The defined approval process can be automated with a skill that manages invoice approvals based on predefined rules. |
| **AR-001** | **Collections Management:** The collections workflow can be translated into a skill that manages delinquent accounts, sends notices, and escalates cases as needed. |
| **FIN-001** | **Bank Reconciliation:** The upcoming automated bank reconciliation feature presents an opportunity for a skill that can match transactions and identify exceptions. |
| **INT-001** | **API Integration:** The available API endpoints can be used to build a skill that integrates Entrata with other systems. |

## 5. Treasury Capture Opportunities

The research has identified several opportunities for an AI-powered Treasury OS to capture and manage financial workflows within the Entrata ecosystem:

*   **Invoice Approval and Payments:** The AP workflow, with its defined approval process, is a prime opportunity for an AI agent to manage invoice approvals and trigger payments.
*   **Owner Payouts:** Although detailed information was not readily available, the generation and distribution of owner statements and payouts represent a critical treasury function that could be automated.
*   **Fund Segregation:** The management of security deposits, trust accounts, and reserves is a key area for a Treasury OS to ensure compliance and proper fund segregation.

## 6. Training Data Candidates

To train the AI skills, the following artifacts and scenarios can be used as training data:

*   **Sample Invoices:** A collection of various invoice formats to train the invoice data extraction skill.
*   **Collections Notices:** Examples of pre-collection letters and other notices to train the collections management skill.
*   **Bank Statements:** Anonymized bank statements to train the bank reconciliation skill.
*   **Edge Cases:** Scenarios such as disputed charges, partial payments, and early lease terminations to test the robustness of the AI skills.
