# RentalReady - Skill Inventory

> **Source**: `rentalready_complete_prd_original.md`
> **Extracted**: January 2026
> **Vertical**: STR + Boutique Hotels (10-1000+ properties)
> **Type**: All-in-One PMS + AI Assistant (Maia)

---

## 📊 Extraction Summary

| Category | Count | New vs Existing |
|----------|-------|-----------------|
| Skills | 58 | 9 NEW, 49 overlap (with depth) |
| Tools | 12 | 3 NEW |
| Memory Types | 6 | 1 NEW |
| Workflows | 9 | 3 NEW |

---

## 🎯 RentalReady Context

**RentalReady is the "AI-Powered All-in-One PMS for Professional STR"** with:
- **60k+ active listings**, 7k+ properties
- **~4.9/5.0 ratings** on Capterra (top 5%)
- **80%+ automation rate** for guest communications (Maia AI)
- **70% reduction in operational time**
- **10+ years French PM expertise** (European-first design)
- **Ecosystem apps** for guests, owners, staff, service providers
- **Flexible property grouping** (unique feature!)

**Target**: Professional STR operators (10-1000+ properties)

**Key Differentiators**:
- **Maia AI** with confidence-based routing (auto-send vs human review)
- **Flexible Property Grouping** by location/type/ownership (unique!)
- **Personal Account Manager** for ALL customers (not just enterprise)
- **Service Provider Ecosystem** with native mobile app + offline support
- **European-First** GDPR, multi-language, EU compliance

---

## 🆕 NEW Skills (Not in Previous PRDs)

### NEW-RR-001: Flexible Property Grouping
**Category**: operations
**Priority**: P1
**Status**: NEEDED

**Description**: 
Group properties by location, type, ownership, or any custom criterion with different rules, policies, and staff per group.

**Unique Value** (Not in any other PRD!):
- Group by geographic location (Barcelona, Paris, London)
- Group by property type (Luxury Villas, Urban Apartments)
- Group by ownership model (Owner-Managed, Managed-For-Owners)
- Different pricing rules per group
- Different check-in/out policies per group
- Different service providers per group
- Different staff assignments per group

**Use Cases**:
1. Multi-city operator with 300 properties across 5 cities
2. Mixed portfolio (villas + apartments + studios)
3. Multi-owner agency with different commission structures

**Knowledge Required**:
- KG-RR-001: Property grouping patterns

---

### NEW-RR-002: AI Confidence-Based Routing
**Category**: ai-messaging
**Priority**: P0
**Status**: NEEDED

**Description**: 
Route AI-generated messages based on confidence score (high/medium/low).

**Unique Mechanism**:
```
Maia generates reply → Confidence Score assigned:

HIGH (>90%):
  → Auto-send without human review (configurable)
  
MEDIUM (70-90%):
  → Human-in-the-loop: show "approve" button
  → Or auto-send with notification
  
LOW (<70%):
  → ALWAYS hold for human review
```

**Why Better Than Others**:
- Visito: No confidence routing
- Boom: No auto-send control
- Besty: No human-in-loop
- RentalReady: Full control over AI autonomy level

**Configuration Options**:
- Set auto-send threshold per account/property
- Select message categories for auto-respond
- Set office hours for complex messages
- Custom knowledge base upload

---

### NEW-RR-003: AI Property Quality Audit
**Category**: quality
**Priority**: P1
**Status**: NEEDED

**Description**: 
Monitor declining property quality from guest reviews and generate improvement recommendations.

**Workflow**:
1. **Review Ingestion**: Pull reviews from Airbnb, Booking, Vrbo
2. **Sentiment & Issue Extraction**: Identify complaint patterns
3. **Quality Scoring**: Aggregate into scores (Cleanliness: 4.2/5)
4. **Trend Detection**: Flag declining scores
5. **Recommendations**: Suggest improvements

**Output Dashboard Example**:
```
Property: Malibu Beach Villa
Overall Quality Score: 4.3/5 (↓0.3 vs. last month)

Category Scores:
• Cleanliness: 4.0/5 (↓0.4) ← ALERT: Declining
• Comfort: 4.5/5 (→ No change)
• Amenities: 4.6/5 (↑0.2)

Recent Complaint Themes:
1. Dirty (3 reviews): "Bathroom wasn't clean"
2. Broken Items (2 reviews): "TV remote broken"

Recommendations:
✓ Increase cleaning frequency for bathrooms
✓ Do property walkthrough; replace broken items
```

---

### NEW-RR-004: AI Review Reply Generation
**Category**: ai-messaging
**Priority**: P1
**Status**: NEEDED

**Description**: 
Auto-generate public replies to guest reviews on OTAs.

**How It Works**:
1. Review received (5-star or 1-star)
2. AI determines sentiment and themes
3. AI generates appropriate response
4. Manager reviews/edits
5. Reply posted to OTA

**Examples**:
```
5-Star Review:
"Amazing place! Beautiful views..."

AI Reply:
"Thank you so much for the lovely feedback! We're 
thrilled you enjoyed your stay..."

1-Star Review:
"Disappointed. Place was dirty, WiFi didn't work..."

AI Reply:
"We sincerely apologize for falling short of your 
expectations. Cleanliness and communication are 
our priorities..."
```

**Benefits**:
- Increases reply rate (many never reply)
- Professional, consistent tone
- Shows responsiveness to future guests

---

### NEW-RR-005: Dynamic Min-Stay Optimization
**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Auto-adjust minimum stay requirements to fill calendar gaps.

**Problem Solved**:
```
Property: 2-Bedroom Apartment
Current Min-Stay: 3 nights

Calendar:
• July 20-22: [Booked]
• July 22-24: [Available, 2 nights] → TOO SHORT!
• July 24-28: [Booked]

Without optimization: Gap stays empty
With optimization: Reduce min-stay to 2 for that window

Result: +$300 revenue from 2-night booking
```

**Similar To**: Besty's Gap Night Fill
**Improvement**: More sophisticated rule engine

---

### NEW-RR-006: Lead-Time Based Pricing
**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Set different prices based on booking advance window.

**Example Rules**:
```
Base Rate: $150/night

• 90+ days advance: +20% = $180/night (premium)
• 30-90 days: +5% = $157.50/night
• 14-30 days: Baseline = $150/night
• 0-14 days: -15% = $127.50/night (last-minute)
```

**Why Valuable**:
- Capture premium for early bookers
- Fill last-minute gaps with discounts
- Optimize revenue across booking windows

---

### NEW-RR-007: Service Provider Ecosystem
**Category**: operations
**Priority**: P0
**Status**: NEEDED

**Description**: 
Complete ecosystem for managing cleaners, maintenance, key handlers with native mobile app.

**Mobile App Features**:
- Task list view (today, tomorrow, upcoming)
- Checklist execution with timestamps
- Photo/video evidence capture
- Problem reporting with photos
- Navigation/maps integration
- In-app messaging with manager
- **Offline-first design** (works with spotty connectivity!)
- Payment tracking (unpaid, paid, disputed)

**Why Better Than Others**:
- Guesty: Basic task management
- Boom: Limited contractor features
- RentalReady: Full ecosystem with offline support

---

### NEW-RR-008: Occupancy-Based Pricing Rules
**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Automatically adjust rates based on portfolio occupancy.

**Example Rules**:
```
IF Next 30-day occupancy > 80%:
THEN Increase all unsold dates by 10%
(Protect high-demand period)

IF Next 30-day occupancy < 50%:
THEN Apply -15% discount to all dates
(Stimulate demand in slow period)
```

---

### NEW-RR-009: Multi-Office Staff Separation
**Category**: operations
**Priority**: P1
**Status**: NEEDED

**Description**: 
Large portfolio management with city managers who only see/manage their properties.

**Implementation**:
1. Create 5 property groups (one per city)
2. Assign city managers to respective groups
3. City managers only see their properties
4. Central finance has read-only access to all
5. CEO dashboard shows aggregated KPIs

**Benefits**:
- Autonomy for local teams
- Corporate policy enforcement
- Easy new city spinup
- Aggregated + per-city reporting

---

## 🔄 Feature Comparison: RentalReady vs Others

| Feature | RentalReady | Cloudbeds | Guesty | Inntelo |
|---------|-------------|-----------|--------|---------|
| **Property Grouping** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| **AI Confidence Routing** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ❌ | ⭐⭐⭐⭐ |
| **Quality Audit** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ |
| **Review Replies** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ |
| **Min-Stay Optimization** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ❌ |
| **Lead-Time Pricing** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ❌ |
| **Service Provider App** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| **Offline Support** | ⭐⭐⭐⭐⭐ | ❌ | ❌ | ❌ |
| **Multi-Office** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Forecast Accuracy** | ❌ | ⭐⭐⭐⭐⭐ (96%) | ⭐⭐⭐ | ❌ |
| **Channels** | ⭐⭐⭐ (major) | ⭐⭐⭐⭐⭐ (300+) | ⭐⭐⭐⭐⭐ (200+) | ⭐⭐ |

---

## 📊 Maia AI Deep Dive

**Maia AI vs Other Guest Messaging AI**:

| Aspect | Maia (RentalReady) | Engage (Cloudbeds) | Visito | Besty |
|--------|--------------------|--------------------|--------|-------|
| Confidence Routing | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ |
| Human-in-Loop | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| Auto-Send Control | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| Learning from Edits | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ |
| Office Hours | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ |
| Template Override | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |

**Maia Confidence Levels**:
```
┌─────────────────────────────────────────────────────────────┐
│                    MAIA AI ROUTING                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  INCOMING MESSAGE                                           │
│         ↓                                                   │
│  [Intent Analysis + Sentiment + Context]                    │
│         ↓                                                   │
│  GENERATE RESPONSE + CONFIDENCE SCORE                       │
│         ↓                                                   │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ HIGH (>90%)     → Auto-send (if enabled)            │   │
│  │ MEDIUM (70-90%) → Human review OR auto+notify       │   │
│  │ LOW (<70%)      → ALWAYS human review               │   │
│  └─────────────────────────────────────────────────────┘   │
│         ↓                                                   │
│  HUMAN EDITS → Feed back into learning                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔧 NEW Tools Required

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-RR-001 | optimize_min_stay | Calculate optimal min-stay for gaps | BUILD |
| TOOL-RR-002 | calculate_lead_time_price | Price by booking window | BUILD |
| TOOL-RR-003 | analyze_review_quality | Extract quality scores from reviews | BUILD/BUY |

---

## 💾 NEW Memory/Data Requirements

| ID | Memory Type | Description | Retention |
|----|-------------|-------------|-----------|
| MEM-RR-001 | AI Response Edits | Manager edits to Maia responses | Permanent (learning) |

---

## 🔀 NEW Workflows from RentalReady

| ID | Workflow | Trigger | Steps |
|----|----------|---------|-------|
| WF-RR-001 | AI Confidence Routing | Message received | Analyze → Score → Route → Send/Hold |
| WF-RR-002 | Quality Audit | Review received | Ingest → Analyze → Score → Recommend |
| WF-RR-003 | Min-Stay Optimization | Calendar gap detected | Detect → Calculate → Apply → Monitor |

---

## 📋 Knowledge Gaps from RentalReady

| ID | Knowledge Needed | Skills Blocked | Priority |
|----|------------------|----------------|----------|
| KG-RR-001 | Property grouping patterns | Flexible Grouping | MEDIUM |
| KG-RR-002 | AI confidence scoring | Confidence Routing | HIGH |
| KG-RR-003 | Review quality extraction | Quality Audit | MEDIUM |
| KG-RR-004 | Min-stay optimization algorithms | Gap Fill | LOW |
| KG-RR-005 | Lead-time pricing strategies | Lead-Time Pricing | LOW |

---

## 🏆 What RentalReady Adds to Our Solution

**ADOPT (Critical)**:
1. **AI Confidence-Based Routing** - Most sophisticated AI control
2. **Flexible Property Grouping** - Unique feature, no competitor has it
3. **Service Provider Ecosystem** - Best mobile app with offline support

**ADOPT (Valuable)**:
1. **AI Property Quality Audit** - Reviews → Quality Score → Recommendations
2. **AI Review Reply Generation** - Auto-reply to guest reviews
3. **Dynamic Min-Stay Optimization** - Fill calendar gaps
4. **Lead-Time Based Pricing** - Advanced pricing control

**LEARN FROM**:
1. **Personal Account Manager Model** - Business model differentiation
2. **European-First Design** - GDPR, localization approach
3. **Offline-First Mobile** - Field worker reliability

---

## 📊 Strategic Positioning Update (9 Competitors)

| Dimension | RentalReady | Cloudbeds | Inntelo | Boom | Guesty |
|-----------|-------------|-----------|---------|------|--------|
| **Type** | All-in-One | Unified PMS | Hotel AI | AiPMS | STR PMS |
| **AI Control** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| **Grouping** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| **Contractor Mgmt** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| **Quality Audit** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ |
| **Offline** | ⭐⭐⭐⭐⭐ | ❌ | ❌ | ❌ | ❌ |
| **Forecast** | ❌ | ⭐⭐⭐⭐⭐ | ❌ | ⭐⭐⭐ | ⭐⭐⭐ |

**Bottom Line**: RentalReady provides **AI confidence control**, **flexible property grouping**, and **service provider ecosystem** that no other competitor matches for operational control.

---

## 🎯 Complete Best-of-Breed Synthesis (9 Competitors)

| Feature | Best Source | Why |
|---------|-------------|-----|
| **STR Operations** | Guesty | 67 skills |
| **Foundation AI** | Cloudbeds | Signals, hospitality-specific |
| **Demand Forecast** | Cloudbeds | 96% @ 180 days |
| **Channels** | Cloudbeds | 300+ |
| **AI Confidence Routing** | **RentalReady** | High/Medium/Low + human-in-loop |
| **Property Grouping** | **RentalReady** | Unique! Location/type/ownership |
| **Service Provider App** | **RentalReady** | Offline-first, full featured |
| **Quality Audit** | **RentalReady** | Reviews → Scores → Recommendations |
| **Review Replies** | **RentalReady** | Auto-generate public responses |
| **Min-Stay Optimization** | **RentalReady** + Besty | Fill gaps dynamically |
| **Voice AI** | Boom | 24/7 phone, BAM |
| **CDP** | Inntelo | Full stack |
| **Multi-Agent** | Inntelo | 5 agents |
| **Revenue Upsells** | Besty | Psychology |
| **Digital Key** | Mews | Apple Wallet |
| **Languages** | Visito | 100+ |
| **No-Code** | Visito | 2-min setup |

