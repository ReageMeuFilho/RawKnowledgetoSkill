Blitzy
W
Wesley
Free
Maintanance
New product • Tech spec ready


Select destination


1
Build prompt
2
Target tech spec
3
Code
4
Project guide
Sections
1.
introduction
1.1
executive summary
1.2
system overview
1.3
scope
2.
product requirements
2.1
feature catalog
2.2
feature relationships
2.3
implementation considerations
2.4
traceability matrix
3.
technology stack
3.1
programming languages
3.2
frameworks & libraries
3.3
open source dependencies
3.4
third-party services
3.5
databases & storage
3.6
development & deployment
3.7
technology integration architecture
4.
process flowchart
4.1
system workflows
4.2
flowchart requirements
4.3
validation rules
4.4
technical implementation
4.5
required diagrams
5.
system architecture
5.1
high-level architecture
5.2
component details
5.3
technical decisions
5.4
cross-cutting concerns
6.
system components design
6.1
component architecture overview
6.2
intake layer components
6.3
brain layer components
6.4
action layer components
6.5
orchestration layer components
6.1
core services architecture
7.
user interface design
7.1
ui technology stack
7.2
user interface use cases
7.3
ui/backend interaction boundaries
7.4
ui schema definitions
7.5
screen specifications
7.6
user interaction patterns
7.7
visual design considerations
8.1
deployment environment
9.
appendices
9.1
additional technical information
9.2
glossary
9.3
acronyms
9.4
environment variables configuration
9.5
message queue topics and events
9.6
api reference summary
9.7
database schema ddl
9.8
troubleshooting knowledge base sample entries
9.9
notification template library
9.10
vendor communication scripts
1. Introduction
1. Introduction
1.1 Executive Summary
1.1.1 Brief Overview Of The Project
The AI Maintenance Coordinator represents a transformative agentic AI system designed to revolutionize property maintenance operations through end-to-end automation. This system handles work orders from start to finish: triage, troubleshooting, vendor selection, coordination, scheduling and job completion verification, functioning as a 24/7 digital maintenance dispatcher that eliminates the chaos and inefficiencies plaguing traditional property management operations.


1.1.2 Core Business Problem Being Solved
Property maintenance coordination currently suffers from systemic inefficiencies that create cascading operational problems. The industry data is clear: operational efficiency is the top challenge facing property managers heading into 2026. Teams are overloaded, spending most of their time on routine, reactive work. Traditional maintenance workflows rely heavily on manual coordination, resulting in delayed responses, missed communications, vendor scheduling conflicts, and inconsistent service quality.


Buildium's research shows that maintenance is the single greatest source of stress for rental owners, outweighing concerns about leasing, accounting, or compliance. AppFolio's findings reinforce that maintenance is a primary driver of day-to-day inefficiency, consuming a disproportionate share of staff time through reactive work and coordination overhead.


The current state involves property managers juggling multiple communication channels, manually triaging requests, playing phone tag with vendors, and struggling to maintain visibility across hundreds of active work orders. This reactive approach leads to extended resolution times, increased costs, and deteriorating resident satisfaction.


1.1.3 Key Stakeholders And Users
Stakeholder Group        Primary Pain Points        Expected Benefits
Property Managers        Manual coordination overhead, after-hours coverage gaps, vendor management complexity        80% reduction in coordination tasks, 24/7 automated coverage, streamlined vendor relationships
Residents/Tenants        Slow response times, lack of status visibility, repeated follow-up calls        Instant acknowledgment, real-time updates, faster issue resolution
Property Owners        High maintenance costs, lack of transparency, delayed repairs affecting asset value        Cost optimization, detailed reporting, proactive maintenance recommendations
Maintenance Vendors        Inconsistent job flow, unclear work orders, payment delays        Streamlined job assignments, clear specifications, automated invoicing
1.1.4 Expected Business Impact And Value Proposition
The AI Maintenance Coordinator delivers measurable operational transformation through automation and intelligence. A property management firm managing 1,200 doors used Direct to cut maintenance tasks by 80 percent, avoided hiring two new coordinators, and seamlessly absorbed 300 more doors.


Quantified Value Metrics:


Cost Reduction: $12/door maintenance cost reduction through optimized vendor selection and reduced truck rolls
Time Savings: Users report saving an average of 10 hours weekly on tasks
Response Improvement: Every call answered immediately. Residents stop asking the same questions. Vendors are already booked before your team finishes reading the work order
Operational Efficiency: Target 80% AI-handled tasks without human intervention
1.2 System Overview
1.2.1 Project Context
Business Context And Market Positioning
The AI Maintenance Coordinator emerges at a critical inflection point in property management technology adoption. As the industry looks toward 2026, a quieter, more disciplined shift is underway. Early enthusiasm for "AI at any cost" is giving way to a focus on measurable operational value. The question is no longer whether to use AI-enabled tools, but where they deliver real, tangible results.


As maintenance becomes more tightly linked to renewals, owner trust, and NOI, operators are treating it less as a reactive function and more as a formal operating discipline. Property Meld describes this shift as the emergence of Property Maintenance Operations (PMO), where performance is planned, measured, and managed with the same rigor as leasing or finance.


Current System Limitations
Existing maintenance management solutions fall into three categories, each with significant limitations:


Manual/Spreadsheet-Based Systems: Still prevalent among smaller operators, these systems lack scalability, consistency, and real-time visibility. Work orders are tracked on paper or basic spreadsheets, leading to lost requests and billing gaps.


Traditional Maintenance Software: Solutions like Property Meld provide workflow automation and tracking but still require human decision-making for triage, vendor selection, and coordination. Many operators are overwhelmed by tools that promise automation but fail to meaningfully change outcomes in maintenance. Solutions that add complexity without improving accuracy, speed, or reliability are increasingly viewed as noise.


Human Call Centers: Services like Latchel provide 24/7 coverage through human operators but lack the scalability, consistency, and cost-effectiveness of AI-driven solutions. They cannot learn property-specific patterns or optimize decisions based on historical data.


Integration With Existing Enterprise Landscape
The AI Maintenance Coordinator is designed as a native integration layer that enhances rather than replaces existing property management systems. AI teammates work inside your PMS and daily tools, keeping everything in sync. The system integrates bidirectionally with major PMS platforms (AppFolio, Yardi, RentManager), telephony providers (Twilio), payment systems, and communication tools (Slack, Microsoft Teams).


1.2.2 High-level Description
Primary System Capabilities
The AI Maintenance Coordinator operates as an autonomous digital workforce member with five core capabilities:


Instant Multi-Channel Intake: Handles calls, texts, emails, and portal messages in your brand voice, eliminating missed calls, reducing questions, and giving residents and prospects a seamless experience


Intelligent Triage and Troubleshooting: Remotely solve major problems and prevent unnecessary truck rolls through guided diagnostic conversations


Automated Vendor Management: From vendor assignment to scheduling and invoice collection, your Roos keep operations flowing


Continuous Coordination: Real-time status updates, scheduling coordination, and stakeholder communication throughout the work order lifecycle


Completion Verification and Billing: Automated job verification, invoice processing, and financial reconciliation


Major System Components
The system architecture follows a layered approach optimized for both real-time AI reasoning and durable workflow orchestration:


Intake Layer: Multi-channel request reception (voice, SMS, email, portal) with unified processing pipeline
Brain Layer: AI-powered triage, classification, and troubleshooting engine using LangGraph and large language models
Action Layer: Vendor selection, dispatch, scheduling, and notification systems
Orchestration Layer: Temporal-based workflow management for durable, long-running processes
Integration Layer: MCP (Model Context Protocol) servers for seamless external system connectivity


Core Technical Approach
The system implements a dual-path architecture distinguishing between "Hot Path" and "Cold Path" operations:


Hot Path: Real-time AI reasoning for immediate decisions (triage, troubleshooting, vendor selection) with sub-500ms latency requirements
Cold Path: Durable workflow orchestration for long-running processes (work order lifecycle, billing, compliance) with exactly-once execution guarantees
1.2.3 Success Criteria
Measurable Objectives
Metric Category        Target        Measurement Method
Response Time        <30 seconds first response        System timestamps
Resolution Speed        50% reduction in completion time        Historical comparison
Cost Efficiency        $12/door cost reduction        Financial analysis
Automation Rate        80% AI-handled without human intervention        Process analytics
Critical Success Factors
Seamless Integration: Zero disruption to existing PMS workflows with bidirectional data synchronization
Resident Satisfaction: Maintained or improved satisfaction scores despite automation
Vendor Adoption: High vendor response rates to AI-generated communications
Staff Acceptance: Property manager confidence in AI decision-making with appropriate oversight controls
Scalability: System performance maintained under peak load conditions (storm surges, emergency situations)
Key Performance Indicators (kpis)
Operational KPIs:


First response time: <30 seconds (target: 95th percentile)
Troubleshooting resolution rate: 20-35% of issues resolved without vendor dispatch
Time to vendor dispatch: <30 minutes urgent, <4 hours routine
First-time fix rate: >85% resolved in single vendor visit
Quality KPIs:


Resident satisfaction: >4.5/5 post-completion survey
Vendor performance: >4.0/5 composite score
Escalation rate: <15% requiring human intervention
Reopen rate: <5% within 30 days
Financial KPIs:


Cost per work order: 5% year-over-year decrease
Cost per door: <$50/door monthly maintenance cost
Invoice accuracy: >90% within 20% of estimates
1.3 Scope
1.3.1 In-scope
Core Features And Functionalities
Multi-Channel Request Intake:


Voice agent with real-time speech processing and natural conversation capabilities
SMS/text messaging with context-aware responses and conversation threading
Email parsing with attachment processing and automatic categorization
Portal API integration for seamless PMS connectivity
Unified request processing pipeline with consistent data normalization
AI-Powered Triage and Classification:


Intelligent issue categorization across plumbing, HVAC, electrical, appliance, structural, and pest categories
Urgency determination with emergency keyword detection and contextual analysis
Property-specific context loading including historical issues and owner preferences
Intent recognition for distinguishing maintenance requests from status inquiries
Remote Troubleshooting Engine:


Comprehensive knowledge base covering top 50 maintenance scenarios
Interactive troubleshooting sessions with step-by-step guidance
Multi-modal support including photo analysis and video instructions
Resolution tracking with continuous knowledge base improvement
Automated Vendor Management:


Intelligent vendor selection based on performance, cost, location, and availability
Multi-channel vendor communication (SMS, email, portal) with confirmation tracking
Automated scheduling with calendar integration and conflict resolution
Performance monitoring and vendor scorecard maintenance
Work Order Lifecycle Management:


Complete state machine from intake to completion with 12 distinct states
Automated transitions with timeout handling and escalation triggers
Real-time status tracking with stakeholder notifications
Audit trail maintenance for compliance and analysis
Implementation Boundaries
System Boundaries:


Operates within existing property management ecosystem without requiring system replacement
Integrates with major PMS platforms (AppFolio, Yardi, RentManager) through native APIs
Supports properties ranging from single-family homes to large multifamily complexes
Handles concurrent operations across multiple properties and portfolios
User Groups Covered:


Property managers and maintenance coordinators
Residents and tenants across all communication preferences
Approved vendor networks and service providers
Property owners requiring approval workflows and reporting
Geographic/Market Coverage:


North American property markets with English and Spanish language support
Local vendor networks with geographic routing optimization
Regional compliance requirements and business hour variations
Multi-timezone operation with 24/7 availability
Data Domains Included:


Property and unit profiles with historical maintenance data
Resident contact information and communication preferences
Vendor databases with performance metrics and availability
Work order records with complete audit trails
Financial data for cost tracking and owner billing
1.3.2 Out-of-scope
Explicitly Excluded Features/Capabilities:


Physical maintenance execution (the system coordinates but does not perform repairs)
Emergency services dispatch (fire, police, medical) - system alerts appropriate authorities but does not replace 911
Legal dispute resolution or tenant-landlord mediation
Property acquisition, disposition, or major capital improvement planning
Rent collection, lease management, or non-maintenance resident services
Future Phase Considerations:


Predictive maintenance with IoT sensor integration
Multi-agent workforce coordination with leasing and accounting AI systems
Advanced analytics and machine learning model optimization
International market expansion with additional language support
Integration with smart home and building automation systems
Integration Points Not Covered:


Direct integration with municipal permitting systems
Automated insurance claim filing and processing
Integration with specialized trade contractor management systems
Direct connection to manufacturer warranty systems (manual lookup required)
Unsupported Use Cases:


Emergency situations requiring immediate human intervention (system escalates but does not handle)
Complex construction projects or major renovations
Warranty claims requiring legal documentation
Maintenance on properties without digital communication infrastructure
Situations requiring physical presence for security or safety verification


2. Product Requirements
2.1 Feature Catalog
2.1.1 Multi-channel Request Intake
Feature Metadata        Details
Feature ID        F-001
Feature Name        Multi-Channel Request Intake
Feature Category        Core Infrastructure
Priority Level        Critical
Status        Proposed
Description
Overview: The AI Maintenance Coordinator handles work orders from start to finish: triage, troubleshooting, vendor selection, coordination, scheduling and job completion verification, functioning as a 24/7 digital maintenance dispatcher. The multi-channel intake system serves as the primary entry point for all maintenance requests, supporting voice calls, SMS/text messaging, email, and portal API submissions.


Business Value: Eliminates missed maintenance requests by providing residents with multiple convenient communication channels. Every call answered immediately. Residents stop asking the same questions. Vendors are already booked before your team finishes reading the work order.


User Benefits: Residents can report issues through their preferred communication method without being forced into a single channel. Property managers receive all requests in a unified format regardless of source channel.


Technical Context: Implements a unified processing pipeline that normalizes requests from different channels into a standardized MaintenanceRequest data structure for downstream processing.


Dependencies
Dependency Type        Details
Prerequisite Features        None (foundational feature)
System Dependencies        LangGraph 1.0.5 for AI orchestration, Twilio REST APIs for voice/SMS
External Dependencies        Twilio for telephony, SendGrid for email, PMS webhook endpoints
Integration Requirements        Property Management System API access for resident verification
Functional Requirements
Requirement ID        F-001-RQ-001
Description        Voice call intake with real-time speech processing
Acceptance Criteria        System answers calls within 2 rings, converts speech to text with >95% accuracy, maintains natural conversation flow
Priority        Must-Have
Complexity        High
Requirement ID        F-001-RQ-002
Description        SMS/text message processing with conversation threading
Acceptance Criteria        Processes inbound SMS within 5 seconds, maintains conversation context for 24 hours, supports MMS photo attachments
Priority        Must-Have
Complexity        Medium
Requirement ID        F-001-RQ-003
Description        Email parsing with attachment handling
Acceptance Criteria        Extracts issue details from email body/subject, processes photo attachments up to 5MB, maintains email thread continuity
Priority        Must-Have
Complexity        Medium
Requirement ID        F-001-RQ-004
Description        Portal API integration for PMS systems
Acceptance Criteria        Accepts structured JSON requests, validates required fields, returns work order ID within 1 second
Priority        Must-Have
Complexity        Low
2.1.2 Ai-powered Triage And Classification
Feature Metadata        Details
Feature ID        F-002
Feature Name        AI-Powered Triage and Classification
Feature Category        AI Intelligence
Priority Level        Critical
Status        Proposed
Description
Overview: Intelligent categorization and urgency determination system that analyzes maintenance requests to classify issue types, determine priority levels, and load relevant property context for informed decision-making.


Business Value: Operational efficiency is the top challenge facing property managers heading into 2026. Teams are overloaded, spending most of their time on routine, reactive work. Automated triage reduces manual classification overhead and ensures consistent prioritization.


User Benefits: Property managers receive pre-classified requests with appropriate urgency levels, enabling faster response to critical issues while optimizing resource allocation for routine maintenance.


Technical Context: Uses fine-tuned classification models and rule-based urgency determination algorithms to process natural language descriptions into structured maintenance categories.


Dependencies
Dependency Type        Details
Prerequisite Features        F-001 (Multi-Channel Request Intake)
System Dependencies        LangGraph's low-level primitives provide the flexibility needed to create fully customizable agents
External Dependencies        Property Management System for historical data access
Integration Requirements        Property and unit profile data for context loading
Functional Requirements
Requirement ID        F-002-RQ-001
Description        Issue category classification across 6 primary categories
Acceptance Criteria        Classifies plumbing, HVAC, electrical, appliance, structural, and pest issues with >90% accuracy
Priority        Must-Have
Complexity        High
Requirement ID        F-002-RQ-002
Description        Emergency keyword detection and escalation
Acceptance Criteria        Detects emergency keywords (fire, flood, gas leak) with 100% recall, triggers immediate escalation protocols
Priority        Must-Have
Complexity        Medium
Requirement ID        F-002-RQ-003
Description        Property context loading for informed decisions
Acceptance Criteria        Loads property profile, unit details, resident info, and historical issues within 2 seconds
Priority        Must-Have
Complexity        Medium
2.1.3 Remote Troubleshooting Engine
Feature Metadata        Details
Feature ID        F-003
Feature Name        Remote Troubleshooting Engine
Feature Category        AI Intelligence
Priority Level        High
Status        Proposed
Description
Overview: Interactive troubleshooting system that guides residents through diagnostic steps to potentially resolve issues without vendor dispatch. Remotely solve major problems and prevent unnecessary truck rolls through guided diagnostic conversations.


Business Value: Reduces maintenance costs by resolving 20-35% of issues through remote guidance, eliminating unnecessary vendor visits and associated costs.


User Benefits: Residents receive immediate assistance and may resolve issues instantly. Property managers reduce vendor coordination overhead for simple fixes.


Technical Context: Implements decision tree logic with step-by-step guidance, response parsing, and outcome tracking to determine when vendor dispatch is necessary.


Dependencies
Dependency Type        Details
Prerequisite Features        F-002 (AI-Powered Triage and Classification)
System Dependencies        Vector database for troubleshooting knowledge base
External Dependencies        None
Integration Requirements        Communication channels for interactive guidance
Functional Requirements
Requirement ID        F-003-RQ-001
Description        Comprehensive troubleshooting knowledge base
Acceptance Criteria        Covers top 50 maintenance scenarios with step-by-step guidance, achieves 25% average resolution rate
Priority        Must-Have
Complexity        High
Requirement ID        F-003-RQ-002
Description        Interactive troubleshooting sessions
Acceptance Criteria        Maintains conversation state, processes resident responses, adapts flow based on outcomes
Priority        Must-Have
Complexity        High
Requirement ID        F-003-RQ-003
Description        Resolution tracking and knowledge base improvement
Acceptance Criteria        Tracks success rates per troubleshooting entry, flags entries for review when success rate drops below 15%
Priority        Should-Have
Complexity        Medium
2.1.4 Intelligent Vendor Management
Feature Metadata        Details
Feature ID        F-004
Feature Name        Intelligent Vendor Management
Feature Category        Automation
Priority Level        Critical
Status        Proposed
Description
Overview: Automated vendor selection, dispatch, and communication system that chooses optimal vendors based on performance metrics, availability, cost, and property-specific preferences.


Business Value: Optimizes vendor selection to reduce costs and improve service quality while eliminating manual coordination overhead.


User Benefits: Property managers benefit from automated vendor dispatch with optimal selection criteria. Vendors receive clear, structured job assignments with all necessary details.


Technical Context: Implements scoring algorithms that evaluate vendors across multiple criteria including performance history, cost competitiveness, geographic proximity, and availability.


Dependencies
Dependency Type        Details
Prerequisite Features        F-003 (Remote Troubleshooting Engine)
System Dependencies        Vendor database with performance metrics
External Dependencies        Vendor communication channels (SMS, email, portal)
Integration Requirements        Vendor portal API for job assignment and status updates
Functional Requirements
Requirement ID        F-004-RQ-001
Description        Multi-criteria vendor scoring algorithm
Acceptance Criteria        Scores vendors on performance (40%), cost (25%), familiarity (20%), availability (15%), selects top 3 candidates
Priority        Must-Have
Complexity        High
Requirement ID        F-004-RQ-002
Description        Automated vendor dispatch with confirmation tracking
Acceptance Criteria        Contacts vendors via preferred method, tracks confirmations, retries with backup vendors if no response within timeout
Priority        Must-Have
Complexity        Medium
Requirement ID        F-004-RQ-003
Description        Vendor performance monitoring and scorecard maintenance
Acceptance Criteria        Tracks response times, completion rates, resident satisfaction, updates vendor scores after each job
Priority        Should-Have
Complexity        Medium
2.1.5 Work Order Lifecycle Management
Feature Metadata        Details
Feature ID        F-005
Feature Name        Work Order Lifecycle Management
Feature Category        Core Workflow
Priority Level        Critical
Status        Proposed
Description
Overview: Complete state machine managing work orders from initial request through completion, with automated transitions, timeout handling, and escalation triggers.


Business Value: Ensures no work orders fall through cracks while providing complete visibility into maintenance operations. Temporal Workflows automatically capture state at every step, and in the event of failure, can pick up exactly where they left off. No lost progress, no orphaned processes, and no manual recovery required.


User Benefits: Property managers gain real-time visibility into all work order statuses. Residents receive proactive updates throughout the repair process.


Technical Context: Write your business logic as code as a Temporal Workflow. Because the full running state of a Workflow is durable and fault tolerant by default, your business logic can be recovered, replayed, or paused at any point.


Dependencies
Dependency Type        Details
Prerequisite Features        F-004 (Intelligent Vendor Management)
System Dependencies        The Temporal Service persists the state of your application and has built-in retries, task queues, signals, and timers
External Dependencies        PMS integration for work order synchronization
Integration Requirements        Notification system for status updates
Functional Requirements
Requirement ID        F-005-RQ-001
Description        Complete state machine with 12 distinct states
Acceptance Criteria        Implements NEW, TRIAGING, TROUBLESHOOTING, AWAITING_DISPATCH, AWAITING_APPROVAL, DISPATCHING, SCHEDULED, VENDOR_EN_ROUTE, IN_PROGRESS, NEEDS_PARTS, PENDING_VERIFICATION, COMPLETED states
Priority        Must-Have
Complexity        High
Requirement ID        F-005-RQ-002
Description        Automated state transitions with timeout handling
Acceptance Criteria        Transitions occur based on events or timeouts, escalates to human intervention when timeouts exceeded
Priority        Must-Have
Complexity        Medium
Requirement ID        F-005-RQ-003
Description        Complete audit trail for compliance
Acceptance Criteria        Logs all state changes, decisions, and communications with timestamps and responsible actors
Priority        Must-Have
Complexity        Low
2.1.6 Approval Workflow And Cost Management
Feature Metadata        Details
Feature ID        F-006
Feature Name        Approval Workflow and Cost Management
Feature Category        Financial Controls
Priority Level        High
Status        Proposed
Description
Overview: Configurable approval system that enforces spending limits, routes high-cost repairs for authorization, and manages owner notification preferences.


Business Value: Provides financial controls to prevent unauthorized spending while maintaining operational efficiency for routine repairs.


User Benefits: Property owners maintain control over maintenance spending. Property managers operate within clear authorization limits without delays for routine work.


Technical Context: Implements hierarchical approval workflows with configurable thresholds and emergency override capabilities.


Dependencies
Dependency Type        Details
Prerequisite Features        F-005 (Work Order Lifecycle Management)
System Dependencies        Cost estimation algorithms, approval notification system
External Dependencies        Owner communication channels
Integration Requirements        Financial system integration for payment processing
Functional Requirements
Requirement ID        F-006-RQ-001
Description        Configurable approval thresholds by property and category
Acceptance Criteria        Supports auto-approve below $250, manager approval $250-$1000, owner approval above $1000, with category-specific overrides
Priority        Must-Have
Complexity        Medium
Requirement ID        F-006-RQ-002
Description        Emergency override capabilities
Acceptance Criteria        Allows emergency repairs up to $500 with immediate owner notification, maintains audit trail
Priority        Must-Have
Complexity        Medium
Requirement ID        F-006-RQ-003
Description        Cost estimation based on historical data
Acceptance Criteria        Provides low/mid/high estimates using historical costs, vendor rates, and market averages with confidence scores
Priority        Should-Have
Complexity        High
2.1.7 Scheduling And Calendar Integration
Feature Metadata        Details
Feature ID        F-007
Feature Name        Scheduling and Calendar Integration
Feature Category        Coordination
Priority Level        High
Status        Proposed
Description
Overview: Automated appointment scheduling system that coordinates vendor availability, resident preferences, and property access constraints to optimize service delivery timing.


Business Value: Reduces scheduling coordination overhead while optimizing vendor routing and resident convenience.


User Benefits: Residents receive convenient appointment times that match their availability. Vendors receive optimized schedules that minimize travel time.


Technical Context: Implements constraint-based scheduling algorithms that consider multiple factors including vendor calendars, travel time optimization, and property access hours.


Dependencies
Dependency Type        Details
Prerequisite Features        F-004 (Intelligent Vendor Management)
System Dependencies        Calendar integration APIs, vendor availability data
External Dependencies        Vendor calendar systems
Integration Requirements        Resident communication preferences
Functional Requirements
Requirement ID        F-007-RQ-001
Description        Multi-constraint appointment optimization
Acceptance Criteria        Considers vendor availability, resident preferences, property access hours, and travel time optimization
Priority        Must-Have
Complexity        High
Requirement ID        F-007-RQ-002
Description        Automated reminder system
Acceptance Criteria        Sends reminders to vendors (1 day, 1 hour before) and residents (1 day before), tracks delivery status
Priority        Must-Have
Complexity        Low
Requirement ID        F-007-RQ-003
Description        Rescheduling protocol with conflict resolution
Acceptance Criteria        Handles resident/vendor-initiated reschedules, finds alternative slots, notifies all parties of changes
Priority        Should-Have
Complexity        Medium
2.1.8 Notification And Communication System
Feature Metadata        Details
Feature ID        F-008
Feature Name        Notification and Communication System
Feature Category        Communication
Priority Level        High
Status        Proposed
Description
Overview: Comprehensive notification engine that keeps all stakeholders informed throughout the maintenance process with configurable templates and delivery preferences.


Business Value: Maintains transparency and reduces follow-up inquiries by proactively communicating status updates to residents, staff, and owners.


User Benefits: Residents stay informed about repair progress without needing to call for updates. Staff receive alerts only when intervention is needed.


Technical Context: Multi-channel notification delivery with template rendering, quiet hours respect, and delivery confirmation tracking.


Dependencies
Dependency Type        Details
Prerequisite Features        F-005 (Work Order Lifecycle Management)
System Dependencies        Template engine, communication preferences database
External Dependencies        SMS, email, and push notification providers
Integration Requirements        Slack/Teams integration for staff notifications
Functional Requirements
Requirement ID        F-008-RQ-001
Description        Multi-channel notification delivery
Acceptance Criteria        Delivers notifications via SMS, email, push, and Slack with appropriate channel selection based on recipient preferences
Priority        Must-Have
Complexity        Medium
Requirement ID        F-008-RQ-002
Description        Configurable notification templates
Acceptance Criteria        Supports customizable templates for all notification types, includes dynamic content insertion, maintains brand consistency
Priority        Must-Have
Complexity        Low
Requirement ID        F-008-RQ-003
Description        Quiet hours and preference management
Acceptance Criteria        Respects resident quiet hours except for emergencies, allows per-resident communication preferences
Priority        Should-Have
Complexity        Low
2.1.9 Escalation And Human-in-the-loop
Feature Metadata        Details
Feature ID        F-009
Feature Name        Escalation and Human-in-the-Loop
Feature Category        Safety and Oversight
Priority Level        Critical
Status        Proposed
Description
Overview: Comprehensive escalation system that identifies when human intervention is required and provides seamless handoff capabilities with full context transfer.


Business Value: Ensures safety and quality by escalating complex situations while maintaining operational efficiency for routine tasks.


User Benefits: Residents receive human assistance when needed. Staff intervene only when their expertise is required, with full context provided.


Technical Context: Implements trigger-based escalation with configurable rules, sentiment analysis, and structured handoff protocols.


Dependencies
Dependency Type        Details
Prerequisite Features        All core features (F-001 through F-008)
System Dependencies        Sentiment analysis, escalation notification system
External Dependencies        Staff communication channels
Integration Requirements        Human-in-the-loop dashboard
Functional Requirements
Requirement ID        F-009-RQ-001
Description        Automatic escalation trigger detection
Acceptance Criteria        Detects emergency keywords, vendor unavailability, resident frustration, AI uncertainty, and SLA breaches
Priority        Must-Have
Complexity        Medium
Requirement ID        F-009-RQ-002
Description        Hierarchical escalation protocols
Acceptance Criteria        Routes to property manager (15 min SLA), regional manager (30 min SLA), emergency on-call (5 min SLA)
Priority        Must-Have
Complexity        Medium
Requirement ID        F-009-RQ-003
Description        Context transfer and handoff briefing
Acceptance Criteria        Provides complete conversation transcript, AI analysis, property context, and recommended actions to human operator
Priority        Must-Have
Complexity        Low
2.1.10 Metrics, Analytics And Reporting
Feature Metadata        Details
Feature ID        F-010
Feature Name        Metrics, Analytics and Reporting
Feature Category        Business Intelligence
Priority Level        Medium
Status        Proposed
Description
Overview: Comprehensive analytics system that tracks operational KPIs, quality metrics, and financial performance to demonstrate value and identify optimization opportunities.


Business Value: A property management firm managing 1,200 doors used Direct to cut maintenance tasks by 80 percent, avoided hiring two new coordinators, and seamlessly absorbed 300 more doors. Provides quantifiable metrics to demonstrate ROI and operational improvements.


User Benefits: Property managers gain insights into maintenance operations performance. Owners receive transparent reporting on maintenance spending and outcomes.


Technical Context: Implements real-time metrics collection, time-series data storage, and automated report generation with configurable dashboards.


Dependencies
Dependency Type        Details
Prerequisite Features        All operational features for data collection
System Dependencies        Time-series database, analytics engine
External Dependencies        Business intelligence tools
Integration Requirements        Data export capabilities for external systems
Functional Requirements
Requirement ID        F-010-RQ-001
Description        Real-time operational KPI tracking
Acceptance Criteria        Tracks first response time (<30s), resolution rate (20-35%), time to dispatch (<30 min urgent), completion time
Priority        Should-Have
Complexity        Medium
Requirement ID        F-010-RQ-002
Description        Automated report generation
Acceptance Criteria        Generates daily operations, weekly performance, monthly owner, and quarterly portfolio reports
Priority        Should-Have
Complexity        Low
Requirement ID        F-010-RQ-003
Description        Cost analysis and benchmarking
Acceptance Criteria        Tracks cost per work order, cost per door, invoice accuracy, provides year-over-year comparisons
Priority        Should-Have
Complexity        Medium
2.2 Feature Relationships
2.2.1 Feature Dependencies Map
F-001: Multi-Channel Intake


F-002: AI Triage & Classification


F-003: Remote Troubleshooting


F-004: Vendor Management


F-005: Work Order Lifecycle


F-006: Approval Workflow


F-007: Scheduling System


F-008: Notification System


F-009: Escalation System


F-010: Analytics & Reporting


2.2.2 Integration Points
Integration Point        Connected Features        Shared Components
Request Processing Pipeline        F-001, F-002, F-003        MaintenanceRequest data structure, session state management
Vendor Coordination        F-004, F-007, F-008        Vendor database, communication templates
State Management        F-005, F-006, F-009        Work order state machine, escalation triggers
Communication Hub        F-008, F-009, F-010        Notification engine, template system
2.2.3 Common Services
Service        Used By Features        Purpose
Property Context Service        F-002, F-004, F-006, F-007        Loads property profiles, unit details, owner preferences
Communication Service        F-001, F-008, F-009        Handles multi-channel message delivery
Workflow Orchestration        F-005, F-006, F-007        Temporal Service persists the state of your application and has built-in retries, task queues, signals, and timers
Analytics Collection        All features        Captures metrics and events for reporting
2.3 Implementation Considerations
2.3.1 Technical Constraints
Constraint Category        Details
Performance Requirements        <500ms latency for AI reasoning (Hot Path), <5s for durable operations (Cold Path)
Scalability Requirements        Support 100 concurrent requests, handle storm surge scenarios
Integration Constraints        Must work within existing PMS ecosystems without replacement
Technology Constraints        LangGraph 1.0.5 provides low-level supporting infrastructure for any long-running, stateful workflow or agent
2.3.2 Security Implications
Security Aspect        Requirements
Data Classification        PII protection for resident information, access code encryption
Access Control        Role-based permissions for residents, staff, vendors, and AI agents
Audit Requirements        Immutable logging of all decisions and actions for 7-year retention
Compliance        Data retention policies, privacy consent management
2.3.3 Maintenance Requirements
Maintenance Area        Considerations
Knowledge Base Updates        Continuous improvement of troubleshooting content based on outcomes
Vendor Performance Monitoring        Regular scorecard updates and performance metric tracking
AI Model Maintenance        Periodic retraining of classification models, accuracy monitoring
System Health Monitoring        Real-time metrics, alerting, and performance optimization
2.4 Traceability Matrix
Business Requirement        Features        Acceptance Criteria
24/7 Maintenance Coverage        F-001, F-009        Answer all calls immediately, provide after-hours support
Cost Reduction Target        F-003, F-004, F-006        Achieve $12/door cost reduction through optimization
Response Time Improvement        F-001, F-002, F-008        <30 second first response, real-time status updates
Automation Rate Target        F-002, F-003, F-004, F-005        80% AI-handled tasks without human intervention
Quality Maintenance        F-004, F-009, F-010        >85% first-time fix rate, >4.5/5 resident satisfaction
3. Technology Stack
3.1 Programming Languages
3.1.1 Primary Language Selection
Component        Language        Version        Justification
Backend Services        Python        3.11+        LangGraph 1.0.5 is the latest stable release with full Python support. Python provides excellent AI/ML ecosystem integration, extensive library support for NLP and workflow orchestration, and mature async capabilities required for real-time voice processing.
AI/ML Components        Python        3.11+        Native integration with LangGraph's low-level primitives provide the flexibility needed to create fully customizable agents. Python's rich ecosystem includes libraries for speech processing, natural language understanding, and machine learning model inference.
API Services        Python        3.11+        FastAPI is a modern, fast (high-performance), web framework for building APIs with Python based on standard Python type hints. Provides automatic OpenAPI documentation generation and excellent async performance.
Workflow Orchestration        Python        3.11+        Write your business logic as code as a Temporal Workflow. Because the full running state of a Workflow is durable and fault tolerant by default, your business logic can be recovered, replayed, or paused at any point.
3.1.2 Language Constraints And Dependencies
Python Version Requirements:


Minimum: Python 3.11 for optimal performance and modern async features
Any Python 3.8 installer would just refuse to install the latest version of FastAPI and would only install 0.124.4
Target: Python 3.12+ for production deployments to leverage performance improvements
Language-Specific Considerations:


Type hints mandatory for all API endpoints and data models
Async/await patterns required for all I/O operations
Pydantic v2 for data validation and serialization
Support for concurrent execution patterns required for multi-channel intake
3.2 Frameworks & Libraries
3.2.1 Core Frameworks
Framework        Version        Purpose        Justification
FastAPI        0.125.0+        REST API Framework        Independent TechEmpower benchmarks show FastAPI applications running under Uvicorn as one of the fastest Python frameworks available. Provides automatic OpenAPI documentation, dependency injection, and excellent async performance.
LangGraph        1.0.5        AI Workflow Orchestration        LangGraph 1.0.5 is the latest stable release. LangGraph 1.0 is the first stable major release in the durable agent framework space —a major milestone for production-ready AI systems. After more than a year of powering agents at companies like Uber, LinkedIn, and Klarna.
Temporal        1.25.0+        Workflow Orchestration        The Temporal Service persists the state of your application and has built-in retries, task queues, signals, and timers. Essential for durable execution of long-running maintenance workflows.
Starlette        Latest        ASGI Foundation        Underlying framework for FastAPI, provides WebSocket support and async capabilities.
3.2.2 Supporting Libraries
AI and Natural Language Processing:


# Core AI Libraries
langgraph==1.0.5           # AI workflow orchestration
langchain-core==0.3.0      # Core LangChain components
langchain-openai==0.2.0    # OpenAI integration
langchain-anthropic==0.2.0 # Anthropic Claude integration


#### Speech Processing
deepgram-sdk==3.5.0        # Speech-to-text processing
elevenlabs==1.8.0          # Text-to-speech synthesis
whisper-openai==20231117   # Backup speech recognition


#### Vector Database
chromadb==0.5.0            # Vector storage for troubleshooting KB
sentence-transformers==3.0.0 # Text embeddings
Web Framework and API:


# Web Framework
fastapi[standard]==0.125.0  # Web framework with standard dependencies
uvicorn[standard]==0.30.0   # ASGI server with performance optimizations
starlette==0.40.0           # ASGI framework foundation


#### Data Validation
pydantic==2.10.0           # Data validation and serialization
pydantic-settings==2.6.0   # Configuration management
Workflow and State Management:


# Workflow Orchestration
temporalio==1.8.0          # Temporal workflow SDK
temporal-sdk==1.8.0        # Temporal Python SDK


#### State Management
redis==5.2.0               # Session state and caching
redis-py-cluster==2.1.3    # Redis cluster support
3.2.3 Compatibility Requirements
Framework Compatibility Matrix:


FastAPI 0.125.0+ requires Python 3.9+
LangGraph 1.0.5 requires Python 3.9+
Temporal SDK 1.8.0+ requires Python 3.8+
All frameworks support async/await patterns
Integration Requirements:


All frameworks must support dependency injection patterns
WebSocket support required for real-time voice processing
OpenAPI 3.1 compatibility for API documentation
Prometheus metrics integration for observability
3.3 Open Source Dependencies
3.3.1 Third-party Libraries
Communication and Telephony:


# Telephony Integration
twilio==9.3.0              # Voice and SMS communication
twilio-python==9.3.0       # Twilio Python SDK


#### Email Processing
sendgrid==6.11.0           # Email delivery service
email-validator==2.2.0     # Email validation utilities
Data Processing and Storage:


# Database Drivers
motor==3.6.0               # Async MongoDB driver
pymongo==4.10.0            # MongoDB Python driver
redis==5.2.0               # Redis Python client


#### Data Processing
pandas==2.2.0              # Data manipulation and analysis
numpy==2.1.0               # Numerical computing
python-dateutil==2.9.0     # Date/time utilities
Security and Authentication:


# Security
cryptography==43.0.0       # Cryptographic operations
bcrypt==4.2.0              # Password hashing
python-jose[cryptography]==3.3.0  # JWT token handling
passlib[bcrypt]==1.7.4     # Password hashing utilities
Monitoring and Observability:


# Metrics and Monitoring
prometheus-client==0.21.0  # Prometheus metrics
structlog==24.4.0          # Structured logging
opentelemetry-api==1.27.0  # Distributed tracing
opentelemetry-sdk==1.27.0  # OpenTelemetry SDK
3.3.2 Package Dependencies And Registries
Primary Package Registry:


PyPI (Python Package Index) for all Python dependencies
Package management via pip with requirements.txt and pip-tools
Dependency pinning strategy: exact versions for production, compatible versions for development
Dependency Management Strategy:


# requirements.in (high-level dependencies)
fastapi[standard]>=0.125.0,<0.126.0
langgraph>=1.0.5,<1.1.0
temporalio>=1.8.0,<1.9.0
twilio>=9.3.0,<10.0.0


## requirements.txt (generated with pip-compile)
#### Exact pinned versions for reproducible builds
Security Scanning:


Regular dependency vulnerability scanning with safety
Automated dependency updates via Dependabot
License compliance checking for all dependencies
3.4 Third-party Services
3.4.1 External Apis And Integrations
Service Category        Provider        Purpose        Integration Method
Telephony        Twilio        Voice calls, SMS messaging        The Twilio APIs are organized around REST. Behind these APIs is a software layer connecting and optimizing communications networks around the world
Email Delivery        SendGrid        Email notifications and parsing        REST API with webhook integration
Property Management        AppFolio, Yardi        Work order synchronization        OAuth 2.0 REST APIs with webhooks
AI Language Models        OpenAI, Anthropic        Natural language processing        API key authentication with rate limiting
Payment Processing        Treasury/TigerBeetle        Invoice and payment handling        MCP server integration
3.4.2 Authentication Services
API Authentication:


OAuth 2.0 for PMS integrations (AppFolio, Yardi)
API key authentication for Twilio, SendGrid
Bearer token authentication for AI services
Webhook signature verification for all inbound integrations
Security Requirements:


TLS 1.3 for all external communications
API key rotation capabilities
Rate limiting and circuit breaker patterns
Audit logging for all external service calls
3.4.3 Monitoring And Observability Tools
Monitoring Stack:


# Observability Services
prometheus:
  version: "2.50.0"
  purpose: "Metrics collection and alerting"
  
grafana:
  version: "11.0.0"
  purpose: "Metrics visualization and dashboards"
  
jaeger:
  version: "1.60.0"
  purpose: "Distributed tracing"
  
elk-stack:
  elasticsearch: "8.15.0"
  logstash: "8.15.0"
  kibana: "8.15.0"
  purpose: "Centralized logging and log analysis"
3.5 Databases & Storage
3.5.1 Primary Database Systems
Database        Version        Purpose        Justification
MongoDB        8.0.17+        Primary Data Store        MongoDB 8.0.17 contains a fix for CVE-2025-14847. For the latest information about MongoDB security updates, see MongoDB Security Bulletins. Document-oriented storage ideal for flexible maintenance data schemas.
Redis        8.4+        Session State & Caching        This is the General Availability release of Redis 8.4 in Redis Open Source. For developers, who are building real-time data-driven applications, Redis is the preferred, fastest, and most feature-rich cache, data structure server.
TimescaleDB        2.17+        Time-Series Metrics        Specialized for time-series analytics and performance metrics storage.
3.5.2 Data Persistence Strategies
MongoDB Collections:


// Primary Collections
{
  "work_orders": {
    "indexes": ["property_id", "status", "created_at", "resident_id"],
    "sharding_key": "property_id",
    "retention": "7_years"
  },
  "properties": {
    "indexes": ["property_id", "owner_id", "zip_code"],
    "retention": "indefinite"
  },
  "vendors": {
    "indexes": ["vendor_id", "service_types", "coverage_area"],
    "retention": "indefinite"
  },
  "communications": {
    "indexes": ["work_order_id", "timestamp", "channel"],
    "retention": "3_years",
    "time_series": true
  }
}
Redis Data Structures:


# Session State Management
session_state = {
    "pattern": "session:{session_id}",
    "ttl": 86400,  # 24 hours
    "structure": "hash"
}


#### Conversation Context
conversation_cache = {
    "pattern": "conv:{work_order_id}",
    "ttl": 3600,   # 1 hour
    "structure": "list"
}


#### Rate Limiting
rate_limits = {
    "pattern": "rate:{endpoint}:{client_id}",
    "ttl": 60,     # 1 minute
    "structure": "counter"
}
3.5.3 Caching Solutions
Multi-Layer Caching Strategy:


# L1 Cache: Application Memory
app_cache = {
    "type": "in_memory",
    "library": "cachetools",
    "ttl": 300,  # 5 minutes
    "max_size": 1000,
    "use_cases": ["property_profiles", "vendor_lists"]
}


#### L2 Cache: Redis
redis_cache = {
    "type": "distributed",
    "ttl": 3600,  # 1 hour
    "use_cases": ["troubleshooting_kb", "vendor_availability"]
}


#### L3 Cache: Database Query Cache
db_cache = {
    "type": "query_result",
    "ttl": 86400,  # 24 hours
    "use_cases": ["historical_costs", "vendor_performance"]
}
3.5.4 Storage Services
File Storage:


AWS S3 for document attachments (photos, invoices)
CloudFront CDN for static asset delivery
Local filesystem for temporary file processing
Backup and Recovery:


MongoDB Atlas automated backups with point-in-time recovery
Redis persistence with AOF and RDB snapshots
Cross-region replication for disaster recovery
3.6 Development & Deployment
3.6.1 Development Tools
Development Environment:


# Development Stack
python_version: "3.12"
package_manager: "pip-tools"
virtual_environment: "venv"
code_formatter: "black==24.0.0"
import_sorter: "isort==5.13.0"
linter: "ruff==0.7.0"
type_checker: "mypy==1.13.0"
testing_framework: "pytest==8.3.0"
IDE and Editor Support:


VS Code with Python extension pack
PyCharm Professional for advanced debugging
Jupyter notebooks for data analysis and model experimentation
Git hooks for automated code quality checks
3.6.2 Build System
Build Configuration:


# Multi-stage Dockerfile
FROM python:3.12-slim as base
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt


FROM base as development
COPY requirements-dev.txt .
RUN pip install --no-cache-dir -r requirements-dev.txt
COPY . .
CMD ["fastapi", "dev", "main.py"]


FROM base as production
COPY . .
RUN pip install --no-cache-dir -e .
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
Build Automation:


Docker multi-stage builds for optimized production images
Docker has made its catalogue of more than 1,000 hardened container images freely available under an open source licence. Docker Hardened Images were previously a commercial offering launched in May 2025, but are now accessible to all developers under an Apache 2.0 licence
Automated dependency vulnerability scanning
Image size optimization with distroless base images
3.6.3 Containerization
Container Strategy:


# Docker Compose for Development
version: '3.8'
services:
  ai-coordinator:
    build: .
    ports:
      - "8000:8000"
    environment:
      - MONGODB_URL=mongodb://mongo:27017
      - REDIS_URL=redis://redis:6379
    depends_on:
      - mongo
      - redis
      - temporal


  mongo:
    image: mongo:8.0
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db


  redis:
    image: redis:8.4-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data


  temporal:
    image: temporalio/temporal:1.25.0
    ports:
      - "7233:7233"
      - "8233:8233"
    environment:
      - DB=postgresql
      - DB_PORT=5432
Production Container Configuration:


Hardened base images with minimal attack surface
Non-root user execution for security
Resource limits and health checks
Multi-architecture support (AMD64, ARM64)
3.6.4 Ci/cd Requirements
Continuous Integration Pipeline:


# GitHub Actions Workflow
name: CI/CD Pipeline
on: [push, pull_request]


jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: [3.11, 3.12]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install dependencies
        run: |
          pip install -r requirements-dev.txt
      - name: Run tests
        run: |
          pytest --cov=src --cov-report=xml
      - name: Upload coverage
        uses: codecov/codecov-action@v4


  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run security scan
        run: |
          pip install safety bandit
          safety check
          bandit -r src/


  deploy:
    needs: [test, security]
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - name: Deploy to staging
        run: |
          docker build -t ai-coordinator:latest .
          docker push ${{ secrets.REGISTRY_URL }}/ai-coordinator:latest
Deployment Strategy:


Blue-green deployments for zero-downtime updates
Automated rollback on health check failures
Environment-specific configuration management
Database migration automation with Temporal workflows
3.7 Technology Integration Architecture
3.7.1 Service Communication Patterns
External Services


Cold Path (Durable Workflows)


Hot Path (Real-time AI)


FastAPI REST API


LangGraph AI Engine


Redis Session Store


Temporal Workflows


MongoDB Data Store


TimescaleDB Metrics


Twilio Voice/SMS


SendGrid Email


Property Management Systems


OpenAI/Anthropic APIs


3.7.2 Technology Selection Rationale
Hot Path Architecture:


FastAPI: Very high performance, on par with NodeJS and Go (thanks to Starlette and Pydantic)
LangGraph: LangGraph's low-level primitives provide the flexibility needed to create fully customizable agents. Trusted by companies shaping the future of agents – including Klarna, Replit, Elastic, and more
Redis: For developers, who are building real-time data-driven applications, Redis is the preferred, fastest, and most feature-rich cache, data structure server
Cold Path Architecture:


Temporal: Temporal Workflows automatically capture state at every step, and in the event of failure, can pick up exactly where they left off. No lost progress, no orphaned processes, and no manual recovery required
MongoDB: Document-oriented storage ideal for flexible maintenance data schemas with strong consistency guarantees
TimescaleDB: Optimized for time-series analytics and performance metrics
3.7.3 Scalability And Performance Considerations
Horizontal Scaling Strategy:


Stateless FastAPI services with load balancing
Redis cluster for distributed session management
MongoDB sharding by property_id for data distribution
Temporal workers auto-scaling based on queue depth
Performance Optimization:


Connection pooling for all database connections
Async I/O throughout the application stack
Caching at multiple layers (application, Redis, CDN)
Background task processing for non-critical operations
Resource Requirements:


# Production Resource Allocation
services:
  fastapi:
    cpu: "1000m"
    memory: "2Gi"
    replicas: 3
  
  langgraph:
    cpu: "2000m"
    memory: "4Gi"
    replicas: 2
  
  temporal-worker:
    cpu: "1000m"
    memory: "2Gi"
    replicas: 5
This technology stack provides a robust foundation for the AI Maintenance Coordinator system, balancing performance, reliability, and developer productivity while ensuring compatibility with existing property management ecosystems.


4. Process Flowchart
4.1 System Workflows
4.1.1 Core Business Processes
End-to-end Maintenance Request Workflow
The AI Maintenance Coordinator implements a comprehensive end-to-end workflow that transforms maintenance operations from reactive chaos to proactive automation. LangGraph is a low-level orchestration framework for building, managing, and deploying long-running, stateful agents and is the first stable major release in the durable agent framework space, providing the foundation for complex maintenance workflows.


External Systems


Orchestration Layer - Cold Path


Action Layer


Decision Points


Brain Layer - Hot Path


Intake Layer


Resident Channels


Yes


No


Yes


No


Yes


No


Approved


Denied


Phone Call


SMS/Text


Email


Portal Request


Unified Request Processor


Request Validation


Create Work Order


AI Triage Engine


Issue Classification


Load Property Context


Troubleshooting Engine


Emergency
Detected?


Issue
Resolved?


Cost Exceeds
Threshold?


Vendor Selection


Vendor Dispatch


Appointment Scheduling


Notification Engine


Temporal Workflows


State Management


Billing Workflow


Property Management System


Vendor Network


Payment System


Immediate Escalation


Close as Resolved


Approval Workflow


Close as Declined


Human Intervention


User Journey Mapping
Resident Experience Journey:


Stage        Touchpoint        AI Action        Resident Experience        SLA Target
1. Issue Occurs        Any channel (phone/SMS/email/portal)        Instant acknowledgment        "My call was answered immediately"        <30 seconds
2. Issue Description        Conversational interface        Natural language understanding        "I explained the problem naturally"        <2 minutes
3. Troubleshooting        Interactive guidance        Step-by-step instructions        "They walked me through simple fixes"        3-10 minutes
4. Resolution Path        Automated decision        Vendor dispatch or self-resolution        "Either I fixed it myself or help is coming"        <30 minutes
5. Scheduling        Calendar coordination        Optimal appointment booking        "Got a convenient appointment time"        <1 hour
6. Service Delivery        Vendor coordination        Real-time updates        "I knew exactly when they'd arrive"        Real-time
7. Completion        Verification process        Quality confirmation        "They confirmed everything was fixed"        <24 hours
8. Follow-up        Satisfaction tracking        Feedback collection        "They cared about my experience"        48 hours
Property Manager Experience Journey:


Stage        Touchpoint        AI Action        Manager Experience        Value Delivered
1. Request Intake        Dashboard notification        Automatic work order creation        "Requests appear without my input"        100% capture rate
2. Triage        AI classification        Intelligent categorization        "Issues are pre-sorted by priority"        80% time savings
3. Vendor Management        Automated dispatch        Optimal vendor selection        "Best vendors are already contacted"        Cost optimization
4. Coordination        Status updates        Real-time progress tracking        "I see everything without managing it"        Full visibility
5. Escalation        Exception handling        Human-in-the-loop when needed        "I only handle complex cases"        85% automation
6. Reporting        Analytics dashboard        Performance insights        "I have data to optimize operations"        Data-driven decisions
System Interaction Patterns
Hot Path vs Cold Path Architecture:


Because the full running state of a Workflow is durable and fault tolerant by default, your business logic can be recovered, replayed, or paused at any point, enabling the system to handle both immediate AI decisions and long-running maintenance processes.


Cold Path - Durable Workflows


Hot Path - Real-time AI Reasoning


<500ms


<5s


Maintenance Request


LangGraph AI Engine


Immediate Decision


Real-time Response


Work Order Creation


Temporal Workflow


State Tracking


Completion Processing


4.1.2 Integration Workflows
Property Management System Integration Flow
The system integrates bidirectionally with major PMS platforms through a unified integration layer using Model Context Protocol (MCP) servers for seamless connectivity.


Temporal Workflow
Vendor
Property Management System
AI Coordinator
Resident
Temporal Workflow
Vendor
Property Management System
AI Coordinator
Resident
Reports maintenance issue
Validate resident/property
Property context & history
Classify & triage issue
Create work order
Work order ID
Start workflow orchestration
Vendor selection request
Dispatch vendor
Confirmation & ETA
Update work order status
Notify appointment scheduled
Monitor progress
Job completion
Close work order
Trigger billing workflow
Data Flow Between Systems
Inbound Data Flow:


PMS → AI Coordinator: Property profiles, unit details, resident information, existing work orders
Residents → AI Coordinator: Maintenance requests, status inquiries, feedback
Vendors → AI Coordinator: Job confirmations, status updates, completion reports, invoices
Outbound Data Flow:


AI Coordinator → PMS: New work orders, status updates, completion records, cost data
AI Coordinator → Residents: Acknowledgments, status updates, appointment confirmations
AI Coordinator → Vendors: Job assignments, property details, scheduling information
AI Coordinator → Payment Systems: Invoice processing, payment authorizations
Event Processing Flows
Agent execution state persists automatically. If your server restarts mid-conversation or a long-running workflow gets interrupted, it picks up exactly where it left off without losing context.


Persistence Layer


Event Handlers


Event Processing Pipeline


Event Sources


PMS Webhook Events


Resident Communications


Vendor Updates


System Events


Event Router


Event Validation


Context Enrichment


Event Dispatcher


Work Order Handler


Notification Handler


State Update Handler


Metrics Handler


Event Store


State Store


Audit Log


Batch Processing Sequences
Daily Synchronization Process:


Error Handling


Daily Sync Workflow


No


Yes


Max Retries


Start Daily Sync


Sync Property Data


Sync Vendor Data


Calculate Daily Metrics


Generate Reports


Cleanup Old Data


Complete Sync


Sync Error?


Retry with Backoff


Escalate to Admin


4.2 Flowchart Requirements
4.2.1 Process Steps And Decision Points
Maintenance Request Processing Flow
Vendor Dispatch Process


Troubleshooting Decision Tree


Triage and Classification


Request Intake Process


Voice


SMS


Email


Portal


Yes


No


Yes


No


Yes


No


No


Yes


Request Received


Channel Type?


Voice Processing


SMS Processing


Email Processing


Portal Processing


Convert to Unified Format


Load Property Context


Classify Issue Category


Determine Urgency Level


Emergency Keywords?


Contextual Analysis


Attempt Troubleshooting?


Load Knowledge Base Entry


Interactive Troubleshooting


Issue Resolved?


Document Outcome


Vendor Selection Algorithm


Check Vendor Availability


Dispatch to Vendor


Vendor Confirms?


Try Next Vendor


Schedule Appointment


Emergency Escalation


Close as Resolved


Approval Workflow Process
Approval Response


Approval Routing


Cost Analysis


No


Yes


Yes


No


Yes


No


Approved


Denied


More Info


Estimate Repair Cost


Cost > Threshold?


Category Exception?


Emergency Override?


Property Manager Approval


Owner Approval


Auto-Approve


Approval Decision?


Proceed with Dispatch


Deny Request


Request More Information


4.2.2 System Boundaries And User Touchpoints
System Boundary Definition
External Systems


AI Maintenance Coordinator System Boundary


External Actors


Integration Layer


Core System


Phone/SMS/Email


Dashboard/API


Portal/SMS/Email


Portal/Email


Data Layer


MongoDB


Redis Cache


Vector Database


Residents/Tenants


Property Managers


Maintenance Vendors


Property Owners


Intake Layer


Brain Layer


Action Layer


Orchestration Layer


MCP Servers


API Gateway


Webhook Handlers


Property Management Systems


Twilio Telephony


SendGrid Email


Payment Systems


AI Model Providers


4.2.3 Error States And Recovery Paths
Comprehensive Error Handling Flow
LangGraph 1.0 stabilizes four core runtime features that separate production agents from demos. Durable Execution. Your agent is three steps into a ten-step workflow when the server restarts. With LangGraph, it picks up exactly where it left off. Checkpointing saves state at every node execution.


Recovery Verification


Escalation Paths


Recovery Strategies


Error Detection


Network/Timeout


Service Unavailable


Data Corruption


System Error Detected


Error Type?


Transient Error


Recoverable Error


Critical Error


Exponential Backoff Retry


Circuit Breaker Pattern


Fallback Mechanism


Graceful Degradation


Automatic Recovery


Alert Operations Team


Human Intervention Required


Emergency Protocol


Health Check


State Validation


Resume Normal Operation


Generate Incident Report


Vendor Communication Error Handling
Resident Communication


Recovery Actions


Vendor Dispatch Errors


Yes


No


Yes


No


No


Yes


Start Vendor Dispatch


Contact Primary Vendor


Response Timeout?


Vendor Declines?


All Vendors Unavailable?


Try Next Vendor


Extend Search Radius


Contact Emergency Vendor


Escalate to Human


Notify Resident of Delay


Provide Status Update


Offer Alternatives


Apologize and Resolve


Vendor Confirmed


4.3 Validation Rules
4.3.1 Business Rules At Each Step
Request Validation Rules
Validation Point        Rule        Action if Failed        Recovery Path
**Resident Identity**        Must be valid resident of property        Request additional verification        Ask for unit number and name
**Property Access**        Property must be in managed portfolio        Reject request politely        Provide correct contact information
**Issue Description**        Must contain actionable information        Request clarification        Ask follow-up questions
**Urgency Classification**        Must match emergency keyword patterns        Default to routine priority        Allow manual override
**Vendor Eligibility**        Must be active and compliant        Skip to next vendor        Expand search criteria
Data Validation Requirements
Work Order Data Validation:


class WorkOrderValidation:
    required_fields = [
        "property_id", "unit_id", "resident_id", 
        "issue_description", "issue_category", "urgency"
    ]
    
    validation_rules = {
        "property_id": "must_exist_in_pms",
        "unit_id": "must_belong_to_property", 
        "resident_id": "must_be_current_resident",
        "issue_description": "min_length_10_chars",
        "urgency": "must_be_valid_enum",
        "estimated_cost": "must_be_positive_number"
    }
    
    business_rules = {
        "emergency_validation": "require_human_confirmation_for_emergency",
        "cost_validation": "require_approval_above_threshold",
        "vendor_validation": "must_be_active_and_compliant"
    }
4.3.2 Authorization Checkpoints
Role-based Authorization Matrix
Action        Resident        Property Manager        Regional Manager        Owner        AI Agent
Create Work Order        Own unit only        All managed properties        All properties        Own properties        All (with validation)
View Work Orders        Own only        All managed        All        Own properties        All (context-aware)
Approve Costs        N/A        Up to $500        Up to $2000        Unlimited        Up to threshold
Override AI Decision        N/A        Yes        Yes        Yes        N/A
Access Financial Data        N/A        Property level        Portfolio level        Own properties        Aggregated only
Escalate to Human        Yes        Yes        Yes        Yes        Automatic triggers
Authorization Flow
Special Cases


Authorization Process


No


Yes


No


Yes


Yes


No


Yes


No


Authorization Request


Identify User/Agent


Load Role Permissions


Resource Access?


Action Permitted?


Grant Access


Deny Access


Log Access Attempt


Emergency Override?


Owner Override?


AI Within Limits?


4.3.3 Regulatory Compliance Checks
Compliance Validation Flow
Compliance Actions


Regulatory Requirements


Compliance Checkpoints


Data Retention Policy Check


Privacy Consent Validation


Audit Log Requirements


Access Code Security


GDPR Compliance


CCPA Compliance


Local Housing Laws


Insurance Requirements


Data Minimization


Consent Management


Secure Data Storage


Compliance Reporting


4.4 Technical Implementation
4.4.1 State Management
Work Order State Machine Implementation
Because the full running state of a Workflow is durable and fault tolerant by default, your business logic can be recovered, replayed, or paused at any point, ensuring no work orders are lost during system failures.


Auto-transition (30s)


Non-emergency


Skip troubleshooting


Emergency detected


Issue fixed remotely


Vendor needed


Timeout (10 min)


Cost > threshold


Auto-approve


Approved


Denied


Timeout (24h)


Vendor confirmed


No vendor available (30 min)


Vendor departing


Schedule change


Cancellation


Vendor arrived


Vendor no-show


Parts required


Work completed


Complications


Parts obtained


Verified


Not satisfied


Issue recurred


Issue recurred


Restart process


Human resolved


Find replacement


New time confirmed


NEW


TRIAGING


TROUBLESHOOTING


AWAITING_DISPATCH


ESCALATED


RESOLVED


AWAITING_APPROVAL


DISPATCHING


CANCELLED


SCHEDULED


VENDOR_EN_ROUTE


RESCHEDULED


IN_PROGRESS


NO_SHOW


NEEDS_PARTS


PENDING_VERIFICATION


COMPLETED


REOPENED


State Persistence Strategy
Temporal Workflow State Management:


@workflow.defn
class MaintenanceWorkflow:
    def __init__(self):
        self.state = WorkOrderState()
        self.context = MaintenanceContext()
        
    @workflow.run
    async def run(self, request: MaintenanceRequest) -> WorkOrderResult:
        # State automatically persisted at each step
        self.state.status = WorkOrderStatus.NEW
        await workflow.sleep(30)  # Auto-transition delay
        
        # Triage phase - state persisted
        self.state.status = WorkOrderStatus.TRIAGING
        triage_result = await workflow.execute_activity(
            triage_activity,
            request,
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        # State transitions with automatic persistence
        if triage_result.is_emergency:
            self.state.status = WorkOrderStatus.ESCALATED
            return await self.handle_emergency()
        
        # Continue workflow with durable state...
4.4.2 Data Persistence Points
Critical Persistence Checkpoints
Checkpoint        Data Persisted        Storage System        Recovery Strategy
**Request Intake**        Raw request data, channel info, timestamp        MongoDB        Replay from intake
**Triage Completion**        Classification, urgency, context        MongoDB + Redis        Resume from triage
**Troubleshooting Steps**        Q&A transcript, outcomes        MongoDB        Resume troubleshooting
**Vendor Dispatch**        Vendor selection, communication log        MongoDB        Retry dispatch
**Appointment Scheduling**        Calendar data, confirmations        MongoDB        Reschedule if needed
**Work Completion**        Resolution details, costs, feedback        MongoDB        Verify completion
**Billing Processing**        Invoice data, payment status        MongoDB + Payment System        Resume billing
Transaction Boundaries
Rollback Scenarios


Transaction Scope 3: Completion


Transaction Scope 2: Vendor Dispatch


Transaction Scope 1: Request Processing


Failure


Failure


Failure


Begin Transaction


Create Work Order


Update PMS


Send Acknowledgment


Commit Transaction


Begin Transaction


Select Vendor


Contact Vendor


Update Status


Commit Transaction


Begin Transaction


Verify Work


Process Invoice


Close Work Order


Commit Transaction


Rollback T1


Rollback T2


Rollback T3


Compensating Actions


4.4.3 Caching Requirements
Multi-layer Caching Strategy
Cache Invalidation


Property Data Update


Invalidate L1


Vendor Data Update


Configuration Change


Invalidate L2


Invalidate L3


L3 Cache - Database Query Cache


Historical Costs


Vendor Performance


Property History


TTL: 24 hours


L2 Cache - Redis Distributed


Session State


Conversation Context


Troubleshooting KB


TTL: 1 hour


L1 Cache - Application Memory


Property Profiles


Vendor Lists


Configuration Data


TTL: 5 minutes


4.5 Required Diagrams
4.5.1 High-level System Workflow
Data Layer


Integration Layer


Workflow Orchestration Layer


AI Processing Layer


Resident Interaction Layer


Multi-Channel Intake
Phone • SMS • Email • Portal


Instant Response
<30 seconds


AI Maintenance Coordinator


Intelligent Triage


Remote Troubleshooting


Vendor Management


Temporal Workflow Engine


Durable State Management


Process Orchestration


PMS Integration


Vendor Portal


Payment Integration


Notification System


MongoDB
Work Orders • Properties • Vendors


Redis
Session State • Cache


Vector DB
Troubleshooting KB


4.5.2 Detailed Process Flows For Core Features
Voice Call Processing Flow
Error Handling


Voice Call Workflow


No


Yes


Yes


No


Error


Incoming Call


Answer Call
Twilio WebSocket


Play Greeting
Text-to-Speech


Listen for Speech
Speech-to-Text


Process Speech
NLU Engine


Intent
Understood?


Ask for Clarification


Extract Issue Details


Confirm Understanding


Create Work Order


Start Troubleshooting


Interactive Troubleshooting


Issue
Resolved?


Dispatch Vendor


Confirm Appointment


End Call Gracefully


Speech Recognition Error


Technical Issue


Transfer to Human


Vendor Selection And Dispatch Flow
Escalation Paths


Communication Methods


Vendor Selection Process


Timeout


Response


Yes


No


No More Vendors


Start Vendor Selection


Load Eligible Vendors


Filter by Service Category


Filter by Coverage Area


Filter by Availability


Score Vendors
Performance • Cost • Familiarity


Rank Top 3 Vendors


Select Primary Vendor


Contact Vendor


Vendor
Response?


Vendor
Accepts?


Schedule Appointment


Try Next Vendor


No Vendors Available


SMS Contact


Phone Contact


Email Contact


Portal Contact


Extend Search Radius


Emergency Vendor Network


Escalate to Human


4.5.3 State Transition Diagrams
Comprehensive State Transition Matrix
Recovery States


Terminal States


Execution States


Processing States


Initial States


30s auto


Non-emergency


Skip troubleshooting


Emergency


Timeout 2min


Resolved


Vendor needed


Timeout 10min


Cost > threshold


Auto-approve


Approved


Denied


Timeout 24h


Vendor confirmed


No vendors 30min


Vendor departing


Schedule change


Cancelled


Arrived


No show


Parts needed


Work done


Complications


Parts obtained


Verified


Not satisfied


Timeout 24h


Issue recurred


Issue recurred


Human resolved


NEW
Request received


TRIAGING
AI analyzing


TROUBLESHOOTING
Interactive guidance


AWAITING_DISPATCH
Ready for vendor


AWAITING_APPROVAL
Cost approval needed


DISPATCHING
Contacting vendors


SCHEDULED
Appointment confirmed


VENDOR_EN_ROUTE
Vendor traveling


IN_PROGRESS
Work being performed


NEEDS_PARTS
Parts required


PENDING_VERIFICATION
Awaiting confirmation


COMPLETED
Successfully resolved


RESOLVED
Self-resolved


CANCELLED
Request cancelled


ESCALATED
Human intervention


REOPENED
Issue recurred


RESCHEDULED
Time changed


NO_SHOW
Vendor missed


4.5.4 Integration Sequence Diagrams
Pms Integration Sequence
Vendor
Temporal Workflow
AppFolio/Yardi
MCP-PMS Server
AI Coordinator
Resident
Vendor
Temporal Workflow
AppFolio/Yardi
MCP-PMS Server
AI Coordinator
Resident
Complete PMS Integration Flow
loop
[Progress Monitoring]
Submit maintenance request
Validate resident identity
GET /residents/{id}
Resident data
Validation result
Load property context
GET /properties/{id}
Property profile
Property context
Triage and classify
Create work order
POST /work-orders
Work order ID
Work order created
Start maintenance workflow
Request vendor dispatch
Contact vendor
Accept job
Update work order status
PATCH /work-orders/{id}
Update confirmed
Check status
Get work order status
GET /work-orders/{id}
Current status
Status data
Status update
Job completed
Close work order
PATCH /work-orders/{id}
Closure confirmed
Complete workflow
4.5.5 Timing And Sla Considerations
Performance Requirements Matrix
Process Stage        Target Latency        SLA Requirement        Escalation Trigger        Recovery Action
**Request Acknowledgment**        <5 seconds        95% under 30s        >30s response time        Immediate alert to ops
**AI Triage**        <30 seconds        90% under 2 min        >2 min processing        Escalate to human
**Troubleshooting**        <5 minutes        80% resolution in 10 min        >10 min session        Skip to vendor dispatch
**Vendor Dispatch**        <15 minutes        95% under 30 min        >30 min no vendor        Emergency vendor network
**Appointment Scheduling**        <1 hour        90% same day        >24h delay        Manager notification
**Work Completion**        <24 hours        85% within SLA        >48h for urgent        Escalate to regional manager
Sla Monitoring Flow
Escalation Levels


SLA Monitoring System


Yes


Warning


Breach


No Response


No Response


SLA Timer Started


Check Progress


Within SLA?


Continue Monitoring


SLA Warning Alert


SLA Breach Alert


Trigger Escalation


Property Manager
15 min SLA


Regional Manager
30 min SLA


Emergency On-Call
5 min SLA


This comprehensive process flowchart section provides detailed workflows, decision points, error handling paths, and technical implementation details for the AI Maintenance Coordinator system. Built-in persistence enables saving and resuming agent workflows at any point without writing custom database logic, enabling multi-day approval processes, background jobs, and workflows that span multiple sessions, ensuring robust and reliable maintenance operations.


5. System Architecture
5.1 High-level Architecture
5.1.1 System Overview
The AI Maintenance Coordinator implements a sophisticated dual-path architecture that separates real-time AI reasoning from durable workflow orchestration. LangGraph 1.0 is the first stable major release in the durable agent framework space —a major milestone for production-ready AI systems. Agent execution state persists automatically. If your server restarts mid-conversation or a long-running workflow gets interrupted, it picks up exactly where it left off without losing context.


The system follows a layered architectural pattern optimized for both immediate responsiveness and long-term reliability. The Hot Path handles real-time AI decisions with sub-500ms latency requirements, while the Cold Path manages durable workflows with exactly-once execution guarantees. Write your business logic as code as a Temporal Workflow. Because the full running state of a Workflow is durable and fault tolerant by default, your business logic can be recovered, replayed, or paused at any point. The Temporal Service persists the state of your application and has built-in retries, task queues, signals, and timers.


Key Architectural Principles:


Separation of Concerns: Clear boundaries between intake, intelligence, action, and orchestration layers
Fault Tolerance: Temporal Workflows automatically capture state at every step, and in the event of failure, can pick up exactly where they left off. No lost progress, no orphaned processes, and no manual recovery required.
Scalability: Horizontal scaling with stateless services and distributed state management
Integration-First: Native integration with existing property management ecosystems without replacement
System Boundaries:


The system operates within the existing property management technology ecosystem, integrating seamlessly with major PMS platforms through standardized APIs and webhook patterns. External boundaries include resident communication channels (voice, SMS, email, portal), vendor networks, payment systems, and property management platforms.


5.1.2 Core Components Table
Component Name        Primary Responsibility        Key Dependencies        Integration Points        Critical Considerations
**Intake Layer**        Multi-channel request reception and normalization        Twilio, SendGrid, PMS webhooks        Voice/SMS/Email/Portal channels        Real-time processing, channel unification
**Brain Layer**        AI-powered triage, classification, and troubleshooting        LangGraph trusted by companies shaping the future of agents – including Klarna, Replit, Elastic, and more        OpenAI/Anthropic APIs, Vector DB        Sub-500ms response times, confidence scoring
**Action Layer**        Vendor dispatch, scheduling, and notification delivery        Vendor databases, calendar systems        SMS/Email providers, vendor portals        Reliability, timeout handling
**Orchestration Layer**        Durable workflow management and state persistence        The Temporal Service persists the state of your application and has built-in retries, task queues, signals, and timers        MongoDB, payment systems        Exactly-once execution, state durability
5.1.3 Data Flow Description
Primary Data Flows:


The system processes maintenance requests through a unified pipeline that transforms multi-channel inputs into structured work orders. Resident requests enter through voice calls (processed via Twilio WebSocket streaming), SMS messages, email parsing, or direct portal API submissions. All channels converge into a standardized MaintenanceRequest data structure that feeds the AI Brain Layer.


The Brain Layer performs intelligent triage using LangGraph is a lower level framework and runtime, useful for highly custom and controllable agents, designed to support production-grade, long running agents for complex decision workflows. Property context loading occurs dynamically, pulling relevant historical data, vendor preferences, and unit-specific information from MongoDB collections.


Integration Patterns:


Bidirectional data synchronization with Property Management Systems occurs through Model Context Protocol (MCP) servers, ensuring real-time consistency between the AI Coordinator and existing business systems. Vendor communication flows through multiple channels with confirmation tracking and automatic retry logic.


Data Transformation Points:


Channel Normalization: Raw inputs transformed to unified MaintenanceRequest schema
Context Enrichment: Property and unit data merged with request details
Vendor Selection: Multi-criteria scoring algorithms produce ranked vendor lists
State Transitions: Work order status updates propagated across all integrated systems
5.1.4 External Integration Points
System Name        Integration Type        Data Exchange Pattern        Protocol/Format        SLA Requirements
**AppFolio/Yardi PMS**        Bidirectional API + Webhooks        Work orders, property data, resident info        OAuth 2.0 REST + JSON        <2s response time
**Twilio Telephony**        Real-time WebSocket + REST        Voice streams, SMS messages        WebSocket + REST API        <200ms voice latency
**Vendor Networks**        Multi-channel dispatch        Job assignments, status updates        SMS/Email/Portal API        95% delivery rate
**Payment Systems**        MCP Server Integration        Invoice processing, payment tracking        TigerBeetle/Treasury API        Exactly-once processing
5.2 Component Details
5.2.1 Intake Layer Architecture
Purpose and Responsibilities:


The Intake Layer serves as the unified entry point for all maintenance requests, handling the complexity of multi-channel communication while presenting a consistent interface to downstream systems. It implements real-time voice processing, SMS conversation threading, email parsing with attachment handling, and structured API request validation.


Technologies and Frameworks:


FastAPI 0.125.0+: One of the fastest Python frameworks available. Provides high-performance REST API endpoints with automatic OpenAPI documentation
Twilio WebSocket: Real-time voice processing with speech-to-text and text-to-speech capabilities
SendGrid: Email processing with attachment handling and thread management
Pydantic v2: Data validation and serialization for all request types
Key Interfaces and APIs:


# Unified Request Processing Interface
class MaintenanceRequest:
    request_id: str
    source_channel: Literal["phone", "sms", "email", "portal"]
    property_id: str
    unit_id: str
    resident_id: str
    issue_description: str
    urgency: UrgencyLevel
    attachments: List[Attachment]
    session_id: str
Scaling Considerations:


The Intake Layer scales horizontally with stateless FastAPI services behind a load balancer. Voice processing requires session affinity for WebSocket connections, while SMS and email processing can distribute freely across instances. Redis provides distributed session state management for conversation threading.


5.2.2 Brain Layer Architecture
Purpose and Responsibilities:


The Brain Layer implements the core AI intelligence for maintenance coordination, including issue classification, urgency determination, property context loading, and interactive troubleshooting. LangGraph provides low-level supporting infrastructure for any long-running, stateful workflow or agent. LangGraph does not abstract prompts or architecture, and provides the following central benefits: Durable execution: Build agents that persist through failures and can run for extended periods, automatically resuming from exactly where they left off.


Technologies and Frameworks:


LangGraph 1.0.5: After more than a year of powering agents at companies like Uber, LinkedIn, and Klarna, LangGraph is officially v1. Provides the orchestration framework for complex AI decision workflows
OpenAI/Anthropic APIs: Large language model inference for natural language understanding
ChromaDB: Vector database for troubleshooting knowledge base storage and retrieval
Redis: Session state management for multi-turn conversations
Key Interfaces and APIs:


# AI Triage Interface
class TriageResult:
    issue_category: IssueCategory
    urgency: UrgencyLevel
    confidence: float
    recommended_action: ActionType
    context: MaintenanceContext


#### Troubleshooting Session Interface
class TroubleshootingSession:
    session_id: str
    work_order_id: str
    current_step: int
    outcome: Optional[TroubleshootingOutcome]
Data Persistence Requirements:


The Brain Layer maintains conversation state in Redis with 24-hour TTL for active sessions. Troubleshooting knowledge base entries are stored in ChromaDB with vector embeddings for semantic search. All AI decisions and confidence scores are logged to MongoDB for audit trails and continuous improvement.


5.2.3 Action Layer Architecture
Purpose and Responsibilities:


The Action Layer executes the decisions made by the Brain Layer, handling vendor selection and dispatch, appointment scheduling, and multi-channel notification delivery. It implements the business logic for vendor scoring algorithms, calendar optimization, and communication template rendering.


Technologies and Frameworks:


FastAPI Services: Stateless microservices for vendor management and scheduling
Redis: Vendor availability caching and rate limiting
MongoDB: Vendor performance metrics and scheduling data
Multi-provider Communication: Twilio (SMS), SendGrid (Email), Slack/Teams (Staff notifications)
Key Interfaces and APIs:


# Vendor Selection Interface
class VendorSelectionResult:
    primary_vendor: Vendor
    backup_vendors: List[Vendor]
    selection_criteria: Dict[str, float]
    estimated_response_time: timedelta


#### Scheduling Interface
class AppointmentResult:
    appointment_id: str
    scheduled_window: TimeWindow
    access_instructions: AccessInstructions
    confirmation_status: ConfirmationStatus
Scaling Considerations:


Action Layer services scale horizontally with no session affinity requirements. Vendor communication implements circuit breaker patterns to handle vendor API failures gracefully. Notification delivery uses queue-based processing to handle high-volume scenarios like storm surges.


5.2.4 Orchestration Layer Architecture
Purpose and Responsibilities:


The Orchestration Layer provides durable execution guarantees for long-running maintenance workflows, ensuring no work orders are lost during system failures. Because the full running state of a Workflow is durable and fault tolerant by default, your business logic can be recovered, replayed, or paused at any point.


Technologies and Frameworks:


Temporal Workflows: Temporal delivers an open-source Durable Execution platform that abstracts away the complexity of building scalable, reliable distributed systems. It presents a development abstraction that preserves complete application state so that in the case of a host or software failure it can seamlessly migrate execution to another machine.
MongoDB: Primary data persistence for work orders, properties, and vendor information
TigerBeetle/Treasury: Financial transaction processing with exactly-once guarantees
Key Interfaces and APIs:


# Temporal Workflow Interface
@workflow.defn
class MaintenanceWorkflow:
    @workflow.run
    async def run(self, request: MaintenanceRequest) -> WorkOrderResult:
        # Durable state management with automatic persistence
        pass


#### State Management Interface
class WorkOrderState:
    status: WorkOrderStatus
    transitions: List[StateTransition]
    context: MaintenanceContext
    audit_trail: List[AuditEvent]
5.3 Technical Decisions
5.3.1 Architecture Style Decisions And Tradeoffs
Microservices vs Monolithic Architecture:


The system adopts a hybrid microservices architecture with clear service boundaries but shared data stores for consistency. This decision balances the operational complexity of full microservices with the scalability and maintainability benefits.


Decision Factor        Microservices Benefits        Monolithic Benefits        Chosen Approach
**Scalability**        Independent scaling per service        Simpler deployment        Hybrid: Core services separate, shared data layer
**Development Velocity**        Team autonomy        Faster initial development        Layered services with clear interfaces
**Operational Complexity**        Higher ops overhead        Simpler monitoring        Containerized services with unified observability
**Data Consistency**        Eventual consistency challenges        Strong consistency        Shared MongoDB with service-level boundaries
Event-Driven vs Request-Response Communication:


The architecture implements hybrid communication patterns optimized for different interaction types:


Synchronous: Real-time AI reasoning and immediate responses (Hot Path)
Asynchronous: Workflow orchestration and long-running processes (Cold Path)
Event-Driven: State change notifications and system integration updates
5.3.2 Communication Pattern Choices
Hot Path Communication (Real-time AI):


Hot Path - Synchronous


<500ms


Maintenance Request


LangGraph AI Engine


Immediate Decision


Real-time Response


Cold Path Communication (Durable Workflows):


Cold Path - Asynchronous


<5s


Work Order Creation


Temporal Workflow


State Tracking


Completion Processing


5.3.3 Data Storage Solution Rationale
MongoDB for Primary Data Storage:


MongoDB was selected for its document-oriented storage model that naturally accommodates the flexible schemas required for maintenance data. Work orders, property profiles, and vendor information benefit from MongoDB's ability to store nested structures and evolve schemas without migrations.


Redis for Session State and Caching:


Redis provides high-performance session state management for multi-turn conversations and caching for frequently accessed data like property profiles and vendor lists. Its atomic operations support rate limiting and distributed locking patterns.


TimescaleDB for Time-Series Analytics:


Specialized time-series database optimized for performance metrics, operational KPIs, and historical trend analysis. Provides efficient storage and querying for maintenance analytics and reporting.


5.3.4 Caching Strategy Justification
Multi-Layer Caching Architecture:


L3 Cache - Database Query Cache


L2 Cache - Redis Distributed


L1 Cache - Application Memory


Property Profiles
TTL: 5 minutes


Vendor Lists
TTL: 5 minutes


Configuration Data
TTL: 5 minutes


Session State
TTL: 1 hour


Conversation Context
TTL: 1 hour


Troubleshooting KB
TTL: 1 hour


Historical Costs
TTL: 24 hours


Vendor Performance
TTL: 24 hours


Property History
TTL: 24 hours


Caching Rationale:


L1 (Application Memory): Frequently accessed, rarely changing data like property profiles and vendor lists
L2 (Redis Distributed): Session-specific data that must persist across service instances
L3 (Database Query Cache): Expensive analytical queries with acceptable staleness tolerance
5.4 Cross-cutting Concerns
5.4.1 Monitoring And Observability Approach
Comprehensive Observability Stack:


The system implements a three-pillar observability approach using industry-standard tools:


Metrics: Prometheus for operational metrics with Grafana dashboards
Logging: ELK Stack (Elasticsearch, Logstash, Kibana) for centralized log analysis
Tracing: Jaeger for distributed tracing across service boundaries
Key Metrics and Monitoring:


Metric Category        Specific Metrics        Target Values        Alert Thresholds
**Performance**        First response time, AI processing latency        <30s, <500ms        >60s, >1s
**Quality**        Troubleshooting resolution rate, first-time fix rate        20-35%, >85%        <15%, <80%
**Reliability**        Escalation rate, system availability        <15%, >99.9%        >20%, <99.5%
**Business**        Cost per work order, resident satisfaction        5% YoY decrease, >4.5/5        Increase, <4.0/5
5.4.2 Logging And Tracing Strategy
Structured Logging Implementation:


# Structured logging configuration
import structlog


logger = structlog.get_logger()


#### Example log entry
logger.info(
    "work_order_created",
    work_order_id="WO-12345",
    property_id="PROP-001",
    issue_category="plumbing",
    urgency="urgent",
    ai_confidence=0.92,
    processing_time_ms=245
)
Distributed Tracing:


OpenTelemetry integration provides end-to-end request tracing across all system components. Each maintenance request receives a unique trace ID that follows the request through intake, AI processing, vendor dispatch, and completion.


5.4.3 Error Handling Patterns
Comprehensive Error Handling Flow:


Recovery Verification


Recovery Strategies


Error Detection and Classification


Network/Timeout


Service Down


Data Issues


System Error Detected


Error Type?


Transient Error
Network/Timeout


Recoverable Error
Service Unavailable


Critical Error
Data Corruption


Exponential Backoff Retry
Max 3 attempts


Circuit Breaker Pattern
5 failures = open


Fallback Mechanism
Graceful degradation


Emergency Protocol
Human escalation


Health Check
Service validation


State Validation
Data consistency


Resume Normal Operation


Generate Incident Report


Error Recovery Patterns:


Transient Errors: Exponential backoff retry with jitter to prevent thundering herd
Circuit Breaker: Fail-fast pattern for degraded external services
Bulkhead: Isolation of critical vs non-critical operations
Timeout: Aggressive timeouts with fallback to human escalation
5.4.4 Authentication And Authorization Framework
Role-Based Access Control (RBAC):


Role        Permissions        Approval Limits        Data Access
**Resident**        Create own requests, view own work orders        N/A        Own unit only
**Property Manager**        Manage property work orders, override AI decisions        Up to $500        All managed properties
**Regional Manager**        Multi-property oversight, staff management        Up to $2000        Portfolio level
**AI Agent**        Automated operations within configured limits        Configurable threshold        Context-aware access
Security Implementation:


API Authentication: OAuth 2.0 for PMS integrations, API keys for external services
Data Encryption: AES-256 at rest, TLS 1.3 in transit
Access Code Protection: Additional encryption layer for sensitive property access codes
Audit Logging: Immutable logging of all decisions and actions with 7-year retention
5.4.5 Performance Requirements And Slas
Service Level Agreements:


Process Stage        Target Latency        SLA Requirement        Escalation Trigger        Recovery Action
**Request Acknowledgment**        <5 seconds        95% under 30s        >30s response time        Immediate ops alert
**AI Triage**        <30 seconds        90% under 2 min        >2 min processing        Escalate to human
**Troubleshooting**        <5 minutes        80% resolution in 10 min        >10 min session        Skip to vendor dispatch
**Vendor Dispatch**        <15 minutes        95% under 30 min        >30 min no vendor        Emergency vendor network
**Work Completion**        <24 hours        85% within SLA        >48h for urgent        Regional manager escalation
5.4.6 Disaster Recovery Procedures
Business Continuity Strategy:


Disaster Recovery


Primary Operations


Replication


Continuous


Backup


Recovery Procedures


Yes


Primary
Unavailable?


Automatic Failover
DNS switch


Data Synchronization
Verify consistency


Manual Failover
Ops intervention


Primary Region
us-east-1


Primary MongoDB
Atlas M30


Primary Redis
3-node cluster


DR Region
us-west-2


DR MongoDB
Cross-region replica


DR Redis
Backup cluster


Recovery Time Objectives (RTO) and Recovery Point Objectives (RPO):


RTO: 15 minutes for automatic failover, 1 hour for manual recovery
RPO: <5 minutes data loss for MongoDB, <1 minute for Redis session state
Backup Strategy: Continuous replication with point-in-time recovery capabilities
Testing: Monthly disaster recovery drills with automated validation
Graceful Degradation Modes:


AI Unavailable: Route all requests to human operators with full context transfer
PMS Unavailable: Continue operations with local data, sync when restored
Telephony Unavailable: Fall back to email/SMS only with resident notification
Vendor Portal Unavailable: Use direct communication channels (SMS/email)
This comprehensive system architecture provides a robust foundation for the AI Maintenance Coordinator, balancing performance, reliability, and scalability while ensuring seamless integration with existing property management ecosystems. LangGraph 1.0 addresses these gaps with a powerful graph-based execution model, and it provides production-ready features for reliable agentic systems: Durable state - Your agent's execution state persists automatically, so if your server restarts mid-conversation or a long-running workflow gets interrupted, it picks up exactly where it left off without losing context or forcing users to start over. Built-in persistence - Save and resume agent workflows at any point without writing custom database logic, enabling use cases like multi-day approval processes or background jobs that run across multiple sessions.


Engineering Specification: Ai Maintenance Coordinator
Skill ID: SKILL-254
Gap ID: GAP-AF-002
Version: 1.0
Created: January 6, 2026
Author: Engineering Agent
Status: Draft


Document Control
Version        Date        Author        Changes
1.0        2026-01-06        Engineering Agent        Initial specification
6. System Components Design
6.1 Component Architecture Overview
6.1.1 System Component Hierarchy
The AI Maintenance Coordinator implements a sophisticated four-layer architecture optimized for both real-time AI reasoning and durable workflow orchestration. LangGraph 1.0 is the first stable major release in the durable agent framework space —a major milestone for production-ready AI systems. After more than a year of powering agents at companies like Uber, LinkedIn, and Klarna, LangGraph is officially v1.


Primary System Components:


Component Layer        Primary Responsibility        Technology Stack        Scaling Strategy
**Intake Layer**        Multi-channel request reception and normalization        FastAPI + Twilio + SendGrid        Horizontal with load balancing
**Brain Layer**        AI-powered triage, classification, and troubleshooting        LangGraph - Trusted by companies shaping the future of agents – including Klarna, Replit, Elastic, and more        Horizontal with session affinity
**Action Layer**        Vendor dispatch, scheduling, and notification delivery        FastAPI microservices        Horizontal stateless scaling
**Orchestration Layer**        Durable workflow management and state persistence        The Temporal Service persists the state of your application and has built-in retries, task queues, signals, and timers        Horizontal worker scaling
6.1.2 Component Interaction Patterns
Hot Path vs Cold Path Architecture:


LangGraph 1.0 addresses these gaps with a powerful graph-based execution model, and it provides production-ready features for reliable agentic systems: Durable state - Your agent's execution state persists automatically, so if your server restarts mid-conversation or a long-running workflow gets interrupted, it picks up exactly where it left off without losing context or forcing users to start over.


Data Persistence Layer


Cold Path - Durable Workflows


Hot Path - Real-time AI Reasoning


<500ms


<5s


Maintenance Request


LangGraph AI Engine


Immediate Decision


Real-time Response


Work Order Creation


Temporal Workflow


State Tracking


Completion Processing


MongoDB 8.0.17
Primary Data Store


Redis 8.4
Session & Cache


ChromaDB
Knowledge Base


6.1.3 Component Communication Protocols
Inter-Component Communication Matrix:


Source Component        Target Component        Communication Type        Protocol        Latency Requirement
Intake Layer        Brain Layer        Synchronous        HTTP/WebSocket        <100ms
Brain Layer        Action Layer        Asynchronous        Message Queue        <1s
Action Layer        Orchestration Layer        Event-driven        Temporal Signals        <2s
Orchestration Layer        External Systems        Asynchronous        REST API/Webhooks        <5s
6.2 Intake Layer Components
6.2.1 Voice Agent Component
Purpose and Responsibilities:


The Voice Agent Component handles real-time voice interactions with residents, providing natural language conversation capabilities for maintenance request intake and troubleshooting guidance. It implements speech-to-text processing, natural language understanding, and text-to-speech synthesis for seamless voice interactions.


Technical Implementation:


class VoiceAgentComponent:
    def __init__(self):
        self.speech_processor = DeepgramSTTProcessor()
        self.tts_engine = ElevenLabsTTSEngine()
        self.conversation_manager = ConversationManager()
        
    async def handle_incoming_call(self, call_sid: str) -> VoiceSession:
        """Handle incoming voice call with real-time processing."""
        session = VoiceSession(
            call_sid=call_sid,
            start_time=datetime.utcnow(),
            state=VoiceSessionState.GREETING
        )
        
        # Play greeting with property-specific branding
        greeting = await self.generate_greeting(session.property_id)
        await self.tts_engine.speak(greeting, session.call_sid)
        
        # Start speech recognition stream
        await self.speech_processor.start_stream(
            call_sid=session.call_sid,
            callback=self.process_speech_input
        )
        
        return session
Integration Points:


Twilio WebSocket: Real-time voice streaming with sub-200ms latency
Deepgram/Whisper: Speech-to-text processing with 95%+ accuracy
ElevenLabs/Azure Neural: Text-to-speech synthesis with natural voice
Redis Session Store: Conversation state persistence
Performance Requirements:


Metric        Target        Measurement
Call Answer Time        <2 rings        System response time
Speech Recognition Latency        <200ms        Processing time
Voice Response Latency        <500ms        End-to-end response
Concurrent Call Capacity        100+ simultaneous        Load testing
6.2.2 Sms Handler Component
Purpose and Responsibilities:


The SMS Handler Component processes text message communications with residents and vendors, maintaining conversation context and supporting multimedia attachments. It implements conversation threading, auto-response generation, and integration with the unified request processing pipeline.


Technical Implementation:


class SMSHandlerComponent:
    def __init__(self):
        self.twilio_client = TwilioClient()
        self.conversation_cache = RedisConversationCache()
        self.message_parser = MessageParser()
        
    async def process_incoming_sms(self, webhook_data: TwilioSMSWebhook) -> SMSResponse:
        """Process incoming SMS with conversation context."""
        # Load conversation context
        conversation = await self.conversation_cache.get_conversation(
            phone_number=webhook_data.from_number,
            ttl_hours=24
        )
        
        # Parse message intent and extract entities
        parsed_message = await self.message_parser.parse(
            text=webhook_data.body,
            context=conversation.context,
            attachments=webhook_data.media_urls
        )
        
        # Generate contextual response
        response = await self.generate_response(
            parsed_message=parsed_message,
            conversation_history=conversation.messages
        )
        
        # Send response via Twilio
        await self.twilio_client.send_message(
            to=webhook_data.from_number,
            body=response.text,
            media_urls=response.attachments
        )
        
        return SMSResponse(
            message_id=response.message_id,
            status="sent",
            conversation_id=conversation.id
        )
Message Processing Pipeline:


Context Management


SMS Processing Flow


Incoming SMS


Validate Phone Number


Load Conversation Context


Parse Message Content


Extract Intent & Entities


Generate AI Response


Send SMS Response


Update Conversation Context


Redis Conversation Cache


Message History


Session State


6.2.3 Email Parser Component
Purpose and Responsibilities:


The Email Parser Component processes email-based maintenance requests, extracting issue details from email content, handling attachments, and maintaining email thread continuity. It implements intelligent parsing algorithms to extract structured data from unstructured email content.


Technical Implementation:


class EmailParserComponent:
    def __init__(self):
        self.sendgrid_client = SendGridClient()
        self.attachment_processor = AttachmentProcessor()
        self.content_extractor = EmailContentExtractor()
        
    async def process_incoming_email(self, email_data: EmailWebhook) -> ParsedEmailRequest:
        """Parse incoming email into structured maintenance request."""
        # Extract email metadata
        metadata = EmailMetadata(
            message_id=email_data.message_id,
            from_address=email_data.from_email,
            subject=email_data.subject,
            received_at=email_data.timestamp,
            thread_id=self.extract_thread_id(email_data.headers)
        )
        
        # Parse email content
        content = await self.content_extractor.extract(
            html_body=email_data.html,
            text_body=email_data.text,
            subject=email_data.subject
        )
        
        # Process attachments
        attachments = []
        for attachment in email_data.attachments:
            if self.is_supported_attachment(attachment):
                processed = await self.attachment_processor.process(attachment)
                attachments.append(processed)
        
        # Extract maintenance request details
        request_details = await self.extract_maintenance_details(
            content=content,
            attachments=attachments
        )
        
        return ParsedEmailRequest(
            metadata=metadata,
            content=content,
            attachments=attachments,
            maintenance_request=request_details
        )
Email Content Extraction Rules:


Content Type        Extraction Method        Priority
**Subject Line**        Keyword pattern matching        High
**Email Body**        NLP entity extraction        Medium
**Photo Attachments**        Image analysis (optional)        Low
**Previous Thread**        Thread context loading        Medium
6.2.4 Portal Api Component
Purpose and Responsibilities:


The Portal API Component provides structured REST API endpoints for property management system integrations and resident portal submissions. It implements request validation, authentication, and standardized response formatting.


Technical Implementation:


from fastapi import FastAPI, HTTPException, Depends
from pydantic import BaseModel, Field
from typing import List, Optional


class MaintenanceRequestAPI(BaseModel):
    property_id: str = Field(..., description="Property identifier")
    unit_id: str = Field(..., description="Unit identifier")
    resident_id: str = Field(..., description="Resident identifier")
    issue_category: Optional[str] = Field(None, description="Issue category")
    description: str = Field(..., min_length=10, description="Issue description")
    urgency: UrgencyLevel = Field(UrgencyLevel.ROUTINE, description="Urgency level")
    photos: List[str] = Field(default=[], max_items=5, description="Photo URLs")
    preferred_times: List[datetime] = Field(default=[], description="Preferred appointment times")


class PortalAPIComponent:
    def __init__(self):
        self.app = FastAPI(title="AI Maintenance Coordinator API")
        self.request_processor = RequestProcessor()
        
    @self.app.post("/api/v1/maintenance/requests")
    async def create_maintenance_request(
        self,
        request: MaintenanceRequestAPI,
        auth: AuthContext = Depends(authenticate_request)
    ) -> MaintenanceRequestResponse:
        """Create new maintenance request via API."""
        # Validate request data
        validated_request = await self.validate_request(request, auth)
        
        # Convert to unified format
        unified_request = MaintenanceRequest(
            request_id=generate_request_id(),
            source_channel="portal",
            property_id=validated_request.property_id,
            unit_id=validated_request.unit_id,
            resident_id=validated_request.resident_id,
            issue_description=validated_request.description,
            urgency=validated_request.urgency,
            attachments=validated_request.photos,
            created_at=datetime.utcnow(),
            session_id=generate_session_id()
        )
        
        # Submit to processing pipeline
        result = await self.request_processor.process(unified_request)
        
        return MaintenanceRequestResponse(
            work_order_id=result.work_order_id,
            status="received",
            estimated_response_time="30 minutes",
            next_steps="Your request is being processed by our AI coordinator"
        )
6.2.5 Channel Unification Component
Purpose and Responsibilities:


The Channel Unification Component normalizes requests from all input channels into a standardized MaintenanceRequest data structure, ensuring consistent processing regardless of the source channel.


Unified Data Structure:


from enum import Enum
from typing import List, Optional
from datetime import datetime
from pydantic import BaseModel


class SourceChannel(str, Enum):
    PHONE = "phone"
    SMS = "sms"
    EMAIL = "email"
    PORTAL = "portal"


class UrgencyLevel(str, Enum):
    ROUTINE = "routine"
    URGENT = "urgent"
    EMERGENCY = "emergency"


class Attachment(BaseModel):
    attachment_id: str
    filename: str
    content_type: str
    size_bytes: int
    url: str
    uploaded_at: datetime


class ContactInfo(BaseModel):
    phone: Optional[str] = None
    email: Optional[str] = None
    preferred_method: str = "sms"


class MaintenanceRequest(BaseModel):
    """Unified maintenance request structure for all channels."""
    request_id: str
    source_channel: SourceChannel
    property_id: str
    unit_id: str
    resident_id: str
    resident_contact: ContactInfo
    issue_description: str
    issue_category: Optional[str] = None  # Determined by AI
    urgency: UrgencyLevel
    attachments: List[Attachment] = []
    raw_transcript: Optional[str] = None  # For voice calls
    created_at: datetime
    session_id: str
    
    class Config:
        json_encoders = {
            datetime: lambda v: v.isoformat()
        }
Channel Normalization Logic:


Unified Output


Normalization Process


Channel Inputs


Voice Call
Speech + Context


SMS Message
Text + MMS


Email
Body + Attachments


Portal API
Structured JSON


Channel Detection


Content Extraction


Entity Extraction


Structure Builder


Request Validation


MaintenanceRequest
Standardized Structure


6.3 Brain Layer Components
6.3.1 Ai Triage Engine
Purpose and Responsibilities:


The AI Triage Engine performs intelligent classification and urgency determination for maintenance requests using advanced natural language processing and contextual analysis. LangGraph is a lower level framework and runtime, useful for highly custom and controllable agents, designed to support production-grade, long running agents


Classification Taxonomy:


class IssueCategory(str, Enum):
    PLUMBING = "plumbing"
    ELECTRICAL = "electrical"
    HVAC = "hvac"
    APPLIANCE = "appliance"
    STRUCTURAL = "structural"
    PEST = "pest"


class IssueTaxonomy:
    """Comprehensive issue classification system."""
    
    CATEGORIES = {
        IssueCategory.PLUMBING: {
            "subcategories": ["leak", "clog", "no_water", "water_heater", "toilet", "faucet", "garbage_disposal"],
            "default_vendor_type": "plumber",
            "emergency_keywords": ["flood", "burst_pipe", "sewage", "gas_smell"],
            "typical_resolution_time": "2-4 hours"
        },
        IssueCategory.ELECTRICAL: {
            "subcategories": ["no_power", "outlet", "lighting", "breaker", "smoke_detector"],
            "default_vendor_type": "electrician",
            "emergency_keywords": ["sparking", "burning_smell", "no_power_whole_unit"],
            "typical_resolution_time": "1-3 hours"
        },
        IssueCategory.HVAC: {
            "subcategories": ["ac_not_cooling", "heat_not_working", "thermostat", "strange_noise", "filter"],
            "default_vendor_type": "hvac_tech",
            "emergency_keywords": ["no_heat_winter", "gas_smell"],
            "typical_resolution_time": "2-6 hours"
        },
        IssueCategory.APPLIANCE: {
            "subcategories": ["refrigerator", "stove", "dishwasher", "washer", "dryer", "microwave"],
            "default_vendor_type": "appliance_tech",
            "emergency_keywords": ["gas_smell", "fire"],
            "typical_resolution_time": "1-4 hours"
        },
        IssueCategory.STRUCTURAL: {
            "subcategories": ["door", "window", "lock", "ceiling", "floor", "wall", "roof_leak"],
            "default_vendor_type": "handyman",
            "emergency_keywords": ["roof_collapse", "flood_from_above"],
            "typical_resolution_time": "2-8 hours"
        },
        IssueCategory.PEST: {
            "subcategories": ["rodent", "insect", "bed_bugs", "birds"],
            "default_vendor_type": "pest_control",
            "emergency_keywords": ["snake", "aggressive_animal"],
            "typical_resolution_time": "1-2 hours"
        }
    }
Urgency Determination Algorithm:


class UrgencyDeterminationEngine:
    """Advanced urgency classification with contextual analysis."""
    
    EMERGENCY_KEYWORDS = [
        "flood", "fire", "gas", "no heat", "sewage", "sparking",
        "burst pipe", "electrical fire", "carbon monoxide"
    ]
    
    async def determine_urgency(
        self, 
        request: MaintenanceRequest,
        property_context: PropertyContext
    ) -> UrgencyClassification:
        """Determine urgency level with contextual analysis."""
        
        # Emergency keyword detection (highest priority)
        if self.contains_emergency_keywords(request.issue_description):
            return UrgencyClassification(
                level=UrgencyLevel.EMERGENCY,
                confidence=0.95,
                reasoning="Emergency keywords detected",
                escalation_required=True
            )
        
        # Time-sensitive contextual analysis
        urgency_factors = []
        
        # Weather-based urgency
        if self.is_winter_season(property_context.location):
            if "no heat" in request.issue_description.lower():
                urgency_factors.append(("winter_no_heat", 0.9))
        
        if self.is_extreme_heat_warning(property_context.location):
            if "ac" in request.issue_description.lower() and "not cooling" in request.issue_description.lower():
                urgency_factors.append(("extreme_heat_no_ac", 0.8))
        
        # After-hours urgency boost
        if self.is_after_hours():
            if request.issue_category in ["plumbing", "hvac"]:
                urgency_factors.append(("after_hours_critical", 0.7))
        
        # Historical pattern analysis
        if property_context.has_recurring_issue(request.issue_category):
            urgency_factors.append(("recurring_issue", 0.6))
        
        # Calculate composite urgency score
        max_factor = max([factor[1] for factor in urgency_factors], default=0.3)
        
        if max_factor >= 0.8:
            return UrgencyClassification(
                level=UrgencyLevel.URGENT,
                confidence=max_factor,
                reasoning=f"High urgency factors: {urgency_factors}",
                escalation_required=False
            )
        elif max_factor >= 0.5:
            return UrgencyClassification(
                level=UrgencyLevel.URGENT,
                confidence=max_factor,
                reasoning=f"Moderate urgency factors: {urgency_factors}",
                escalation_required=False
            )
        else:
            return UrgencyClassification(
                level=UrgencyLevel.ROUTINE,
                confidence=0.8,
                reasoning="No urgent factors detected",
                escalation_required=False
            )
6.3.2 Troubleshooting Engine
Purpose and Responsibilities:


The Troubleshooting Engine guides residents through diagnostic steps to potentially resolve issues without vendor dispatch, implementing interactive decision trees and outcome tracking for continuous improvement.


Knowledge Base Structure:


class TroubleshootingEntry(BaseModel):
    """Individual troubleshooting knowledge base entry."""
    entry_id: str
    issue_category: IssueCategory
    issue_subcategory: str
    keywords: List[str]
    steps: List[TroubleshootingStep]
    resolution_rate: float  # Historical success rate
    avg_time_to_resolve: int  # Minutes
    last_updated: datetime
    
class TroubleshootingStep(BaseModel):
    """Individual step in troubleshooting sequence."""
    step_number: int
    question: Optional[str] = None
    instruction: Optional[str] = None
    expected_responses: List[ExpectedResponse]
    timeout_seconds: int = 300  # 5 minutes default
    
class ExpectedResponse(BaseModel):
    """Expected response pattern and next action."""
    response_pattern: str
    next_step: Optional[int] = None
    result: Optional[TroubleshootingResult] = None
    clarification: Optional[str] = None


class TroubleshootingResult(str, Enum):
    RESOLVED = "resolved"
    DISPATCH_NEEDED = "dispatch_needed"
    ESCALATE = "escalate"
Garbage Disposal Troubleshooting Example:


GARBAGE_DISPOSAL_TROUBLESHOOTING = TroubleshootingEntry(
    entry_id="plumbing_garbage_disposal_001",
    issue_category=IssueCategory.PLUMBING,
    issue_subcategory="garbage_disposal",
    keywords=["garbage disposal", "disposal not working", "disposal jammed"],
    resolution_rate=0.65,
    avg_time_to_resolve=4,
    steps=[
        TroubleshootingStep(
            step_number=1,
            question="Is the disposal making any sound when you flip the switch?",
            expected_responses=[
                ExpectedResponse(
                    response_pattern="yes|sound|humming|noise",
                    next_step=2
                ),
                ExpectedResponse(
                    response_pattern="no|silent|nothing|quiet",
                    next_step=3
                )
            ]
        ),
        TroubleshootingStep(
            step_number=2,
            question="Is it humming but not spinning?",
            expected_responses=[
                ExpectedResponse(
                    response_pattern="yes|humming|stuck",
                    instruction="Turn OFF disposal. Look underneath for a hex key slot. Insert 1/4\" Allen wrench and rotate back and forth. Then press reset button. Try again.",
                    next_step=4
                ),
                ExpectedResponse(
                    response_pattern="no|grinding|spinning",
                    instruction="The disposal is working but may be clogged. Turn off disposal and check for objects in the drain.",
                    result=TroubleshootingResult.DISPATCH_NEEDED
                )
            ]
        ),
        TroubleshootingStep(
            step_number=3,
            question="Can you find a reset button on the bottom of the disposal?",
            expected_responses=[
                ExpectedResponse(
                    response_pattern="yes|found|see",
                    instruction="Press the reset button firmly. Try the switch again.",
                    next_step=4
                ),
                ExpectedResponse(
                    response_pattern="no|can't find|don't see",
                    result=TroubleshootingResult.DISPATCH_NEEDED,
                    clarification="This may be an electrical issue requiring a technician."
                )
            ]
        ),
        TroubleshootingStep(
            step_number=4,
            question="Did that fix the problem? Is the disposal working now?",
            expected_responses=[
                ExpectedResponse(
                    response_pattern="yes|working|fixed|good",
                    result=TroubleshootingResult.RESOLVED
                ),
                ExpectedResponse(
                    response_pattern="no|still broken|not working",
                    result=TroubleshootingResult.DISPATCH_NEEDED
                )
            ]
        )
    ]
)
Interactive Troubleshooting Session Management:


class TroubleshootingSession:
    """Manages interactive troubleshooting sessions."""
    
    def __init__(self, work_order_id: str, entry: TroubleshootingEntry):
        self.session_id = generate_session_id()
        self.work_order_id = work_order_id
        self.entry = entry
        self.current_step = 1
        self.responses: List[StepResponse] = []
        self.start_time = datetime.utcnow()
        self.outcome: Optional[TroubleshootingOutcome] = None
        
    async def execute_step(self, step: TroubleshootingStep) -> StepResult:
        """Execute a troubleshooting step and process response."""
        # Present question or instruction to resident
        if step.question:
            await self.send_to_resident(step.question)
        elif step.instruction:
            await self.send_to_resident(step.instruction)
        
        # Wait for response with timeout
        try:
            response = await self.await_response(timeout=step.timeout_seconds)
        except TimeoutError:
            return StepResult(
                outcome=TroubleshootingOutcome.TIMEOUT,
                next_action="escalate_to_vendor"
            )
        
        # Match response to expected patterns
        matched = self.match_response(response, step.expected_responses)
        
        # Record response
        self.responses.append(StepResponse(
            step_number=step.step_number,
            resident_response=response,
            matched_pattern=matched.response_pattern if matched else None,
            timestamp=datetime.utcnow()
        ))
        
        # Determine next action
        if matched and matched.result:
            self.outcome = TroubleshootingOutcome(matched.result)
            return StepResult(outcome=self.outcome)
        elif matched and matched.next_step:
            self.current_step = matched.next_step
            return StepResult(next_step=matched.next_step)
        else:
            # Unclear response - ask for clarification
            if matched and matched.clarification:
                await self.send_to_resident(matched.clarification)
                return await self.execute_step(step)  # Retry same step
            else:
                return StepResult(outcome=TroubleshootingOutcome.DISPATCH_NEEDED)
6.3.3 Property Context Loader
Purpose and Responsibilities:


The Property Context Loader retrieves and assembles relevant property, unit, and historical data to inform AI decision-making, implementing progressive disclosure patterns to optimize performance.


Context Loading Strategy:


class PropertyContextLoader:
    """Loads property context with progressive disclosure."""
    
    def __init__(self):
        self.property_service = PropertyService()
        self.unit_service = UnitService()
        self.history_service = MaintenanceHistoryService()
        self.cache = RedisCache()
        
    async def load_maintenance_context(
        self, 
        work_order: WorkOrder
    ) -> MaintenanceContext:
        """Load comprehensive context for maintenance request."""
        
        # Tier 1: Always load (cached for 5 minutes)
        property_profile = await self.cache.get_or_set(
            key=f"property:{work_order.property_id}",
            loader=lambda: self.property_service.get_property(work_order.property_id),
            ttl=300
        )
        
        unit_profile = await self.cache.get_or_set(
            key=f"unit:{work_order.unit_id}",
            loader=lambda: self.unit_service.get_unit(work_order.unit_id),
            ttl=300
        )
        
        resident_profile = await self.unit_service.get_current_resident(work_order.unit_id)
        
        context = MaintenanceContext(
            property=property_profile,
            unit=unit_profile,
            resident=resident_profile,
            request_timestamp=work_order.created_at
        )
        
        # Tier 2: Conditional loading based on issue type
        await self._load_conditional_context(context, work_order)
        
        return context
        
    async def _load_conditional_context(
        self, 
        context: MaintenanceContext, 
        work_order: WorkOrder
    ) -> None:
        """Load additional context based on issue characteristics."""
        
        # Load recent similar issues
        if work_order.issue_category:
            recent_similar = await self.history_service.find_similar_issues(
                unit_id=work_order.unit_id,
                category=work_order.issue_category,
                days_back=90
            )
            
            if recent_similar:
                context.related_history = recent_similar
                context.is_potential_recurring = len(recent_similar) >= 2
        
        # Load appliance details for appliance/HVAC issues
        if work_order.issue_category in [IssueCategory.APPLIANCE, IssueCategory.HVAC]:
            appliance_details = await self._find_relevant_appliance(
                unit_appliances=context.unit.appliances,
                issue_description=work_order.issue_description
            )
            
            if appliance_details:
                context.appliance_details = appliance_details
                context.warranty_status = await self._check_warranty(appliance_details)
        
        # Load owner preferences for approval workflows
        if await self._might_need_approval(work_order):
            context.owner_preferences = context.property.owner.preferences
            context.approval_threshold = context.property.owner.preferences.approval_threshold
Property Profile Schema:


class PropertyProfile(BaseModel):
    """Comprehensive property information for AI context."""
    property_id: str
    address: PropertyAddress
    type: PropertyType
    units: List[str]  # Unit IDs
    
    # Access and security information
    access: PropertyAccess
    systems: PropertySystems
    
    # Vendor preferences
    vendors: VendorPreferences
    
    # Owner configuration
    owner: OwnerProfile
    
    # Historical maintenance data
    maintenance_history: MaintenanceHistory


class PropertyAccess(BaseModel):
    office_hours: TimeRange
    after_hours_contact: ContactInfo
    gate_code: Optional[str] = None
    key_storage: KeyStorageType
    lockbox_code: Optional[str] = None
    special_instructions: Optional[str] = None


class PropertySystems(BaseModel):
    hvac_type: str
    water_heater_type: str
    electrical_panel_location: str
    shutoff_locations: ShutoffLocations


class ShutoffLocations(BaseModel):
    water_main: str
    gas_main: str
    electrical_main: str


class VendorPreferences(BaseModel):
    preferred: Dict[str, List[str]]  # Category -> Vendor IDs
    blacklisted: List[str]
    
class OwnerProfile(BaseModel):
    owner_id: str
    preferences: OwnerPreferences


class OwnerPreferences(BaseModel):
    notification_frequency: NotificationFrequency
    approval_threshold: float
    require_photos: bool
    require_estimates_over: float
6.4 Action Layer Components
6.4.1 Vendor Selection Engine
Purpose and Responsibilities:


The Vendor Selection Engine implements sophisticated scoring algorithms to select optimal vendors based on performance metrics, cost competitiveness, geographic proximity, and property-specific preferences.


Vendor Scoring Algorithm:


class VendorSelectionEngine:
    """Advanced vendor selection with multi-criteria scoring."""
    
    def __init__(self):
        self.vendor_service = VendorService()
        self.performance_analyzer = VendorPerformanceAnalyzer()
        self.cost_analyzer = CostAnalyzer()
        
    async def select_vendors(
        self,
        request: MaintenanceRequest,
        property: PropertyProfile,
        max_vendors: int = 3
    ) -> RankedVendorList:
        """Select and rank vendors using multi-criteria scoring."""
        
        # Step 1: Filter eligible vendors
        eligible_vendors = await self._filter_eligible_vendors(request, property)
        
        if not eligible_vendors:
            raise NoEligibleVendorsError(
                f"No eligible vendors found for {request.issue_category} at {property.address}"
            )
        
        # Step 2: Score each vendor
        scored_vendors = []
        for vendor in eligible_vendors:
            score = await self._calculate_vendor_score(vendor, request, property)
            scored_vendors.append(ScoredVendor(vendor=vendor, score=score))
        
        # Step 3: Sort by score and return top candidates
        scored_vendors.sort(key=lambda x: x.score, reverse=True)
        
        return RankedVendorList(
            vendors=scored_vendors[:max_vendors],
            selection_criteria=self._get_selection_criteria(),
            timestamp=datetime.utcnow()
        )
    
    async def _calculate_vendor_score(
        self,
        vendor: Vendor,
        request: MaintenanceRequest,
        property: PropertyProfile
    ) -> VendorScore:
        """Calculate comprehensive vendor score."""
        
        score_components = {}
        
        # Performance weight: 40%
        performance_score = (
            vendor.performance.resident_satisfaction_avg * 10 +  # 0-50 points
            (1 - vendor.performance.avg_response_time_minutes / 120) * 20 +  # 0-20 points
            vendor.performance.first_time_fix_rate * 20  # 0-20 points
        )
        score_components["performance"] = min(performance_score, 40)
        
        # Cost weight: 25%
        avg_cost = (vendor.financials.typical_job_cost_range.min + 
                   vendor.financials.typical_job_cost_range.max) / 2
        market_avg = await self.cost_analyzer.get_market_average(
            request.issue_category, 
            property.address.zip_code
        )
        cost_ratio = avg_cost / market_avg if market_avg > 0 else 1.0
        cost_score = max(0, (2 - cost_ratio)) * 12.5  # Cheaper = better
        score_components["cost"] = min(cost_score, 25)
        
        # Familiarity weight: 20%
        jobs_at_property = await self.performance_analyzer.count_jobs_at_property(
            vendor.vendor_id, 
            property.property_id
        )
        familiarity_score = min(jobs_at_property / 5, 1) * 20
        score_components["familiarity"] = familiarity_score
        
        # Availability weight: 15%
        if request.urgency == UrgencyLevel.EMERGENCY:
            availability_score = 15 if vendor.availability.emergency_available else 0
        else:
            response_likelihood = await self._estimate_response_likelihood(vendor)
            availability_score = response_likelihood * 15
        score_components["availability"] = availability_score
        
        # Owner preference boost (bonus points)
        if vendor.vendor_id in property.vendors.preferred.get(request.issue_category, []):
            score_components["owner_preference"] = 10
        else:
            score_components["owner_preference"] = 0
        
        total_score = sum(score_components.values())
        
        return VendorScore(
            total=total_score,
            components=score_components,
            vendor_id=vendor.vendor_id,
            calculated_at=datetime.utcnow()
        )
6.4.2 Vendor Dispatch Component
Purpose and Responsibilities:


The Vendor Dispatch Component handles automated vendor communication, job assignment, and confirmation tracking across multiple communication channels with intelligent retry logic.


Dispatch Protocol Implementation:


class VendorDispatchComponent:
    """Automated vendor dispatch with multi-channel communication."""
    
    def __init__(self):
        self.sms_client = TwilioSMSClient()
        self.email_client = SendGridClient()
        self.vendor_portal = VendorPortalAPI()
        self.template_engine = TemplateEngine()
        
    async def dispatch_to_vendor(
        self,
        vendor: Vendor,
        work_order: WorkOrder,
        property: PropertyProfile
    ) -> DispatchResult:
        """Dispatch work order to vendor with confirmation tracking."""
        
        dispatch_attempt = DispatchAttempt(
            vendor_id=vendor.vendor_id,
            work_order_id=work_order.id,
            started_at=datetime.utcnow(),
            timeout_minutes=self._get_timeout_for_urgency(work_order.urgency)
        )
        
        # Try preferred communication method first
        primary_method = vendor.preferences.preferred_contact_method
        result = await self._contact_vendor(vendor, work_order, property, primary_method)
        
        if result.status == ContactStatus.CONFIRMED:
            return DispatchResult(
                status=DispatchStatus.CONFIRMED,
                vendor_id=vendor.vendor_id,
                eta=result.eta,
                confirmation_method=primary_method,
                attempt=dispatch_attempt
            )
        
        # Try backup methods if primary fails
        backup_methods = [m for m in ["sms", "phone", "email"] if m != primary_method]
        
        for method in backup_methods:
            result = await self._contact_vendor(vendor, work_order, property, method)
            
            if result.status == ContactStatus.CONFIRMED:
                return DispatchResult(
                    status=DispatchStatus.CONFIRMED,
                    vendor_id=vendor.vendor_id,
                    eta=result.eta,
                    confirmation_method=method,
                    attempt=dispatch_attempt
                )
        
        # All methods failed
        return DispatchResult(
            status=DispatchStatus.NO_RESPONSE,
            vendor_id=vendor.vendor_id,
            attempt=dispatch_attempt,
            next_action="try_next_vendor"
        )
    
    async def _contact_vendor(
        self,
        vendor: Vendor,
        work_order: WorkOrder,
        property: PropertyProfile,
        method: str
    ) -> ContactResult:
        """Contact vendor via specified method."""
        
        if method == "sms":
            return await self._send_sms_dispatch(vendor, work_order, property)
        elif method == "email":
            return await self._send_email_dispatch(vendor, work_order, property)
        elif method == "phone":
            return await self._make_phone_dispatch(vendor, work_order, property)
        elif method == "portal":
            return await self._send_portal_dispatch(vendor, work_order, property)
        else:
            raise ValueError(f"Unsupported contact method: {method}")
SMS Dispatch Template:


SMS_DISPATCH_TEMPLATE = """
[Maintenance Request]
Property: {property_address}
Unit: {unit_number}
Issue: {issue_category} - {issue_description}
Urgency: {urgency}
Contact: {resident_name} {resident_phone}


Access: {access_instructions}


Reply YES to accept. Expected arrival: {requested_time}
Reply NO if unavailable.


Job ID: {work_order_id}
"""


class SMSDispatchHandler:
    async def send_dispatch(
        self,
        vendor: Vendor,
        work_order: WorkOrder,
        property: PropertyProfile
    ) -> ContactResult:
        """Send SMS dispatch to vendor."""
        
        # Render template with work order data
        message = self.template_engine.render(
            template=SMS_DISPATCH_TEMPLATE,
            context={
                "property_address": property.address.full_address,
                "unit_number": work_order.unit_id,
                "issue_category": work_order.issue_category,
                "issue_description": work_order.issue_description[:100],
                "urgency": work_order.urgency.value.upper(),
                "resident_name": work_order.resident_contact.name,
                "resident_phone": work_order.resident_contact.phone,
                "access_instructions": property.access.get_instructions(),
                "requested_time": self._suggest_appointment_time(work_order.urgency),
                "work_order_id": work_order.id
            }
        )
        
        # Send SMS
        sms_result = await self.sms_client.send_message(
            to=vendor.phone,
            body=message,
            callback_url=f"/webhooks/vendor-response/{work_order.id}"
        )
        
        # Wait for response with timeout
        timeout_minutes = self._get_timeout_for_urgency(work_order.urgency)
        
        try:
            response = await self._wait_for_vendor_response(
                work_order.id,
                timeout_minutes=timeout_minutes
            )
            
            return self._parse_vendor_response(response)
            
        except TimeoutError:
            return ContactResult(
                status=ContactStatus.TIMEOUT,
                method="sms",
                message_id=sms_result.message_id
            )
6.4.3 Scheduling Coordinator
Purpose and Responsibilities:


The Scheduling Coordinator optimizes appointment scheduling by considering vendor availability, resident preferences, property access constraints, and travel time optimization for efficient routing.


Appointment Optimization Algorithm:


class SchedulingCoordinator:
    """Advanced appointment scheduling with multi-constraint optimization."""
    
    def __init__(self):
        self.calendar_service = CalendarService()
        self.routing_optimizer = RoutingOptimizer()
        self.availability_checker = AvailabilityChecker()
        
    async def schedule_appointment(
        self,
        work_order: WorkOrder,
        vendor: Vendor,
        resident_preferences: Optional[List[TimeSlot]] = None
    ) -> SchedulingResult:
        """Find optimal appointment time with multi-constraint optimization."""
        
        # Get vendor's available slots for next 7 days
        vendor_availability = await self.availability_checker.get_vendor_slots(
            vendor_id=vendor.vendor_id,
            days_ahead=7,
            include_emergency=work_order.urgency == UrgencyLevel.EMERGENCY
        )
        
        # Filter by property access hours
        property_hours = work_order.property.access.office_hours
        accessible_slots = self._filter_by_access_hours(
            vendor_availability, 
            property_hours
        )
        
        # Optimize for vendor routing (minimize travel time)
        optimized_slots = await self.routing_optimizer.optimize_slots(
            vendor=vendor,
            available_slots=accessible_slots,
            property_location=work_order.property.address.coordinates
        )
        
        # Match against resident preferences if provided
        if resident_preferences:
            matched_slots = self._match_resident_preferences(
                optimized_slots, 
                resident_preferences
            )
            
            if matched_slots:
                selected_slot = matched_slots[0]
            else:
                # Negotiate alternative times
                selected_slot = await self._negotiate_alternative_time(
                    optimized_slots[:3], 
                    work_order.resident_contact
                )
        else:
            # Select optimal slot based on urgency
            selected_slot = self._select_optimal_slot(optimized_slots, work_order.urgency)
        
        # Create appointment record
        appointment = Appointment(
            appointment_id=generate_appointment_id(),
            work_order_id=work_order.id,
            vendor_id=vendor.vendor_id,
            property_id=work_order.property_id,
            unit_id=work_order.unit_id,
            scheduled_window=selected_slot,
            access_instructions=self._generate_access_instructions(work_order.property),
            status=AppointmentStatus.CONFIRMED,
            created_at=datetime.utcnow()
        )
        
        # Schedule automated reminders
        await self._schedule_reminders(appointment)
        
        return SchedulingResult(
            appointment=appointment,
            optimization_score=selected_slot.optimization_score,
            alternatives_considered=len(optimized_slots)
        )
Reminder Scheduling System:


class ReminderScheduler:
    """Automated reminder system for appointments."""
    
    REMINDER_SCHEDULE = {
        "vendor_24h": timedelta(hours=24),
        "resident_24h": timedelta(hours=24),
        "vendor_1h": timedelta(hours=1),
        "vendor_30min": timedelta(minutes=30)
    }
    
    async def schedule_reminders(self, appointment: Appointment) -> List[ScheduledReminder]:
        """Schedule all reminders for an appointment."""
        
        reminders = []
        
        for reminder_type, time_before in self.REMINDER_SCHEDULE.items():
            reminder_time = appointment.scheduled_window.start_time - time_before
            
            # Don't schedule reminders in the past
            if reminder_time > datetime.utcnow():
                reminder = ScheduledReminder(
                    reminder_id=generate_reminder_id(),
                    appointment_id=appointment.appointment_id,
                    reminder_type=reminder_type,
                    scheduled_time=reminder_time,
                    recipient=self._get_reminder_recipient(reminder_type, appointment),
                    template=self._get_reminder_template(reminder_type),
                    status=ReminderStatus.SCHEDULED
                )
                
                # Schedule with Temporal
                await self.temporal_client.start_workflow(
                    ReminderWorkflow.run,
                    reminder,
                    id=f"reminder-{reminder.reminder_id}",
                    task_queue="reminders",
                    start_delay=time_before
                )
                
                reminders.append(reminder)
        
        return reminders
6.4.4 Notification Engine
Purpose and Responsibilities:


The Notification Engine delivers multi-channel notifications to all stakeholders throughout the maintenance process, respecting communication preferences and quiet hours while ensuring critical messages are delivered immediately.


Multi-Channel Notification System:


class NotificationEngine:
    """Comprehensive notification delivery across multiple channels."""
    
    def __init__(self):
        self.sms_provider = TwilioSMSProvider()
        self.email_provider = SendGridProvider()
        self.push_provider = PushNotificationProvider()
        self.slack_provider = SlackProvider()
        self.template_service = NotificationTemplateService()
        
    async def send_notification(
        self,
        notification_type: NotificationType,
        recipient: Recipient,
        context: NotificationContext,
        priority: Priority = Priority.NORMAL
    ) -> NotificationResult:
        """Send notification across configured channels."""
        
        # Load notification template
        template = await self.template_service.get_template(
            notification_type=notification_type,
            recipient_type=recipient.type
        )
        
        # Get recipient's preferred channels
        channels = await self._get_channels_for_recipient(recipient, notification_type)
        
        delivery_results = []
        
        for channel in channels:
            # Respect quiet hours for non-emergency notifications
            if priority != Priority.EMERGENCY:
                if await self._is_quiet_hours(recipient, channel):
                    delivery_results.append(DeliveryResult(
                        channel=channel,
                        status=DeliveryStatus.DEFERRED,
                        reason="quiet_hours"
                    ))
                    continue
            
            # Render template for specific channel
            content = await self.template_service.render_template(
                template=template,
                context=context,
                channel=channel
            )
            
            # Send via appropriate provider
            try:
                result = await self._send_via_channel(channel, recipient, content)
                delivery_results.append(result)
                
                # Break on first successful delivery for non-critical notifications
                if result.status == DeliveryStatus.DELIVERED and priority == Priority.NORMAL:
                    break
                    
            except Exception as e:
                delivery_results.append(DeliveryResult(
                    channel=channel,
                    status=DeliveryStatus.FAILED,
                    error=str(e)
                ))
        
        return NotificationResult(
            notification_id=generate_notification_id(),
            notification_type=notification_type,
            recipient=recipient,
            delivery_results=delivery_results,
            sent_at=datetime.utcnow()
        )
Notification Templates:


NOTIFICATION_TEMPLATES = {
    NotificationType.REQUEST_RECEIVED: {
        RecipientType.RESIDENT: {
            "sms": "Your maintenance request has been received. Reference: {work_order_id}. We're working on it and will update you shortly.",
            "email": """
            <h2>Maintenance Request Received</h2>
            <p>Your maintenance request has been received and assigned reference number <strong>{work_order_id}</strong>.</p>
            <p><strong>Issue:</strong> {issue_summary}</p>
            <p>We're working on it and will update you shortly with next steps.</p>
            """,
            "push": "Maintenance request received - {issue_summary}"
        }
    },
    NotificationType.VENDOR_SCHEDULED: {
        RecipientType.RESIDENT: {
            "sms": "Good news! A technician has been scheduled. Date: {date}, Time: {time_window}, Technician: {vendor_name}. They will contact you before arrival.",
            "email": """
            <h2>Technician Scheduled</h2>
            <p>Good news! We've scheduled a technician for your maintenance request.</p>
            <ul>
                <li><strong>Date:</strong> {date}</li>
                <li><strong>Time Window:</strong> {time_window}</li>
                <li><strong>Technician:</strong> {vendor_name}</li>
                <li><strong>Contact:</strong> {vendor_phone}</li>
            </ul>
            <p>They will contact you before arrival to confirm access.</p>
            """
        }
    },
    NotificationType.ESCALATION_ALERT: {
        RecipientType.STAFF: {
            "slack": """
            ⚠️ **ESCALATION REQUIRED**
            
            **Work Order:** {work_order_id}
            **Property:** {property_address}
            **Resident:** {resident_name} ({resident_phone})
            **Issue:** {issue_summary}
            **Reason:** {escalation_reason}
            
            [View Details]({dashboard_url})
            """,
            "email": """
            <h2 style="color: #ff6b35;">Escalation Required</h2>
            <p>A maintenance request requires your immediate attention.</p>
            <table>
                <tr><td><strong>Work Order:</strong></td><td>{work_order_id}</td></tr>
                <tr><td><strong>Property:</strong></td><td>{property_address}</td></tr>
                <tr><td><strong>Resident:</strong></td><td>{resident_name} ({resident_phone})</td></tr>
                <tr><td><strong>Issue:</strong></td><td>{issue_summary}</td></tr>
                <tr><td><strong>Escalation Reason:</strong></td><td>{escalation_reason}</td></tr>
            </table>
            <p><a href="{dashboard_url}">View Full Details</a></p>
            """
        }
    }
}
6.5 Orchestration Layer Components
6.5.1 Temporal Workflow Engine
Purpose and Responsibilities:


The Temporal Workflow Engine provides durable execution guarantees for long-running maintenance workflows, ensuring no work orders are lost during system failures. Temporal Workflows automatically capture state at every step, and in the event of failure, can pick up exactly where they left off. No lost progress, no orphaned processes, and no manual recovery required.


Main Maintenance Workflow:


from temporalio import workflow, activity
from datetime import timedelta


@workflow.defn
class MaintenanceWorkflow:
    """Durable maintenance workflow with automatic state persistence."""
    
    def __init__(self):
        self.state = WorkOrderState()
        self.context = MaintenanceContext()
        
    @workflow.run
    async def run(self, request: MaintenanceRequest) -> WorkOrderResult:
        """Execute complete maintenance workflow with durable state."""
        
        # Initialize work order state
        self.state.status = WorkOrderStatus.NEW
        self.state.request = request
        self.state.created_at = workflow.now()
        
        # Auto-transition to triage after 30 seconds
        await workflow.sleep(30)
        self.state.status = WorkOrderStatus.TRIAGING
        
        # Load property context
        self.context = await workflow.execute_activity(
            load_property_context,
            request,
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        # AI triage and classification
        triage_result = await workflow.execute_activity(
            ai_triage_activity,
            request,
            self.context,
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        # Handle emergency escalation
        if triage_result.urgency == UrgencyLevel.EMERGENCY:
            self.state.status = WorkOrderStatus.ESCALATED
            await workflow.execute_activity(
                emergency_escalation_activity,
                request,
                triage_result,
                start_to_close_timeout=timedelta(minutes=1)
            )
            return WorkOrderResult(
                status=WorkOrderStatus.ESCALATED,
                escalation_reason="Emergency detected"
            )
        
        # Attempt troubleshooting for non-emergency issues
        self.state.status = WorkOrderStatus.TROUBLESHOOTING
        troubleshooting_result = await workflow.execute_activity(
            troubleshooting_activity,
            request,
            triage_result,
            start_to_close_timeout=timedelta(minutes=10)
        )
        
        # Check if issue was resolved via troubleshooting
        if troubleshooting_result.outcome == TroubleshootingOutcome.RESOLVED:
            self.state.status = WorkOrderStatus.RESOLVED
            await workflow.execute_activity(
                close_work_order_activity,
                request.request_id,
                "Resolved via troubleshooting",
                start_to_close_timeout=timedelta(minutes=1)
            )
            return WorkOrderResult(
                status=WorkOrderStatus.RESOLVED,
                resolution_method="troubleshooting"
            )
        
        # Proceed to vendor dispatch
        self.state.status = WorkOrderStatus.AWAITING_DISPATCH
        
        # Check if approval is needed
        cost_estimate = await workflow.execute_activity(
            estimate_cost_activity,
            triage_result,
            self.context,
            start_to_close_timeout=timedelta(minutes=1)
        )
        
        if cost_estimate.amount > self.context.property.owner.approval_threshold:
            self.state.status = WorkOrderStatus.AWAITING_APPROVAL
            
            approval_result = await workflow.execute_activity(
                request_approval_activity,
                request,
                cost_estimate,
                start_to_close_timeout=timedelta(hours=24)
            )
            
            if not approval_result.approved:
                self.state.status = WorkOrderStatus.CANCELLED
                return WorkOrderResult(
                    status=WorkOrderStatus.CANCELLED,
                    cancellation_reason="Approval denied"
                )
        
        # Dispatch to vendor
        self.state.status = WorkOrderStatus.DISPATCHING
        dispatch_result = await workflow.execute_activity(
            vendor_dispatch_activity,
            request,
            triage_result,
            self.context,
            start_to_close_timeout=timedelta(minutes=30)
        )
        
        if not dispatch_result.vendor_confirmed:
            self.state.status = WorkOrderStatus.ESCALATED
            return WorkOrderResult(
                status=WorkOrderStatus.ESCALATED,
                escalation_reason="No vendor available"
            )
        
        # Schedule appointment
        self.state.status = WorkOrderStatus.SCHEDULED
        appointment = await workflow.execute_activity(
            schedule_appointment_activity,
            dispatch_result.vendor,
            request,
            start_to_close_timeout=timedelta(minutes=15)
        )
        
        # Wait for work completion with timeout
        completion_result = await workflow.wait_condition(
            lambda: self.state.status == WorkOrderStatus.COMPLETED,
            timeout=timedelta(days=7)
        )
        
        if not completion_result:
            # Timeout - escalate
            self.state.status = WorkOrderStatus.ESCALATED
            return WorkOrderResult(
                status=WorkOrderStatus.ESCALATED,
                escalation_reason="Work completion timeout"
            )
        
        # Process completion and billing
        await workflow.execute_activity(
            process_completion_activity,
            request.request_id,
            start_to_close_timeout=timedelta(minutes=5)
        )
        
        return WorkOrderResult(
            status=WorkOrderStatus.COMPLETED,
            completion_time=workflow.now(),
            total_duration=workflow.now() - self.state.created_at
        )
6.5.2 State Management Component
Purpose and Responsibilities:


The State Management Component maintains work order state consistency across all system components, implementing the complete state machine with automated transitions, timeout handling, and audit trail maintenance.


Work Order State Machine:


class WorkOrderStateMachine:
    """Complete state machine for work order lifecycle."""
    
    STATES = {
        WorkOrderStatus.NEW: {
            "description": "Request received, not yet processed",
            "allowed_transitions": [WorkOrderStatus.TRIAGING, WorkOrderStatus.CANCELLED],
            "auto_transition": {
                "target": WorkOrderStatus.TRIAGING,
                "delay_seconds": 30
            },
            "timeout": None
        },
        WorkOrderStatus.TRIAGING: {
            "description": "AI analyzing issue, checking history",
            "allowed_transitions": [
                WorkOrderStatus.TROUBLESHOOTING, 
                WorkOrderStatus.AWAITING_DISPATCH, 
                WorkOrderStatus.ESCALATED
            ],
            "timeout": {
                "duration_minutes": 2,
                "target": WorkOrderStatus.ESCALATED
            }
        },
        WorkOrderStatus.TROUBLESHOOTING: {
            "description": "AI guiding resident through troubleshooting",
            "allowed_transitions": [
                WorkOrderStatus.RESOLVED, 
                WorkOrderStatus.AWAITING_DISPATCH, 
                WorkOrderStatus.ESCALATED
            ],
            "timeout": {
                "duration_minutes": 10,
                "target": WorkOrderStatus.AWAITING_DISPATCH
            }
        },
        WorkOrderStatus.AWAITING_DISPATCH: {
            "description": "Ready to assign vendor",
            "allowed_transitions": [
                WorkOrderStatus.DISPATCHING, 
                WorkOrderStatus.AWAITING_APPROVAL, 
                WorkOrderStatus.ESCALATED
            ],
            "timeout": None
        },
        WorkOrderStatus.AWAITING_APPROVAL: {
            "description": "Cost exceeds threshold, waiting for approval",
            "allowed_transitions": [
                WorkOrderStatus.DISPATCHING, 
                WorkOrderStatus.CANCELLED, 
                WorkOrderStatus.ESCALATED
            ],
            "timeout": {
                "duration_hours": 24,
                "target": WorkOrderStatus.ESCALATED
            }
        },
        WorkOrderStatus.DISPATCHING: {
            "description": "Contacting vendors for assignment",
            "allowed_transitions": [
                WorkOrderStatus.SCHEDULED, 
                WorkOrderStatus.ESCALATED
            ],
            "timeout": {
                "duration_minutes": 30,
                "target": WorkOrderStatus.ESCALATED
            }
        },
        WorkOrderStatus.SCHEDULED: {
            "description": "Vendor confirmed, appointment set",
            "allowed_transitions": [
                WorkOrderStatus.VENDOR_EN_ROUTE, 
                WorkOrderStatus.R
6.1 Core Services Architecture
6.1.1 Service Architecture Overview
The AI Maintenance Coordinator implements a sophisticated microservices architecture optimized for both real-time AI reasoning and durable workflow orchestration. LangGraph 1.0 is the first stable major release in the durable agent framework space —a major milestone for production-ready AI systems. After more than a year of powering agents at companies like Uber, LinkedIn, and Klarna, LangGraph is officially v1.


The system follows a hybrid microservices approach with clear service boundaries but shared data stores for consistency. This architectural decision balances the operational complexity of full microservices with the scalability and maintainability benefits while ensuring exactly-once execution guarantees for critical maintenance workflows.


6.1.2 Service Boundaries And Responsibilities
Service Name        Primary Responsibility        Technology Stack        Scaling Strategy        Communication Pattern
**Intake Service**        Multi-channel request reception and normalization        FastAPI (Very high performance, on par with NodeJS and Go thanks to Starlette and Pydantic). One of the fastest Python frameworks available.        Horizontal stateless scaling        Synchronous HTTP/WebSocket
**Brain Service**        AI-powered triage, classification, and troubleshooting        LangGraph - Trusted by companies shaping the future of agents – including Klarna, Replit, Elastic, and more – LangGraph is a low-level orchestration framework for building, managing, and deploying long-running, stateful agents.        Horizontal with session affinity        Asynchronous message queues
**Action Service**        Vendor dispatch, scheduling, and notification delivery        FastAPI microservices with Redis caching        Horizontal stateless scaling        Event-driven messaging
**Workflow Service**        Durable workflow orchestration and state management        The Temporal Service persists the state of your application and has built-in retries, task queues, signals, and timers, to make sure your code always picks up where it left off.        Horizontal worker scaling        Temporal workflow signals
6.1.3 Inter-service Communication Patterns
Hot Path Communication (Real-time AI Reasoning):


The Hot Path handles immediate AI decisions with sub-500ms latency requirements. Durable state: Agent execution state persists automatically. If your server restarts mid-conversation or a long-running workflow gets interrupted, it picks up exactly where it left off without losing context.


Hot Path Services


HTTP/WebSocket


Read/Write


<500ms


Intake Service
FastAPI


Brain Service
LangGraph


Redis Cache
Session State


Cold Path Communication (Durable Workflows):


The Cold Path manages long-running processes with exactly-once execution guarantees. Temporal Workflows automatically capture state at every step, and in the event of failure, can pick up exactly where they left off. No lost progress, no orphaned processes, and no manual recovery required.


Cold Path Services


Temporal Signals


Event Streams


State Persistence


Workflow Service
Temporal


Action Service
FastAPI


MongoDB
Persistent State


6.1.4 Service Discovery Mechanisms
Service Registry Configuration:


Service        Discovery Method        Health Check Endpoint        Load Balancer Type
**Intake Service**        Kubernetes Service Discovery        `/health`        Round-robin with session affinity for WebSocket
**Brain Service**        Consul Service Mesh        `/health/ready`        Consistent hashing for session affinity
**Action Service**        Kubernetes DNS        `/health/live`        Weighted round-robin
**Workflow Service**        Temporal Service Discovery        Temporal health checks        Queue-based worker distribution
Service Registration Pattern:


class ServiceRegistry:
    """Service discovery and registration for microservices."""
    
    def __init__(self):
        self.consul_client = ConsulClient()
        self.k8s_client = KubernetesClient()
        
    async def register_service(
        self,
        service_name: str,
        service_id: str,
        address: str,
        port: int,
        health_check_url: str
    ) -> ServiceRegistration:
        """Register service with discovery mechanism."""
        
        registration = ServiceRegistration(
            service_name=service_name,
            service_id=service_id,
            address=address,
            port=port,
            health_check=HealthCheck(
                http=f"http://{address}:{port}{health_check_url}",
                interval="10s",
                timeout="3s",
                deregister_critical_service_after="30s"
            ),
            tags=[
                f"version:{get_service_version()}",
                f"environment:{get_environment()}",
                "ai-maintenance-coordinator"
            ]
        )
        
        await self.consul_client.agent.service.register(registration)
        return registration
6.1.5 Load Balancing Strategy
6.1.6 Service-specific Load Balancing
Intake Service Load Balancing:


Intake Service Instances


Load Balancer Layer


Round Robin


Round Robin


Round Robin


Session Affinity


Session Affinity


Session Affinity


Application Load Balancer
AWS ALB


Network Load Balancer
WebSocket Sticky Sessions


Intake Service 1
HTTP + WebSocket


Intake Service 2
HTTP + WebSocket


Intake Service 3
HTTP + WebSocket


Brain Service Load Balancing:


The Brain Service requires session affinity for multi-turn conversations while maintaining horizontal scalability for new sessions.


class BrainServiceLoadBalancer:
    """Custom load balancer for Brain Service with session affinity."""
    
    def __init__(self):
        self.consistent_hash = ConsistentHashRing()
        self.service_instances = []
        
    async def route_request(
        self, 
        request: MaintenanceRequest
    ) -> BrainServiceInstance:
        """Route request to appropriate Brain Service instance."""
        
        # Use session_id for consistent routing
        if request.session_id:
            target_instance = self.consistent_hash.get_node(request.session_id)
            
            # Check if target instance is healthy
            if await self.is_instance_healthy(target_instance):
                return target_instance
            else:
                # Failover to next available instance
                return await self.get_healthy_instance()
        
        # New session - route to least loaded instance
        return await self.get_least_loaded_instance()
    
    async def get_least_loaded_instance(self) -> BrainServiceInstance:
        """Select instance with lowest current load."""
        instance_loads = []
        
        for instance in self.service_instances:
            if await self.is_instance_healthy(instance):
                load = await self.get_instance_load(instance)
                instance_loads.append((instance, load))
        
        # Sort by load and return least loaded
        instance_loads.sort(key=lambda x: x[1])
        return instance_loads[0][0] if instance_loads else None
6.1.7 Circuit Breaker Patterns
6.1.8 Service-level Circuit Breakers
Circuit Breaker Implementation:


from enum import Enum
from datetime import datetime, timedelta
from typing import Optional, Callable, Any


class CircuitState(Enum):
    CLOSED = "closed"      # Normal operation
    OPEN = "open"          # Failing, reject requests
    HALF_OPEN = "half_open" # Testing recovery


class CircuitBreakerConfig:
    """Configuration for circuit breaker behavior."""
    failure_threshold: int = 5
    recovery_timeout: timedelta = timedelta(seconds=60)
    success_threshold: int = 3  # For half-open state
    timeout: timedelta = timedelta(seconds=30)


class ServiceCircuitBreaker:
    """Circuit breaker implementation for service resilience."""
    
    def __init__(self, service_name: str, config: CircuitBreakerConfig):
        self.service_name = service_name
        self.config = config
        self.state = CircuitState.CLOSED
        self.failure_count = 0
        self.success_count = 0
        self.last_failure_time: Optional[datetime] = None
        
    async def call(self, func: Callable, *args, **kwargs) -> Any:
        """Execute function with circuit breaker protection."""
        
        if self.state == CircuitState.OPEN:
            if self._should_attempt_reset():
                self.state = CircuitState.HALF_OPEN
                self.success_count = 0
            else:
                raise CircuitBreakerOpenError(
                    f"Circuit breaker OPEN for {self.service_name}"
                )
        
        try:
            # Execute the function with timeout
            result = await asyncio.wait_for(
                func(*args, **kwargs),
                timeout=self.config.timeout.total_seconds()
            )
            
            # Success - handle state transitions
            await self._on_success()
            return result
            
        except Exception as e:
            # Failure - handle state transitions
            await self._on_failure(e)
            raise
    
    def _should_attempt_reset(self) -> bool:
        """Check if enough time has passed to attempt reset."""
        if not self.last_failure_time:
            return True
            
        return (
            datetime.utcnow() - self.last_failure_time 
            >= self.config.recovery_timeout
        )
    
    async def _on_success(self):
        """Handle successful execution."""
        if self.state == CircuitState.HALF_OPEN:
            self.success_count += 1
            if self.success_count >= self.config.success_threshold:
                self.state = CircuitState.CLOSED
                self.failure_count = 0
        elif self.state == CircuitState.CLOSED:
            self.failure_count = 0
    
    async def _on_failure(self, exception: Exception):
        """Handle failed execution."""
        self.failure_count += 1
        self.last_failure_time = datetime.utcnow()
        
        if self.failure_count >= self.config.failure_threshold:
            self.state = CircuitState.OPEN
            
        # Log failure for monitoring
        logger.warning(
            "Circuit breaker failure",
            service=self.service_name,
            failure_count=self.failure_count,
            state=self.state.value,
            exception=str(exception)
        )
Service-Specific Circuit Breaker Configuration:


Service Integration        Failure Threshold        Recovery Timeout        Fallback Strategy
**PMS Integration**        5 failures        60 seconds        Queue requests locally, sync when available
**Telephony (Twilio)**        3 failures        30 seconds        Route to backup number, email notifications
**Vendor Portal**        5 failures        120 seconds        Direct SMS/email communication
**Payment System**        2 failures        300 seconds        Manual invoice processing queue
6.1.9 Retry And Fallback Mechanisms
6.1.10 Exponential Backoff Retry Strategy
import asyncio
import random
from typing import TypeVar, Callable, Any


T = TypeVar('T')


class RetryConfig:
    """Configuration for retry behavior."""
    max_attempts: int = 3
    base_delay: float = 1.0
    max_delay: float = 60.0
    exponential_base: float = 2.0
    jitter: bool = True


async def retry_with_exponential_backoff(
    func: Callable[..., T],
    config: RetryConfig,
    *args,
    **kwargs
) -> T:
    """Execute function with exponential backoff retry."""
    
    last_exception = None
    
    for attempt in range(config.max_attempts):
        try:
            return await func(*args, **kwargs)
            
        except Exception as e:
            last_exception = e
            
            # Don't retry on final attempt
            if attempt == config.max_attempts - 1:
                break
            
            # Calculate delay with exponential backoff
            delay = min(
                config.base_delay * (config.exponential_base ** attempt),
                config.max_delay
            )
            
            # Add jitter to prevent thundering herd
            if config.jitter:
                delay *= (0.5 + random.random() * 0.5)
            
            logger.info(
                "Retrying after failure",
                attempt=attempt + 1,
                delay=delay,
                exception=str(e)
            )
            
            await asyncio.sleep(delay)
    
    # All attempts failed
    raise RetryExhaustedError(
        f"Failed after {config.max_attempts} attempts"
    ) from last_exception
Service-Specific Retry Configurations:


RETRY_CONFIGURATIONS = {
    "pms_integration": RetryConfig(
        max_attempts=3,
        base_delay=2.0,
        max_delay=30.0,
        exponential_base=2.0,
        jitter=True
    ),
    "vendor_communication": RetryConfig(
        max_attempts=2,
        base_delay=1.0,
        max_delay=10.0,
        exponential_base=1.5,
        jitter=True
    ),
    "notification_delivery": RetryConfig(
        max_attempts=5,
        base_delay=0.5,
        max_delay=15.0,
        exponential_base=1.8,
        jitter=True
    ),
    "ai_inference": RetryConfig(
        max_attempts=2,
        base_delay=0.5,
        max_delay=5.0,
        exponential_base=2.0,
        jitter=False  # Consistent timing for AI calls
    )
}
6.1.11 Fallback Mechanism Implementation
Error Handling


Fallback Chain


Primary Service Path


Yes


No


Open


Closed


Yes


No


No


No


Primary Service


Success?


Return Result


Circuit Breaker
Open?


Fallback Service


Success?


Graceful Degradation


Emergency Mode


Log Failure


Alert Operations


Update Metrics


6.1.12 Scalability Design
6.1.13 Horizontal Scaling Approach
Auto-Scaling Configuration:


7. User Interface Design
7.1 Ui Technology Stack
7.1.1 Core Frontend Technologies
The AI Maintenance Coordinator implements a modern, responsive user interface architecture designed to provide seamless access to maintenance operations across multiple stakeholder groups. Horizon UI Next.js Admin Dashboard is a cutting-edge open-source admin template designed using Chakra UI, Next.js 15, and React. It uses modern UI elements and provides an aesthetic look, making it perfect for building beautiful websites and web applications. Packed with numerous elements, design blocks, and fully coded pages. Horizon UI Dashboard enables the creation of a stunning admin dashboard without any hassle.


Primary UI Technology Stack:


Technology        Version        Purpose        Justification
**Next.js**        15.0+        React framework with SSR/SSG        Monster NextJs Admin is a premium admin dashboard template built on Next.js 15, React hooks, and Redux Toolkit. It is designed to empower developers to create exceptional web applications and products effortlessly.
**React**        19.0+        Component-based UI library        Designed specifically for React.js to deliver maximum compatibility and performance. Fully optimized for all devices and browsers, ensuring a consistent experience for every user.
**TypeScript**        5.0+        Type-safe JavaScript development        This dashboard is built with Typescript and React Bootstrap, using the App Router.
**Tailwind CSS**        4.0+        Utility-first CSS framework        TailAdmin is a free and open-source Next.js and Tailwind CSS admin dashboard, featuring a complete redesign and numerous new features. With 500+ dashboard UI elements, enhanced responsiveness, and 7 Dashboard Variation options.
**Material-UI (MUI)**        6.0+        React component library        A free Material UI admin dashboard template built with React. Offers everything you need to create dashboards that include high-end features. Dashboard, user profile, tables, forms, maps, notifications, charts.
7.1.2 Ui Component Architecture
Component Library Structure:


// Core UI component architecture
interface UIComponentLibrary {
  // Layout Components
  layout: {
    DashboardLayout: React.ComponentType;
    SidebarNavigation: React.ComponentType;
    TopNavigation: React.ComponentType;
    ContentArea: React.ComponentType;
  };
  
  // Data Display Components
  dataDisplay: {
    WorkOrderCard: React.ComponentType<WorkOrderCardProps>;
    PropertyCard: React.ComponentType<PropertyCardProps>;
    VendorCard: React.ComponentType<VendorCardProps>;
    MetricsCard: React.ComponentType<MetricsCardProps>;
    StatusIndicator: React.ComponentType<StatusIndicatorProps>;
  };
  
  // Interactive Components
  interactive: {
    WorkOrderTable: React.ComponentType<WorkOrderTableProps>;
    FilterPanel: React.ComponentType<FilterPanelProps>;
    SearchBar: React.ComponentType<SearchBarProps>;
    ActionButtons: React.ComponentType<ActionButtonsProps>;
  };
  
  // Communication Components
  communication: {
    ChatInterface: React.ComponentType<ChatInterfaceProps>;
    NotificationCenter: React.ComponentType<NotificationCenterProps>;
    MessageThread: React.ComponentType<MessageThreadProps>;
  };
}
7.1.3 Responsive Design Framework
Multi-Device Support Strategy:


Fully optimized for all devices and browsers, ensuring a consistent experience for every user. Easily adapt colors, typography, and layouts to match your brand's identity—no design degree required.


Device Category        Breakpoint        Layout Strategy        Key Adaptations
**Mobile**        <768px        Single column, stacked cards        Simplified navigation, touch-optimized controls
**Tablet**        768px-1024px        Two-column grid        Collapsible sidebar, medium-density information
**Desktop**        >1024px        Multi-column dashboard        Full feature set, high information density
**Large Screens**        >1440px        Extended grid layouts        Additional data panels, enhanced visualizations
7.2 User Interface Use Cases
7.2.1 Property Manager Dashboard
Primary Use Case: Operational Command Center


The Property Manager Dashboard serves as the central command center for maintenance operations, providing real-time visibility into all work orders, vendor activities, and system performance. We designed the desktop dashboard to give managers an immediate, comprehensive overview of their properties. We created a unified dashboard to streamline workflows and centralize property management tasks.


Core Dashboard Components:


interface PropertyManagerDashboard {
  // Real-time work order overview
  workOrderOverview: {
    activeWorkOrders: WorkOrderSummary[];
    urgentItems: WorkOrder[];
    completedToday: number;
    escalationQueue: EscalatedWorkOrder[];
  };
  
  // AI activity monitoring
  aiActivityFeed: {
    recentActions: AIAction[];
    confidenceScores: ConfidenceMetric[];
    interventionOpportunities: InterventionAlert[];
  };
  
  // Vendor performance tracking
  vendorPerformance: {
    activeVendors: VendorStatus[];
    responseMetrics: VendorMetric[];
    performanceAlerts: VendorAlert[];
  };
  
  // Financial oversight
  financialOverview: {
    dailySpend: number;
    monthlyBudget: BudgetStatus;
    pendingApprovals: ApprovalRequest[];
    costTrends: CostTrend[];
  };
}
Dashboard Layout Design:


Property Manager Dashboard Layout


Main Content Area


Right Column - Context


Center Column - Overview


Left Column - Primary Actions


Vendor Status Panel
Available, Busy, Offline


Top Navigation Bar
Property Selector, User Menu, Notifications


Quick Actions Panel
Create Work Order, Emergency Alert


Key Metrics Cards
Response Time, Completion Rate, Cost


Pending Approvals
Cost Overruns, Owner Decisions


Recent Alerts
Escalations, System Issues


Active Work Orders Table
Status, Property, Vendor, ETA


Performance Trend Charts
Volume, Cost, Satisfaction


Work Order Queue
Urgent, Today, This Week


AI Activity Feed
Real-time AI Actions


Bottom Action Panel
Bulk Actions, Export, Settings


7.2.2 Resident Communication Interface
Use Case: Simplified Maintenance Request Experience


The Resident Interface provides an intuitive, conversational experience for submitting and tracking maintenance requests. Analysis showed that the streamlined workflows and automated processes led to significantly faster maintenance responses and improved tenant communication, directly boosting satisfaction rates. Shows a strong improvement, indicating that users are highly pleased with the new platform experience.


Resident Portal Components:


interface ResidentPortal {
  // Request submission
  requestSubmission: {
    issueDescriptionForm: IssueForm;
    photoUpload: PhotoUploadComponent;
    urgencySelector: UrgencySelector;
    submitButton: SubmitButton;
  };
  
  // Request tracking
  requestTracking: {
    activeRequests: ResidentWorkOrder[];
    statusTimeline: StatusTimeline;
    vendorInformation: VendorContact;
    estimatedCompletion: ETADisplay;
  };
  
  // Communication
  communication: {
    chatInterface: ChatInterface;
    notificationPreferences: NotificationSettings;
    feedbackForm: FeedbackForm;
  };
}
Mobile-First Design Pattern:


Resident Mobile Interface


Messages Screen


Request Screen


Home Screen


Main Navigation


Conversation List
Work Order Threads


Mobile Header
Property Name, Menu Toggle


Bottom Navigation Tabs
Home, Requests, Messages, Profile


Quick Submit Button
Report Issue


New Request Form
Issue Type, Description, Photos


Chat Interface
AI/Human Communication


Request History
Past Work Orders


Active Requests
Status Cards


Recent Updates
Notification Feed


7.2.3 Vendor Work Order Interface
Use Case: Streamlined Job Management


The Vendor Interface provides efficient job assignment, status updates, and completion reporting capabilities optimized for mobile field work.


Vendor Mobile App Components:


interface VendorMobileApp {
  // Job management
  jobManagement: {
    availableJobs: JobListing[];
    acceptedJobs: AcceptedJob[];
    jobDetails: JobDetailView;
    routeOptimization: RouteMap;
  };
  
  // Status updates
  statusUpdates: {
    checkInButton: CheckInButton;
    progressUpdates: ProgressForm;
    completionForm: CompletionForm;
    photoCapture: PhotoCapture;
  };
  
  // Communication
  communication: {
    residentContact: ContactInfo;
    propertyManagerChat: ChatInterface;
    emergencyContact: EmergencyButton;
  };
}
7.2.4 Owner Oversight Dashboard
Use Case: Financial and Performance Oversight


The Owner Dashboard provides high-level visibility into maintenance operations, costs, and property performance with emphasis on financial transparency and approval workflows.


Owner Dashboard Layout:


interface OwnerDashboard {
  // Financial overview
  financialOverview: {
    monthlySpend: SpendSummary;
    costTrends: CostTrendChart;
    budgetStatus: BudgetIndicator;
    pendingApprovals: ApprovalQueue;
  };
  
  // Property performance
  propertyPerformance: {
    maintenanceMetrics: PropertyMetrics[];
    residentSatisfaction: SatisfactionScore;
    vendorPerformance: VendorScorecard;
    issueFrequency: IssueAnalytics;
  };
  
  // Approval workflow
  approvalWorkflow: {
    pendingRequests: ApprovalRequest[];
    approvalHistory: ApprovalHistory;
    thresholdSettings: ThresholdConfig;
  };
}
7.3 Ui/backend Interaction Boundaries
7.3.1 Api Integration Patterns
Frontend-Backend Communication Architecture:


The UI layer communicates with the AI Maintenance Coordinator backend through a well-defined API boundary that separates presentation logic from business logic while maintaining real-time responsiveness.


// API client architecture for UI components
class MaintenanceAPIClient {
  private baseURL: string;
  private authToken: string;
  private websocketConnection: WebSocket;
  
  // Work order operations
  async getWorkOrders(filters: WorkOrderFilters): Promise<WorkOrder[]> {
    return this.get('/api/v1/work-orders', { params: filters });
  }
  
  async createWorkOrder(request: MaintenanceRequestCreate): Promise<WorkOrderResponse> {
    return this.post('/api/v1/maintenance/requests', request);
  }
  
  async updateWorkOrderStatus(
    workOrderId: string, 
    status: WorkOrderStatus
  ): Promise<void> {
    return this.patch(`/api/v1/work-orders/${workOrderId}`, { status });
  }
  
  // Real-time updates via WebSocket
  subscribeToWorkOrderUpdates(
    workOrderId: string,
    callback: (update: WorkOrderUpdate) => void
  ): void {
    this.websocketConnection.send(JSON.stringify({
      type: 'subscribe',
      channel: `work_order_${workOrderId}`,
      callback
    }));
  }
  
  // AI interaction endpoints
  async getAIRecommendations(workOrderId: string): Promise<AIRecommendation[]> {
    return this.get(`/api/v1/ai/recommendations/${workOrderId}`);
  }
  
  async overrideAIDecision(
    workOrderId: string,
    decision: AIDecisionOverride
  ): Promise<void> {
    return this.post(`/api/v1/ai/override/${workOrderId}`, decision);
  }
}
7.3.2 Real-time Data Synchronization
WebSocket Integration for Live Updates:


// Real-time data synchronization
interface RealTimeDataManager {
  // Work order status updates
  workOrderUpdates: {
    channel: 'work_order_updates';
    events: [
      'status_changed',
      'vendor_assigned',
      'vendor_en_route',
      'work_completed',
      'escalation_triggered'
    ];
    updateFrequency: 'immediate';
  };
  
  // AI activity feed
  aiActivityFeed: {
    channel: 'ai_activity';
    events: [
      'triage_completed',
      'troubleshooting_started',
      'vendor_dispatched',
      'decision_made'
    ];
    updateFrequency: 'real_time';
  };
  
  // Vendor status updates
  vendorStatus: {
    channel: 'vendor_status';
    events: [
      'vendor_available',
      'vendor_busy',
      'vendor_offline',
      'job_accepted',
      'job_declined'
    ];
    updateFrequency: '30_seconds';
  };
}


// WebSocket event handling
class RealTimeEventHandler {
  handleWorkOrderUpdate(event: WorkOrderUpdateEvent): void {
    // Update work order in local state
    this.updateWorkOrderState(event.workOrderId, event.newStatus);
    
    // Show notification to user
    this.showNotification({
      type: 'info',
      message: `Work order ${event.workOrderId} status changed to ${event.newStatus}`,
      duration: 5000
    });
    
    // Update relevant UI components
    this.refreshWorkOrderTable();
    this.updateMetricsCards();
  }
  
  handleAIActivity(event: AIActivityEvent): void {
    // Add to AI activity feed
    this.addToActivityFeed({
      timestamp: event.timestamp,
      action: event.action,
      workOrderId: event.workOrderId,
      confidence: event.confidence,
      details: event.details
    });
    
    // Update AI performance metrics
    this.updateAIMetrics(event);
  }
}
7.3.3 State Management Architecture
Redux Toolkit for Complex State Management:


// Redux store structure for maintenance operations
interface MaintenanceState {
  // Work orders
  workOrders: {
    items: Record<string, WorkOrder>;
    filters: WorkOrderFilters;
    loading: boolean;
    error: string | null;
  };
  
  // Properties and units
  properties: {
    items: Record<string, PropertyProfile>;
    selectedProperty: string | null;
    loading: boolean;
  };
  
  // Vendors
  vendors: {
    items: Record<string, Vendor>;
    availability: Record<string, VendorAvailability>;
    performance: Record<string, VendorPerformance>;
  };
  
  // UI state
  ui: {
    sidebarCollapsed: boolean;
    activeView: DashboardView;
    selectedWorkOrder: string | null;
    notifications: Notification[];
  };
  
  // Real-time data
  realTime: {
    aiActivity: AIActivity[];
    systemStatus: SystemStatus;
    activeConnections: number;
  };
}


// Redux slices for modular state management
const workOrderSlice = createSlice({
  name: 'workOrders',
  initialState: {
    items: {},
    filters: defaultFilters,
    loading: false,
    error: null
  },
  reducers: {
    setWorkOrders: (state, action) => {
      state.items = action.payload.reduce((acc, wo) => {
        acc[wo.id] = wo;
        return acc;
      }, {});
    },
    updateWorkOrderStatus: (state, action) => {
      const { workOrderId, status } = action.payload;
      if (state.items[workOrderId]) {
        state.items[workOrderId].status = status;
        state.items[workOrderId].updatedAt = new Date().toISOString();
      }
    },
    setFilters: (state, action) => {
      state.filters = { ...state.filters, ...action.payload };
    }
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchWorkOrders.pending, (state) => {
        state.loading = true;
        state.error = null;
      })
      .addCase(fetchWorkOrders.fulfilled, (state, action) => {
        state.loading = false;
        state.items = action.payload.reduce((acc, wo) => {
          acc[wo.id] = wo;
          return acc;
        }, {});
      })
      .addCase(fetchWorkOrders.rejected, (state, action) => {
        state.loading = false;
        state.error = action.error.message || 'Failed to fetch work orders';
      });
  }
});
7.3.4 Authentication And Authorization Ui
Role-Based UI Component Rendering:


// Role-based component access control
interface RoleBasedUIAccess {
  resident: {
    canView: ['own_work_orders', 'request_form', 'communication_history'];
    canEdit: ['own_requests', 'communication_preferences'];
    canApprove: [];
    hiddenComponents: ['vendor_management', 'cost_details', 'ai_override'];
  };
  
  property_manager: {
    canView: ['all_property_work_orders', 'vendor_performance', 'ai_activity'];
    canEdit: ['work_order_status', 'vendor_assignments', 'ai_overrides'];
    canApprove: ['costs_up_to_500'];
    hiddenComponents: ['owner_financial_details'];
  };
  
  regional_manager: {
    canView: ['portfolio_overview', 'staff_performance', 'system_metrics'];
    canEdit: ['all_work_orders', 'staff_assignments', 'system_settings'];
    canApprove: ['costs_up_to_2000', 'policy_changes'];
    hiddenComponents: [];
  };
  
  owner: {
    canView: ['own_property_reports', 'financial_summaries', 'performance_metrics'];
    canEdit: ['approval_thresholds', 'vendor_preferences'];
    canApprove: ['unlimited_costs', 'major_decisions'];
    hiddenComponents: ['detailed_ai_logs', 'staff_management'];
  };
}


// Role-based component wrapper
const RoleBasedComponent: React.FC<{
  requiredRole: UserRole;
  requiredPermission?: string;
  children: React.ReactNode;
}> = ({ requiredRole, requiredPermission, children }) => {
  const { user } = useAuth();
  const hasAccess = usePermissionCheck(user.role, requiredRole, requiredPermission);
  
  if (!hasAccess) {
    return null; // Hide component if no access
  }
  
  return <>{children}</>;
};


// Usage example
<RoleBasedComponent requiredRole="property_manager" requiredPermission="view_vendor_performance">
  <VendorPerformancePanel />
</RoleBasedComponent>
7.4 Ui Schema Definitions
7.4.1 Component Props Interfaces
Work Order Display Components:


// Work order card component props
interface WorkOrderCardProps {
  workOrder: WorkOrder;
  showActions?: boolean;
  compact?: boolean;
  onStatusChange?: (workOrderId: string, newStatus: WorkOrderStatus) => void;
  onVendorReassign?: (workOrderId: string) => void;
  onEscalate?: (workOrderId: string, reason: string) => void;
}


interface WorkOrder {
  id: string;
  workOrderNumber: string;
  property: {
    id: string;
    address: string;
    name: string;
  };
  unit: {
    id: string;
    number: string;
  };
  resident: {
    id: string;
    name: string;
    phone: string;
    email: string;
  };
  issue: {
    category: IssueCategory;
    subcategory: string;
    description: string;
    urgency: UrgencyLevel;
    photos: string[];
  };
  status: WorkOrderStatus;
  vendor?: {
    id: string;
    name: string;
    phone: string;
    eta?: string;
  };
  timeline: WorkOrderEvent[];
  costs: {
    estimated: CostEstimate;
    actual?: number;
    approved: boolean;
  };
  aiAnalysis: {
    confidence: number;
    classification: string;
    troubleshootingAttempted: boolean;
    recommendedAction: string;
  };
  createdAt: string;
  updatedAt: string;
  completedAt?: string;
}
Property and Vendor Management Components:


// Property card component props
interface PropertyCardProps {
  property: PropertyProfile;
  showMetrics?: boolean;
  onSelect?: (propertyId: string) => void;
  onEdit?: (propertyId: string) => void;
}


interface PropertyProfile {
  id: string;
  name: string;
  address: {
    street: string;
    city: string;
    state: string;
    zip: string;
    coordinates: { lat: number; lng: number };
  };
  type: PropertyType;
  unitCount: number;
  activeWorkOrders: number;
  monthlyMaintenanceCost: number;
  residentSatisfaction: number;
  preferredVendors: Record<IssueCategory, string[]>;
  owner: {
    id: string;
    name: string;
    approvalThreshold: number;
    notificationPreferences: NotificationPreferences;
  };
  access: {
    officeHours: TimeRange;
    afterHoursContact: ContactInfo;
    accessInstructions: string;
  };
}


// Vendor card component props
interface VendorCardProps {
  vendor: Vendor;
  showPerformance?: boolean;
  showAvailability?: boolean;
  onAssign?: (vendorId: string, workOrderId: string) => void;
  onViewDetails?: (vendorId: string) => void;
}


interface Vendor {
  id: string;
  companyName: string;
  contactName: string;
  phone: string;
  email: string;
  serviceTypes: VendorType[];
  coverage: {
    zipCodes: string[];
    maxRadius: number;
  };
  availability: {
    businessHours: TimeRange;
    afterHoursAvailable: boolean;
    emergencyAvailable: boolean;
    currentStatus: VendorStatus;
  };
  performance: {
    responseTime: number;
    completionTime: number;
    firstTimeFix: number;
    residentSatisfaction: number;
    totalJobs: number;
  };
  financials: {
    hourlyRate: number;
    emergencyMultiplier: number;
    typicalCostRange: { min: number; max: number };
  };
}
7.4.2 Form Schemas And Validation
Maintenance Request Form Schema:


// Maintenance request form validation schema
import { z } from 'zod';


const MaintenanceRequestSchema = z.object({
  propertyId: z.string().min(1, 'Property is required'),
  unitId: z.string().min(1, 'Unit is required'),
  residentId: z.string().min(1, 'Resident identification required'),
  issueCategory: z.enum([
    'plumbing', 'electrical', 'hvac', 'appliance', 'structural', 'pest'
  ]).optional(),
  description: z.string()
    .min(10, 'Please provide at least 10 characters describing the issue')
    .max(1000, 'Description too long'),
  urgency: z.enum(['routine', 'urgent', 'emergency']).default('routine'),
  photos: z.array(z.string().url()).max(5, 'Maximum 5 photos allowed'),
  preferredTimes: z.array(z.string().datetime()).optional(),
  residentContact: z.object({
    phone: z.string().regex(/^\+?1?[0-9]{10}$/, 'Invalid phone number'),
    email: z.string().email('Invalid email address'),
    preferredMethod: z.enum(['phone', 'sms', 'email']).default('sms')
  })
});


type MaintenanceRequestForm = z.infer<typeof MaintenanceRequestSchema>;


// Form component with validation
const MaintenanceRequestForm: React.FC = () => {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    watch,
    setValue
  } = useForm<MaintenanceRequestForm>({
    resolver: zodResolver(MaintenanceRequestSchema)
  });
  
  const onSubmit = async (data: MaintenanceRequestForm) => {
    try {
      const response = await maintenanceAPI.createWorkOrder(data);
      
      // Show success notification
      showNotification({
        type: 'success',
        message: `Work order ${response.workOrderId} created successfully`,
        duration: 5000
      });
      
      // Redirect to work order details
      router.push(`/work-orders/${response.workOrderId}`);
      
    } catch (error) {
      showNotification({
        type: 'error',
        message: 'Failed to create work order. Please try again.',
        duration: 5000
      });
    }
  };
  
  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-6">
      {/* Form fields with validation */}
    </form>
  );
};
7.4.3 Data Flow Patterns
Unidirectional Data Flow Architecture:


Backend Services


API Layer


UI Layer


React Components


Component State


Redux Store


API Client


WebSocket Manager


Response Cache


REST API Endpoints


WebSocket Server


Database Layer


7.5 Screen Specifications
7.5.1 Property Manager Main Dashboard
Dashboard Layout and Components:


Now that your data is ready, it's time to design your dashboard—the visual command center for your property management journey. Here are some principles to guide you: 1. Visualization is Key: Choose clear and concise visualizations like charts, graphs, and tables. Remember, less is often more. Aim for easily understandable visuals that communicate information quickly and effectively.


// Property Manager Dashboard screen component
const PropertyManagerDashboard: React.FC = () => {
  const { workOrders, properties, vendors, metrics } = useMaintenanceData();
  const { user } = useAuth();
  
  return (
    <DashboardLayout>
      {/* Top Navigation */}
      <TopNavigation>
        <PropertySelector 
          properties={properties}
          selectedProperty={user.selectedProperty}
          onPropertyChange={handlePropertyChange}
        />
        <NotificationBell 
          unreadCount={metrics.pendingEscalations}
          onClick={openNotificationCenter}
        />
        <UserMenu user={user} />
      </TopNavigation>
      
      {/* Main Content Grid */}
      <div className="grid grid-cols-12 gap-6 p-6">
        {/* Left Column - Quick Actions */}
        <div className="col-span-3 space-y-6">
          <QuickActionsPanel>
            <CreateWorkOrderButton />
            <EmergencyAlertButton />
            <BulkActionsButton />
          </QuickActionsPanel>
          
          <WorkOrderQueue
            urgentItems={workOrders.urgent}
            todayItems={workOrders.today}
            thisWeekItems={workOrders.thisWeek}
          />
          
          <AIActivityFeed
            activities={metrics.aiActivity}
            showConfidence={true}
            allowIntervention={true}
          />
        </div>
        
        {/* Center Column - Main Overview */}
        <div className="col-span-6 space-y-6">
          <MetricsCardsGrid>
            <MetricCard
              title="Response Time"
              value={metrics.avgResponseTime}
              target="<30s"
              trend={metrics.responseTimeTrend}
              status={metrics.responseTimeStatus}
            />
            <MetricCard
              title="Completion Rate"
              value={metrics.completionRate}
              target=">85%"
              trend={metrics.completionRateTrend}
              status={metrics.completionRateStatus}
            />
            <MetricCard
              title="AI Automation"
              value={metrics.aiAutomationRate}
              target=">80%"
              trend={metrics.automationTrend}
              status={metrics.automationStatus}
            />
            <MetricCard
              title="Cost per Door"
              value={metrics.costPerDoor}
              target="<$50"
              trend={metrics.costTrend}
              status={metrics.costStatus}
            />
          </MetricsCardsGrid>
          
          <WorkOrderTable
            workOrders={workOrders.active}
            columns={[
              'workOrderNumber',
              'property',
              'issue',
              'status',
              'vendor',
              'eta',
              'actions'
            ]}
            sortable={true}
            filterable={true}
            onRowClick={openWorkOrderDetails}
            onStatusChange={handleStatusChange}
          />
          
          <PerformanceTrendsChart
            data={metrics.trends}
            timeRange="30_days"
            metrics={['volume', 'cost', 'satisfaction']}
          />
        </div>
        
        {/* Right Column - Context and Alerts */}
        <div className="col-span-3 space-y-6">
          <VendorStatusPanel
            vendors={vendors.active}
            showAvailability={true}
            showPerformance={true}
          />
          
          <PendingApprovalsPanel
            approvals={metrics.pendingApprovals}
            onApprove={handleApproval}
            onDeny={handleDenial}
          />
          
          <RecentAlertsPanel
            alerts={metrics.recentAlerts}
            onDismiss={dismissAlert}
            onEscalate={escalateAlert}
          />
        </div>
      </div>
    </DashboardLayout>
  );
};
7.5.2 Work Order Detail Screen
Comprehensive Work Order Management Interface:


// Work order detail screen with full context
const WorkOrderDetailScreen: React.FC<{ workOrderId: string }> = ({ workOrderId }) => {
  const { workOrder, loading, error } = useWorkOrder(workOrderId);
  const { canEdit, canApprove } = usePermissions();
  
  if (loading) return <LoadingSpinner />;
  if (error) return <ErrorMessage error={error} />;
  
  return (
    <div className="max-w-7xl mx-auto p-6">
      {/* Header with status and actions */}
      <WorkOrderHeader
        workOrder={workOrder}
        onStatusChange={handleStatusChange}
        onEscalate={handleEscalation}
        onClose={handleClose}
      />
      
      <div className="grid grid-cols-12 gap-6 mt-6">
        {/* Left Column - Work Order Details */}
        <div className="col-span-8 space-y-6">
          <IssueDetailsCard
            issue={workOrder.issue}
            property={workOrder.property}
            unit={workOrder.unit}
            resident={workOrder.resident}
          />
          
          <ConversationTimeline
            events={workOrder.timeline}
            communications={workOrder.communications}
            showAIAnalysis={true}
          />
          
          {workOrder.troubleshootingSession && (
            <TroubleshootingSessionCard
              session={workOrder.troubleshootingSession}
              outcome={workOrder.troubleshootingSession.outcome}
            />
          )}
          
          {workOrder.vendor && (
            <VendorAssignmentCard
              vendor={workOrder.vendor}
              appointment={workOrder.appointment}
              onReassign={handleVendorReassign}
            />
          )}
          
          <CommunicationPanel
            workOrderId={workOrder.id}
            participants={[workOrder.resident, workOrder.vendor]}
            onSendMessage={handleSendMessage}
          />
        </div>
        
        {/* Right Column - Context and Actions */}
        <div className="col-span-4 space-y-6">
          <StatusProgressCard
            currentStatus={workOrder.status}
            timeline={workOrder.timeline}
            estimatedCompletion={workOrder.estimatedCompletion}
          />
          
          <PropertyContextCard
            property={workOrder.property}
            unit={workOrder.unit}
            relatedHistory={workOrder.relatedHistory}
          />
          
          <CostManagementCard
            estimate={workOrder.costs.estimated}
            actual={workOrder.costs.actual}
            approvalRequired={workOrder.costs.approvalRequired}
            onApprove={canApprove ? handleCostApproval : undefined}
          />
          
          <AIInsightsCard
            analysis={workOrder.aiAnalysis}
            recommendations={workOrder.aiRecommendations}
            onOverride={canEdit ? handleAIOverride : undefined}
          />
          
          <ActionButtonsPanel>
            {canEdit && (
              <>
                <Button variant="primary" onClick={handleEdit}>
                  Edit Work Order
                </Button>
                <Button variant="secondary" onClick={handleReassignVendor}>
                  Reassign Vendor
                </Button>
              </>
            )}
            {canApprove && workOrder.costs.approvalRequired && (
              <Button variant="success" onClick={handleApprove}>
                Approve Cost
              </Button>
            )}
            <Button variant="outline" onClick={handleEscalate}>
              Escalate to Human
            </Button>
          </ActionButtonsPanel>
        </div>
      </div>
    </div>
  );
};
7.5.3 Ai Activity Monitoring Screen
Real-Time AI Operations Dashboard:


// AI activity monitoring interface
const AIActivityMonitoringScreen: React.FC = () => {
  const { aiMetrics, aiActivity, systemHealth } = useAIMonitoring();
  
  return (
    <div className="p-6 space-y-6">
      {/* AI Performance Overview */}
      <div className="grid grid-cols-4 gap-6">
        <AIMetricCard
          title="Classification Accuracy"
          value={aiMetrics.classificationAccuracy}
          target={0.90}
          format="percentage"
          trend={aiMetrics.accuracyTrend}
        />
        <AIMetricCard
          title="Average Confidence"
          value={aiMetrics.averageConfidence}
          target={0.85}
          format="percentage"
          trend={aiMetrics.confidenceTrend}
        />
        <AIMetricCard
          title="Troubleshooting Success"
          value={aiMetrics.troubleshootingSuccess}
          target={0.30}
          format="percentage"
          trend={aiMetrics.troubleshootingTrend}
        />
        <AIMetricCard
          title="Automation Rate"
          value={aiMetrics.automationRate}
          target={0.80}
          format="percentage"
          trend={aiMetrics.automationTrend}
        />
      </div>
      
      {/* Real-time AI Activity Feed */}
      <div className="grid grid-cols-2 gap-6">
        <Card title="Live AI Activity">
          <AIActivityFeed
            activities={aiActivity}
            realTime={true}
            showConfidence={true}
            showRecommendations={true}
            onIntervene={handleAIIntervention}
          />
        </Card>
        
        <Card title="AI Decision Analysis">
          <AIDecisionAnalytics
            decisions={aiMetrics.recentDecisions}
            showBreakdown={true}
            onDrillDown={handleDecisionDrillDown}
          />
        </Card>
      </div>
      
      {/* AI Model Performance */}
      <Card title="Model Performance Metrics">
        <div className="grid grid-cols-3 gap-6">
          <ModelPerformanceChart
            model="triage_classifier"
            metrics={aiMetrics.triageModel}
            timeRange="24h"
          />
          <ModelPerformanceChart
            model="urgency_detector"
            metrics={aiMetrics.urgencyModel}
            timeRange="24h"
          />
          <ModelPerformanceChart
            model="troubleshooting_engine"
            metrics={aiMetrics.troubleshootingModel}
            timeRange="24h"
          />
        </div>
      </Card>
      
      {/* AI Intervention Opportunities */}
      <Card title="Intervention Opportunities">
        <InterventionOpportunitiesTable
          opportunities={aiMetrics.interventionOpportunities}
          onTakeAction={handleInterventionAction}
          onDismiss={handleDismissOpportunity}
        />
      </Card>
    </div>
  );
};
7.5.4 Vendor Portal Interface
Mobile-Optimized Vendor Experience:


// Vendor mobile portal interface
const VendorPortalInterface: React.FC = () => {
  const { vendor, availableJobs, acceptedJobs } = useVendorData();
  
  return (
    <MobileLayout>
      {/* Header with vendor info */}
      <VendorHeader
        vendor={vendor}
        onlineStatus={vendor.onlineStatus}
        onToggleAvailability={handleToggleAvailability}
      />
      
      {/* Tab Navigation */}
      <TabNavigation>
        <Tab id="available" label="Available Jobs" />
        <Tab id="accepted" label="My Jobs" />
        <Tab id="completed" label="Completed" />
        <Tab id="profile" label="Profile" />
      </TabNavigation>
      
      {/* Available Jobs Tab */}
      <TabPanel id="available">
        <JobListings
          jobs={availableJobs}
          onAccept={handleJobAccept}
          onDecline={handleJobDecline}
          onViewDetails={handleViewJobDetails}
        />
      </TabPanel>
      
      {/* Accepted Jobs Tab */}
      <TabPanel id="accepted">
        <AcceptedJobsList
          jobs={acceptedJobs}
          onCheckIn={handleCheckIn}
          onUpdateStatus={handleStatusUpdate}
          onComplete={handleJobComplete}
        />
      </TabPanel>
      
      {/* Job Detail Modal */}
      <JobDetailModal
        job={selectedJob}
        onAccept={handleJobAccept}
        onDecline={handleJobDecline}
        onGetDirections={handleGetDirections}
        onContactResident={handleContactResident}
      />
    </MobileLayout>
  );
};


// Job card component for vendor interface
interface JobCardProps {
  job: VendorJob;
  onAccept: (jobId: string) => void;
  onDecline: (jobId: string, reason: string) => void;
  onViewDetails: (jobId: string) => void;
}


const JobCard: React.FC<JobCardProps> = ({ job, onAccept, onDecline, onViewDetails }) => {
  return (
    <Card className="mb-4 border-l-4 border-l-blue-500">
      <CardHeader>
        <div className="flex justify-between items-start">
          <div>
            <h3 className="font-semibold text-lg">{job.issueCategory}</h3>
            <p className="text-gray-600">{job.property.address}</p>
          </div>
          <UrgencyBadge urgency={job.urgency} />
        </div>
      </CardHeader>
      
      <CardContent>
        <p className="text-sm mb-3">{job.description}</p>
        
        <div className="grid grid-cols-2 gap-4 text-sm">
          <div>
            <span className="font-medium">Unit:</span> {job.unit.number}
          </div>
          <div>
            <span className="font-medium">Resident:</span> {job.resident.name}
          </div>
          <div>
            <span className="font-medium">Estimated Cost:</span> ${job.estimatedCost}
          </div>
          <div>
            <span className="font-medium">Requested Time:</span> {job.requestedTime}
          </div>
        </div>
        
        {job.accessInstructions && (
          <div className="mt-3 p-2 bg-blue-50 rounded">
            <span className="font-medium text-blue-800">Access:</span>
            <p className="text-blue-700 text-sm">{job.accessInstructions}</p>
          </div>
        )}
      </CardContent>
      
      <CardFooter>
        <div className="flex space-x-2">
          <Button 
            variant="primary" 
            size="sm"
            onClick={() => onAccept(job.id)}
          >
            Accept Job
          </Button>
          <Button 
            variant="outline" 
            size="sm"
            onClick={() => onDecline(job.id, 'unavailable')}
          >
            Decline
          </Button>
          <Button 
            variant="ghost" 
            size="sm"
            onClick={() => onViewDetails(job.id)}
          >
            View Details
          </Button>
        </div>
      </CardFooter>
    </Card>
  );
};
7.5.5 Resident Request Submission Screen
Simplified Request Creation Interface:


// Resident request submission interface
const ResidentRequestScreen: React.FC = () => {
  const { properties, units } = useResidentData();
  const [formData, setFormData] = useState<MaintenanceRequestForm>();
  
  return (
    <div className="max-w-2xl mx-auto p-6">
      <PageHeader
        title="Submit Maintenance Request"
        subtitle="Describe your issue and we'll get help on the way"
      />
      
      <Card>
        <CardContent className="space-y-6">
          {/* Issue Category Selection */}
          <IssueCategorySelector
            categories={issueCategories}
            selectedCategory={formData?.issueCategory}
            onCategorySelect={handleCategorySelect}
          />
          
          {/* Issue Description */}
          <div>
            <Label htmlFor="description">Describe the Issue</Label>
            <Textarea
              id="description"
              placeholder="Please describe what's happening in detail..."
              value={formData?.description || ''}
              onChange={handleDescriptionChange}
              rows={4}
              className="mt-1"
            />
            <p className="text-sm text-gray-500 mt-1">
              Be specific - this helps our AI provide better assistance
            </p>
          </div>
          
          {/* Photo Upload */}
          <PhotoUploadSection
            photos={formData?.photos || []}
            onPhotosChange={handlePhotosChange}
            maxPhotos={5}
            acceptedTypes={['image/jpeg', 'image/png']}
          />
          
          {/* Urgency Selection */}
          <UrgencySelector
            urgency={formData?.urgency || 'routine'}
            onUrgencyChange={handleUrgencyChange}
            showEmergencyWarning={true}
          />
          
          {/* Preferred Times (Optional) */}
          <PreferredTimesSelector
            preferredTimes={formData?.preferredTimes || []}
            onTimesChange={handlePreferredTimesChange}
            showOptionalLabel={true}
          />
          
          {/* Contact Preferences */}
          <ContactPreferencesSection
            preferences={formData?.residentContact}
            onPreferencesChange={handleContactPreferencesChange}
          />
        </CardContent>
        
        <CardFooter>
          <div className="flex justify-between">
            <Button variant="outline" onClick={handleCancel}>
              Cancel
            </Button>
            <Button 
              variant="primary" 
              onClick={handleSubmit}
              disabled={!isFormValid}
              loading={isSubmitting}
            >
              Submit Request
            </Button>
          </div>
        </CardFooter>
      </Card>
      
      {/* AI Assistance Panel */}
      <AIAssistancePanel
        issueCategory={formData?.issueCategory}
        description={formData?.description}
        onTroubleshootingStart={handleTroubleshootingStart}
      />
    </div>
  );
};
7.6 User Interaction Patterns
7.6.1 Conversational Ui Components
AI Chat Interface for Troubleshooting:


// Conversational troubleshooting interface
const TroubleshootingChatInterface: React.FC<{
  workOrderId: string;
  onResolutionComplete: (outcome: TroubleshootingOutcome) => void;
}> = ({ workOrderId, onResolutionComplete }) => {
  const { session, messages, isActive } = useTroubleshootingSession(workOrderId);
  const [userInput, setUserInput] = useState('');
  
  return (
    <Card className="h-96 flex flex-col">
      <CardHeader>
        <div className="flex items-center space-x-2">
          <Bot className="w-5 h-5 text-blue-500" />
          <h3 className="font-semibold">AI Troubleshooting Assistant</h3>
          {isActive && <StatusIndicator status="active" />}
        </div>
      </CardHeader>
      
      <CardContent className="flex-1 overflow-y-auto">
        <MessageList>
          {messages.map((message, index) => (
            <Message
              key={index}
              sender={message.sender}
              content={message.content}
              timestamp={message.timestamp}
              type={message.type}
            />
          ))}
        </MessageList>
      </CardContent>
      
      <CardFooter>
        {isActive ? (
          <div className="flex space-x-2 w-full">
            <Input
              value={userInput}
              onChange={(e) => setUserInput(e.target.value)}
              placeholder="Type your response..."
              onKeyPress={handleKeyPress}
              className="flex-1"
            />
            <Button 
              onClick={handleSendResponse}
              disabled={!userInput.trim()}
            >
              Send
            </Button>
          </div>
        ) : (
          <div className="text-center text-gray-500">
            Troubleshooting session completed
          </div>
        )}
      </CardFooter>
    </Card>
  );
};


// Message component for chat interface
const Message: React.FC<{
  sender: 'ai' | 'resident' | 'system';
  content: string;
  timestamp: string;
  type?: 'text' | 'instruction' | 'question' | 'image';
}> = ({ sender, content, timestamp, type = 'text' }) => {
  const isAI = sender === 'ai';
  
  return (
    <div className={`flex ${isAI ? 'justify-start' : 'justify-end'} mb-4`}>
      <div className={`max-w-xs lg:max-w-md px-4 py-2 rounded-lg ${
        isAI 
          ? 'bg-blue-100 text-blue-900' 
          : 'bg-gray-100 text-gray-900'
      }`}>
        {type === 'instruction' && (
          <div className="flex items-center space-x-1 mb-1">
            <Wrench className="w-4 h-4" />
            <span className="text-xs font-medium">INSTRUCTION</span>
          </div>
        )}
        
        <p className="text-sm">{content}</p>
        
        <p className="text-xs text-gray-500 mt-1">
          {new Date(timestamp).toLocaleTimeString()}
        </p>
      </div>
    </div>
  );
};
7.6.2 Drag-and-drop Interfaces
Work Order Assignment Interface:


// Drag-and-drop vendor assignment
const VendorAssignmentBoard: React.FC = () => {
  const { unassignedWorkOrders, vendors } = useVendorAssignment();
  
  const handleDrop = (workOrderId: string, vendorId: string) => {
    assignWorkOrderToVendor(workOrderId, vendorId);
  };
  
  return (
    <div className="grid grid-cols-4 gap-6 h-full">
      {/* Unassigned Work Orders */}
      <Card title="Unassigned Work Orders">
        <DragDropContext onDragEnd={handleDragEnd}>
          <Droppable droppableId="unassigned">
            {(provided) => (
              <div {...provided.droppableProps} ref={provided.innerRef}>
                {unassignedWorkOrders.map((workOrder, index) => (
                  <Draggable
                    key={workOrder.id}
                    draggableId={workOrder.id}
                    index={index}
                  >
                    {(provided) => (
                      <div
                        ref={provided.innerRef}
                        {...provided.draggableProps}
                        {...provided.dragHandleProps}
                      >
                        <WorkOrderDragCard workOrder={workOrder} />
                      </div>
                    )}
                  </Draggable>
                ))}
                {provided.placeholder}
              </div>
            )}
          </Droppable>
        </DragDropContext>
      </Card>
      
      {/* Vendor Columns */}
      {vendors.map((vendor) => (
        <Card key={vendor.id} title={vendor.companyName}>
          <VendorDropZone
            vendor={vendor}
            assignedWorkOrders={vendor.assignedWorkOrders}
            onDrop={handleDrop}
          />
        </Card>
      ))}
    </div>
  );
};
7.6.3 Real-time Status Updates
Live Status Indicator Components:


// Real-time status indicators
const LiveStatusIndicator: React.FC<{
  workOrderId: string;
  currentStatus: WorkOrderStatus;
}> = ({ workOrderId, currentStatus }) => {
  const { status, lastUpdate } = useRealTimeStatus(workOrderId);
  
  const getStatusColor = (status: WorkOrderStatus): string => {
    const statusColors = {
      'NEW': 'bg-gray-500',
      'TRIAGING': 'bg-blue-500 animate-pulse',
      'TROUBLESHOOTING': 'bg-yellow-500 animate-pulse',
      'AWAITING_DISPATCH': 'bg-orange-500',
      'DISPATCHING': 'bg-purple-500 animate-pulse',
      'SCHEDULED': 'bg-green-500',
      'VENDOR_EN_ROUTE': 'bg-green-600 animate-pulse',
      'IN_PROGRESS': 'bg-blue-600 animate-pulse',
      'PENDING_VERIFICATION': 'bg-yellow-600',
      'COMPLETED': 'bg-green-700',
      'ESCALATED': 'bg-red-500 animate-pulse'
    };
    return statusColors[status] || 'bg-gray-400';
  };
  
  return (
    <div className="flex items-center space-x-2">
      <div className={`w-3 h-3 rounded-full ${getStatusColor(status)}`} />
      <span className="text-sm font-medium">{status.replace('_', ' ')}</span>
      <span className="text-xs text-gray-500">
        Updated {formatRelativeTime(lastUpdate)}
      </span>
    </div>
  );
};


// Progress timeline component
const WorkOrderProgressTimeline: React.FC<{
  timeline: WorkOrderEvent[];
  currentStatus: WorkOrderStatus;
}> = ({ timeline, currentStatus }) => {
  return (
    <div className="space-y-4">
      {timeline.map((event, index) => (
        <TimelineEvent
          key={index}
          event={event}
          isActive={event.status === currentStatus}
          isCompleted={index < timeline.length - 1}
        />
      ))}
    </div>
  );
};
7.7 Visual Design Considerations
7.7.1 Design System And Branding
Comprehensive Design System:


As part of crafting a cohesive RE Management Tool - Real Estate SaaS ui / ux, the team developed a modern visual system to ensure emotional resonance across every screen. The chosen typography balances elegance with readability, using distinct heading and body styles for clear information hierarchy. The color palette combines bright, energetic yellow with calming blue, complemented by white and black to maintain contrast and accessibility.


// Design system configuration
const designSystem = {
  colors: {
    primary: {
      50: '#eff6ff',
      100: '#dbeafe',
      500: '#3b82f6',  // Primary blue
      600: '#2563eb',
      700: '#1d4ed8',
      900: '#1e3a8a'
    },
    secondary: {
      50: '#fefce8',
      100: '#fef3c7',
      500: '#f59e0b',  // Warning yellow
      600: '#d97706',
      700: '#b45309'
    },
    success: {
      50: '#f0fdf4',
      500: '#10b981',  // Success green
      700: '#047857'
    },
    danger: {
      50: '#fef2f2',
      500: '#ef4444',  // Error red
      700: '#b91c1c'
    },
    gray: {
      50: '#f9fafb',
      100: '#f3f4f6',
      200: '#e5e7eb',
      500: '#6b7280',
      700: '#374151',
      900: '#111827'
    }
  },
  
  typography: {
    fontFamily: {
      sans: ['Inter', 'system-ui', 'sans-serif'],
      mono: ['JetBrains Mono', 'monospace']
    },
    fontSize: {
      xs: '0.75rem',
      sm: '0.875rem',
      base: '1rem',
      lg: '1.125rem',
      xl: '1.25rem',
      '2xl': '1.5rem',
      '3xl': '1.875rem'
    },
    fontWeight: {
      normal: '400',
      medium: '500',
      semibold: '600',
      bold: '700'
    }
  },
  
  spacing: {
    xs: '0.25rem',
    sm: '0.5rem',
    md: '1rem',
    lg: '1.5rem',
    xl: '2rem',
    '2xl': '3rem'
  },
  
  borderRadius: {
    sm: '0.25rem',
    md: '0.375rem',
    lg: '0.5rem',
    xl: '0.75rem'
  },
  
  shadows: {
    sm: '0 1px 2px 0 rgb(0 0 0 / 0.05)',
    md: '0 4px 6px -1px rgb(0 0 0 / 0.1)',
    lg: '0 10px 15px -3px rgb(0 0 0 / 0.1)',
    xl: '0 20px 25px -5px rgb(0 0 0 / 0.1)'
  }
};
7.7.2 Status Visualization Patterns
Work Order Status Visual Language:


Aggregate status cards show a total number of objects and an aggregated status for them. For example, they can be used to provide users with a quick count of the number of nodes making up a large distributed network and identify the numbers that are down, that need maintenance, etc. There would also typically be a link to examine more details.


// Status visualization components
const StatusVisualization = {
  // Color coding for work order statuses
  statusColors: {
    'NEW': { bg: 'bg-gray-100', text: 'text-gray-800', border: 'border-gray-300' },
    'TRIAGING': { bg: 'bg-blue-100', text: 'text-blue-800', border: 'border-blue-300' },
    'TROUBLESHOOTING': { bg: 'bg-yellow-100', text: 'text-yellow-800', border: 'border-yellow-300' },
    'AWAITING_DISPATCH': { bg: 'bg-orange-100', text: 'text-orange-800', border: 'border-orange-300' },
    'DISPATCHING': { bg: 'bg-purple-100', text: 'text-purple-800', border: 'border-purple-300' },
    'SCHEDULED': { bg: 'bg-green-100', text: 'text-green-800', border: 'border-green-300' },
    'VENDOR_EN_ROUTE': { bg: 'bg-green-200', text: 'text-green-900', border: 'border-green-400' },
    'IN_PROGRESS': { bg: 'bg-blue-200', text: 'text-blue-900', border: 'border-blue-400' },
    'PENDING_VERIFICATION': { bg: 'bg-yellow-200', text: 'text-yellow-900', border: 'border-yellow-400' },
    'COMPLETED': { bg: 'bg-green-200', text: 'text-green-900', border: 'border-green-400' },
    'ESCALATED': { bg: 'bg-red-100', text: 'text-red-800', border: 'border-red-300' }
  },
  
  // Urgency indicators
  urgencyIndicators: {
    'routine': { icon: 'Clock', color: 'text-gray-500', priority: 'Low' },
    'urgent': { icon: 'AlertTriangle', color: 'text-orange-500', priority: 'High' },
    'emergency': { icon: 'AlertCircle', color: 'text-red-500', priority: 'Critical' }
  },
  
  // Progress indicators
  progressIndicators: {
    'linear': 'LinearProgressBar',
    'circular': 'CircularProgressIndicator',
    'stepped': 'SteppedProgressIndicator'
  }
};


// Status badge component
const StatusBadge: React.FC<{
  status: WorkOrderStatus;
  size?: 'sm' | 'md' | 'lg';
  showIcon?: boolean;
}> = ({ status, size = 'md', showIcon = true }) => {
  const colors = StatusVisualization.statusColors[status];
  const sizeClasses = {
    sm: 'px-2 py-1 text-xs',
    md: 'px-3 py-1 text-sm',
    lg: 'px-4 py-2 text-base'
  };
  
  return (
    <span className={`
      inline-flex items-center space-x-1 rounded-full font-medium
      ${colors.bg} ${colors.text} ${colors.border} border
      ${sizeClasses[size]}
    `}>


# 8. Infrastructure


## 8.1 Deployment Environment


### 8.1.1 Target Environment Assessment


The AI Maintenance Coordinator requires a robust, scalable cloud infrastructure capable of supporting both real-time AI reasoning and durable workflow orchestration. Cloud readiness in 2026 means thoughtful placement of workloads across Microsoft 365, Azure, and hybrid environments, paired with modern identity, cost governance, and continuous security. The system operates as a distributed application with stringent performance requirements and 24/7 availability expectations.


**Environment Type: Hybrid Multi-Cloud**


The system implements a hybrid multi-cloud strategy optimized for resilience and cost efficiency. "Resilience and redundancy" are the two Rs that attract companies to a multi-cloud setup. If one provider faces downtime or changes its pricing, your business doesn't take the hit — you've got backup options.


| Environment Aspect | Specification | Justification |
|---|---|---|
| **Primary Cloud Provider** | Amazon Web Services (AWS) | AWS runs the control plane for you, highly available across AZs, hardened and kept current, while you retain the levers that matter: node strategy (EC2, Fargate, or hybrid), networking and IAM boundaries, autoscaling policy, and cost discipline. The payoff is predictable operations at scale, with native hooks into the AWS stack you already trust. |
| **Secondary Provider** | Microsoft Azure | Disaster recovery and geographic distribution |
| **Container Orchestration** | Amazon EKS (Elastic Kubernetes Service) | Amazon Elastic Kubernetes Service (EKS) is a managed service and certified Kubernetes conformant to run Kubernetes on AWS and on-premises. Run production-grade workloads in a highly reliable, scalable, and secure environment leveraging the proven reliability of AWS' global infrastructure and native integrations with AWS Security Services. |
| **Geographic Distribution** | Multi-region (us-east-1 primary, us-west-2 DR) | Latency optimization and disaster recovery |


**Resource Requirements:**


| Resource Category | Specification | Scaling Strategy |
|---|---|---|
| **Compute** | 50-200 vCPUs (auto-scaling) | Auto-scaling is a crucial feature in Kubernetes, allowing businesses to automatically scale their applications based on demand. In 2026, expect more advanced auto-scaling capabilities, including predictive scaling, which uses machine learning algorithms to forecast future demand and adjust resource allocation accordingly. This feature will help businesses optimize resource utilization, reduce costs, and improve overall application performance. |
| **Memory** | 100-400 GB RAM | Dynamic allocation based on AI processing load |
| **Storage** | 10 TB persistent, 5 TB cache | MongoDB, Redis, and TimescaleDB requirements |
| **Network** | 10 Gbps bandwidth | Real-time voice processing and high-volume API calls |


**Compliance and Regulatory Requirements:**


| Compliance Framework | Requirements | Implementation |
|---|---|---|
| **SOC 2 Type II** | Security controls, audit trails | Automated compliance monitoring |
| **GDPR/CCPA** | Data privacy, retention policies | Automated data lifecycle management |
| **HIPAA** | Healthcare data protection | Encryption at rest and in transit |
| **PCI DSS** | Payment data security | Tokenization and secure payment processing |


### 8.1.2 Environment Management


**Infrastructure as Code (IaC) Approach:**


Terraform is HashiCorp's infrastructure as code tool. It lets you define resources and infrastructure in human-readable, declarative configuration files, and manages your infrastructure's lifecycle. The system implements a comprehensive IaC strategy using Terraform for infrastructure provisioning and Kubernetes manifests for application deployment.


```hcl
9. Appendices
9.1 Additional Technical Information
9.1.1 Model Context Protocol (mcp) Server Architecture
The AI Maintenance Coordinator leverages Model Context Protocol (MCP) servers, bringing the same security rigor to the AI agent infrastructure that developers are rapidly adopting. MCP provides a standardized interface for AI systems to integrate with external tools and data sources, enabling seamless connectivity with property management systems, telephony services, and payment processors.


MCP Server Implementation Strategy:


MCP Server        Purpose        Integration Method        Security Features
**mcp-pms-appfolio**        AppFolio property management integration        OAuth 2.0 + REST API        Encrypted credentials, audit logging
**mcp-pms-yardi**        Yardi property management integration        OAuth 2.0 + REST API        Role-based access control
**mcp-telephony**        Twilio voice and SMS integration        API key authentication        Rate limiting, webhook validation
**mcp-payment**        Treasury/TigerBeetle payment processing        Certificate-based auth        Exactly-once transaction guarantees
9.1.2 Ai Model Integration Framework
Large Language Model Integration:


The system integrates with multiple AI providers to ensure reliability and cost optimization. LangGraph 1.0 addresses these gaps with a powerful graph-based execution model, and it provides production-ready features for reliable agentic systems: Durable state - Your agent's execution state persists automatically, so if your server restarts mid-conversation or a long-running workflow gets interrupted, it picks up exactly where it left off without losing context or forcing users to start over. Built-in persistence - Save and resume agent workflows at any point without writing custom database logic, enabling use cases like multi-day approval processes or background jobs that run across multiple sessions.


AI Provider        Model        Use Case        Fallback Strategy
**OpenAI**        GPT-4 Turbo        Primary triage and classification        Anthropic Claude
**Anthropic**        Claude 3.5 Sonnet        Complex reasoning and troubleshooting        OpenAI GPT-4
**Deepgram**        Nova-2        Speech-to-text processing        OpenAI Whisper
**ElevenLabs**        Turbo v2.5        Text-to-speech synthesis        Azure Neural Voices
9.1.3 Container Security Implementation
Docker Hardened Images Integration:


For this reason, we launched Docker Hardened Images (DHI), a secure, minimal, production-ready set of images, in May 2025, and since then have hardened over 1,000 images and helm charts in our catalog. The result: dramatically reduced CVEs (guaranteed near zero in DHI Enterprise), images up to 95 percent smaller, and secure defaults without ever compromising transparency or trust.


Hardened Image Configuration:


# Production Dockerfile using Docker Hardened Images
FROM docker.io/docker/hardened-python:3.12-slim as production


#### Copy application code
COPY --from=builder /app/src /app/src
COPY --from=builder /app/main.py /app/


#### Create non-root user (already configured in hardened image)
USER 1000:1000


#### Set secure environment variables
ENV PYTHONPATH=/app
ENV PYTHONUNBUFFERED=1
ENV PYTHONDONTWRITEBYTECODE=1


#### Health check with timeout
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD python -c "import requests; requests.get('http://localhost:8000/health', timeout=2)"


#### Expose port and run
EXPOSE 8000
CMD ["python", "main.py"]
9.1.4 Performance Optimization Techniques
Database Performance Optimizations:


MongoDB 8.0 delivers a significant throughput and latency boost compared with previous versions. 8.0 vs 7.0 using internal testing with public benchmarks: 32% faster for 95/5 mix of reads and writes (Yahoo! Cloud Serving Benchmark, YCSB) More than 200% faster for time series data aggregations and up to 60% faster queries for time series data (Timescale Time Series Benchmark Suite) 20% faster concurrent writes during data replication


Redis Performance Enhancements:


For developers, who are building real-time data-driven applications, Redis is the preferred, fastest, and most feature-rich cache, data structure server, and document and vector query engine. I/O threading: substantial throughput increase (e.g. >30% for caching use cases (10% SET, 90% GET), 4 cores) JSON: substantial memory reduction for homogenous arrays (up to 92%)


9.1.5 Advanced Troubleshooting Knowledge Base
Extended Troubleshooting Scenarios:


Issue Category        Scenario        Resolution Steps        Success Rate
**HVAC**        AC not cooling in summer        Check thermostat → Check filter → Check breaker → Check outdoor unit        45%
**Plumbing**        Low water pressure        Check aerator → Check shutoff valve → Check water heater → Check main line        35%
**Electrical**        GFCI outlet not working        Press reset button → Check breaker → Test with different device → Check wiring        60%
**Appliance**        Refrigerator not cooling        Check temperature settings → Check door seals → Check coils → Check power        40%
9.1.6 Vendor Communication Templates
SMS Dispatch Templates:


[EMERGENCY] Maintenance Request
Property: {property_address}
Unit: {unit_number}
URGENT: {issue_description}
Resident: {resident_name} {resident_phone}
IMMEDIATE RESPONSE REQUIRED
Reply YES with ETA or call {emergency_number}
Job ID: {work_order_id}
[Routine] Maintenance Request
Property: {property_address}
Unit: {unit_number}
Issue: {issue_category} - {issue_description}
Contact: {resident_name} {resident_phone}
Access: {access_instructions}
Reply YES to accept. Preferred time: {requested_time}
Job ID: {work_order_id}
9.1.7 Compliance Framework Implementation
Multi-Framework Compliance Matrix:


Compliance Requirement        Implementation        Monitoring        Reporting
**GDPR Article 32**        Encryption at rest and in transit        Automated compliance checks        Quarterly compliance reports
**CCPA Section 1798.100**        Data minimization and consent        Privacy impact assessments        Annual privacy audits
**SOC 2 Type II**        Access controls and audit trails        Continuous monitoring        Semi-annual SOC 2 reports
**HIPAA 164.312**        Administrative, physical, technical safeguards        Real-time security monitoring        Monthly HIPAA compliance reviews
9.2 Glossary
9.2.1 Technical Terms
Term        Definition
**Cold Path**        Durable workflow orchestration for long-running processes with exactly-once execution guarantees
**Hot Path**        Real-time AI reasoning and decision-making with sub-500ms latency requirements
**MCP Server**        Model Context Protocol server providing standardized AI-to-system integration
**Work Order State Machine**        Complete lifecycle management system with 12 distinct states and automated transitions
9.2.2 Business Terms
Term        Definition
**Cost per Door**        Monthly maintenance cost divided by total managed units, target <$50/door
**First-Time Fix Rate**        Percentage of issues resolved in single vendor visit, target >85%
**Troubleshooting Resolution Rate**        Percentage of issues resolved without vendor dispatch, target 20-35%
**Escalation Rate**        Percentage of requests requiring human intervention, target <15%
9.2.3 System Terms
Term        Definition
**Durable Execution**        Temporal's guarantee that workflows survive failures and resume exactly where they left off
**Session Affinity**        Routing strategy ensuring multi-turn conversations stay with the same service instance
**Circuit Breaker**        Fault tolerance pattern that prevents cascading failures by failing fast when services are degraded
**Exactly-Once Processing**        Guarantee that each operation is processed once and only once, even in failure scenarios
9.3 Acronyms
9.3.1 Technology Acronyms
Acronym        Expanded Form
**API**        Application Programming Interface
**DHI**        Docker Hardened Images
**EKS**        Amazon Elastic Kubernetes Service
**HITL**        Human-in-the-Loop
**HVAC**        Heating, Ventilation, and Air Conditioning
**JWT**        JSON Web Token
**MCP**        Model Context Protocol
**NLU**        Natural Language Understanding
**RBAC**        Role-Based Access Control
**SLA**        Service Level Agreement
**TTS**        Text-to-Speech
**VPC**        Virtual Private Cloud
9.3.2 Business Acronyms
Acronym        Expanded Form
**KPI**        Key Performance Indicator
**NOI**        Net Operating Income
**PMS**        Property Management System
**PMO**        Property Maintenance Operations
**ROI**        Return on Investment
**SLI**        Service Level Indicator
**SLO**        Service Level Objective
**YoY**        Year-over-Year
9.3.3 Compliance Acronyms
Acronym        Expanded Form
**CCPA**        California Consumer Privacy Act
**GDPR**        General Data Protection Regulation
**HIPAA**        Health Insurance Portability and Accountability Act
**PCI DSS**        Payment Card Industry Data Security Standard
**SOC 2**        Service Organization Control 2
**SOX**        Sarbanes-Oxley Act
9.4 Environment Variables Configuration
9.4.1 Core Service Configuration
# AI Maintenance Coordinator Environment Variables


#### Database Configuration
MONGODB_URL=mongodb+srv://cluster.mongodb.net/ai_maintenance_coordinator
MONGODB_DATABASE=ai_maintenance_coordinator
REDIS_URL=redis://redis-cluster:6379
TIMESCALE_URL=postgresql://user:pass@timescale:5432/metrics


#### AI Service Configuration
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...
DEEPGRAM_API_KEY=...
ELEVENLABS_API_KEY=...


#### Telephony Configuration
TWILIO_ACCOUNT_SID=AC...
TWILIO_AUTH_TOKEN=...
TWILIO_PHONE_NUMBER=+1555...


#### Email Configuration
SENDGRID_API_KEY=SG...
SENDGRID_FROM_EMAIL=maintenance@company.com


#### PMS Integration
APPFOLIO_CLIENT_ID=...
APPFOLIO_CLIENT_SECRET=...
YARDI_CLIENT_ID=...
YARDI_CLIENT_SECRET=...


#### Security Configuration
JWT_SECRET_KEY=...
ENCRYPTION_KEY=...
API_KEY_SALT=...


#### Temporal Configuration
TEMPORAL_HOST=temporal:7233
TEMPORAL_NAMESPACE=ai-maintenance


#### Monitoring Configuration
PROMETHEUS_URL=http://prometheus:9090
GRAFANA_URL=http://grafana:3000
JAEGER_ENDPOINT=http://jaeger:14268


#### Application Configuration
LOG_LEVEL=INFO
DEBUG=false
ENVIRONMENT=production
9.4.2 Feature Flags Configuration
# Feature flags for gradual rollout
feature_flags:
  voice_agent_enabled: true
  troubleshooting_engine_enabled: true
  automated_vendor_dispatch: true
  cost_approval_automation: true
  emergency_escalation: true
  multi_language_support: false  # Phase 2 feature
  predictive_maintenance: false  # Future feature
  
# A/B testing configuration
ab_testing:
  troubleshooting_flow_v2:
    enabled: true
    traffic_percentage: 10
    control_group: "original_flow"
    test_group: "enhanced_flow"
  
  vendor_selection_algorithm_v2:
    enabled: false
    traffic_percentage: 0
9.5 Message Queue Topics And Events
9.5.1 Event Schema Definitions
# Event schemas for system integration
event_schemas:
  maintenance_request_received:
    type: object
    properties:
      event_id: { type: string }
      timestamp: { type: string, format: date-time }
      work_order_id: { type: string }
      source_channel: { type: string, enum: [phone, sms, email, portal] }
      property_id: { type: string }
      issue_category: { type: string }
      urgency: { type: string, enum: [routine, urgent, emergency] }
    required: [event_id, timestamp, work_order_id, source_channel]
  
  vendor_dispatched:
    type: object
    properties:
      event_id: { type: string }
      timestamp: { type: string, format: date-time }
      work_order_id: { type: string }
      vendor_id: { type: string }
      contact_method: { type: string }
      eta: { type: string, format: date-time }
    required: [event_id, timestamp, work_order_id, vendor_id]
  
  escalation_triggered:
    type: object
    properties:
      event_id: { type: string }
      timestamp: { type: string, format: date-time }
      work_order_id: { type: string }
      escalation_reason: { type: string }
      escalation_level: { type: integer, minimum: 1, maximum: 3 }
      assigned_to: { type: string }
    required: [event_id, timestamp, work_order_id, escalation_reason]
9.5.2 Temporal Task Queue Configuration
# Temporal task queue definitions
task_queues:
  maintenance_requests:
    description: "Primary queue for maintenance request processing"
    max_concurrent_activities: 100
    max_concurrent_workflows: 50
    task_timeout: "5m"
    
  vendor_dispatch:
    description: "Queue for vendor communication and dispatch"
    max_concurrent_activities: 200
    max_concurrent_workflows: 100
    task_timeout: "30m"
    
  notifications:
    description: "Queue for notification delivery"
    max_concurrent_activities: 500
    max_concurrent_workflows: 200
    task_timeout: "2m"
    
  escalations:
    description: "High-priority queue for escalation handling"
    max_concurrent_activities: 50
    max_concurrent_workflows: 25
    task_timeout: "1m"
9.6 Api Reference Summary
9.6.1 Core Api Endpoints
Maintenance Request Management:


Endpoint        Method        Purpose        Authentication
`/api/v1/maintenance/requests`        POST        Create new maintenance request        Bearer token
`/api/v1/work-orders/{id}`        GET        Retrieve work order details        Bearer token
`/api/v1/work-orders/{id}/status`        PATCH        Update work order status        Bearer token + RBAC
`/api/v1/troubleshooting/{id}/response`        POST        Submit troubleshooting response        Session token
Vendor Management:


Endpoint        Method        Purpose        Authentication
`/api/v1/vendor-portal/jobs`        GET        List assigned jobs        API key
`/api/v1/vendor-portal/jobs/{id}/accept`        POST        Accept job assignment        API key
`/api/v1/vendor-portal/jobs/{id}/complete`        POST        Mark job complete        API key
`/api/v1/vendors/{id}/performance`        GET        Get vendor performance metrics        Bearer token + RBAC
9.6.2 Webhook Endpoints
Inbound Webhooks:


Endpoint        Source        Purpose        Validation
`/webhooks/twilio/voice/incoming`        Twilio        Incoming voice calls        Signature validation
`/webhooks/twilio/sms/incoming`        Twilio        Incoming SMS messages        Signature validation
`/webhooks/appfolio/work-orders`        AppFolio        Work order updates        OAuth 2.0 + signature
`/webhooks/vendor/completion`        Vendor Portal        Job completion notifications        HMAC signature
9.7 Database Schema Ddl
9.7.1 Mongodb Collection Schemas
// MongoDB collection creation scripts
db.createCollection("work_orders", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["work_order_id", "property_id", "unit_id", "resident_id", "issue_description", "status", "created_at"],
      properties: {
        work_order_id: { bsonType: "string" },
        property_id: { bsonType: "string" },
        unit_id: { bsonType: "string" },
        resident_id: { bsonType: "string" },
        vendor_id: { bsonType: ["string", "null"] },
        issue_category: { enum: ["plumbing", "electrical", "hvac", "appliance", "structural", "pest"] },
        issue_description: { bsonType: "string", minLength: 10 },
        urgency: { enum: ["routine", "urgent", "emergency"] },
        status: { enum: ["NEW", "TRIAGING", "TROUBLESHOOTING", "AWAITING_DISPATCH", "DISPATCHING", "SCHEDULED", "VENDOR_EN_ROUTE", "IN_PROGRESS", "NEEDS_PARTS", "PENDING_VERIFICATION", "COMPLETED", "RESOLVED", "ESCALATED", "CANCELLED"] },
        estimated_cost: { bsonType: ["number", "null"], minimum: 0 },
        actual_cost: { bsonType: ["number", "null"], minimum: 0 },
        created_at: { bsonType: "date" },
        updated_at: { bsonType: "date" },
        completed_at: { bsonType: ["date", "null"] }
      }
    }
  }
});


// Create indexes for optimal query performance
db.work_orders.createIndex({ "property_id": 1, "status": 1, "created_at": -1 });
db.work_orders.createIndex({ "resident_id": 1, "created_at": -1 });
db.work_orders.createIndex({ "vendor_id": 1, "status": 1 });
db.work_orders.createIndex({ "issue_category": 1, "urgency": 1 });
9.7.2 Timescaledb Hypertable Schemas
-- Performance metrics hypertable
CREATE TABLE performance_metrics (
    time TIMESTAMPTZ NOT NULL,
    metric_name TEXT NOT NULL,
    metric_value DOUBLE PRECISION NOT NULL,
    dimensions JSONB,
    property_id TEXT,
    work_order_id TEXT,
    vendor_id TEXT
);


-- Convert to hypertable with 1-day chunks
SELECT create_hypertable(
    'performance_metrics', 
    'time',
    chunk_time_interval => INTERVAL '1 day'
);


-- Create continuous aggregate for real-time dashboards
CREATE MATERIALIZED VIEW daily_performance_summary
WITH (timescaledb.continuous) AS
SELECT 
    time_bucket('1 day', time) AS day,
    metric_name,
    property_id,
    AVG(metric_value) AS avg_value,
    MAX(metric_value) AS max_value,
    MIN(metric_value) AS min_value,
    COUNT(*) AS sample_count
FROM performance_metrics
GROUP BY day, metric_name, property_id;
9.8 Troubleshooting Knowledge Base Sample Entries
9.8.1 Complete Troubleshooting Flows
HVAC - Air Conditioner Not Cooling:


entry_id: "hvac_ac_not_cooling_001"
issue_category: "hvac"
issue_subcategory: "ac_not_cooling"
keywords: ["ac not cooling", "air conditioner", "not cold", "warm air"]
resolution_rate: 0.42
avg_time_to_resolve: 6


steps:
  - step_number: 1
    question: "What temperature is your thermostat set to, and what temperature is it showing?"
    expected_responses:
      - response_pattern: "set.*([0-9]+).*showing.*([0-9]+)"
        condition: "if set_temp - current_temp > 5"
        next_step: 2
      - response_pattern: "same|equal|matching"
        instruction: "The thermostat may not be calling for cooling. Try lowering the temperature by 5 degrees and wait 10 minutes."
        next_step: 5
  
  - step_number: 2
    question: "Is the thermostat set to 'COOL' mode (not AUTO or HEAT)?"
    expected_responses:
      - response_pattern: "yes|cool|cooling"
        next_step: 3
      - response_pattern: "no|auto|heat|off"
        instruction: "Please set the thermostat to COOL mode and lower the temperature. Wait 10 minutes and see if cold air starts coming out."
        next_step: 5
  
  - step_number: 3
    question: "When did you last change the air filter?"
    expected_responses:
      - response_pattern: "month|week|recently|new"
        next_step: 4
      - response_pattern: "long|year|never|don't know|dirty"
        instruction: "A dirty filter can block airflow. Please check your air filter - it's usually behind a vent or in the unit. If it's dirty or clogged, replace it and try again."
        result: "DISPATCH_NEEDED"
        clarification: "If you're not sure how to change the filter, we'll send a technician."
  
  - step_number: 4
    question: "Is the outdoor unit running? You should hear the fan and compressor."
    expected_responses:
      - response_pattern: "yes|running|hear"
        instruction: "The outdoor unit is running but not cooling. This likely requires refrigerant service or component repair."
        result: "DISPATCH_NEEDED"
      - response_pattern: "no|silent|not running"
        instruction: "Check if the circuit breaker for the AC unit has tripped. It's usually labeled 'AC' or 'Air Conditioner' in your electrical panel."
        next_step: 6
  
  - step_number: 5
    question: "After waiting 10 minutes, is cold air now coming from the vents?"
    expected_responses:
      - response_pattern: "yes|cold|working|better"
        result: "RESOLVED"
      - response_pattern: "no|still warm|not working"
        next_step: 4
  
  - step_number: 6
    question: "Did you find a tripped breaker? If so, flip it fully OFF then back ON."
    expected_responses:
      - response_pattern: "yes|found|tripped|reset"
        instruction: "Wait 5 minutes for the system to restart, then check if the outdoor unit is now running."
        next_step: 7
      - response_pattern: "no|not tripped|all on"
        result: "DISPATCH_NEEDED"
        clarification: "This appears to be an electrical or component issue requiring a technician."
  
  - step_number: 7
    question: "Is the outdoor unit now running and producing cold air?"
    expected_responses:
      - response_pattern: "yes|working|cold"
        result: "RESOLVED"
      - response_pattern: "no|still not working"
        result: "DISPATCH_NEEDED"
9.8.2 Emergency Detection Patterns
emergency_keywords:
  fire_related:
    keywords: ["fire", "smoke", "burning", "flames", "electrical fire"]
    action: "immediate_emergency_escalation"
    notify: ["fire_department", "on_call_manager", "property_manager"]
  
  flood_related:
    keywords: ["flood", "flooding", "water everywhere", "burst pipe", "major leak"]
    action: "immediate_escalation"
    notify: ["on_call_manager", "emergency_plumber"]
  
  gas_related:
    keywords: ["gas smell", "gas leak", "propane", "natural gas"]
    action: "immediate_emergency_escalation"
    notify: ["gas_company", "fire_department", "on_call_manager"]
  
  electrical_emergency:
    keywords: ["sparking", "electrical fire", "shock", "electrocuted"]
    action: "immediate_escalation"
    notify: ["on_call_manager", "emergency_electrician"]
  
  no_heat_winter:
    keywords: ["no heat", "freezing", "pipes freezing"]
    condition: "temperature < 40F"
    action: "urgent_escalation"
    notify: ["on_call_manager", "emergency_hvac"]
9.9 Notification Template Library
9.9.1 Resident Notification Templates
SMS Templates:


sms_templates:
  request_received:
    text: "Your maintenance request has been received. Reference: {work_order_id}. We're working on it and will update you shortly."
    max_length: 160
  
  vendor_scheduled:
    text: "Good news! {vendor_name} is scheduled for {date} at {time}. They'll contact you before arrival. Ref: {work_order_id}"
    max_length: 160
  
  vendor_en_route:
    text: "Heads up! {vendor_name} is on the way. ETA: {eta}. Please ensure access to {unit}. Ref: {work_order_id}"
    max_length: 160
  
  work_completed:
    text: "Your maintenance has been completed! Resolution: {resolution_summary}. Please confirm everything looks good by replying YES. Ref: {work_order_id}"
    max_length: 160
Email Templates:


<!-- Request Received Email Template -->
<html>
<head>
    <title>Maintenance Request Received</title>
</head>
<body style="font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto;">
    <div style="background-color: #f8f9fa; padding: 20px; border-radius: 8px;">
        <h2 style="color: #2563eb;">Maintenance Request Received</h2>
        <p>Your maintenance request has been received and assigned reference number <strong>{work_order_id}</strong>.</p>
        
        <div style="background-color: white; padding: 15px; border-radius: 6px; margin: 15px 0;">
            <h3>Request Details:</h3>
            <ul>
                <li><strong>Property:</strong> {property_address}</li>
                <li><strong>Unit:</strong> {unit_number}</li>
                <li><strong>Issue:</strong> {issue_summary}</li>
                <li><strong>Priority:</strong> {urgency}</li>
                <li><strong>Submitted:</strong> {created_at}</li>
            </ul>
        </div>
        
        <p>We're working on it and will update you shortly with next steps.</p>
        
        <div style="margin-top: 20px; padding-top: 15px; border-top: 1px solid #e5e7eb;">
            <p style="font-size: 12px; color: #6b7280;">
                Questions? Reply to this email or call {property_phone}.<br>
                Reference: {work_order_id}
            </p>
        </div>
    </div>
</body>
</html>
9.9.2 Staff Notification Templates
Slack Templates:


slack_templates:
  escalation_alert:
    text: |
      ⚠️ **ESCALATION REQUIRED**
      
      **Work Order:** {work_order_id}
      **Property:** {property_address}
      **Resident:** {resident_name} ({resident_phone})
      **Issue:** {issue_summary}
      **Reason:** {escalation_reason}
      **Time in Queue:** {time_in_queue}
      
      [View Details]({dashboard_url}) | [Claim]({claim_url})
    
    attachments:
      - color: "#ff6b35"
        fields:
          - title: "Priority"
            value: "{urgency}"
            short: true
          - title: "Category"
            value: "{issue_category}"
            short: true
    
  daily_summary:
    text: |
      📊 **Daily Maintenance Summary** - {date}
      
      **New Requests:** {new_count}
      **Completed:** {completed_count}
      **In Progress:** {in_progress_count}
      **Escalations:** {escalation_count}
      
      **Performance:**
      • Avg Response Time: {avg_response_time}
      • AI Automation Rate: {automation_rate}%
      • First-Time Fix Rate: {first_time_fix_rate}%
      
      [View Dashboard]({dashboard_url})
9.10 Vendor Communication Scripts
9.10.1 Phone Call Scripts
Vendor Dispatch Call Script:


vendor_call_script:
  greeting: "Hello, this is the AI maintenance coordinator for {property_name}. I have a {urgency} maintenance request that matches your services."
  
  job_details: |
    Here are the details:
    - Property: {property_address}
    - Unit: {unit_number}
    - Issue: {issue_description}
    - Resident Contact: {resident_name} at {resident_phone}
    - Preferred Time: {preferred_time}
  
  access_info: |
    Access information:
    {access_instructions}
  
  confirmation_request: "Can you accept this job? If yes, what's your estimated arrival time?"
  
  responses:
    accept_patterns: ["yes", "accept", "can do", "available", "on my way"]
    decline_patterns: ["no", "can't", "unavailable", "busy", "booked"]
    reschedule_patterns: ["later", "tomorrow", "different time", "can do"]
  
  closing: "Thank you. I'll send you the details via text and notify the resident. The job reference is {work_order_id}."
9.10.2 Email Communication Templates
Vendor Job Assignment Email:


<html>
<head>
    <title>New Maintenance Job Assignment</title>
</head>
<body style="font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto;">
    <div style="background-color: #f8f9fa; padding: 20px; border-radius: 8px;">
        <h2 style="color: #2563eb;">New Job Assignment</h2>
        
        <div style="background-color: #fef3c7; padding: 15px; border-radius: 6px; margin: 15px 0; border-left: 4px solid #f59e0b;">
            <h3 style="margin-top: 0; color: #92400e;">Priority: {urgency}</h3>
            <p style="margin-bottom: 0;"><strong>Job ID:</strong> {work_order_id}</p>
        </div>
        
        <div style="background-color: white; padding: 15px; border-radius: 6px; margin: 15px 0;">
            <h3>Property Information:</h3>
            <ul>
                <li><strong>Address:</strong> {property_address}</li>
                <li><strong>Unit:</strong> {unit_number}</li>
                <li><strong>Property Manager:</strong> {property_manager_name}</li>
                <li><strong>Property Phone:</strong> {property_phone}</li>
            </ul>
        </div>
        
        <div style="background-color: white; padding: 15px; border-radius: 6px; margin: 15px 0;">
            <h3>Issue Details:</h3>
            <ul>
                <li><strong>Category:</strong> {issue_category}</li>
                <li><strong>Description:</strong> {issue_description}</li>
                <li><strong>Reported:</strong> {created_at}</li>
                <li><strong>Estimated Cost:</strong> ${estimated_cost_range}</li>
            </ul>
        </div>
        
        <div style="background-color: white; padding: 15px; border-radius: 6px; margin: 15px 0;">
            <h3>Resident Contact:</h3>
            <ul>
                <li><strong>Name:</strong> {resident_name}</li>
                <li><strong>Phone:</strong> {resident_phone}</li>
                <li><strong>Preferred Contact:</strong> {resident_preferred_contact}</li>
                <li><strong>Language:</strong> {resident_language}</li>
            </ul>
        </div>
        
        <div style="background-color: #e0f2fe; padding: 15px; border-radius: 6px; margin: 15px 0;">
            <h3>Access Instructions:</h3>
            <p>{access_instructions}</p>
            {#if lockbox_code}
            <p><strong>Lockbox Code:</strong> {lockbox_code}</p>
            {/if}
        </div>
        
        <div style="text-align: center; margin: 20px 0;">
            <a href="{accept_url}" style="background-color: #10b981; color: white; padding: 12px 24px; text-decoration: none; border-radius: 6px; margin-right: 10px;">Accept Job</a>
            <a href="{decline_url}" style="background-color: #ef4444; color: white; padding: 12px 24px; text-decoration: none; border-radius: 6px;">Decline Job</a>
        </div>
        
        <div style="margin-top: 20px; padding-top: 15px; border-top: 1px solid #e5e7eb;">
            <p style="font-size: 12px; color: #6b7280;">
                Please respond within {response_deadline}.<br>
                Questions? Contact {property_manager_name} at {property_manager_phone}
            </p>
        </div>
    </div>
</body>
</html>
This comprehensive Appendices section provides essential reference material, configuration details, and implementation examples that support the AI Maintenance Coordinator system. LangGraph 1.0 is the first stable major release in the durable agent framework space —a major milestone for production-ready AI systems. After more than a year of powering agents at companies like Uber, LinkedIn, and Klarna, LangGraph is officially v1. The system leverages the latest stable versions of all core technologies to ensure reliability and performance in production environments.