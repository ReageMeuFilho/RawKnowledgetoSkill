# Skill Inventory: Short-Term Rental PMS (Host OS)

> **Based on**: Host OS PRD + NEXUS Core PRD
> **Last Updated**: January 2026
> **Total Skills Identified**: 47
> **Skills Existing**: 0
> **Skills Needed**: 47

---

## 📊 Executive Summary

| Category | Skills | Priority | Status |
|----------|--------|----------|--------|
| Guest Experience | 8 | P0-P1 | NEEDED |
| Booking & Reservations | 7 | P0 | NEEDED |
| Pricing & Revenue | 6 | P1 | NEEDED |
| Operations | 9 | P0-P1 | NEEDED |
| Financial | 7 | P1-P2 | NEEDED |
| Compliance & Trust | 5 | P1 | NEEDED |
| Channel Management | 5 | P2 | NEEDED |

---

## 🎯 MVP Skills (P0 - Critical Path)

These skills are **required for launch**.

### Guest Communication & Experience

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-001 | `guest-inquiry-handler` | Respond to booking inquiries with property info, availability, pricing | Guest Experience Agent | Superhost guides, Hospitable training |
| STR-002 | `guest-message-responder` | Handle general guest messages during stay | Guest Experience Agent | PM interviews, response templates |
| STR-003 | `check-in-coordinator` | Send pre-arrival info, access codes, directions | Guest Experience Agent | Airbnb guides, PM SOPs |
| STR-004 | `issue-resolver` | Handle guest complaints and issues | Guest Experience Agent | Conflict resolution training |

### Booking & Reservations

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-005 | `availability-checker` | Check real-time availability across calendars | Polymorphic Inventory | iCal specs, channel APIs |
| STR-006 | `booking-creator` | Create new reservations with all details | Booking Management | Booking flow docs |
| STR-007 | `booking-modifier` | Handle date changes, guest count changes | Booking Management | Modification policies |
| STR-008 | `booking-cancellation-handler` | Process cancellations per policy | Booking Management | Cancellation policy docs |
| STR-009 | `instant-book-processor` | Auto-accept qualifying instant bookings | Booking Management | Instant book criteria |

### Operations - Housekeeping

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-010 | `turnover-scheduler` | Schedule cleanings based on checkout/checkin | Operations | TurnoverBnB, Breezeway |
| STR-011 | `cleaner-dispatcher` | Assign cleaners to properties | Operations | Cleaning company SOPs |
| STR-012 | `turnover-quality-checker` | Verify cleaning completion with photos | Operations | Inspection checklists |

### Operations - Maintenance

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-013 | `maintenance-classifier` | Categorize issues by urgency/type | Maintenance Agent | Maintenance triage docs |
| STR-014 | `emergency-handler` | Handle urgent issues (water, fire, security) | Maintenance Agent | Emergency protocols |
| STR-015 | `vendor-dispatcher` | Dispatch appropriate vendor for issue | Maintenance Agent | Vendor management SOPs |

---

## 🔶 Phase 1 Skills (P1 - Important)

These skills are **needed within 30 days of launch**.

### Pricing & Revenue

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-016 | `base-rate-setter` | Set and adjust base nightly rates | Revenue Agent | Pricing strategy docs |
| STR-017 | `dynamic-pricing-adjuster` | Apply demand-based pricing adjustments | Revenue Agent | PriceLabs, Beyond Pricing |
| STR-018 | `minimum-stay-optimizer` | Set minimum stay requirements | Revenue Agent | Revenue management courses |
| STR-019 | `last-minute-discounter` | Apply discounts for gap nights | Revenue Agent | Gap night strategies |

### Guest Experience - Reviews

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-020 | `review-requester` | Request reviews post-checkout | Review Management Agent | Review optimization guides |
| STR-021 | `review-responder` | Craft responses to guest reviews | Review Management Agent | Response templates, PM interviews |
| STR-022 | `negative-review-handler` | Handle negative reviews professionally | Review Management Agent | Reputation management training |

### Financial - Basic

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-023 | `guest-folio-creator` | Create itemized guest bills | Trust Accounting | Hospitality accounting |
| STR-024 | `payment-collector` | Collect and process guest payments | Trust Accounting | Payment processing docs |
| STR-025 | `payout-calculator` | Calculate owner payouts after fees | Trust Accounting | PM agreements, split rules |

### Compliance

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-026 | `guest-id-verifier` | Verify guest identity documents | Compliance | ID verification APIs, regulations |
| STR-027 | `occupancy-tax-calculator` | Calculate applicable lodging taxes | Compliance | Local tax regulations |
| STR-028 | `party-risk-assessor` | Assess booking for party risk | Compliance | Party prevention guides |

---

## 🔷 Phase 2 Skills (P2 - Enhanced)

These skills are **planned for 60-90 days post-launch**.

### Revenue Optimization

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-029 | `competitor-rate-analyzer` | Monitor competitor pricing | Revenue Agent | Comp analysis methods |
| STR-030 | `demand-forecaster` | Predict demand for pricing decisions | Revenue Agent | Forecasting models |
| STR-031 | `seasonal-strategy-planner` | Plan seasonal pricing strategies | Revenue Agent | Revenue management courses |
| STR-032 | `upsell-orchestrator` | Offer add-ons (early checkin, etc.) | Revenue Agent | Upselling strategies |

### Channel Management

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-033 | `channel-calendar-syncer` | Sync calendars across OTAs | Channel Manager | iCal, API integration docs |
| STR-034 | `channel-rate-pusher` | Push rates to all channels | Channel Manager | Channel API docs |
| STR-035 | `channel-listing-optimizer` | Optimize listings per channel | Channel Manager | Listing optimization guides |
| STR-036 | `direct-booking-handler` | Handle website direct bookings | Direct Brand | Direct booking strategies |

### Owner Relations

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-037 | `owner-statement-generator` | Generate monthly owner statements | Owner Reporting | PM accounting standards |
| STR-038 | `owner-performance-reporter` | Report property performance metrics | Owner Reporting | KPI definitions |
| STR-039 | `owner-communication-handler` | Handle owner inquiries | Owner Relations | PM communication templates |

---

## 🔹 Phase 3 Skills (P3 - Advanced)

These skills are **planned for 6+ months post-launch**.

### Advanced Financial

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-040 | `tax-report-generator` | Generate tax reports (1099, etc.) | Financial | Tax reporting requirements |
| STR-041 | `trust-account-reconciler` | Reconcile trust accounts | Trust Accounting | Trust accounting standards |
| STR-042 | `revenue-forecaster` | Forecast future revenue | Analytics | Forecasting methods |

### Advanced Operations

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-043 | `inventory-manager` | Track linens, supplies, amenities | Operations | Inventory management SOPs |
| STR-044 | `preventive-maintenance-scheduler` | Schedule preventive maintenance | Operations | PM maintenance calendars |
| STR-045 | `vendor-performance-tracker` | Track vendor performance metrics | Operations | Vendor scorecards |

### Guest Experience - Advanced

| ID | Skill Name | Description | PRD Feature | Sources Needed |
|----|------------|-------------|-------------|----------------|
| STR-046 | `local-recommendation-provider` | Provide local area recommendations | Guest Experience | Local guides, partnerships |
| STR-047 | `repeat-guest-recognizer` | Recognize and reward repeat guests | Guest Experience | Loyalty program designs |

---

## 📋 Skills by Domain

### Guest Experience (8 skills)
```
STR-001 guest-inquiry-handler          [P0] MVP
STR-002 guest-message-responder        [P0] MVP
STR-003 check-in-coordinator           [P0] MVP
STR-004 issue-resolver                 [P0] MVP
STR-020 review-requester               [P1] Phase 1
STR-021 review-responder               [P1] Phase 1
STR-022 negative-review-handler        [P1] Phase 1
STR-046 local-recommendation-provider  [P3] Phase 3
STR-047 repeat-guest-recognizer        [P3] Phase 3
```

### Booking & Reservations (5 skills)
```
STR-005 availability-checker           [P0] MVP
STR-006 booking-creator                [P0] MVP
STR-007 booking-modifier               [P0] MVP
STR-008 booking-cancellation-handler   [P0] MVP
STR-009 instant-book-processor         [P0] MVP
```

### Pricing & Revenue (7 skills)
```
STR-016 base-rate-setter               [P1] Phase 1
STR-017 dynamic-pricing-adjuster       [P1] Phase 1
STR-018 minimum-stay-optimizer         [P1] Phase 1
STR-019 last-minute-discounter         [P1] Phase 1
STR-029 competitor-rate-analyzer       [P2] Phase 2
STR-030 demand-forecaster              [P2] Phase 2
STR-031 seasonal-strategy-planner      [P2] Phase 2
STR-032 upsell-orchestrator            [P2] Phase 2
```

### Operations (9 skills)
```
STR-010 turnover-scheduler             [P0] MVP
STR-011 cleaner-dispatcher             [P0] MVP
STR-012 turnover-quality-checker       [P0] MVP
STR-013 maintenance-classifier         [P0] MVP
STR-014 emergency-handler              [P0] MVP
STR-015 vendor-dispatcher              [P0] MVP
STR-043 inventory-manager              [P3] Phase 3
STR-044 preventive-maintenance-scheduler [P3] Phase 3
STR-045 vendor-performance-tracker     [P3] Phase 3
```

### Financial (7 skills)
```
STR-023 guest-folio-creator            [P1] Phase 1
STR-024 payment-collector              [P1] Phase 1
STR-025 payout-calculator              [P1] Phase 1
STR-037 owner-statement-generator      [P2] Phase 2
STR-038 owner-performance-reporter     [P2] Phase 2
STR-040 tax-report-generator           [P3] Phase 3
STR-041 trust-account-reconciler       [P3] Phase 3
STR-042 revenue-forecaster             [P3] Phase 3
```

### Compliance (3 skills)
```
STR-026 guest-id-verifier              [P1] Phase 1
STR-027 occupancy-tax-calculator       [P1] Phase 1
STR-028 party-risk-assessor            [P1] Phase 1
```

### Channel Management (4 skills)
```
STR-033 channel-calendar-syncer        [P2] Phase 2
STR-034 channel-rate-pusher            [P2] Phase 2
STR-035 channel-listing-optimizer      [P2] Phase 2
STR-036 direct-booking-handler         [P2] Phase 2
```

### Owner Relations (3 skills)
```
STR-037 owner-statement-generator      [P2] Phase 2
STR-038 owner-performance-reporter     [P2] Phase 2
STR-039 owner-communication-handler    [P2] Phase 2
```

---

## 🎯 MVP Launch Checklist

### Must Have for Launch (15 skills)

- [ ] STR-001 guest-inquiry-handler
- [ ] STR-002 guest-message-responder
- [ ] STR-003 check-in-coordinator
- [ ] STR-004 issue-resolver
- [ ] STR-005 availability-checker
- [ ] STR-006 booking-creator
- [ ] STR-007 booking-modifier
- [ ] STR-008 booking-cancellation-handler
- [ ] STR-009 instant-book-processor
- [ ] STR-010 turnover-scheduler
- [ ] STR-011 cleaner-dispatcher
- [ ] STR-012 turnover-quality-checker
- [ ] STR-013 maintenance-classifier
- [ ] STR-014 emergency-handler
- [ ] STR-015 vendor-dispatcher

---

## 📚 Knowledge Sources to Acquire

### High Priority Sources

| Source Type | Examples | Skills Covered |
|-------------|----------|----------------|
| **Airbnb Superhost Training** | Host Academy, Help Center | Guest communication, reviews |
| **PriceLabs Documentation** | Pricing guides, webinars | Dynamic pricing, revenue |
| **TurnoverBnB/Breezeway Training** | Platform tutorials | Operations, cleaning |
| **Property Manager Interviews** | 3-5 experienced PMs | All domains, edge cases |
| **Local Regulations** | City/state STR laws | Compliance, taxes |

### Source Acquisition Priority

1. **Week 1**: Property Manager Interviews (3-5)
2. **Week 2**: Platform Documentation (Airbnb, PriceLabs, TurnoverBnB)
3. **Week 3**: Industry Training Videos (Udemy, YouTube)
4. **Week 4**: Compliance/Regulatory Documents

---

## 📈 Progress Tracking

| Phase | Skills | Target Date | Status |
|-------|--------|-------------|--------|
| MVP (P0) | 15 | TBD | Not Started |
| Phase 1 (P1) | 13 | TBD | Not Started |
| Phase 2 (P2) | 12 | TBD | Not Started |
| Phase 3 (P3) | 7 | TBD | Not Started |

---

## 🔗 Related Documents

- [Host OS PRD](../../docs/PRD_Host_OS.md)
- [NEXUS Core PRD](../../docs/PRD_NEXUS_Core.md)
- [Source Plan](./SOURCE_PLAN.md) - Knowledge sourcing details
- [Knowledge-to-Skills Pipeline](../docs/methodology/README.md)



