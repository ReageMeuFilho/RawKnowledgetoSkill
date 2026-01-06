# Lodgify - Skill Inventory

> **Source**: LODGIFY (v2.0)PRD.md
> **Analysis Date**: January 2026
> **Focus**: Website-First Platform for Small Operators (1-50 properties)

---

## 🎯 **CRITICAL: Lodgify Fills the SMB Gap**

While Guesty/Hostaway target enterprise (50-1000+), Lodgify serves:
- **1-50 properties** (sweet spot: 1-30)
- **$16/month starting price** (cheapest in market)
- **Website-first** (not PMS-first like competitors)
- **Non-technical users** (drag-and-drop everything)

This is the **entry market** that enterprise platforms explicitly don't serve.

---

## Executive Summary

| Metric | Count |
|--------|-------|
| **Total Features Analyzed** | 45+ |
| **New Unique Skills** | 6 |
| **Overlapping with Registry** | 35+ |
| **Knowledge Gaps Identified** | 5 |

---

## 🆕 Unique Skills (New to Registry)

### 1. SKILL-187: website-first-architecture

**Priority**: P1
**Category**: platform-design

**Description**: 
Platform designed as website builder first, with PMS layered on top (inverse of traditional PMS platforms).

**Philosophy**:
- Website + booking engine = primary value proposition
- Channel manager = supporting feature
- PMS = basic, sufficient for small portfolios
- Accounting = minimal (export to external)

**Key Differentiator**: Most competitors are PMS-first; Lodgify is **website-first**.

**Strategic Insight**: For direct-booking focused operators, this makes sense. They want brand presence first, PMS features second.

---

### 2. SKILL-188: drag-drop-website-builder

**Priority**: P1
**Category**: direct-booking

**Description**: 
Visual drag-and-drop website builder for non-technical users to create professional vacation rental sites.

**Features**:
- Visual section editor (no code required)
- Industry-specific templates (VR optimized)
- Mobile responsive + SEO-ready
- Custom branding (colors, fonts, logos)
- Custom domains with SSL included
- Built-in booking engine integration

**Key Differentiator**: More advanced than Hostaway's "basic" website builder, simpler than custom development.

---

### 3. SKILL-189: embeddable-booking-widgets

**Priority**: P2
**Category**: direct-booking

**Description**: 
External booking widgets that can be embedded into any existing website.

**Use Cases**:
- Add booking to existing WordPress/Squarespace site
- Embed in property-specific landing pages
- Add to blog or content sites
- Integration with custom-built sites

**Features**:
- Search widget (date picker, property filter)
- Property card widgets
- Availability calendar widget
- Quote/booking widgets

**Key Differentiator**: Don't need to use Lodgify's website - just the booking engine.

---

### 4. SKILL-190: google-vacation-rentals-integration

**Priority**: P2
**Category**: distribution

**Description**: 
Direct integration with Google Vacation Rentals for search exposure (on higher plans).

**Benefits**:
- Properties appear in Google Search
- Google Maps integration
- Direct booking from Google
- Reduced OTA dependency

**Key Differentiator**: Direct Google VR integration at SMB pricing.

---

### 5. SKILL-191: booking-fee-pricing-model

**Priority**: P2
**Category**: commercial

**Description**: 
Hybrid pricing with 1.9% booking fee on lower tiers, fee-free on higher tiers.

**Model**:
- **Starter**: $16/month + 1.9% per booking
- **Professional**: $40/month, no fees
- **Ultimate**: $59/month, no fees

**Strategic Insight**: Low entry barrier but incentivizes upgrade as volume grows.

---

### 6. SKILL-192: owner-statement-strategies

**Priority**: P1
**Category**: owner-management

**Description**: 
Configurable "strategies" for owner statements defining fee/tax allocation and revenue splits.

**Features**:
- Create reusable statement templates
- Define which fees/taxes apply
- Configure revenue split rules
- Monthly/quarterly statement generation
- Export or email directly to owners

**Key Differentiator**: More structured than ad-hoc statements, but simpler than trust accounting.

---

## 🔄 Overlapping Skills (Lodgify Perspective)

| Existing Skill | Lodgify Version | Comparison |
|----------------|-----------------|------------|
| SKILL-006: channel-management | Basic (60+ channels) | Simpler than Guesty |
| SKILL-007: direct-booking | **ADVANCED** | Best-in-class for SMB |
| SKILL-028: owner-statements | With strategies | Better than basic |
| SKILL-XXX: guest-messaging | Basic templates | Weaker than AI platforms |
| SKILL-XXX: pricing | Add-on (0.8%) | Not built-in |
| SKILL-XXX: task-management | Basic (2025) | New feature |

---

## 🏆 Best-in-Class Features

| Feature | Why Best | For Whom |
|---------|----------|----------|
| **Website Builder** | Most advanced drag-drop | Non-technical hosts |
| **Entry Price** | $16/month lowest | Budget-conscious |
| **Time to Launch** | 1-2 weeks | Quick starters |
| **Ease of Use** | Easiest in category | Solo hosts |
| **Direct Booking Focus** | Primary value prop | OTA-tired hosts |

---

## 📊 Market Positioning

### Where Lodgify Wins

| Segment | Why Lodgify |
|---------|-------------|
| 1-5 properties | Simplest, cheapest |
| Direct-booking focus | Best website builder |
| Non-technical | No code needed |
| Budget-conscious | Lowest entry price |
| Brand-focused | Best templates |

### Where Lodgify Loses

| Segment | Better Alternative |
|---------|-------------------|
| 50+ properties | Hostaway/Guesty |
| Complex accounting | OwnerRez/Hostaway |
| AI automation | Hospitable |
| Enterprise scale | Guesty |
| Multi-owner trust | Hostaway |

---

## 📈 Architectural Insights

### Lodgify Architecture Pattern
```
┌─────────────────────────────────────────────────────────────────┐
│                      LODGIFY PLATFORM                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   ┌──────────────────────────────────────────────────────────┐  │
│   │              WEBSITE BUILDER (Primary)                    │  │
│   │  ┌────────────┐ ┌────────────┐ ┌────────────┐            │  │
│   │  │ Templates  │ │ Drag-Drop  │ │ Branding   │            │  │
│   │  │ (VR-opt)   │ │ Editor     │ │ (domain,   │            │  │
│   │  │            │ │            │ │ SSL, logo) │            │  │
│   │  └────────────┘ └────────────┘ └────────────┘            │  │
│   └──────────────────────────────────────────────────────────┘  │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │                   BOOKING ENGINE                           │ │
│   │  ┌────────────┐ ┌────────────┐ ┌────────────┐             │ │
│   │  │ Search     │ │ Checkout   │ │ Widgets    │             │ │
│   │  │ + Filters  │ │ + Payments │ │ (embed)    │             │ │
│   │  └────────────┘ └────────────┘ └────────────┘             │ │
│   └───────────────────────────────────────────────────────────┘ │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │              BASIC PMS (Supporting)                        │ │
│   │  Calendar │ Reservations │ Messaging │ Owner Statements   │ │
│   └───────────────────────────────────────────────────────────┘ │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │              CHANNEL MANAGER (60+ channels)                │ │
│   └───────────────────────────────────────────────────────────┘ │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Key Insight for Our Platform

Lodgify validates that **different market segments need different architectures**:

| Segment | Primary Need | Secondary Need |
|---------|-------------|----------------|
| SMB (1-50) | Website + brand | Basic PMS |
| Mid-market (50-200) | PMS + automation | Distribution |
| Enterprise (200+) | Scale + compliance | AI + analytics |

We should support **multiple entry points** - not force enterprise complexity on solo hosts.

---

## 🎯 Strategic Implications

### What Lodgify Teaches Us

1. **Website-first is valid** for direct-booking focused operators
2. **Simplicity wins** at SMB scale (1-50 properties)
3. **Low entry price** captures market (then upsell)
4. **Booking widgets** expand reach beyond platform

### Our Competitive Response

| Lodgify Strength | Our Counter |
|------------------|-------------|
| Website builder | Open-source templates + AI generation |
| $16/month entry | Free tier for <5 properties? |
| Simplicity | Guided onboarding + smart defaults |
| Embeddable widgets | MCP-based booking widgets |

---

## 📊 Pricing Comparison

| Properties | Lodgify Starter | Lodgify Pro | Hostaway | Guesty |
|------------|-----------------|-------------|----------|--------|
| 1 | $16 + 1.9% | $40 | ~$20-40 | Custom |
| 5 | $36 + 1.9% | $110 | ~$100-200 | Custom |
| 10 | $52 + 1.9% | $155 | ~$200-500 | Custom |
| 50 | ~$80 + 1.9% | $400+ | ~$750-1250 | Custom |
| 100 | $102 + 1.9% | $813 | $2500+ | Custom |

**Insight**: Lodgify is 3-5x cheaper at SMB scale.

---

## Next Steps

1. **Document website builder patterns** - What makes Lodgify's builder good?
2. **Widget architecture** - How to embed booking in any site?
3. **Statement strategy templates** - Reusable owner statement configs
4. **SMB onboarding flow** - How to make enterprise features optional?


