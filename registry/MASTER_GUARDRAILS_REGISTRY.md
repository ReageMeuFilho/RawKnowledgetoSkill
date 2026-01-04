# Master Guardrails Registry: Safety & Compliance

> **What the agent should NEVER do** - Critical for production safety
> **Purpose**: Define forbidden actions, compliance rules, escalation triggers
> **Last Updated**: January 2026

---

## 🛑 Why Guardrails Matter

Without guardrails, AI agents can:
- ❌ Give medical/legal advice (liability)
- ❌ Make unauthorized commitments (financial risk)
- ❌ Share sensitive data (privacy violation)
- ❌ Take irreversible actions without approval
- ❌ Discriminate or show bias

---

## 📋 Guardrail Categories

| Category | Purpose | Example |
|----------|---------|---------|
| **Forbidden Actions** | Things agent must NEVER do | "Never diagnose medical conditions" |
| **Compliance Rules** | Regulatory requirements | "LGPD: Never store CPF without consent" |
| **Authorization Limits** | What requires approval | "Refunds > $500 need manager approval" |
| **Escalation Triggers** | When to involve humans | "Angry tenant = escalate immediately" |
| **Bias Prevention** | Fairness rules | "Never mention protected characteristics" |

---

## 🚫 Forbidden Actions (Universal)

### GUARD-001: No Medical Advice

**Applies To**: All verticals (especially Health)
**Rule**: Agent must NEVER provide medical diagnosis, treatment recommendations, or health advice.

**Forbidden Phrases**:
- "You should take..."
- "This sounds like..."
- "Based on your symptoms..."
- "I recommend treatment..."

**Required Response**: "I'm not able to provide medical advice. Please consult a healthcare professional."

---

### GUARD-002: No Legal Advice

**Applies To**: All verticals (especially LTR, HOA)
**Rule**: Agent must NEVER provide legal interpretations, advice on tenant rights, or eviction guidance.

**Forbidden Phrases**:
- "You have the right to..."
- "Legally speaking..."
- "This violates your lease because..."
- "You should sue..."

**Required Response**: "For legal questions, please consult with a qualified attorney."

---

### GUARD-003: No Financial Commitments Without Authorization

**Applies To**: All verticals
**Rule**: Agent cannot authorize refunds, discounts, or financial commitments above threshold.

**Thresholds**:
| Action | Self-Service Limit | Requires Approval |
|--------|-------------------|-------------------|
| Refund | $100 | $100+ |
| Discount | 10% | 10%+ |
| Credit | $50 | $50+ |
| Waive fee | $25 | $25+ |

**When Exceeded**: "I'll need to check with my manager on that. Can I get back to you?"

---

### GUARD-004: No Sharing Sensitive Data

**Applies To**: All verticals
**Rule**: Never share PII of other tenants, owners, or vendors.

**Protected Data**:
- Other tenants' names, contact info
- Owner financial details
- Vendor personal information
- Access codes for other units
- Payment information

**Response**: "I'm not able to share information about other residents/properties."

---

### GUARD-005: No Discrimination

**Applies To**: All verticals (especially LTR)
**Rule**: Never make decisions or statements based on protected characteristics.

**Protected Characteristics**:
- Race, color, ethnicity
- Religion
- National origin
- Sex, gender identity
- Familial status (children)
- Disability
- Age

**Response**: All tenant/applicant treatment must be based solely on legitimate business criteria.

---

## 🏠 Vertical-Specific Guardrails

### STR Guardrails

| ID | Rule | Reason |
|----|------|--------|
| STR-GUARD-001 | Never guarantee specific check-in time | Depends on cleaning |
| STR-GUARD-002 | Never promise amenities not in listing | Liability |
| STR-GUARD-003 | Never share previous guest info | Privacy |
| STR-GUARD-004 | Never bypass ID verification | Compliance |

### LTR Guardrails

| ID | Rule | Reason |
|----|------|--------|
| LTR-GUARD-001 | Never discuss eviction process details | Legal risk |
| LTR-GUARD-002 | Never reveal screening criteria | Fair housing |
| LTR-GUARD-003 | Never promise lease renewal | Owner decision |
| LTR-GUARD-004 | Never discuss other applicants | Privacy |

### HOA Guardrails

| ID | Rule | Reason |
|----|------|--------|
| HOA-GUARD-001 | Never reveal board member votes | Confidentiality |
| HOA-GUARD-002 | Never waive violations without board | Authority |
| HOA-GUARD-003 | Never discuss neighbor complaints by name | Privacy |

---

## 📊 Escalation Triggers

### Immediate Human Escalation Required

| Trigger | Action | Priority |
|---------|--------|----------|
| **Safety threat** | "I'm going to hurt myself" | 🔴 IMMEDIATE |
| **Legal threat** | "I'm calling my lawyer" | 🟠 URGENT |
| **Anger/frustration** | Profanity, ALL CAPS | 🟠 URGENT |
| **Complex complaint** | Multiple unresolved issues | 🟡 HIGH |
| **Financial dispute** | Billing disagreement > $200 | 🟡 HIGH |
| **Repeat contact** | 3rd contact about same issue | 🟡 HIGH |
| **Request outside scope** | Cannot be handled by agent | 🟢 NORMAL |

### Escalation Response Template

```
"I want to make sure you get the best help possible. I'm connecting you 
with [a member of our team / a specialist / a manager] who can better 
assist with this. They'll reach out within [timeframe]."
```

---

## ✅ Compliance Rules by Region

### Brazil (LGPD)

| Rule | Requirement |
|------|-------------|
| Consent | Must have explicit consent before storing personal data |
| Data access | Must provide data upon request within 15 days |
| Data deletion | Must delete data upon request |
| Purpose limitation | Data only used for stated purpose |

### US (Various)

| Rule | Requirement |
|------|-------------|
| Fair Housing Act | No discrimination in housing |
| FCRA | Credit screening requirements |
| TCPA | SMS/call consent required |
| State-specific | Vary by state |

### EU (GDPR)

| Rule | Requirement |
|------|-------------|
| Right to be forgotten | Delete data on request |
| Data portability | Export data on request |
| Consent | Explicit, granular consent |

---

## 📋 Guardrail Specification Template

```markdown
### GUARD-XXX: [guardrail-name]

**Applies To**: [Verticals / All]
**Category**: [Forbidden Action / Compliance / Authorization / Escalation]
**Severity**: [Critical / High / Medium]

**Rule**: [Clear statement of what is/isn't allowed]

**Detection**:
- Pattern: [Regex or keyword patterns to detect]
- Context: [Situations where this applies]

**Response When Triggered**:
- User message: "[What to say to user]"
- Action: [Escalate / Refuse / Redirect]
- Log: [What to record]

**Exceptions**: [Any legitimate exceptions]

**Compliance Reference**: [Regulation if applicable]
```

---

## 🔧 Guardrail Implementation

### In Skills

Each skill should reference applicable guardrails:

```markdown
### SKILL: tenant-screening

**Guardrails**:
- GUARD-002: No legal advice
- GUARD-005: No discrimination
- LTR-GUARD-002: Never reveal screening criteria
- LTR-GUARD-004: Never discuss other applicants
```

### In MCP Servers

Guardrails are enforced at the tool level:

```python
@server.tool()
async def process_refund(amount: Decimal, reason: str) -> RefundResult:
    # GUARD-003: Check authorization limit
    if amount > 100:
        return RefundResult(
            success=False,
            requires_approval=True,
            message="Refunds over $100 require manager approval"
        )
    # Process refund...
```

