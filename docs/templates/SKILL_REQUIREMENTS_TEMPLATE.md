# SKILL REQUIREMENTS DOCUMENT

**Skill Name:** `[skill-name-kebab-case]`  
**Vertical:** `[LTR | STR | HOA | Health | Cinema]`  
**Owner:** `[Team/Person Name]`  
**Version:** `1.0`  
**Date:** `[YYYY-MM-DD]`  
**Status:** `[Draft | Review | Approved | Implemented]`

---

## 1. WHEN TO ACTIVATE

### Trigger Conditions
List the specific phrases, keywords, or contexts that should activate this skill:

- ✓ User mentions: `"keyword1"`, `"keyword2"`, `"keyword3"`
- ✓ User asks about: `[specific topic]`
- ✓ Context: `[required conditions, e.g., "active lease", "verified user"]`

### Do NOT Activate When
List scenarios where this skill should NOT be used (to prevent false positives):

- ✗ User mentions `[related but different topic]` → route to `[other-skill]`
- ✗ Context: `[conditions where this doesn't apply]`

---

## 2. BUSINESS LOGIC

### Overview
Brief description of what this skill does from a business perspective.

### Workflow Steps
Detailed step-by-step process the AI should follow:

**Step 1: [Action Name]**
- Condition: IF `[condition]` THEN `[action]`
- Retrieve: `[what data to get]`
- Validate: `[what to check]`

**Step 2: [Action Name]**
- Process: `[what calculation or logic to apply]`
- Decision: IF `[condition]` THEN `[path A]` ELSE `[path B]`

**Step 3: [Action Name]**
- Output: `[what to return to user]`
- Side effects: `[create ticket, send notification, etc.]`

### Decision Tree
```
User Message
    ├─ IF [condition A] → [Path A]
    ├─ IF [condition B] → [Path B]
    └─ ELSE → [Default Path]
```

---

## 3. REQUIRED DATA

### Input Data (from user message)
- `field_name` (type): description

### Database Queries
- `Table.field`: description
- `Table.field`: description

### External APIs
- `API Name`: what data to fetch

### Output Data
- `field_name` (type): description
- Format: `[JSON | text | structured response]`

---

## 4. BUSINESS RULES & CONSTRAINTS

### Business Rules
- Rule 1: `[Clear statement of rule]`
- Rule 2: `[Clear statement of rule]`

### Safety/Compliance Rules
- ⚠️ NEVER: `[prohibited action]`
- ⚠️ ALWAYS: `[required action]`
- ⚠️ MUST: `[compliance requirement]`

### SLAs (Service Level Agreements)
- Response time: `< X minutes`
- Resolution time: `< X hours`
- Accuracy target: `> X%`

### Compliance Requirements
- `[Regulation/Standard]`: `[specific requirement]`
- Data retention: `[period]`
- Audit logging: `[what to log]`

---

## 5. CONVERSATION EXAMPLES

### Example 1: [Happy Path]
**User:** `"[user message]"`

**Expected Response:**
```
[Exact format of response, including:
- Greeting/acknowledgment
- Information provided
- Actions taken
- Next steps
- Call to action]
```

### Example 2: [Edge Case]
**User:** `"[user message]"`

**Expected Response:**
```
[Response format]
```

### Example 3: [Multi-Turn]
**User:** `"[initial message]"`

**Assistant:** `"[response]"`

**User:** `"[follow-up]"`

**Assistant:** `"[final response]"`

---

## 6. EDGE CASES & EXCEPTIONS

### Edge Case 1: [Name]
**Scenario:** `[description]`  
**Handling:** `[what to do]`  
**Escalation:** `[when/how to escalate]`

### Edge Case 2: [Name]
**Scenario:** `[description]`  
**Handling:** `[what to do]`

### Error Handling
- Missing data: `[fallback behavior]`
- API failure: `[fallback behavior]`
- Ambiguous input: `[clarification strategy]`

---

## 7. SUCCESS METRICS

### KPIs (Key Performance Indicators)
- Metric 1: `[name]` → Target: `[value]`
- Metric 2: `[name]` → Target: `[value]`

### Quality Metrics
- Accuracy: `[how to measure]`
- User satisfaction: `[how to measure]`
- Completion rate: `[definition]`

### Monitoring
- Track: `[what events to log]`
- Alert on: `[failure conditions]`
- Review: `[frequency of analysis]`

---

## 8. IMPLEMENTATION NOTES

### Required Scripts
1. `script_name.py`
   - **Purpose:** `[what it does]`
   - **Input:** `field_name (type): description`
   - **Output:** `field_name (type): description`
   - **Logic:** Brief description of algorithm/calculation

2. `script_name.py`
   - **Purpose:** `[what it does]`
   - **Input:** `[parameters]`
   - **Output:** `[return value]`

### Database Changes
- **Table:** `table_name`
  - Add column: `column_name (TYPE)`: description
  - Add index: `index_name` on `column_name`

### External Integrations
- **Service:** `[API/Service Name]`
  - Endpoint: `[URL]`
  - Auth: `[method]`
  - Rate limit: `[limit]`

### Dependencies
- Requires skills: `[other-skill-names]`
- Requires services: `[external-services]`

---

## 9. TESTING & VALIDATION

### Test Scenarios
1. **Test:** `[scenario name]`
   - **Given:** `[context]`
   - **When:** `[action]`
   - **Then:** `[expected result]`

2. **Test:** `[scenario name]`
   - **Given:** `[context]`
   - **When:** `[action]`
   - **Then:** `[expected result]`

### Validation Criteria
- [ ] All trigger conditions tested
- [ ] All edge cases handled
- [ ] All safety rules enforced
- [ ] All KPIs measurable
- [ ] All scripts implemented
- [ ] All database changes applied

---

## 10. APPENDIX

### Stakeholder Interview Transcript
```
[Paste relevant excerpts from interviews with SMEs, landlords, users, etc.]
```

### Reference Materials
- Document: `[name/link]`
- Document: `[name/link]`

### Change Log
| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-01-04 | BA Name | Initial draft |

---

## APPROVAL

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Business Owner | | | |
| Product Manager | | | |
| Compliance Officer | | | |
| Technical Lead | | | |

