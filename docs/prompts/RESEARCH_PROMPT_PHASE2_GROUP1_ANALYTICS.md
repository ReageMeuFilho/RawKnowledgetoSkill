# Research Prompt: Phase 2 Group 1 - Advanced Analytics

> **For**: AI Research Agent
> **Output**: Knowledge Document → `knowledge/analytics/KD-PHASE2-G1-advanced-analytics.md`
> **Priority**: High
> **Date**: January 2026

---

## 🎯 Research Objective

Research and document comprehensive knowledge for implementing **6 Advanced Analytics skills** that provide deep insights, forecasting, and business intelligence capabilities for property management operations.

---

## 📋 Skills to Research

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| SKILL-044 | performance-forecasting | analytics | Predictive revenue and occupancy forecasting |
| SKILL-045 | benchmarking | analytics | Competitive benchmarking across markets |
| SKILL-090 | housekeeping-performance-analytics | analytics | Cleaning staff performance metrics |
| SKILL-105 | conversation-summary-intelligence | analytics | AI-powered conversation insights and summaries |
| SKILL-043 | real-time-dashboard | analytics | Live KPI dashboards with drill-down |
| SKILL-106 | market-intelligence | analytics | Market trend analysis and insights |

---

## 🔍 Research Questions Per Skill

### SKILL-044: Performance Forecasting

**Key Questions**:
1. What ML models work best for revenue/occupancy forecasting (Prophet, ARIMA, LSTM)?
2. What features/signals improve forecast accuracy?
3. How far ahead can forecasts be reliably made?
4. How do you handle seasonality, trends, and anomalies?
5. What is the acceptable error rate (MAPE, RMSE)?
6. How do you present confidence intervals to users?

**Research Sources**:
- Facebook Prophet documentation
- PriceLabs forecasting methodology
- Beyond Pricing demand prediction
- Cornell hospitality revenue management
- Time series forecasting best practices

### SKILL-045: Benchmarking

**Key Questions**:
1. How do you define comparable properties (comp sets)?
2. What metrics are benchmarked (ADR, RevPAR, occupancy)?
3. How is market data sourced (AirDNA, STR, OTA data)?
4. What visualization works best for benchmarking dashboards?
5. How do you handle data anonymization and privacy?
6. What percentile rankings are meaningful?

**Research Sources**:
- AirDNA MarketMinder
- STR (Smith Travel Research) methodology
- Transparent Intelligence
- Key Data Dashboard
- Hotel industry benchmarking standards

### SKILL-090: Housekeeping Performance Analytics

**Key Questions**:
1. What KPIs measure cleaning staff performance?
2. How do you track time-per-clean, quality scores, issues?
3. What photo verification systems exist?
4. How do you correlate cleaning quality with guest reviews?
5. What scheduling optimization improves efficiency?
6. How do you handle multi-property cleaner assignments?

**Research Sources**:
- Breezeway operations analytics
- TurnoverBnB performance features
- Properly cleaning management
- Hospitable housekeeping features
- VRScheduler cleaner analytics

### SKILL-105: Conversation Summary Intelligence

**Key Questions**:
1. How do you summarize long guest conversation threads?
2. What NLP techniques extract key topics and sentiment?
3. How do you identify action items from conversations?
4. What privacy considerations apply to conversation analysis?
5. How do you present insights to hosts/managers?
6. What patterns predict guest satisfaction from messages?

**Research Sources**:
- OpenAI GPT summarization capabilities
- Guesty AI conversation analysis
- Hospitable message intelligence
- Customer service AI platforms (Intercom, Zendesk)
- Sentiment analysis research

### SKILL-043: Real-Time Dashboard

**Key Questions**:
1. What KPIs need real-time vs. daily refresh?
2. How do you build performant dashboards for large portfolios?
3. What visualization libraries work best (D3, Recharts, Tremor)?
4. How do you handle drill-down from portfolio to property level?
5. What alerting thresholds make sense for different metrics?
6. How do mobile dashboards differ from desktop?

**Research Sources**:
- Guesty analytics dashboard
- Hostaway reporting
- Metabase/Looker/Tableau patterns
- Dashboard UI/UX best practices
- Real-time data streaming (WebSocket)

### SKILL-106: Market Intelligence

**Key Questions**:
1. What market data sources are available (AirDNA, Transparent)?
2. How do you track market-wide trends (supply, demand, ADR)?
3. What regulatory changes affect market conditions?
4. How do you identify emerging markets or opportunities?
5. What competitive moves should be tracked?
6. How frequently should market intelligence update?

**Research Sources**:
- AirDNA market reports
- Transparent Intelligence
- AllTheRooms analytics
- Short-term rental regulation tracking
- Real estate market analysis tools

---

## 🏗️ Architecture Context

### Dependencies (From Phase 1)
- **SKILL-042**: Analytics Dashboard (base framework)
- **SKILL-060**: Audit Logging (data trail)
- **SKILL-017-019**: Task Management (operations data)

### Technology Stack
| Component | Technology | Purpose |
|-----------|------------|---------|
| Dashboards | React + Tremor/Recharts | Visualization |
| Real-time | WebSocket | Live updates |
| ML Pipeline | Python (Prophet, scikit-learn) | Forecasting |
| Data Warehouse | PostgreSQL + TimescaleDB | Historical data |
| Caching | Redis | Dashboard performance |
| BI Layer | Metabase or custom | Ad-hoc analysis |

### MCP Servers Required
```yaml
mcp_servers:
  - mcp://analytics/query
  - mcp://analytics/forecast
  - mcp://analytics/benchmark
  - mcp://dashboard/refresh
```

---

## 📄 Output Format

Create a comprehensive knowledge document with:

1. **Executive Summary**
2. **Skill-by-Skill Analysis** (6 skills)
3. **Best-in-Class Implementations**
4. **Data Architecture** - Schemas, ETL pipelines
5. **ML Model Specifications** - Algorithms, training, evaluation
6. **Dashboard Design Patterns**
7. **Performance Optimization**
8. **Competitive Comparison**
9. **Implementation Priorities**
10. **Open Questions**

**Quality Requirements**:
- Minimum 1,800 lines
- At least 25 citations/sources
- Include data schemas
- Include dashboard wireframes (mermaid)

---

## 📤 Delivery Instructions

1. Save to: `knowledge/analytics/KD-PHASE2-G1-advanced-analytics.md`
2. Update: `docs/PHASE2_SKILL_TRACKER.md`
3. Notify: Ready for Stage 2

---

**Focus**: Build insights that drive better decisions! 📊

