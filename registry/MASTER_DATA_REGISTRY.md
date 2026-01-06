# Master Data Registry: Context & Information

> **All data objects/schemas** required by skills and tools
> **Last Updated**: January 2026
> **Total Data Objects**: 0

---

## 📊 Data Categories

| Category | Objects | Description |
|----------|---------|-------------|
| `property` | 0 | Property details, amenities, rules |
| `booking` | 0 | Reservations, guests, dates |
| `user` | 0 | Hosts, guests, cleaners, vendors |
| `financial` | 0 | Payments, payouts, invoices |
| `operations` | 0 | Tasks, schedules, checklists |
| `communication` | 0 | Messages, conversations, templates |
| `analytics` | 0 | Metrics, reports, forecasts |
| `compliance` | 0 | Taxes, licenses, regulations |
| `configuration` | 0 | Settings, preferences, rules |

---

## 📋 Data Object Template

```markdown
### DATA-XXX: [object-name]

**Category**: [category]
**Table/Collection**: `[database_table_name]`

**Purpose**: [What this data represents]

**Schema**:
```sql
CREATE TABLE [table_name] (
    id UUID PRIMARY KEY,
    field1 TYPE,          -- Description
    field2 TYPE,          -- Description
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);
```

**Key Fields**:
| Field | Type | Description | Required |
|-------|------|-------------|----------|
| | | | |

**Relationships**:
- Has many: [related objects]
- Belongs to: [parent objects]

**Used By Skills**:
- STR-XXX [skill-name]

**Used By Tools**:
- TOOL-XXX [tool-name]

**Source**: [Where this data comes from]
```

---

## 🏠 Property Data

<!-- Property-related data objects -->



---

## 📅 Booking Data

<!-- Reservation-related data objects -->



---

## 👤 User Data

<!-- User/contact data objects -->



---

## 💰 Financial Data

<!-- Payment/accounting data objects -->



---

## 🔧 Operations Data

<!-- Task/schedule data objects -->



---

## 💬 Communication Data

<!-- Message/conversation data objects -->



---

## 📈 Analytics Data

<!-- Metrics/reporting data objects -->



---

## ✅ Compliance Data

<!-- Regulatory/compliance data objects -->



---

## ⚙️ Configuration Data

<!-- Settings/rules data objects -->



---

## 🔗 Data Flow Diagram

```
                    ┌─────────────┐
                    │   BOOKING   │
                    └─────────────┘
                          │
         ┌────────────────┼────────────────┐
         │                │                │
         ▼                ▼                ▼
   ┌──────────┐    ┌──────────┐    ┌──────────┐
   │ PROPERTY │    │  GUEST   │    │ PAYMENT  │
   └──────────┘    └──────────┘    └──────────┘
         │                │
         ▼                │
   ┌──────────┐           │
   │ CLEANER  │◄──────────┘
   └──────────┘
```

---

## 📈 Data Priority

| Priority | Data Objects | Reason |
|----------|--------------|--------|
| P0 | | Core entities |
| P1 | | Important context |
| P2 | | Enhanced features |
| P3 | | Nice to have |




