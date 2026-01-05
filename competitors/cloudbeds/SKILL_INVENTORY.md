# Cloudbeds Hospitality Platform - Skill Inventory

> **Source**: `cloudbeds_hospitality_prd_original.md`
> **Extracted**: January 2026
> **Vertical**: Unified Hospitality Platform (Hotels 20-500 rooms)
> **Type**: Full-Stack PMS + Foundation AI (Signals)

---

## 📊 Extraction Summary

| Category | Count | New vs Existing |
|----------|-------|-----------------|
| Skills | 52 | 6 NEW, 46 overlap (with DEPTH) |
| Tools | 8 | 2 NEW |
| Memory Types | 5 | 1 NEW |
| Workflows | 7 | 2 NEW |

---

## 🎯 Cloudbeds Context

**Cloudbeds is the "Unified AI-Powered Hospitality Platform"** with:
- **31,000+ hotels** globally (LARGEST installed base!)
- **150+ countries** coverage
- **96%+ demand forecasting accuracy** (180 days out - BEST!)
- **Signals AI** - Hospitality-specific foundation model
- **Engage AI** - Voice + text concierge
- **300+ channel integrations** (MOST!)
- **4 billion data points/hour** processing
- **13+ years** of training data

**Target**: Independent hotels, hostels, B&Bs, boutique properties

**Key Differentiator**:
- **Cloudbeds** = Unified platform + Foundation AI (largest scale)
- **Inntelo** = AI-native for hotels (CDP focus)
- **Boom** = AiPMS for STR (BAM)
- **Visito** = No-code SMB (accessibility)

---

## 🆕 NEW Skills (Not in Previous PRDs)

### NEW-CB-001: Signals Foundation AI Model
**Category**: ai-foundation
**Priority**: P0
**Status**: NEEDED

**Description**: 
Hospitality-specific foundation AI trained on 13+ years of booking data from 31,000+ hotels.

**Unique Capabilities**:
- **96%+ demand forecasting accuracy** (180 days out)
- **Causal AI** - understands cause-and-effect (not just correlations)
- **Time Surface Technology** - proprietary 2D analysis of correlated days
- **4+ billion data points** processed per hour
- **Continuous learning** - retrains weekly with new data
- **Multi-task** - forecasting, pricing, segmentation, marketing

**What Makes It Different**:
- Trained ONLY on hospitality data (vs ChatGPT with 0.004%)
- Models true cause-and-effect (competitor rate → booking change)
- 13+ years of real booking signals

**Knowledge Required**:
- KG-CB-001: Foundation AI architecture

---

### NEW-CB-002: Time Surface Technology
**Category**: ai-foundation
**Priority**: P1
**Status**: NEEDED

**Description**: 
Proprietary "time surface of booking data" that analyzes correlated days in 2D for higher forecasting accuracy.

**Unique Capabilities**:
- 2D analysis of booking patterns
- Correlated day detection
- Seasonal pattern recognition
- Event impact modeling
- Higher accuracy than traditional time series

---

### NEW-CB-003: 180-Day Demand Forecasting
**Category**: pricing
**Priority**: P0
**Status**: NEEDED

**Description**: 
Predict booking pace and demand for the next 180 days with 96%+ accuracy.

**Comparison**:
| Platform | Forecast Horizon | Accuracy |
|----------|------------------|----------|
| **Cloudbeds** | **180 days** | **96%+** |
| Mews (Atomize) | 90 days | 85% |
| Traditional RMS | 30-60 days | 50-70% |

**Unique Capabilities**:
- Demand peaks and troughs identification
- ADR potential forecasting
- Segment-specific demand (leisure, business, events)
- Emerging demand driver detection
- Weekly retraining for accuracy

---

### NEW-CB-004: 300+ Channel Distribution
**Category**: distribution
**Priority**: P1
**Status**: NEEDED

**Description**: 
Most comprehensive channel distribution network with real-time sync.

**Channel Count Comparison**:
| Platform | Channels |
|----------|----------|
| **Cloudbeds** | **300+** |
| Guesty | 200+ |
| Mews | 150+ |
| Boom | 100+ |

**Unique Capabilities**:
- Real-time sync (<5 min delay)
- Zero commission for all channels
- Overbooking prevention 99.99%
- Rate rules by channel
- Metasearch (Google Hotel Ads, Kayak)

---

### NEW-CB-005: Event Impact Analysis
**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Predict booking surge from local events (concerts, conferences, sports).

**Unique Capabilities**:
- Identify events impacting bookings
- Quantify expected demand increase
- Recommend rate adjustments
- Seasonal pattern overlay
- Weather impact correlation

---

### NEW-CB-006: Marketplace with 200+ Integrations
**Category**: integrations
**Priority**: P1
**Status**: NEEDED

**Description**: 
Pre-built integration marketplace with 200+ partners.

**Categories**:
- Accounting (QuickBooks, Xero, Sage, SAP)
- Housekeeping (Zenvie, Alice, RoomChecking)
- Guest Experience (Visito, Inntelo)
- Revenue (TripAdvisor, Google Hotel Ads)
- CRM (Mailchimp, HubSpot, Salesforce)
- Smart locks and digital keys

---

## 🔄 Skills Overlapping with Other PRDs

### Feature Comparison Matrix

| Feature | Cloudbeds | Inntelo | Boom | Guesty | Winner |
|---------|-----------|---------|------|--------|--------|
| **Hotels Scale** | 31,000+ | 100+ | 5,000+ | 25,000+ | **Cloudbeds** |
| **Forecast Accuracy** | 96% | N/A | N/A | N/A | **Cloudbeds** |
| **Forecast Horizon** | 180 days | N/A | 90 days | 30 days | **Cloudbeds** |
| **Channels** | 300+ | 10+ | 50+ | 200+ | **Cloudbeds** |
| **CDP** | Good | ⭐⭐⭐⭐⭐ | Basic | Good | Inntelo |
| **Multi-Agent** | No | ⭐⭐⭐⭐⭐ | BAM | No | Inntelo |
| **Languages** | 5+ | 40+ | 5+ | 10+ | Visito (100+) |
| **Voice AI** | Engage | Phone | Full | No | Boom |
| **Revenue Psychology** | Basic | Good | Basic | Basic | Besty |

### Where Cloudbeds Excels

1. **Scale** - 31,000+ hotels (most)
2. **Forecast Accuracy** - 96% at 180 days (best)
3. **Channel Distribution** - 300+ channels (most)
4. **Foundation AI** - Hospitality-specific (not generic LLM)
5. **Marketplace** - 200+ pre-built integrations

### Where Others Excel

1. **Inntelo** - CDP, Multi-Agent, Cross-Department
2. **Boom** - Voice AI depth, BAM architecture
3. **Besty** - Revenue psychology (gap nights)
4. **Visito** - 100+ languages, no-code
5. **Mews** - Digital key, Apple Wallet

---

## 📊 Signals AI Deep Dive

**Traditional RMS vs. Signals**:

| Aspect | Traditional | Signals |
|--------|-------------|---------|
| Data | Property only | 31,000+ hotels |
| Training | Manual rules | ML continuous |
| Horizon | 30-60 days | 180 days |
| Accuracy | 50-70% | 96%+ |
| Causality | Correlation | True cause-effect |
| Updates | Quarterly | Weekly |

**Signals Capabilities**:

```
┌─────────────────────────────────────────────────────────────┐
│                    SIGNALS FOUNDATION AI                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  INPUT (4B data points/hour)                                │
│  ├── 31,000+ hotel booking data                             │
│  ├── Competitor rates                                        │
│  ├── Events calendar                                         │
│  ├── Weather data                                            │
│  └── Economic indicators                                     │
│                                                             │
│  PROCESSING                                                  │
│  ├── Time Surface Technology (2D analysis)                   │
│  ├── Causal AI (cause-effect modeling)                       │
│  └── Continuous learning (weekly retrain)                    │
│                                                             │
│  OUTPUT                                                      │
│  ├── 180-day demand forecast (96%+)                          │
│  ├── Rate recommendations                                    │
│  ├── Guest segmentation                                      │
│  ├── Churn prediction                                        │
│  └── Marketing optimization                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔧 NEW Tools Required

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-CB-001 | forecast_demand_180 | 180-day demand forecast | BUILD (core IP) |
| TOOL-CB-002 | analyze_event_impact | Event impact on bookings | BUILD |

---

## 💾 NEW Memory/Data Requirements

| ID | Memory Type | Description | Retention |
|----|-------------|-------------|-----------|
| MEM-CB-001 | Signals Training Data | 13+ years booking history | Permanent |

---

## 🔀 NEW Workflows from Cloudbeds

| ID | Workflow | Trigger | Steps |
|----|----------|---------|-------|
| WF-CB-001 | Demand Forecast | Daily | Ingest → Analyze → Forecast → Recommend |
| WF-CB-002 | Event Impact | Event detected | Identify → Quantify → Price → Monitor |

---

## 📋 Knowledge Gaps from Cloudbeds

| ID | Knowledge Needed | Skills Blocked | Priority |
|----|------------------|----------------|----------|
| KG-CB-001 | Foundation AI architecture | Signals Model | HIGH |
| KG-CB-002 | Time Surface Technology | Demand Forecast | HIGH |
| KG-CB-003 | Causal AI implementation | Cause-Effect | MEDIUM |
| KG-CB-004 | Event data sources | Event Impact | LOW |

---

## 🏆 What Cloudbeds Adds to Our Solution

**ADOPT (Critical)**:
1. **Signals-style Foundation AI** - Hospitality-specific, not generic LLM
2. **96% Demand Forecasting** - 180-day horizon
3. **300+ Channel Distribution** - Comprehensive reach

**ADOPT (Valuable)**:
1. **Event Impact Analysis** - Predict booking surges
2. **Time Surface Technology** - Better pattern detection
3. **Marketplace Model** - 200+ pre-built integrations

**CONSIDER**:
1. **Causal AI** - Advanced, requires significant ML expertise

---

## 📊 Strategic Positioning Update (8 Competitors)

| Dimension | Cloudbeds | Inntelo | Boom | Besty | Visito | Guesty |
|-----------|-----------|---------|------|-------|--------|--------|
| **Type** | Unified PMS | Hotel AI | AiPMS | AI Layer | No-Code | STR PMS |
| **Scale** | ⭐⭐⭐⭐⭐ (31K) | ⭐⭐ (100) | ⭐⭐⭐⭐ (5K) | N/A | N/A | ⭐⭐⭐⭐⭐ (25K) |
| **Forecast** | ⭐⭐⭐⭐⭐ (96%) | N/A | ⭐⭐⭐ | N/A | N/A | ⭐⭐⭐ |
| **Channels** | ⭐⭐⭐⭐⭐ (300+) | ⭐⭐ | ⭐⭐⭐ (50) | N/A | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ (200+) |
| **CDP** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ | ❌ | ⭐⭐ | ⭐⭐⭐ |
| **Languages** | ⭐⭐⭐ (5+) | ⭐⭐⭐⭐ (40+) | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ (100+) | ⭐⭐⭐ |
| **Voice AI** | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ❌ | ⭐⭐⭐⭐ | ❌ |

**Bottom Line**: Cloudbeds provides **Foundation AI patterns**, **96% demand forecasting**, and **300+ channel distribution** that no other competitor matches at scale.

---

## 🎯 Complete Best-of-Breed Synthesis (8 Competitors)

| Feature | Best Source | Why |
|---------|-------------|-----|
| **STR Operations** | Guesty | 67 skills |
| **Foundation AI** | **Cloudbeds** | Signals, hospitality-specific |
| **Demand Forecast** | **Cloudbeds** | 96% @ 180 days |
| **Channels** | **Cloudbeds** | 300+ |
| **Event Impact** | **Cloudbeds** | Automatic detection |
| **Voice AI** | Boom | 24/7 phone, BAM |
| **CDP** | Inntelo | Full stack |
| **Multi-Agent** | Inntelo | 5 agents |
| **Revenue Upsells** | Besty | Psychology |
| **Digital Key** | Mews | Apple Wallet |
| **Languages** | Visito | 100+ |
| **No-Code** | Visito | 2-min setup |
| **Knowledge Gaps** | Visito | Auto-detection |



