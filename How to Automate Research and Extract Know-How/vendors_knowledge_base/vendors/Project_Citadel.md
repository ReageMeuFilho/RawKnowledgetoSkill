# Project Citadel Knowledge Document

## 1. Company Overview

Project Citadel is a vertically integrated hospitality and real estate venture, described in its documentation as a "Real World Asset (RWA) Operating System" for sustainable tourism. The project aims to combine land acquisition, modular construction, AI-driven operations, and tokenized fractional financing to create a new model for regenerative tourism. The company's vision is to become a dominant force in this niche, comparing its model to "McDonald's 2.0," where it owns the land and systems while digital investors fund the physical assets.

### Products and Services

Project Citadel's offerings are structured around three core operating systems:

*   **InvestOS:** A capital layer designed for frictionless investment into real estate Special Purpose Vehicles (SPVs) through tokenization. It handles the entire investment lifecycle, from fundraising to yield distribution.
*   **BuildOS:** An asset and grant factory that automates the process of land acquisition, grant applications, and construction management. It aims to significantly reduce project delivery times.
*   **GuestOS:** An AI-powered operator for managing properties with minimal on-site staff. It handles guest communications, bookings, pricing, and maintenance.

### Verticals and Market Position

The primary vertical for Project Citadel is **Hospitality**, with a specific focus on **sustainable and regenerative tourism**. The project appears to be in a pre-launch or early stage, and its market position is not yet established. The business model is highly innovative and ambitious, targeting a niche segment of the real estate and hospitality market.

### Strengths and Limitations

**Strengths:**

*   **Innovative Business Model:** The integration of real estate development, AI operations, and tokenized financing is a unique and potentially disruptive approach.
*   **Focus on Sustainability:** The emphasis on regenerative tourism and green development aligns with growing market trends.
*   **Scalability:** The "Franchise 2.0" model is designed for rapid scaling by separating capital investment from operations.
*   **Efficiency:** The use of AI and automation in operations and construction is intended to create significant cost and time savings.

**Limitations:**

*   **Complexity:** The vertically integrated model is complex and presents significant execution challenges.
*   **Regulatory Uncertainty:** The use of tokenization and smart contracts for real estate investment is subject to evolving regulatory frameworks.
*   **Market Adoption:** The success of the project depends on the willingness of investors and guests to embrace a new and unproven model.
*   **Lack of Public Presence:** The company does not appear to have a public website or significant online presence, which may hinder its ability to attract customers and investors.


## 2. Workflow Deep Dives

### InvestOS: The Capital Layer

**Objective:** To create a frictionless "Capital-in / Yield-out" machine for funding real estate SPVs through tokenization.

#### Workflow: Owner Payouts (Distributions)

This workflow describes the process of distributing rental income to investors (token holders).

*   **Exact Steps and Procedures:**
    1.  **Trigger:** The operating company (OpCo) deposits Fiat currency (EUR) into the designated payment rail.
    2.  **Conversion:** The Fiat currency is automatically converted to a stablecoin (USDC or EUROC).
    3.  **Execution:** A smart contract calculates the pro-rata share for each token holder based on the number of tokens they own.
    4.  **Distribution:** The smart contract automatically airdrops the dividend payments to the whitelisted wallets of the token holders.

*   **Required Inputs and Data Fields:**
    *   SPV details (Name, Valuation, Number of Shares)
    *   Investor wallet addresses (whitelisted)
    *   Deposit amount (in Fiat)

*   **Outputs/Artifacts Produced:**
    *   Dividend payments (in stablecoin)
    *   Transaction records on the blockchain
    *   Updated portfolio view in the Investor Dashboard (real-time NAV, annualized yield)

*   **Roles/Permissions Involved:**
    *   **OpCo:** Initiates the distribution process by depositing funds.
    *   **Smart Contract:** Executes the automated distribution logic.
    *   **Investor:** Receives the dividend payments.

*   **Edge Cases and Exception Handling:**
    *   The PRD does not specify exception handling, but potential issues could include failed transactions, incorrect wallet addresses, or fluctuations in stablecoin value.

*   **Common Failure Modes and How to Resolve Them:**
    *   The PRD does not detail failure modes, but potential problems could involve smart contract bugs, oracle failures (for currency conversion), or issues with the payment rail. Resolving these would likely require manual intervention and potentially updating the smart contract code.


### BuildOS: The Asset & Grant Factory

**Objective:** To automate the process of finding land, applying for grants, and managing construction.

#### Workflow: Grant Application and Construction Management

This workflow describes the process of identifying suitable land, securing grants, and overseeing the construction process.

*   **Exact Steps and Procedures:**
    1.  **Land Identification:** The "Grant Scout" module uses a GIS interface with Google Maps and Cadastre integration to identify suitable land plots.
    2.  **Filtering:** The system applies filters to exclude undesirable plots (e.g., "Proindiviso" or multi-owner plots) and highlight plots within designated "Grant Zones."
    3.  **Grant Application:** An auto-application generator creates pre-filled PDF templates for relevant grant programs (e.g., "Turismo de Portugal," "NextGen EU").
    4.  **Construction Tracking:** A partner portal allows modular builders to provide updates on construction progress.
    5.  **Milestone Verification:** An AI Vision API verifies photographic evidence of construction milestones (e.g., "Foundation Poured") to trigger payment tranches.
    6.  **Supply Chain Management:** A Kanban-style interface provides visual tracking of the status of modular units.

*   **Required Inputs and Data Fields:**
    *   GIS data (maps, Cadastre information)
    *   Grant program requirements and templates
    *   Project database with technical specifications
    *   Builder updates and photographic evidence

*   **Outputs/Artifacts Produced:**
    *   List of suitable land plots
    *   Completed grant application forms
    *   Construction progress reports
    *   Payment authorizations

*   **Roles/Permissions Involved:**
    *   **System Administrator:** Configures and manages the BuildOS modules.
    *   **Modular Builder:** Provides construction updates and evidence.
    *   **AI Vision API:** Verifies construction milestones.

*   **Edge Cases and Exception Handling:**
    *   The PRD does not specify exception handling, but potential issues could include inaccurate GIS data, changes in grant program requirements, or disputes over milestone verification.

*   **Common Failure Modes and How to Resolve Them:**
    *   The PRD does not detail failure modes, but potential problems could involve the AI Vision API failing to correctly identify milestones, delays in the supply chain, or issues with grant application approvals. These would likely require manual review and intervention.


### GuestOS: The "AI Operator"

**Objective:** To run properties with zero on-site staff using AI orchestration.

#### Workflow: Guest Management and Operations

This workflow describes the process of managing guest bookings, communications, and on-site experience.

*   **Exact Steps and Procedures:**
    1.  **Channel Management:** A two-way sync with major booking platforms (Airbnb, Booking.com, VRBO) is maintained via the Beds24 API.
    2.  **Inventory Blocking:** The system instantly syncs calendars to prevent double bookings.
    3.  **Dynamic Pricing:** A dynamic pricing agent updates rental rates every 4 hours based on local demand, competitor pricing, and gap nights.
    4.  **Guest Communication:** A "Ghost Concierge" AI agent handles guest queries via the WhatsApp Business API.
    5.  **Temporal Workflows:** The AI orchestrates complex tasks, such as handling late check-out requests by checking availability, charging the guest's card, and sending a new access code.
    6.  **Upselling:** The system automatically sends offers for additional services (e.g., early check-in, airport transfer) 24 hours before arrival.
    7.  **Maintenance Dispatch:** The AI categorizes maintenance issues as urgent or low priority and automatically dispatches local contractors via SMS.

*   **Required Inputs and Data Fields:**
    *   Booking data from channel managers
    *   Guest communication history
    *   Property availability and pricing parameters
    *   Contractor contact information

*   **Outputs/Artifacts Produced:**
    *   Confirmed bookings
    *   Guest communications
    *   Updated pricing
    *   Upsell offers
    *   Maintenance dispatch requests

*   **Roles/Permissions Involved:**
    *   **AI Agent:** Manages guest communication and operational workflows.
    *   **Dynamic Pricing Agent:** Adjusts rental rates.
    *   **Local Contractors:** Receive and respond to maintenance requests.

*   **Edge Cases and Exception Handling:**
    *   The PRD does not specify exception handling, but potential issues could include the AI failing to understand a guest's request, a contractor not being available for an urgent issue, or problems with the payment processing for upsells.

*   **Common Failure Modes and How to Resolve Them:**
    *   The PRD does not detail failure modes, but potential problems could involve the AI providing incorrect information to a guest, a double booking occurring despite the inventory blocker, or a maintenance issue not being resolved in a timely manner. These would likely require human intervention to resolve the immediate issue and potentially update the AI's logic or the system's workflows.


## 3. Data Model and Artifacts

### Data Model Entities

The PRD for Project Citadel implies the following data model entities:

*   **Property:** Represents the physical land acquired by the PropCo.
*   **Unit:** A specific hospitality unit, such as an "Eco-Pod," funded by investors.
*   **Owner:** An investor who provides capital for a specific unit and holds tokens representing their ownership.
*   **Tenant:** A guest who books and stays in a hospitality unit.
*   **Vendor:** Third-party service providers, including modular builders and local contractors.
*   **GL Account:** Implied by the financial transactions, although not explicitly mentioned.
*   **Fund:** A Special Purpose Vehicle (SPV) created for each project to be tokenized.
*   **Bank Account:** Implied by the deposit of Fiat currency for dividend distributions.

### API Endpoints and Integration Patterns

Project Citadel relies on several external APIs for its operations:

*   **Beds24 API:** For two-way synchronization with channel managers (Airbnb, Booking.com, VRBO).
*   **Google Maps API:** Integrated with the "Grant Scout" module for land identification.
*   **Cadastre Integration:** Used in conjunction with the Google Maps API to provide detailed land plot information.
*   **SumSub:** For Know Your Customer (KYC) and identity verification of investors.
*   **AI Vision API:** To programmatically verify construction milestones from images.
*   **WhatsApp Business API:** For guest communication with the "Ghost Concierge."

### User Roles and Permissions Model

The PRD outlines several user roles with distinct permissions:

*   **Investor:** Can view their portfolio, receive dividend payments, and participate in the secondary market.
*   **OpCo:** Manages the overall operations, including initiating dividend distributions.
*   **System Administrator:** Configures and manages the various OS modules.
*   **Modular Builder:** Can upload construction progress updates and evidence to the partner portal.

### Approval Workflow Patterns

The primary approval workflow identified is in the construction process:

*   **Milestone-Based Payments:** Payments to modular builders are tied to the completion of specific construction milestones. The builder uploads photographic evidence, which is then verified by an AI Vision API to trigger the payment.

### Audit Logging Capabilities

While not explicitly detailed, the use of blockchain technology for tokenization and dividend distribution provides an inherent audit trail. All transactions are recorded on the blockchain, creating an immutable and transparent record of ownership and payments.


## 4. Skill Candidates

The following skill candidates have been identified based on the analysis of Project Citadel's PRD:

*   **CP-001: Guest Communication:** The "Ghost Concierge" in GuestOS directly maps to this skill, handling guest queries and communications via WhatsApp.
*   **CP-002: Booking Management:** The channel manager and inventory blocker in GuestOS are responsible for managing bookings from various platforms.
*   **INT-001: API Integration:** The project relies heavily on integrations with external APIs, including Beds24, Google Maps, Cadastre, SumSub, and the AI Vision API.
*   **FIN-002: Owner Payouts:** The InvestOS distribution workflow is a clear example of this skill, automating the calculation and distribution of rental income to investors.
*   **AP-001: Invoice Processing:** The milestone verification process in BuildOS can be considered a form of invoice processing, where evidence is reviewed before payment is authorized.
*   **AP-003: Payment Processing:** The automated payment tranches in BuildOS and the dividend distributions in InvestOS both map to this skill.
*   **AR-001: Collections:** The upsell engine in GuestOS, which charges guest cards for additional services, is a form of collections.
*   **REP-001: Owner Statements:** The Investor Dashboard in InvestOS, which provides a real-time portfolio view, serves as a dynamic owner statement.
*   **REP-002: Financial Reporting:** The real-time NAV and annualized yield calculations in the Investor Dashboard are a form of financial reporting.
*   **TRE-001: Cash Management:** The conversion of Fiat currency to stablecoins in the InvestOS distribution workflow is a cash management task.
*   **TRE-002: Payouts:** The automated airdrop of dividends to token holders in InvestOS is a direct implementation of this skill.
*   **TRE-004: Fund Management:** The use of SPVs to tokenize and manage individual projects is a form of fund management.
*   **TRE-006: Tokenization:** The entire InvestOS is built around the concept of tokenizing real estate assets.
*   **RA-001: Compliance:** The use of the ERC-3643 token standard for RWA compliance is a key feature of InvestOS.
*   **RA-002: Onboarding:** The integration with SumSub for KYC and investor onboarding is a direct mapping to this skill.


## 5. Treasury Capture Opportunities

Based on the PRD, the following treasury capture opportunities have been identified:

*   **Payouts:** The automated distribution of dividends to token holders in InvestOS is a prime opportunity for an AI agent to own the entire payout process, from calculation to execution.
*   **Fund Segregation:** The use of SPVs for each project creates a clear segregation of funds, which can be managed and monitored by an AI agent.
*   **Approvals:** The milestone verification process in BuildOS, where an AI Vision API approves payments, is a key approval point that can be owned by an AI agent.
*   **Currency Conversion:** The automated conversion of Fiat currency to stablecoins in the InvestOS distribution workflow is another treasury function that can be managed by an AI agent.


## 6. Training Data Candidates

The following are potential candidates for training data that can be used to build and evaluate the identified AI skills:

*   **Example Artifacts:**
    *   Sample grant application forms (for BuildOS)
    *   Example construction milestone photos (for the AI Vision API in BuildOS)
    *   Anonymized guest communication logs from the WhatsApp Business API (for the "Ghost Concierge" in GuestOS)
    *   Sample investor portfolio data (for the Investor Dashboard in InvestOS)

*   **Edge Cases:**
    *   Guest queries that the AI fails to understand or handle correctly
    *   Disputes over construction milestone verification
    *   Failed dividend distribution transactions
    *   Attempts by non-whitelisted users to trade tokens

*   **Evaluation Scenarios:**
    *   Simulating a surge in booking requests to test the performance of the channel manager and dynamic pricing agent
    *   Creating a set of complex guest requests to evaluate the temporal workflow capabilities of the "Ghost Concierge"
    *   Testing the AI Vision API with a variety of images to assess its accuracy in verifying construction milestones
    *   Simulating a scenario where a grant program's requirements change to test the adaptability of the "Grant Scout" module
