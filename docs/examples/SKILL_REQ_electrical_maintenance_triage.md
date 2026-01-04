# SKILL REQUIREMENTS DOCUMENT

**Skill Name:** `electrical-maintenance-triage`  
**Vertical:** `LTR (Long-Term Rentals)`  
**Owner:** Property Operations Team  
**Version:** 1.0  
**Date:** 2026-01-04  
**Status:** Approved

---

## 1. WHEN TO ACTIVATE

### Trigger Conditions
- ✓ Tenant mentions: `"electricity"`, `"eletricidade"`, `"power"`, `"energia"`, `"luz"`
- ✓ Tenant reports: `"lights out"`, `"sem luz"`, `"breaker"`, `"disjuntor"`, `"outlet"`, `"tomada"`, `"shock"`, `"choque"`, `"sparks"`, `"faíscas"`
- ✓ Tenant asks about: electrician, electrical panel, circuit breaker
- ✓ Context: User has active lease AND property has electrical_info on file

### Do NOT Activate When
- ✗ User asking about electricity BILL → route to `billing-support` skill
- ✗ User asking about energy efficiency tips → route to `resident-support` skill
- ✗ User reporting appliance malfunction → route to `appliance-maintenance` skill

---

## 2. BUSINESS LOGIC

### Overview
Triage electrical issues reported by tenants, provide immediate safety guidance, share electrical panel information, and dispatch licensed electrician based on urgency level.

### Workflow Steps

**Step 1: Classify Urgency Level**

Use `classify_urgency.py` to analyze tenant's message for danger keywords.

- **EMERGENCY** (dispatch immediately, instruct to call 911)
  - IF message contains: `"sparks"`, `"fire"`, `"burning smell"`, `"smoke"`, `"shock"`, `"buzzing sound"`, `"arc"`
  - Response time: < 5 minutes
  - Action: Instruct tenant to evacuate, call 911, then dispatch electrician

- **URGENT** (dispatch same-day, <2 hours)
  - IF message contains: `"no power"`, `"breaker tripped"`, `"lights out"`, `"complete outage"`
  - Response time: < 15 minutes
  - Action: Provide panel location, offer reset guidance (if safe), dispatch electrician

- **STANDARD** (schedule within 24-48 hours)
  - IF message contains: `"outlet not working"`, `"light fixture broken"`, `"dimming lights"`, `"switch broken"`
  - Response time: < 1 hour
  - Action: Acknowledge issue, schedule electrician visit

**Step 2: Retrieve Property Electrical Information**

Use `get_electrical_info.py --property_id {{ property_id }}`

Returns:
```json
{
  "panel_location": "Basement near water heater",
  "panel_instructions": "Main breaker is at the top, labeled switches below",
  "electrician_name": "João Silva",
  "electrician_phone": "+55 11 98765-4321",
  "electrician_emergency_phone": "+55 11 91234-5678",
  "license_number": "CREA-SP-123456",
  "last_inspection_date": "2025-12-15"
}
```

**Step 3: Provide Safety Guidance (Emergency Only)**

IF urgency == "emergency":
- Instruct tenant to LEAVE the area immediately
- Do NOT touch any switches, outlets, or the panel
- Call 193 (fire department) immediately
- Do NOT attempt to fix anything
- Wait outside until help arrives

**Step 4: Provide Panel Information (Urgent/Standard Only)**

IF urgency == "urgent" OR "standard":
- Share panel location
- IF urgency == "urgent" AND issue == "breaker tripped":
  - Provide reset instructions
  - Ask tenant if they feel comfortable attempting reset
  - IF tenant says no → proceed to electrician dispatch

**Step 5: Dispatch Electrician**

Use `dispatch_electrician.py --property_id {{ property_id }} --urgency {{ urgency }} --issue "{{ tenant_message }}"`

- **Emergency:** Call electrician immediately, confirm ETA, send SMS with address + urgency
- **Urgent:** Send SMS to electrician, request 2-4 hour ETA, confirm via return SMS
- **Standard:** Create appointment for next business day (10 AM - 2 PM window)

**Step 6: Create Maintenance Ticket**

Use `create_maintenance_ticket.py` with:
```json
{
  "property_id": "{{ property_id }}",
  "tenant_id": "{{ tenant_id }}",
  "issue_type": "electrical",
  "urgency": "{{ urgency }}",
  "description": "{{ tenant_message }}",
  "electrician_dispatched": true,
  "electrician_name": "{{ electrician_name }}",
  "estimated_arrival": "{{ eta }}",
  "safety_notes": "{{ if emergency: safety warnings }}"
}
```

Returns: `{"ticket_id": "M-2026-0123", "created_at": "2026-01-04T14:32:00Z"}`

**Step 7: Confirm with Tenant**

Provide structured response (see templates in Section 5) including:
- Acknowledgment of issue
- Safety instructions (if applicable)
- Panel location (if applicable)
- Electrician details (name, phone, ETA)
- Ticket number for reference
- Request for confirmation/follow-up

**Step 8: Set Follow-Up Reminder**

- Emergency: Check back in 1 hour
- Urgent: Check back in 4 hours
- Standard: Check back in 24 hours

---

## 3. REQUIRED DATA

### Input Data (from user message)
- `tenant_message` (string): Full text of tenant's report
- `tenant_id` (UUID): From session context
- `property_id` (UUID): From tenant's active lease

### Database Queries
- `properties.electrical_panel_location` (TEXT): Where the panel is located
- `properties.electrical_panel_instructions` (TEXT): How to access/reset
- `properties.electrician_name` (TEXT): Name of assigned electrician
- `properties.electrician_phone` (TEXT): Contact number
- `properties.electrician_emergency_phone` (TEXT): After-hours emergency contact
- `leases.tenant_id` → `tenants.phone` (TEXT): For SMS confirmations

### External APIs
- **Twilio SMS API**: Send dispatch notification to electrician
- **Google Maps API** (optional): Generate directions link for electrician

### Output Data
- `ticket_id` (string): Maintenance ticket reference number
- `urgency_level` (enum): emergency | urgent | standard
- `electrician_dispatched` (boolean): Whether electrician was notified
- `eta` (ISO8601 datetime): Expected arrival time
- `safety_warning_given` (boolean): Whether 911 was mentioned

---

## 4. BUSINESS RULES & CONSTRAINTS

### Business Rules
- All electrical issues MUST be handled by licensed electrician (never DIY)
- Emergency electrician dispatch requires landlord SMS confirmation if after 10 PM
- Standard maintenance cannot be scheduled on weekends (unless tenant requests)
- Repeat electrical issues within 7 days must mention "REPEAT ISSUE" in electrician dispatch

### Safety/Compliance Rules
- ⚠️ NEVER instruct tenant to touch electrical panel if:
  - Sparks present
  - Burning smell detected
  - Visible damage to panel
  - Water near panel
  - Buzzing/humming sounds
  
- ⚠️ ALWAYS prioritize life safety:
  - Instruct to call 911 for fire/smoke/shock
  - Instruct to evacuate if danger present
  - Never minimize emergency situations

- ⚠️ MUST validate electrician license is active (checked during property onboarding)

### SLAs (Service Level Agreements)
- **Emergency Response:** < 5 minutes to tenant, electrician on-site < 60 minutes
- **Urgent Response:** < 15 minutes to tenant, electrician on-site < 4 hours
- **Standard Response:** < 60 minutes to tenant, electrician on-site < 48 hours
- **Electrician Availability:** Must have backup electrician if primary unavailable

### Compliance Requirements
- **NR-10 (Brazil):** All electrical work must be performed by certified professionals
- **Data Retention:** Maintain all electrical maintenance records for 5 years (liability)
- **Audit Logging:** Log all emergency dispatches with timestamps and tenant acknowledgments
- **Liability Protection:** Document tenant refusal if they decline to evacuate during emergency

---

## 5. CONVERSATION EXAMPLES

### Example 1: EMERGENCY - Sparks and Burning Smell
**Tenant:** "Socorro! Tô vendo faíscas saindo de uma tomada e tem cheiro de queimado!"

**Expected Response:**
```
🚨 EMERGÊNCIA - SAIA DO LOCAL AGORA!

Por favor, siga estas instruções IMEDIATAMENTE:

1. 🚪 SAIA do cômodo AGORA e feche a porta
2. 📞 Ligue 193 (Bombeiros) IMEDIATAMENTE
3. ⚠️ NÃO toque em NENHUM interruptor ou tomada
4. 🚫 NÃO tente desligar o disjuntor
5. 🏃 Mantenha-se afastado até os bombeiros chegarem

🔧 ELETRICISTA EMERGENCIAL JÁ DESPACHADO:
📞 João Silva - (11) 98765-4321
⏰ Chegada estimada: 20-30 minutos

📋 Chamado emergencial criado: #M-2026-0123
⚡ Registrado às 14:32 como PRIORIDADE MÁXIMA

VOCÊ ESTÁ SEGURO? VOCÊ JÁ SAIU DO LOCAL?
Por favor, confirme sua segurança agora.
```

### Example 2: URGENT - Power Outage
**Tenant:** "Hi, all the power in my apartment just went out. Nothing is working."

**Expected Response:**
```
Entendo sua situação. Vou te ajudar a resolver isso rapidamente.

📍 LOCALIZAÇÃO DO QUADRO ELÉTRICO:
Seu disjuntor fica no subsolo, próximo ao aquecedor de água.

🔧 TESTE RÁPIDO:
Se você se sentir confortável, pode verificar se algum disjuntor está desligado (alavanca para baixo). Se estiver, empurre gentilmente para cima para religar.

⚠️ SE NÃO SE SENTIR SEGURO: Não faça nada, já chamei ajuda!

🔌 ELETRICISTA A CAMINHO:
📞 João Silva - (11) 98765-4321
⏰ Chegada estimada: 2-4 horas (hoje, antes das 18h)

📋 Chamado criado: #M-2026-0124
📱 João vai te ligar 30min antes de chegar.

Você quer tentar verificar o disjuntor ou prefere esperar o eletricista?
```

### Example 3: STANDARD - Single Outlet Not Working
**Tenant:** "One of the outlets in my bedroom stopped working yesterday. Not urgent but wanted to report it."

**Expected Response:**
```
Obrigado por avisar! Vou agendar o eletricista para verificar.

📋 CHAMADO CRIADO: #M-2026-0125
🔧 Eletricista: João Silva
📞 Contato: (11) 98765-4321
📅 Agendado para: Terça-feira, 6 de janeiro
⏰ Horário: Entre 10h e 14h

João vai te ligar 30 minutos antes de chegar.

Algumas perguntas rápidas para ajudar o João:
1. Alguma outra tomada no mesmo cômodo também não funciona?
2. Há algum eletrodoméstico conectado que parou de funcionar?
3. Você prefere manhã ou tarde?
```

### Example 4: Multi-Turn - Tenant Hesitant About Reset
**Tenant:** "The lights in the living room went out."

**Assistant:**
```
Vou te ajudar! Primeiro, vamos verificar se é só na sala ou em outros cômodos também.

Outros cômodos estão com luz?
```

**Tenant:** "Yes, just the living room is dark. Everything else works."

**Assistant:**
```
Perfeito, provavelmente é um disjuntor específico.

📍 Seu quadro de disjuntores fica no subsolo, próximo ao aquecedor.

Você se sente confortável em ir lá verificar se há algum disjuntor desligado? É seguro, só precisa olhar se alguma alavanca está para baixo.

Se preferir, posso chamar o eletricista direto!
```

**Tenant:** "I'm not sure, I've never done that before. Can you just send someone?"

**Assistant:**
```
Claro! Melhor ter ajuda profissional mesmo.

🔌 ELETRICISTA A CAMINHO:
📞 João Silva - (11) 98765-4321
⏰ Chegada estimada: 2-4 horas (hoje)

📋 Chamado: #M-2026-0126

João é super experiente e vai resolver rapidinho. Ele vai te ligar meia hora antes de chegar.

Enquanto isso, se a luz voltar sozinha, me avise que eu cancelo a visita!
```

---

## 6. EDGE CASES & EXCEPTIONS

### Edge Case 1: No Electrician on File
**Scenario:** Property missing `electrician_name` or `electrician_phone` in database

**Handling:**
1. Apologize: "Desculpe, estou tendo dificuldade em acessar as informações do eletricista."
2. Escalate immediately: Send SMS to property manager with HIGH priority
3. Provide interim response: "Já acionei o gerente da propriedade. Você receberá contato em até 15 minutos."
4. Log error for operations team

**Escalation:**
- Send to property manager: "URGENT: Tenant at {{ property_address }} reported electrical issue. No electrician on file. Immediate action required."

### Edge Case 2: After-Hours Emergency (10 PM - 6 AM)
**Scenario:** Emergency electrical issue reported outside business hours

**Handling:**
1. Still prioritize life safety (911 instructions)
2. Use `electrician_emergency_phone` (after-hours number)
3. Send SMS to landlord: "Emergency electrical dispatch at {{ address }}. Electrician: {{ name }}. Estimated cost: ${{ emergency_rate }}/hour. Reply YES to confirm."
4. Wait for landlord confirmation (max 5 minutes)
5. IF no confirmation within 5 min → dispatch anyway, document in ticket

### Edge Case 3: Tenant Reports Issue Resolved
**Scenario:** Before electrician arrives, tenant says "Never mind, it's working now"

**Handling:**
1. Ask clarifying question: "Ótimo! O que aconteceu? Você conseguiu religar o disjuntor ou a luz voltou sozinha?"
2. Document resolution method
3. Ask: "Quer que eu mantenha o agendamento do eletricista para uma verificação de segurança, ou prefere cancelar?"
4. IF cancel: Update ticket status to "resolved_by_tenant", cancel electrician dispatch
5. IF keep: Proceed with appointment

### Edge Case 4: Repeat Issue Within 7 Days
**Scenario:** Query database shows previous electrical ticket for same property < 7 days ago

**Handling:**
1. Retrieve previous ticket: `#M-2026-XXXX`
2. Add context to electrician dispatch: "ATENÇÃO: Problema recorrente. Último chamado: {{ date }}. Descrição anterior: {{ previous_description }}. Considere inspeção mais detalhada."
3. Mention to tenant: "Notei que você teve um problema elétrico em {{ date }}. Vou garantir que o João faça uma verificação completa para evitar que isso se repita."
4. Escalate to property manager if 3+ issues in 30 days

### Edge Case 5: Tenant Not Fluent in Portuguese/English
**Scenario:** Tenant sends message in another language (Spanish, Mandarin, etc.)

**Handling:**
1. Detect language of incoming message
2. Respond in SAME language using LLM translation
3. Safety instructions MUST be translated (critical for emergency)
4. Notify electrician: "Tenant speaks {{ language }}. Consider bringing translator or using Google Translate."

### Edge Case 6: Electrician Unavailable/No Response
**Scenario:** Electrician does not confirm dispatch SMS within 15 minutes (emergency/urgent)

**Handling:**
1. Attempt phone call to electrician
2. If no answer, contact backup electrician (should be in database: `backup_electrician_phone`)
3. Inform tenant of delay: "Estou confirmando disponibilidade do eletricista. Você terá atualização em 10 minutos."
4. Alert property manager if both electricians unavailable

---

## 7. SUCCESS METRICS

### KPIs (Key Performance Indicators)
- **Emergency Response Time:** < 5 minutes (P95) → Target: 100% compliance
- **Urgent Response Time:** < 15 minutes (P95) → Target: 98% compliance
- **Standard Response Time:** < 60 minutes (P95) → Target: 95% compliance
- **Electrician On-Site (Emergency):** < 60 minutes → Target: 90% compliance
- **Electrician On-Site (Urgent):** < 4 hours → Target: 95% compliance
- **Electrician On-Site (Standard):** < 48 hours → Target: 98% compliance

### Quality Metrics
- **Dispatch Accuracy:** Correct urgency classification → Target: > 97%
- **False Positive Rate:** Incorrectly classified as emergency → Target: < 3%
- **Tenant Satisfaction:** Post-resolution survey score → Target: > 4.5/5
- **First-Time Fix Rate:** Issue resolved on first visit → Target: > 85%

### Monitoring
- **Track:** Every activation of this skill (log to `skill_activations` table)
- **Track:** Urgency classification distribution (emergency vs urgent vs standard)
- **Track:** Average electrician response time by urgency level
- **Alert on:** 
  - Emergency response time > 10 minutes
  - Electrician no-show
  - 3+ repeat issues same property within 30 days
- **Review:** Weekly dashboard review by operations team
- **Review:** Monthly trend analysis (are issues increasing?)

---

## 8. IMPLEMENTATION NOTES

### Required Scripts

1. **`classify_urgency.py`**
   - **Purpose:** Analyze tenant message to determine urgency level
   - **Input:** 
     - `message` (string): Tenant's report
   - **Output:** 
     ```json
     {
       "urgency": "emergency | urgent | standard",
       "danger_keywords": ["sparks", "fire"],
       "confidence": 0.95,
       "reasoning": "Message contains fire/shock hazard keywords"
     }
     ```
   - **Logic:** 
     - Use regex pattern matching for danger keywords
     - Emergency: sparks, fire, smoke, shock, burning, arc, buzzing
     - Urgent: no power, breaker tripped, outage, lights out
     - Standard: outlet not working, switch broken, dim lights

2. **`get_electrical_info.py`**
   - **Purpose:** Retrieve electrical panel information and electrician details for a property
   - **Input:** 
     - `property_id` (UUID): Property identifier
   - **Output:** 
     ```json
     {
       "panel_location": "Basement near water heater",
       "panel_instructions": "Main breaker at top, labeled switches below",
       "electrician_name": "João Silva",
       "electrician_phone": "+55 11 98765-4321",
       "electrician_emergency_phone": "+55 11 91234-5678",
       "license_number": "CREA-SP-123456",
       "backup_electrician_name": "Maria Santos",
       "backup_electrician_phone": "+55 11 95555-1234"
     }
     ```
   - **Logic:** 
     - Query `properties` table
     - Validate electrician license is not expired (warn if < 30 days)
     - Return error if missing required fields

3. **`dispatch_electrician.py`**
   - **Purpose:** Send dispatch notification to electrician via SMS, calculate ETA
   - **Input:** 
     - `property_id` (UUID): Property identifier
     - `urgency` (string): emergency | urgent | standard
     - `issue_description` (string): Tenant's report
     - `tenant_phone` (string): For electrician to call ahead
   - **Output:** 
     ```json
     {
       "dispatched": true,
       "sms_sent": true,
       "electrician_name": "João Silva",
       "eta": "2026-01-04T16:30:00Z",
       "confirmation_received": false
     }
     ```
   - **Logic:** 
     - Emergency: SMS + phone call, ETA = current_time + 60 minutes
     - Urgent: SMS only, ETA = current_time + 3 hours
     - Standard: Schedule for next business day 10 AM - 2 PM
     - Use Twilio to send SMS: "URGENTE: {{ address }}. Problema: {{ description }}. Inquilino: {{ phone }}. ETA esperado: {{ eta }}. Confirme recebimento."

4. **`create_maintenance_ticket.py`**
   - **Purpose:** Create maintenance ticket in database
   - **Input:** 
     - `property_id` (UUID)
     - `tenant_id` (UUID)
     - `issue_type` (string): "electrical"
     - `urgency` (string)
     - `description` (string)
     - `electrician_dispatched` (boolean)
     - `electrician_name` (string)
     - `estimated_arrival` (ISO8601 datetime)
   - **Output:** 
     ```json
     {
       "ticket_id": "M-2026-0123",
       "created_at": "2026-01-04T14:32:00Z",
       "status": "dispatched"
     }
     ```
   - **Logic:** 
     - Generate ticket ID: "M-{YEAR}-{sequential_number}"
     - Insert into `maintenance_tickets` table
     - Set status based on urgency: emergency → "critical", urgent → "active", standard → "scheduled"
     - Create audit log entry

### Database Changes

**Table:** `properties`
- Add columns:
  - `electrical_panel_location` (TEXT): Location description
  - `electrical_panel_instructions` (TEXT, nullable): How to reset breaker
  - `electrician_name` (TEXT): Primary electrician name
  - `electrician_phone` (TEXT): Primary contact
  - `electrician_emergency_phone` (TEXT): After-hours contact
  - `electrician_license_number` (TEXT): Professional license
  - `electrician_license_expiry` (DATE): License expiration
  - `backup_electrician_name` (TEXT, nullable): Backup electrician
  - `backup_electrician_phone` (TEXT, nullable): Backup contact

**Table:** `maintenance_tickets`
- Already exists, confirm columns:
  - `id` (UUID, PK)
  - `ticket_number` (TEXT, unique): Human-readable ID
  - `property_id` (UUID, FK)
  - `tenant_id` (UUID, FK)
  - `issue_type` (TEXT): "electrical", "plumbing", "hvac", etc.
  - `urgency` (TEXT): "emergency", "urgent", "standard"
  - `description` (TEXT): Tenant's report
  - `status` (TEXT): "critical", "active", "scheduled", "resolved", "cancelled"
  - `electrician_dispatched` (BOOLEAN)
  - `electrician_name` (TEXT, nullable)
  - `estimated_arrival` (TIMESTAMP, nullable)
  - `actual_arrival` (TIMESTAMP, nullable)
  - `resolution_notes` (TEXT, nullable)
  - `created_at` (TIMESTAMP)
  - `updated_at` (TIMESTAMP)
  - `resolved_at` (TIMESTAMP, nullable)

**Table:** `skill_activations` (new)
- Purpose: Track every time this skill is activated for analytics
- Columns:
  - `id` (UUID, PK)
  - `skill_name` (TEXT): "electrical-maintenance-triage"
  - `tenant_id` (UUID, FK)
  - `property_id` (UUID, FK)
  - `urgency_classified` (TEXT)
  - `ticket_created` (UUID, FK to maintenance_tickets)
  - `response_time_seconds` (INTEGER): Time to first response
  - `electrician_dispatched` (BOOLEAN)
  - `activated_at` (TIMESTAMP)

### External Integrations

**Twilio SMS API** (already exists in UnifiedOS)
- Endpoint: `https://api.twilio.com/2010-04-01/Accounts/{AccountSid}/Messages.json`
- Auth: Basic (Account SID + Auth Token)
- Rate limit: 100 messages/second
- Use for: Electrician dispatch SMS, landlord notifications

**Google Maps API** (optional enhancement)
- Endpoint: `https://maps.googleapis.com/maps/api/directions/json`
- Use for: Generate directions link for electrician
- Format: `https://www.google.com/maps/dir/?api=1&destination={{ property_address }}`

### Dependencies
- **Requires skills:** 
  - `unifiedos-common` (WhatsApp messaging, DB access, audit logging)
  - `memory-management` (to check for repeat issues)
  
- **Requires services:** 
  - Twilio (SMS)
  - PostgreSQL (property data, tickets)

---

## 9. TESTING & VALIDATION

### Test Scenarios

1. **Test:** Emergency classification and 911 instruction
   - **Given:** Tenant message contains "sparks" and "burning smell"
   - **When:** Skill is activated
   - **Then:** 
     - Classified as "emergency"
     - Response includes "SAIA DO LOCAL" and "Ligue 193"
     - Electrician dispatched to emergency_phone
     - Ticket created with status "critical"
     - Response time < 5 seconds

2. **Test:** Urgent with successful DIY reset
   - **Given:** Tenant reports "power out", property has panel_instructions
   - **When:** Skill is activated and tenant says "I tried and it worked"
   - **Then:**
     - Classified as "urgent"
     - Panel location shared
     - Reset instructions provided
     - Tenant confirms resolution
     - Ticket marked "resolved_by_tenant"
     - Electrician dispatch cancelled

3. **Test:** Standard with scheduling
   - **Given:** Tenant reports "one outlet not working" on Tuesday 3 PM
   - **When:** Skill is activated
   - **Then:**
     - Classified as "standard"
     - Electrician scheduled for Wednesday 10 AM - 2 PM
     - Ticket status "scheduled"
     - SMS sent to electrician
     - Response time < 60 seconds

4. **Test:** Missing electrician data (edge case)
   - **Given:** Property has no `electrician_phone` in database
   - **When:** Skill is activated
   - **Then:**
     - Error detected
     - Fallback message: "Acionando gerente..."
     - Property manager notified via SMS
     - Ticket created with flag "missing_electrician_data"
     - Error logged for ops team

5. **Test:** Repeat issue within 7 days
   - **Given:** Property has electrical ticket from 3 days ago
   - **When:** New electrical issue reported
   - **Then:**
     - Previous ticket retrieved
     - Electrician dispatch includes "REPEAT ISSUE" note
     - Tenant informed of previous issue
     - Property manager notified if 3rd occurrence

6. **Test:** After-hours emergency
   - **Given:** Emergency reported at 11 PM
   - **When:** Skill is activated
   - **Then:**
     - Emergency procedures followed
     - `electrician_emergency_phone` called
     - Landlord SMS sent requesting approval
     - If no approval in 5 min, proceed anyway
     - Extra charge noted in ticket

### Validation Criteria
- [x] All trigger conditions tested (electricity keywords, urgency levels)
- [x] All edge cases handled (missing data, after-hours, repeats)
- [x] All safety rules enforced (911 for fire, evacuation instructions)
- [x] All KPIs measurable (response time, dispatch accuracy)
- [x] All scripts implemented and unit tested
- [x] All database changes applied with migrations
- [x] Integration with Twilio SMS tested
- [x] End-to-end test with real tenant conversation
- [x] Load test: 100 concurrent activations

---

## 10. APPENDIX

### Stakeholder Interview Transcript
```
Interview Date: 2026-01-04
Interviewer: Business Analyst (Maria Santos)
Interviewee: Landlord (Carlos Mendes), 15 years experience, 12 properties

BA: Can you walk me through how you currently handle electrical issues?

Landlord: "So when a tenant messages about electricity, first thing I need to know 
is if it's an emergency. Like, if they say sparks or fire, that's drop everything. 
I tell them to get out and call 911, then I call my electrician João right away. 
He's on call 24/7 for emergencies, but I pay him triple rate after 10 PM, so I 
try to confirm it's really an emergency before calling him late.

If it's just like, the power's out, I tell them where the panel is - for my 
properties it's usually in the basement near the water heater - and sometimes they 
can just flip the breaker themselves. But if not, I send João. He's pretty fast, 
usually gets there in 2-3 hours unless it's rush hour.

For small stuff, like an outlet not working, I schedule João for the next day or 
two. No rush. He charges $120 for a regular visit, so I try to batch multiple 
small things if possible.

Oh, and I always keep track of these in a spreadsheet so I can follow up. 
Sometimes tenants forget to tell me it's fixed, and João shows up for nothing, 
which wastes his time and my money."

BA: What information do you provide to the tenant when you respond?

Landlord: "Panel location for sure - they never remember where it is. João's 
number in case they want to call him directly, though I prefer they go through 
me. And an ETA so they know when to be home. João is good about calling them 30 
minutes before he arrives."

BA: Any safety concerns or legal issues I should know about?

Landlord: "Yeah, I never want them messing with the panel if there's smoke or 
sparks. That's dangerous. Just get out. Also, I need to keep records of all 
electrical work for insurance purposes - they asked me for it once when a tenant 
filed a claim. And João has to be licensed, obviously. His license is through 
CREA-SP and it's good until 2028."

BA: What about repeat issues?

Landlord: "That's a red flag. If the same property has electrical problems more 
than twice in a month, something is wrong. Could be old wiring, could be tenant 
overloading circuits. I had one property where the tenant was running three space 
heaters on one circuit and kept tripping the breaker. João had to explain to them 
about electrical load. So yeah, if it repeats, I want to know about it."

BA: What would make your life easier with this AI system?

Landlord: "If it could handle the triage - figure out if it's urgent or not - and 
automatically send João the address and details, that would save me so much time. 
I spend probably 2-3 hours a week just coordinating electricians, plumbers, HVAC 
guys. If the AI could do that and just loop me in for emergencies or weird 
situations, that'd be amazing."

BA: What about tenants who don't speak Portuguese well?

Landlord: "I have a few tenants from China and one from Venezuela. Google 
Translate is my friend [laughs]. But seriously, for safety stuff like electricity, 
I want to make sure they really understand. I've had João bring a translator app 
to a job once just to be safe."
```

### Reference Materials
- **NR-10 (Brazil Electrical Safety Standard):** https://www.gov.br/trabalho-e-previdencia/pt-br/assuntos/inspecao-do-trabalho/seguranca-e-saude-no-trabalho/normas-regulamentadoras/nr-10.pdf
- **CREA-SP Electrician Licensing:** https://www.creasp.org.br/
- **Residential Electrical Code (ABNT NBR 5410):** Brazilian standard for electrical installations

### Change Log
| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-01-04 | Maria Santos (BA) | Initial draft based on landlord interview |
| 1.1 | 2026-01-04 | Tech Lead review | Added script specifications, database schema |
| 1.2 | 2026-01-04 | Compliance Officer | Added NR-10 compliance notes, safety rules |
| 1.3 | 2026-01-04 | Product Manager | Approved for implementation, assigned to Sprint 8 |

---

## APPROVAL

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Business Owner (Landlord Rep) | Carlos Mendes | ✓ Approved | 2026-01-04 |
| Product Manager | Ana Silva | ✓ Approved | 2026-01-04 |
| Compliance Officer | Roberto Lima | ✓ Approved | 2026-01-04 |
| Technical Lead | Paulo Ferreira | ✓ Approved | 2026-01-04 |

