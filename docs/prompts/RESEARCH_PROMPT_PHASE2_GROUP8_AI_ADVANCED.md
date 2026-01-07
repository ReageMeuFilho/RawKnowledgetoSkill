# Research Prompt: Phase 2 Group 8 - AI Advanced

> **For**: AI Research Agent
> **Output**: Knowledge Document → `knowledge/agentic/KD-PHASE2-G8-ai-advanced.md`
> **Priority**: High (Differentiation)
> **Date**: January 2026

---

## 🎯 Research Objective

Research and document comprehensive knowledge for implementing **5 AI Advanced skills** that leverage cutting-edge AI capabilities for predictive intelligence, anomaly detection, and self-optimization.

---

## 📋 Skills to Research

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| SKILL-112 | causal-ai-understanding | agentic | Causal inference for decision support |
| SKILL-128 | predictive-maintenance-ai | agentic | Predictive maintenance scheduling |
| SKILL-129 | churn-prediction | agentic | Guest/owner churn prediction |
| SKILL-130 | anomaly-detection | agentic | Anomaly detection in bookings/operations |
| SKILL-131 | auto-optimization | agentic | Self-optimizing AI parameters |

---

## 🔍 Research Questions Per Skill

### SKILL-112: Causal AI Understanding

**Key Questions**:
1. How does causal inference differ from correlation-based ML?
2. What causal models apply to STR (pricing → bookings, reviews → revenue)?
3. How do you build causal graphs for property management?
4. What interventions can be tested with causal AI?
5. How do you explain causal insights to non-technical users?
6. What tools support causal AI (DoWhy, CausalML)?

**Research Sources**:
- DoWhy library documentation
- Microsoft CausalML
- Judea Pearl's causal inference work
- Causal AI in business applications
- A/B testing vs. causal inference
- Revenue management causal models

### SKILL-128: Predictive Maintenance AI

**Key Questions**:
1. What signals predict equipment failures (IoT, history, age)?
2. What ML models work for maintenance prediction?
3. How do you balance false positives vs. missed failures?
4. What data collection infrastructure is needed?
5. How do you integrate with work order systems?
6. What ROI can predictive maintenance deliver?

**Research Sources**:
- Industrial IoT predictive maintenance
- Building management systems
- HVAC failure prediction research
- Appliance lifetime modeling
- Vendoroo maintenance intelligence
- Property maintenance ML research

### SKILL-129: Churn Prediction

**Key Questions**:
1. What signals indicate guest churn risk (booking patterns, complaints)?
2. What signals indicate owner/property churn (occupancy, satisfaction)?
3. What ML models work best for churn (logistic regression, XGBoost)?
4. What retention actions work for different churn risks?
5. How do you balance prediction confidence vs. intervention cost?
6. What is the economic value of prevented churn?

**Research Sources**:
- Subscription churn prediction literature
- Hotel guest loyalty research
- Property management retention
- Customer lifetime value models
- Churn prevention strategies
- ML churn prediction tutorials

### SKILL-130: Anomaly Detection

**Key Questions**:
1. What anomalies matter in STR (unusual bookings, pricing errors, fraudulent guests)?
2. What algorithms detect anomalies (isolation forest, autoencoders)?
3. How do you reduce false positive noise?
4. What real-time vs. batch detection is needed?
5. How do you handle alert fatigue?
6. What actions trigger on anomaly detection?

**Research Sources**:
- Anomaly detection algorithms (PyOD)
- Fraud detection in hospitality
- Time series anomaly detection
- Booking pattern analysis
- Financial transaction monitoring
- Operational anomaly research

### SKILL-131: Auto-Optimization

**Key Questions**:
1. What parameters should self-optimize (pricing, response timing, messaging)?
2. What optimization algorithms work (Bayesian, reinforcement learning)?
3. How do you ensure safety constraints during optimization?
4. What human oversight is needed for auto-optimization?
5. How do you measure optimization success?
6. What explainability is required for optimized decisions?

**Research Sources**:
- Bayesian optimization for hyperparameters
- Multi-armed bandit algorithms
- Reinforcement learning for pricing
- AutoML approaches
- A/B testing automation
- Revenue management optimization

---

## 🏗️ Architecture Context

### Dependencies (From MVP)
- **SKILL-261-268**: AI Workforce Architecture (agent foundation)
- **SKILL-270-272**: Maintenance Brain (predictive base)
- **SKILL-101-103**: HLP Pricing (optimization target)

### Technology Stack
| Component | Technology | Purpose |
|-----------|------------|---------|
| Causal Inference | DoWhy, CausalML | Causal models |
| ML Pipeline | scikit-learn, XGBoost | Prediction |
| Time Series | Prophet, statsmodels | Forecasting |
| Deep Learning | PyTorch | Autoencoders |
| Optimization | Optuna, Ray Tune | Parameter tuning |
| Streaming | Redpanda | Real-time data |

### MCP Servers Required
```yaml
mcp_servers:
  - mcp://ai/predict
  - mcp://ai/optimize
  - mcp://ai/detect-anomaly
  - mcp://ai/explain
  - mcp://maintenance/predict
```

### EU AI Act Considerations
Reference: `knowledge/infrastructure/KD-PRODUCTION-INFRASTRUCTURE-FINAL.md`
- AI transparency requirements
- Human oversight for automated decisions
- Documentation and logging

---

## 📄 Output Format

Create a comprehensive knowledge document with:

1. **Executive Summary**
2. **Skill-by-Skill Analysis** (5 skills)
3. **Causal AI Framework** - Graphs, interventions, tools
4. **Predictive Maintenance Pipeline** - Data, models, actions
5. **Churn Prediction System** - Features, models, retention
6. **Anomaly Detection Architecture** - Real-time, batch
7. **Auto-Optimization Design** - Algorithms, safety, oversight
8. **ML Ops Requirements** - Training, monitoring, retraining
9. **Compliance Considerations** - Explainability, EU AI Act
10. **Open Questions**

**Quality Requirements**:
- Minimum 2,000 lines
- At least 30 citations/sources
- Include ML pipeline diagrams
- Include causal graph examples

---

## 📤 Delivery Instructions

1. Save to: `knowledge/agentic/KD-PHASE2-G8-ai-advanced.md`
2. Update: `docs/PHASE2_SKILL_TRACKER.md`
3. Notify: Ready for Stage 2

---

**Focus**: Build AI that learns and improves itself! 🤖

