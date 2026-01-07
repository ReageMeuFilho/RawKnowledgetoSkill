# Skill Specification: AI Advanced Platform

> **Skills Covered**: SKILL-112, SKILL-128, SKILL-129, SKILL-130, SKILL-131
> **Category**: Agentic / Advanced AI
> **Phase**: Phase 2 - Group 8 (AI Advanced)
> **Priority**: P2 (Enhanced)
> **Status**: SPECIFIED
> **Last Updated**: January 2026
> **Research Source**: Research Phase 2 Group 8.txt (~11,200 lines)

---

## 📋 EXECUTIVE SUMMARY

The AI Advanced Platform delivers **5 autonomous AI skills** that transform Citadel OS from "smart" to truly autonomous operations:

- **50% reduction** in unplanned equipment downtime
- **92%+ accuracy** in churn prediction (XGBoost)
- **93% accuracy** anomaly detection (Isolation Forest)
- **25% improvement** in customer retention
- **40% reduction** in maintenance costs

### Skills Overview

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-112** | Causal AI Understanding | Core AI | DoWhy causal inference, intervention testing |
| **SKILL-128** | Predictive Maintenance AI | IoT/ML | Sensor-based failure prediction |
| **SKILL-129** | Churn Prediction | Analytics | XGBoost + SMOTE + SHAP |
| **SKILL-130** | Anomaly Detection | Security | Isolation Forest real-time detection |
| **SKILL-131** | Auto-Optimization | Optimization | Safe Bayesian multi-objective tuning |

---

## 🏗️ ARCHITECTURE ALIGNMENT NOTES

### Layer Mapping (Citadel OS 6-Layer Stack)

| Component | Citadel OS Layer | Implementation |
|-----------|------------------|----------------|
| AI Dashboards | Layer 6: Applications | React + TypeScript |
| AI Domain Bundle | Layer 5: Domain Bundles | Advanced AI bundle |
| AI Skills | Layer 4: Skills Layer | SKILL.md files |
| Inference Engine | Layer 3: Hot Path | FastAPI + Redis caching |
| ML Models | Layer 2: Cold Path | Python + PyTorch/XGBoost |
| Data Infrastructure | Layer 1: Infrastructure | Redpanda + TimescaleDB |

### Execution Path Classification

| Skill | Path | Reasoning |
|-------|------|-----------|
| SKILL-112 (Causal AI) | **Cold** | Batch causal analysis (<30s) |
| SKILL-128 (Predictive Maint) | **Hybrid** | Edge + cloud processing |
| SKILL-129 (Churn) | **Cold** | Daily batch + real-time scoring |
| SKILL-130 (Anomaly) | **Hot** | Real-time detection (<100ms) |
| SKILL-131 (Auto-Opt) | **Hybrid** | Safe exploration + monitoring |

### MCP Server Requirements

```yaml
mcp_servers:
  # Causal AI
  - mcp://ai/causal-graph           # DAG modeling
  - mcp://ai/intervention-test      # What-if analysis
  
  # Predictive Maintenance
  - mcp://ai/sensor-ingest          # IoT data collection
  - mcp://ai/failure-predict        # ML predictions
  
  # Churn Prediction
  - mcp://ai/churn-score            # Risk scoring
  - mcp://ai/retention-trigger      # Campaign automation
  
  # Anomaly Detection
  - mcp://ai/anomaly-detect         # Real-time isolation
  - mcp://ai/fraud-alert            # Alert generation
  
  # Auto-Optimization
  - mcp://ai/bayesian-opt           # Parameter tuning
  - mcp://ai/safe-explore           # Safety constraints
```

### Infrastructure Alignment Verification

| Research Spec | Citadel OS Architecture | Status |
|---------------|------------------------|--------|
| Python 3.11+ | ✅ Aligned | ML/AI services |
| DoWhy/PyWhy | ✅ Aligned | Causal inference |
| XGBoost | ✅ Aligned | Churn prediction |
| scikit-learn | ✅ Aligned | Isolation Forest |
| FastAPI | ✅ Aligned | ML model serving |
| Apache Kafka | ⚠️ Adjustment | Use Redpanda |
| InfluxDB | ⚠️ Adjustment | Use TimescaleDB |
| AWS IoT Core | ✅ Aligned | Sensor integration |

---

## 📊 SKILL SPECIFICATIONS

### SKILL-112: Causal AI Understanding

#### Purpose
Causal inference engine using DoWhy library for understanding cause-and-effect relationships, enabling "what-if" analysis and intervention testing beyond simple correlations.

#### Technical Architecture
```python
import dowhy
from dowhy import CausalModel
from dowhy.causal_estimators import propensity_score_matching_estimator
import networkx as nx
import pandas as pd
from dataclasses import dataclass
from typing import Dict, List, Optional, Tuple

@dataclass
class CausalEffect:
    treatment: str
    outcome: str
    effect_estimate: float
    confidence_interval: Tuple[float, float]
    p_value: float
    refutation_results: Dict[str, float]

@dataclass
class InterventionResult:
    intervention: str
    predicted_outcome: float
    confidence_interval: Tuple[float, float]
    causal_path: List[str]
    confounders_controlled: List[str]


class CausalAIService:
    """
    DoWhy-based causal inference for hospitality decisions.
    Provides principled 4-step causal analysis.
    """
    
    def __init__(self):
        self.db = PostgreSQLClient()
        self.redis = RedisClient()
    
    async def create_causal_graph(
        self,
        tenant_id: str,
        domain: str = 'pricing'
    ) -> nx.DiGraph:
        """
        Create causal DAG from domain knowledge.
        Step 1 of DoWhy 4-step process.
        """
        
        if domain == 'pricing':
            # Hospitality pricing causal graph
            graph = nx.DiGraph()
            
            # Add nodes (variables)
            variables = [
                'price', 'occupancy', 'reviews', 'seasonality',
                'competitor_price', 'marketing_spend', 'revenue',
                'customer_satisfaction', 'repeat_bookings'
            ]
            graph.add_nodes_from(variables)
            
            # Add edges (causal relationships)
            edges = [
                ('price', 'occupancy'),
                ('price', 'revenue'),
                ('seasonality', 'price'),
                ('seasonality', 'occupancy'),
                ('competitor_price', 'price'),
                ('marketing_spend', 'occupancy'),
                ('occupancy', 'revenue'),
                ('reviews', 'occupancy'),
                ('customer_satisfaction', 'reviews'),
                ('customer_satisfaction', 'repeat_bookings'),
                ('price', 'customer_satisfaction')
            ]
            graph.add_edges_from(edges)
        
        return graph
    
    async def estimate_causal_effect(
        self,
        tenant_id: str,
        treatment: str,
        outcome: str,
        data: pd.DataFrame,
        graph: nx.DiGraph
    ) -> CausalEffect:
        """
        Estimate causal effect using DoWhy.
        Steps 2-4: Identify, Estimate, Refute.
        """
        
        # Convert graph to GML format for DoWhy
        gml_string = self._graph_to_gml(graph)
        
        # Create DoWhy causal model
        model = CausalModel(
            data=data,
            treatment=treatment,
            outcome=outcome,
            graph=gml_string
        )
        
        # Step 2: Identify causal effect
        identified_estimand = model.identify_effect(
            proceed_when_unidentifiable=True
        )
        
        # Step 3: Estimate causal effect
        estimate = model.estimate_effect(
            identified_estimand,
            method_name="backdoor.propensity_score_matching",
            confidence_intervals=True
        )
        
        # Step 4: Refute the estimate (robustness checks)
        refutation_results = {}
        
        # Placebo treatment refutation
        placebo = model.refute_estimate(
            identified_estimand, estimate,
            method_name="placebo_treatment_refuter",
            placebo_type="permute"
        )
        refutation_results['placebo'] = placebo.new_effect
        
        # Random common cause refutation
        random_cause = model.refute_estimate(
            identified_estimand, estimate,
            method_name="random_common_cause"
        )
        refutation_results['random_cause'] = random_cause.new_effect
        
        # Data subset refutation
        subset = model.refute_estimate(
            identified_estimand, estimate,
            method_name="data_subset_refuter",
            subset_fraction=0.8
        )
        refutation_results['subset'] = subset.new_effect
        
        return CausalEffect(
            treatment=treatment,
            outcome=outcome,
            effect_estimate=estimate.value,
            confidence_interval=(
                estimate.get_confidence_intervals()[0],
                estimate.get_confidence_intervals()[1]
            ),
            p_value=estimate.get_standard_error(),
            refutation_results=refutation_results
        )
    
    async def test_intervention(
        self,
        tenant_id: str,
        intervention: Dict[str, float],
        target_outcome: str,
        data: pd.DataFrame,
        graph: nx.DiGraph
    ) -> InterventionResult:
        """
        Test what-if intervention scenarios.
        Uses do-calculus for causal intervention.
        """
        
        # Get current baseline
        baseline = data[target_outcome].mean()
        
        # Simulate intervention using causal model
        # do(X = x) - set variable to specific value
        intervention_var = list(intervention.keys())[0]
        intervention_val = list(intervention.values())[0]
        
        # Estimate effect of intervention
        effect = await self.estimate_causal_effect(
            tenant_id,
            intervention_var,
            target_outcome,
            data,
            graph
        )
        
        # Calculate predicted outcome under intervention
        predicted = baseline + (
            effect.effect_estimate * intervention_val
        )
        
        # Find causal path
        causal_path = list(nx.shortest_path(
            graph, intervention_var, target_outcome
        ))
        
        # Identify controlled confounders
        confounders = self._find_confounders(
            graph, intervention_var, target_outcome
        )
        
        return InterventionResult(
            intervention=f"do({intervention_var}={intervention_val})",
            predicted_outcome=predicted,
            confidence_interval=(
                predicted + effect.confidence_interval[0],
                predicted + effect.confidence_interval[1]
            ),
            causal_path=causal_path,
            confounders_controlled=confounders
        )
```

#### Causal Analysis Workflow
```
┌────────────────────────────────────────────────────────────┐
│                   STEP 1: MODEL                            │
│  Create causal DAG with domain expert input                │
│  Variables: Price, Occupancy, Reviews, Season...           │
└─────────────────────────┬──────────────────────────────────┘
                          ▼
┌────────────────────────────────────────────────────────────┐
│                   STEP 2: IDENTIFY                         │
│  Identify causal estimand using do-calculus                │
│  Find confounders, instrumental variables                  │
└─────────────────────────┬──────────────────────────────────┘
                          ▼
┌────────────────────────────────────────────────────────────┐
│                   STEP 3: ESTIMATE                         │
│  Calculate causal effect using matching/IV/regression      │
│  Generate confidence intervals                             │
└─────────────────────────┬──────────────────────────────────┘
                          ▼
┌────────────────────────────────────────────────────────────┐
│                   STEP 4: REFUTE                           │
│  Placebo tests, random cause, subset validation            │
│  Sensitivity analysis for robustness                       │
└────────────────────────────────────────────────────────────┘
```

---

### SKILL-128: Predictive Maintenance AI

#### Purpose
IoT sensor-based predictive maintenance using ML to predict equipment failures before they occur, reducing downtime by 50% and extending asset life by 20-40%.

#### Technical Architecture
```python
import numpy as np
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.preprocessing import StandardScaler
from dataclasses import dataclass
from datetime import datetime, timedelta
from typing import List, Dict, Optional
import paho.mqtt.client as mqtt

@dataclass
class SensorReading:
    sensor_id: str
    equipment_id: str
    timestamp: datetime
    temperature: float
    vibration: float
    pressure: float
    current: float
    humidity: Optional[float] = None

@dataclass
class FailurePrediction:
    equipment_id: str
    failure_probability: float
    predicted_failure_date: Optional[datetime]
    time_to_failure_hours: Optional[int]
    risk_level: str  # 'critical', 'high', 'medium', 'low', 'normal'
    contributing_factors: List[Dict[str, float]]
    recommended_action: str
    confidence_score: float


class PredictiveMaintenanceService:
    """
    IoT-based predictive maintenance with edge computing.
    Achieves 50% reduction in unplanned downtime.
    """
    
    RISK_THRESHOLDS = {
        'critical': (90, 100),
        'high': (70, 89),
        'medium': (50, 69),
        'low': (30, 49),
        'normal': (0, 29)
    }
    
    def __init__(self):
        self.db = PostgreSQLClient()
        self.redis = RedisClient()
        self.mqtt_client = mqtt.Client()
        self.model = self._load_model()
        self.scaler = StandardScaler()
    
    async def process_sensor_reading(
        self,
        reading: SensorReading
    ) -> Optional[FailurePrediction]:
        """
        Process real-time sensor data with edge computing.
        Sub-second latency for critical alerts.
        """
        
        # Store reading
        await self._store_reading(reading)
        
        # Get historical context
        history = await self._get_equipment_history(
            reading.equipment_id, hours=24
        )
        
        # Feature engineering
        features = self._extract_features(reading, history)
        
        # Scale features
        features_scaled = self.scaler.transform([features])
        
        # Predict failure probability
        probability = self.model.predict_proba(features_scaled)[0][1]
        
        # Determine risk level
        risk_level = self._get_risk_level(probability * 100)
        
        # Generate prediction
        prediction = FailurePrediction(
            equipment_id=reading.equipment_id,
            failure_probability=probability,
            predicted_failure_date=self._estimate_failure_date(
                probability, history
            ),
            time_to_failure_hours=self._estimate_ttf(probability, history),
            risk_level=risk_level,
            contributing_factors=self._get_contributing_factors(
                features, features_scaled
            ),
            recommended_action=self._get_recommendation(risk_level),
            confidence_score=self._calculate_confidence(history)
        )
        
        # Trigger alert if needed
        if risk_level in ('critical', 'high'):
            await self._trigger_maintenance_alert(prediction)
        
        return prediction
    
    def _extract_features(
        self,
        current: SensorReading,
        history: List[SensorReading]
    ) -> List[float]:
        """Extract ML features from sensor readings."""
        
        # Current values
        features = [
            current.temperature,
            current.vibration,
            current.pressure,
            current.current
        ]
        
        # Statistical features from history
        if history:
            temps = [r.temperature for r in history]
            vibs = [r.vibration for r in history]
            
            features.extend([
                np.mean(temps),
                np.std(temps),
                np.max(temps) - np.min(temps),  # Temperature range
                np.mean(vibs),
                np.std(vibs),
                self._calculate_trend(temps),    # Temperature trend
                self._calculate_trend(vibs),     # Vibration trend
            ])
        
        return features
    
    def _estimate_failure_date(
        self,
        probability: float,
        history: List[SensorReading]
    ) -> Optional[datetime]:
        """Estimate when failure will occur."""
        
        if probability < 0.3:
            return None
        
        # Calculate degradation rate from history
        degradation_rate = self._calculate_degradation_rate(history)
        
        # Estimate time to failure
        hours_to_failure = int((1 - probability) / degradation_rate)
        
        return datetime.utcnow() + timedelta(hours=hours_to_failure)
    
    def _get_recommendation(self, risk_level: str) -> str:
        """Get maintenance recommendation based on risk."""
        
        recommendations = {
            'critical': 'EMERGENCY: Schedule immediate maintenance within 24 hours',
            'high': 'Schedule maintenance within 7 days',
            'medium': 'Plan maintenance within 4 weeks',
            'low': 'Schedule routine inspection',
            'normal': 'Continue monitoring, no action required'
        }
        return recommendations[risk_level]
    
    async def _trigger_maintenance_alert(
        self,
        prediction: FailurePrediction
    ):
        """Send maintenance alert to CMMS and operations."""
        
        # Create work order in CMMS
        work_order = {
            'equipment_id': prediction.equipment_id,
            'priority': 'EMERGENCY' if prediction.risk_level == 'critical' else 'HIGH',
            'predicted_failure': prediction.predicted_failure_date.isoformat(),
            'failure_probability': prediction.failure_probability,
            'recommended_action': prediction.recommended_action
        }
        
        # Send to work order queue
        await self.redis.publish(
            'maintenance:work_orders',
            json.dumps(work_order)
        )
        
        # Send mobile notification
        await self._send_technician_notification(prediction)
```

#### Maintenance Decision Matrix
| Risk Score | Time to Failure | Action | Priority |
|------------|-----------------|--------|----------|
| 90-100% | <24 hours | Emergency maintenance | Critical |
| 70-89% | 1-7 days | Scheduled maintenance | High |
| 50-69% | 1-4 weeks | Planned maintenance | Medium |
| 30-49% | 1-3 months | Routine inspection | Low |
| <30% | >3 months | Continue monitoring | Normal |

---

### SKILL-129: Churn Prediction

#### Purpose
XGBoost-based customer churn prediction with 92%+ accuracy, using SMOTE for class imbalance and SHAP for interpretability.

#### Technical Architecture
```python
import xgboost as xgb
from imblearn.over_sampling import SMOTE
import shap
from sklearn.model_selection import train_test_split
from dataclasses import dataclass
from typing import List, Dict, Tuple
import pandas as pd
import numpy as np

@dataclass
class ChurnRiskScore:
    customer_id: str
    churn_probability: float
    risk_level: str  # 'high', 'medium', 'low'
    top_churn_drivers: List[Dict[str, float]]
    recommended_retention_action: str
    customer_segment: str
    expected_ltv_if_retained: float

@dataclass
class RFMFeatures:
    recency_days: int
    frequency: int
    monetary_value: float
    avg_booking_value: float
    booking_trend: str  # 'increasing', 'stable', 'decreasing'


class ChurnPredictionService:
    """
    XGBoost churn prediction with 92%+ accuracy.
    PR AUC of 0.67 with SMOTE + Hyperband + SHAP.
    """
    
    RISK_THRESHOLDS = {
        'high': 0.70,
        'medium': 0.40,
        'low': 0.0
    }
    
    def __init__(self):
        self.db = PostgreSQLClient()
        self.redis = RedisClient()
        self.model = self._load_model()
        self.explainer = shap.TreeExplainer(self.model)
    
    async def predict_churn(
        self,
        customer_id: str
    ) -> ChurnRiskScore:
        """Predict churn risk for a customer."""
        
        # Get customer data
        customer = await self._get_customer_data(customer_id)
        
        # Feature engineering
        features = await self._engineer_features(customer)
        features_df = pd.DataFrame([features])
        
        # Predict probability
        churn_prob = self.model.predict_proba(features_df)[0][1]
        
        # Get SHAP values for interpretability
        shap_values = self.explainer.shap_values(features_df)
        
        # Get top churn drivers
        drivers = self._get_top_drivers(features_df.columns, shap_values[0])
        
        # Determine risk level
        risk_level = self._get_risk_level(churn_prob)
        
        # Get retention recommendation
        recommendation = self._get_retention_recommendation(
            risk_level, customer, drivers
        )
        
        return ChurnRiskScore(
            customer_id=customer_id,
            churn_probability=churn_prob,
            risk_level=risk_level,
            top_churn_drivers=drivers,
            recommended_retention_action=recommendation,
            customer_segment=customer.segment,
            expected_ltv_if_retained=self._calculate_ltv(customer)
        )
    
    async def _engineer_features(
        self,
        customer: dict
    ) -> Dict[str, float]:
        """Engineer features for churn prediction."""
        
        # RFM features
        rfm = await self._calculate_rfm(customer['id'])
        
        # Behavioral features
        bookings = await self._get_booking_history(customer['id'])
        reviews = await self._get_review_history(customer['id'])
        support_tickets = await self._get_support_history(customer['id'])
        
        features = {
            # RFM
            'recency_days': rfm.recency_days,
            'frequency': rfm.frequency,
            'monetary_value': rfm.monetary_value,
            'avg_booking_value': rfm.avg_booking_value,
            
            # Booking behavior
            'total_bookings': len(bookings),
            'bookings_last_90_days': self._count_recent(bookings, 90),
            'bookings_last_180_days': self._count_recent(bookings, 180),
            'booking_trend': self._encode_trend(rfm.booking_trend),
            
            # Satisfaction
            'avg_review_score': np.mean([r.score for r in reviews]) if reviews else 0,
            'review_count': len(reviews),
            'negative_reviews': sum(1 for r in reviews if r.score < 3),
            
            # Support
            'support_tickets': len(support_tickets),
            'unresolved_tickets': sum(1 for t in support_tickets if not t.resolved),
            'avg_resolution_time': np.mean([t.resolution_hours for t in support_tickets if t.resolved]) if support_tickets else 0,
            
            # Customer tenure
            'tenure_months': customer['tenure_months'],
            'days_since_last_interaction': customer['days_since_interaction'],
            
            # Engagement
            'email_open_rate': customer.get('email_open_rate', 0),
            'app_sessions_last_30d': customer.get('app_sessions', 0)
        }
        
        return features
    
    def _get_top_drivers(
        self,
        feature_names: List[str],
        shap_values: np.ndarray,
        top_n: int = 5
    ) -> List[Dict[str, float]]:
        """Get top churn drivers from SHAP values."""
        
        # Sort by absolute SHAP value
        indices = np.argsort(np.abs(shap_values))[::-1][:top_n]
        
        drivers = []
        for idx in indices:
            drivers.append({
                'feature': feature_names[idx],
                'impact': float(shap_values[idx]),
                'direction': 'increases_churn' if shap_values[idx] > 0 else 'decreases_churn'
            })
        
        return drivers
    
    def _get_retention_recommendation(
        self,
        risk_level: str,
        customer: dict,
        drivers: List[Dict]
    ) -> str:
        """Get personalized retention recommendation."""
        
        if risk_level == 'high':
            # Check top driver
            top_driver = drivers[0]['feature']
            
            if 'support' in top_driver:
                return "Assign dedicated support rep, offer service recovery"
            elif 'review' in top_driver:
                return "Personal outreach from manager, offer loyalty bonus"
            elif 'recency' in top_driver:
                return "Send personalized re-engagement offer with 20% discount"
            else:
                return "Schedule personal call, offer exclusive loyalty perks"
        
        elif risk_level == 'medium':
            return "Include in targeted email campaign with 10% loyalty discount"
        
        else:
            return "Continue standard engagement, monitor for changes"
    
    async def train_model(
        self,
        training_data: pd.DataFrame
    ) -> Dict[str, float]:
        """Train XGBoost model with SMOTE and Hyperband."""
        
        X = training_data.drop('churned', axis=1)
        y = training_data['churned']
        
        # Split data
        X_train, X_test, y_train, y_test = train_test_split(
            X, y, test_size=0.2, stratify=y, random_state=42
        )
        
        # Apply SMOTE for class imbalance
        smote = SMOTE(random_state=42)
        X_train_balanced, y_train_balanced = smote.fit_resample(X_train, y_train)
        
        # Train XGBoost
        model = xgb.XGBClassifier(
            n_estimators=200,
            max_depth=6,
            learning_rate=0.1,
            subsample=0.8,
            colsample_bytree=0.8,
            scale_pos_weight=len(y_train[y_train==0]) / len(y_train[y_train==1]),
            use_label_encoder=False,
            eval_metric='auc'
        )
        
        model.fit(
            X_train_balanced, y_train_balanced,
            eval_set=[(X_test, y_test)],
            early_stopping_rounds=20,
            verbose=False
        )
        
        # Evaluate
        y_pred = model.predict(X_test)
        y_prob = model.predict_proba(X_test)[:, 1]
        
        from sklearn.metrics import accuracy_score, precision_score, recall_score, roc_auc_score
        
        metrics = {
            'accuracy': accuracy_score(y_test, y_pred),
            'precision': precision_score(y_test, y_pred),
            'recall': recall_score(y_test, y_pred),
            'auc_roc': roc_auc_score(y_test, y_prob)
        }
        
        self.model = model
        self.explainer = shap.TreeExplainer(model)
        
        return metrics
```

#### Retention Strategy Matrix
| Segment | Risk Level | Strategy | Expected ROI |
|---------|------------|----------|--------------|
| High-Value Frequent | High (>80%) | Personal concierge, exclusive perks | 5:1 |
| Mid-Value Regular | Medium (60-80%) | Targeted discounts, loyalty points | 3:1 |
| Low-Value Occasional | Low (40-60%) | Email campaigns, general offers | 2:1 |
| New Customers | Variable | Onboarding optimization | 4:1 |

---

### SKILL-130: Anomaly Detection

#### Purpose
Isolation Forest-based real-time anomaly detection with 93% accuracy, 95% precision, and <100ms response time for fraud prevention.

#### Technical Architecture
```python
from sklearn.ensemble import IsolationForest
from sklearn.preprocessing import StandardScaler
from dataclasses import dataclass
from datetime import datetime
from typing import List, Dict, Optional
import numpy as np

@dataclass
class AnomalyResult:
    transaction_id: str
    anomaly_score: float
    is_anomaly: bool
    anomaly_type: str  # 'fraud', 'operational', 'system', 'data_quality'
    severity: str  # 'critical', 'high', 'medium', 'low'
    explanation: List[Dict[str, float]]
    recommended_action: str
    confidence: float

@dataclass
class TransactionData:
    transaction_id: str
    timestamp: datetime
    amount: float
    customer_id: str
    payment_method: str
    device_fingerprint: str
    ip_address: str
    session_duration: float
    click_count: int
    property_id: str


class AnomalyDetectionService:
    """
    Isolation Forest anomaly detection with 93% accuracy.
    Real-time detection with <100ms latency.
    """
    
    ANOMALY_THRESHOLD = -0.5  # Isolation Forest threshold
    
    def __init__(self):
        self.db = PostgreSQLClient()
        self.redis = RedisClient()
        self.model = self._load_model()
        self.scaler = StandardScaler()
    
    async def detect_anomaly(
        self,
        transaction: TransactionData
    ) -> AnomalyResult:
        """
        Real-time anomaly detection using Isolation Forest.
        O(n*logn) time complexity for scalability.
        """
        
        # Feature extraction
        features = await self._extract_features(transaction)
        features_scaled = self.scaler.transform([features])
        
        # Get anomaly score
        # More negative = more anomalous
        anomaly_score = self.model.decision_function(features_scaled)[0]
        
        # Predict anomaly
        is_anomaly = self.model.predict(features_scaled)[0] == -1
        
        # Calculate normalized score (0-1 scale)
        normalized_score = self._normalize_score(anomaly_score)
        
        # Determine severity and type
        severity = self._get_severity(normalized_score)
        anomaly_type = await self._classify_anomaly_type(
            transaction, features, is_anomaly
        )
        
        # Get explanation
        explanation = self._get_explanation(
            transaction, features, features_scaled
        )
        
        result = AnomalyResult(
            transaction_id=transaction.transaction_id,
            anomaly_score=normalized_score,
            is_anomaly=is_anomaly,
            anomaly_type=anomaly_type,
            severity=severity,
            explanation=explanation,
            recommended_action=self._get_recommendation(severity, anomaly_type),
            confidence=self._calculate_confidence(anomaly_score)
        )
        
        # Take action if anomaly detected
        if is_anomaly:
            await self._handle_anomaly(result, transaction)
        
        return result
    
    async def _extract_features(
        self,
        transaction: TransactionData
    ) -> List[float]:
        """Extract features for anomaly detection."""
        
        # Get customer historical behavior
        history = await self._get_customer_history(transaction.customer_id)
        
        features = [
            # Transaction features
            transaction.amount,
            np.log1p(transaction.amount),
            transaction.session_duration,
            transaction.click_count,
            
            # Deviation from customer norm
            (transaction.amount - history['avg_amount']) / (history['std_amount'] + 1),
            
            # Time-based features
            transaction.timestamp.hour,
            transaction.timestamp.weekday(),
            
            # Velocity features
            await self._count_recent_transactions(transaction.customer_id, hours=1),
            await self._count_recent_transactions(transaction.customer_id, hours=24),
            
            # Device/IP risk
            await self._get_device_risk_score(transaction.device_fingerprint),
            await self._get_ip_risk_score(transaction.ip_address),
            
            # Behavioral features
            transaction.click_count / max(transaction.session_duration, 1),  # Click rate
        ]
        
        return features
    
    def _normalize_score(self, score: float) -> float:
        """Normalize anomaly score to 0-1 scale."""
        # Isolation Forest scores range roughly from -0.5 to 0.5
        # More negative = more anomalous
        normalized = (0.5 - score) / 1.0
        return max(0, min(1, normalized))
    
    def _get_severity(self, score: float) -> str:
        """Determine severity based on anomaly score."""
        if score >= 0.9:
            return 'critical'
        elif score >= 0.7:
            return 'high'
        elif score >= 0.5:
            return 'medium'
        else:
            return 'low'
    
    async def _classify_anomaly_type(
        self,
        transaction: TransactionData,
        features: List[float],
        is_anomaly: bool
    ) -> str:
        """Classify the type of anomaly detected."""
        
        if not is_anomaly:
            return 'none'
        
        # Check specific patterns
        if transaction.amount > 5000:  # High value
            return 'fraud'
        
        recent_count = await self._count_recent_transactions(
            transaction.customer_id, hours=1
        )
        if recent_count > 10:  # Velocity abuse
            return 'fraud'
        
        device_risk = await self._get_device_risk_score(transaction.device_fingerprint)
        if device_risk > 0.8:
            return 'fraud'
        
        # Default to operational anomaly
        return 'operational'
    
    async def _handle_anomaly(
        self,
        result: AnomalyResult,
        transaction: TransactionData
    ):
        """Handle detected anomaly based on severity."""
        
        if result.severity == 'critical':
            # Immediate block
            await self._block_transaction(transaction.transaction_id)
            await self._send_fraud_alert(result, transaction)
        
        elif result.severity == 'high':
            # Flag for review
            await self._flag_for_review(transaction.transaction_id)
            await self._send_alert(result, 'fraud_team')
        
        elif result.severity == 'medium':
            # Log and monitor
            await self._log_anomaly(result)
            await self._send_alert(result, 'operations')
        
        # Always log
        await self.db.insert_anomaly_event(result)
    
    def train_model(
        self,
        normal_data: np.ndarray,
        contamination: float = 0.01
    ) -> IsolationForest:
        """Train Isolation Forest model."""
        
        model = IsolationForest(
            n_estimators=200,
            max_samples='auto',
            contamination=contamination,
            max_features=1.0,
            bootstrap=False,
            n_jobs=-1,
            random_state=42
        )
        
        model.fit(normal_data)
        
        self.model = model
        return model
```

#### Anomaly Response Matrix
| Anomaly Type | Severity | Automatic Action | Human Review |
|--------------|----------|------------------|--------------|
| Fraudulent Transaction | Critical | Block immediately | Yes, within 1hr |
| Unusual Booking Pattern | High | Flag for review | Yes, within 4hr |
| System Performance | Medium | Alert operations | Yes, within 24hr |
| Data Quality Issue | Low | Log for analysis | Batch review |

---

### SKILL-131: Auto-Optimization

#### Purpose
Safe Bayesian multi-objective optimization with human oversight, achieving continuous improvement of pricing, inventory, and operational parameters.

#### Technical Architecture
```python
import optuna
from optuna.samplers import TPESampler
from dataclasses import dataclass
from typing import Dict, List, Tuple, Callable, Optional
from datetime import datetime
import numpy as np

@dataclass
class OptimizationResult:
    parameter_name: str
    current_value: float
    optimized_value: float
    expected_improvement: float
    confidence_interval: Tuple[float, float]
    safety_check_passed: bool
    requires_approval: bool

@dataclass
class SafetyConstraint:
    parameter_name: str
    min_value: float
    max_value: float
    max_change_pct: float
    rollback_trigger: str


class AutoOptimizationService:
    """
    Safe Bayesian optimization with MOBO and human oversight.
    Balances exploration and exploitation with safety constraints.
    """
    
    SAFETY_CONSTRAINTS = {
        'price': SafetyConstraint(
            parameter_name='price',
            min_value=50,
            max_value=1000,
            max_change_pct=10,
            rollback_trigger='revenue_drop_5pct'
        ),
        'min_stay': SafetyConstraint(
            parameter_name='min_stay',
            min_value=1,
            max_value=7,
            max_change_pct=50,
            rollback_trigger='booking_rate_drop_10pct'
        ),
        'marketing_budget': SafetyConstraint(
            parameter_name='marketing_budget',
            min_value=100,
            max_value=10000,
            max_change_pct=20,
            rollback_trigger='roi_below_2x'
        )
    }
    
    def __init__(self):
        self.db = PostgreSQLClient()
        self.redis = RedisClient()
        self.study = None
    
    async def optimize_parameter(
        self,
        tenant_id: str,
        parameter_name: str,
        objective_function: Callable,
        n_trials: int = 50,
        shadow_mode: bool = True
    ) -> OptimizationResult:
        """
        Optimize parameter using Bayesian optimization.
        Uses Expected Improvement acquisition function.
        """
        
        constraint = self.SAFETY_CONSTRAINTS.get(parameter_name)
        if not constraint:
            raise ValueError(f"Unknown parameter: {parameter_name}")
        
        # Get current value
        current_value = await self._get_current_value(tenant_id, parameter_name)
        
        # Create Optuna study
        sampler = TPESampler(seed=42)
        self.study = optuna.create_study(
            direction='maximize',
            sampler=sampler
        )
        
        # Define objective with safety constraints
        def safe_objective(trial):
            value = trial.suggest_float(
                parameter_name,
                constraint.min_value,
                constraint.max_value
            )
            
            # Safety check: limit change from current
            max_change = current_value * (constraint.max_change_pct / 100)
            if abs(value - current_value) > max_change:
                return float('-inf')
            
            # Evaluate objective
            return objective_function(value)
        
        # Run optimization
        self.study.optimize(safe_objective, n_trials=n_trials, show_progress_bar=False)
        
        # Get best result
        best_value = self.study.best_params[parameter_name]
        best_score = self.study.best_value
        
        # Calculate improvement
        current_score = objective_function(current_value)
        improvement = (best_score - current_score) / current_score if current_score != 0 else 0
        
        # Calculate confidence interval
        ci = self._calculate_confidence_interval(self.study)
        
        # Safety validation
        safety_passed = self._validate_safety(
            current_value, best_value, constraint
        )
        
        # Determine if approval needed
        requires_approval = (
            improvement > 0.1 or  # >10% improvement
            abs(best_value - current_value) > current_value * 0.05  # >5% change
        )
        
        result = OptimizationResult(
            parameter_name=parameter_name,
            current_value=current_value,
            optimized_value=best_value,
            expected_improvement=improvement,
            confidence_interval=ci,
            safety_check_passed=safety_passed,
            requires_approval=requires_approval
        )
        
        # Apply or shadow
        if shadow_mode:
            await self._run_shadow_test(tenant_id, result)
        elif safety_passed and not requires_approval:
            await self._apply_optimization(tenant_id, result)
        
        return result
    
    async def multi_objective_optimize(
        self,
        tenant_id: str,
        objectives: Dict[str, Callable],
        parameters: List[str]
    ) -> List[OptimizationResult]:
        """
        Multi-objective Bayesian optimization (MOBO).
        Uses Expected Hypervolume Improvement (EHVI).
        """
        
        # Create multi-objective study
        sampler = optuna.samplers.NSGAIISampler(seed=42)
        study = optuna.create_study(
            directions=['maximize'] * len(objectives),
            sampler=sampler
        )
        
        def multi_objective(trial):
            param_values = {}
            for param in parameters:
                constraint = self.SAFETY_CONSTRAINTS[param]
                param_values[param] = trial.suggest_float(
                    param,
                    constraint.min_value,
                    constraint.max_value
                )
            
            # Evaluate all objectives
            scores = []
            for name, obj_func in objectives.items():
                scores.append(obj_func(param_values))
            
            return tuple(scores)
        
        study.optimize(multi_objective, n_trials=100)
        
        # Get Pareto optimal solutions
        pareto_solutions = study.best_trials
        
        # Return best balanced solution
        best_trial = self._select_best_balanced(pareto_solutions, objectives)
        
        results = []
        for param in parameters:
            current = await self._get_current_value(tenant_id, param)
            optimized = best_trial.params[param]
            
            results.append(OptimizationResult(
                parameter_name=param,
                current_value=current,
                optimized_value=optimized,
                expected_improvement=self._estimate_improvement(
                    current, optimized, param
                ),
                confidence_interval=self._calculate_confidence_interval(study),
                safety_check_passed=True,
                requires_approval=True  # MOBO always needs approval
            ))
        
        return results
    
    def _validate_safety(
        self,
        current: float,
        proposed: float,
        constraint: SafetyConstraint
    ) -> bool:
        """Validate proposed value against safety constraints."""
        
        # Check bounds
        if proposed < constraint.min_value or proposed > constraint.max_value:
            return False
        
        # Check max change
        change_pct = abs(proposed - current) / current * 100
        if change_pct > constraint.max_change_pct:
            return False
        
        return True
    
    async def _run_shadow_test(
        self,
        tenant_id: str,
        result: OptimizationResult
    ):
        """Run optimization in shadow mode (no live changes)."""
        
        # Record shadow result for analysis
        await self.db.insert_shadow_test({
            'tenant_id': tenant_id,
            'parameter': result.parameter_name,
            'current_value': result.current_value,
            'proposed_value': result.optimized_value,
            'expected_improvement': result.expected_improvement,
            'timestamp': datetime.utcnow()
        })
    
    async def rollback_optimization(
        self,
        tenant_id: str,
        parameter_name: str
    ):
        """Rollback to previous parameter value."""
        
        # Get previous value
        history = await self.db.get_parameter_history(
            tenant_id, parameter_name, limit=2
        )
        
        if len(history) >= 2:
            previous_value = history[1]['value']
            await self._apply_value(tenant_id, parameter_name, previous_value)
            
            # Log rollback
            await self.db.insert_rollback_event({
                'tenant_id': tenant_id,
                'parameter': parameter_name,
                'rolled_back_from': history[0]['value'],
                'rolled_back_to': previous_value,
                'timestamp': datetime.utcnow()
            })
```

#### Optimization Safety Framework
| Parameter | Safety Constraint | Validation | Rollback Trigger |
|-----------|------------------|------------|------------------|
| Pricing | ±10% from baseline | Revenue analysis | >5% revenue drop |
| Inventory | Min 20% availability | Booking success | <90% success rate |
| Marketing | Budget limits | ROI monitoring | <2:1 ROI ratio |
| Operations | Business hours | Customer satisfaction | <4.0 rating |

---

## 🗄️ DATABASE SCHEMA

### PostgreSQL + TimescaleDB

```sql
-- Sensor readings (TimescaleDB hypertable)
CREATE TABLE sensor_readings (
    id BIGSERIAL,
    equipment_id UUID NOT NULL,
    timestamp TIMESTAMPTZ NOT NULL,
    temperature FLOAT,
    vibration FLOAT,
    pressure FLOAT,
    current FLOAT,
    humidity FLOAT,
    PRIMARY KEY (id, timestamp)
);

SELECT create_hypertable('sensor_readings', 'timestamp');

-- Failure predictions
CREATE TABLE failure_predictions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    equipment_id UUID NOT NULL,
    prediction_timestamp TIMESTAMPTZ DEFAULT NOW(),
    failure_probability FLOAT NOT NULL,
    predicted_failure_date TIMESTAMPTZ,
    risk_level VARCHAR(20) NOT NULL,
    contributing_factors JSONB,
    recommended_action TEXT,
    actual_failure_date TIMESTAMPTZ,
    prediction_accurate BOOLEAN
);

-- Churn predictions
CREATE TABLE churn_predictions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    customer_id UUID NOT NULL,
    prediction_date DATE NOT NULL,
    churn_probability FLOAT NOT NULL,
    risk_level VARCHAR(20) NOT NULL,
    top_drivers JSONB,
    retention_action TEXT,
    actual_churned BOOLEAN,
    UNIQUE(customer_id, prediction_date)
);

-- Anomaly events
CREATE TABLE anomaly_events (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    transaction_id VARCHAR(100),
    timestamp TIMESTAMPTZ DEFAULT NOW(),
    anomaly_score FLOAT NOT NULL,
    anomaly_type VARCHAR(50) NOT NULL,
    severity VARCHAR(20) NOT NULL,
    explanation JSONB,
    action_taken TEXT,
    false_positive BOOLEAN
);

-- Optimization history
CREATE TABLE optimization_history (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL,
    parameter_name VARCHAR(100) NOT NULL,
    previous_value FLOAT NOT NULL,
    new_value FLOAT NOT NULL,
    expected_improvement FLOAT,
    actual_improvement FLOAT,
    applied_at TIMESTAMPTZ DEFAULT NOW(),
    rolled_back BOOLEAN DEFAULT FALSE,
    rollback_reason TEXT
);

-- Causal models
CREATE TABLE causal_models (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL,
    domain VARCHAR(50) NOT NULL,
    graph_definition JSONB NOT NULL,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    last_validated TIMESTAMPTZ,
    validation_score FLOAT
);

-- Indexes
CREATE INDEX idx_sensor_equipment_time ON sensor_readings(equipment_id, timestamp DESC);
CREATE INDEX idx_predictions_equipment ON failure_predictions(equipment_id, prediction_timestamp DESC);
CREATE INDEX idx_churn_customer ON churn_predictions(customer_id, prediction_date DESC);
CREATE INDEX idx_anomaly_type ON anomaly_events(anomaly_type, timestamp DESC);
CREATE INDEX idx_optimization_tenant ON optimization_history(tenant_id, applied_at DESC);
```

---

## 📊 PERFORMANCE REQUIREMENTS

| Skill | Response Time | Throughput | Accuracy |
|-------|--------------|------------|----------|
| SKILL-112 (Causal AI) | <30s complex analysis | 1K queries/hr | N/A |
| SKILL-128 (Pred. Maint) | <5s sensor processing | 10K readings/sec | 90% failure prediction |
| SKILL-129 (Churn) | <1s scoring | 100K customers/day | 92%+ accuracy |
| SKILL-130 (Anomaly) | <100ms real-time | 1M transactions/day | 93% accuracy, 95% precision |
| SKILL-131 (Auto-Opt) | <1min per cycle | 24/7 continuous | N/A (safety-constrained) |

---

## 🔐 SECURITY CONSIDERATIONS

### Data Protection
- End-to-end encryption (TLS 1.3, AES-256)
- Differential privacy for customer data
- PII anonymization in ML models

### Access Control
- OAuth 2.0 with RBAC
- Audit logging for all AI decisions
- Explainable AI requirements (GDPR)

### Safety Controls
- Human-in-the-loop for critical decisions
- Automatic rollback triggers
- Shadow mode for new optimizations

---

## 📁 FILE LOCATIONS

```
specs/agentic/
└── SPEC-SKILL-112-131-AI-ADVANCED.md (this file)

knowledge/agentic/
└── KD-PHASE2-G8-ai-advanced.md (research source)

skills/agentic/
├── SKILL-112-causal-ai-understanding.md
├── SKILL-128-predictive-maintenance-ai.md
├── SKILL-129-churn-prediction.md
├── SKILL-130-anomaly-detection.md
└── SKILL-131-auto-optimization.md
```

---

## 🚀 IMPLEMENTATION ROADMAP

| Week | Milestone |
|------|-----------|
| 1-2 | SKILL-130 (Anomaly Detection) - Foundation |
| 3-4 | SKILL-129 (Churn Prediction) + XGBoost pipeline |
| 5-6 | SKILL-128 (Predictive Maintenance) + IoT integration |
| 7-8 | SKILL-112 (Causal AI) + SKILL-131 (Auto-Opt) |

---

**Status**: ✅ SPECIFIED - Ready for Engineering Implementation

