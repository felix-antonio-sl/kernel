# 08_Crisis_Management

**Versión:** 1.4.0 | **Estado:** Definitivo | **Audiencia:** C-level, Crisis Teams, Transformation Leaders

---

## §1. PROPÓSITO Y SCOPE

### Definición

**Crisis Management** en KERNEL es el conjunto de estructuras, procesos y decisiones necesarios para **estabilizar una organización** cuando indicadores críticos caen por debajo de umbrales de viabilidad (H_Score < 45 o cualquier observable < 30).

Este documento **consolida**:

- **P52 Crisis Governance Pattern** (estructura, dynamics, roles)
- **AP31-AP33** (antipatrones crisis: Theater, Forcing, Transforming During)
- **Path 1-2 Implementation** (triage emergency)
- **Activation triggers** (thresholds automáticos)

**Relación con Invariantes**:

- **I3 Trazabilidad**: Crisis Management conecta H_Score (D2) → Decisión activar (D3) → Governance structure (D1) → Actions (D4) → Outcomes medibles
- **I2 Ortogonalidad**: Crisis es **estado temporal** de operación, no dominio separado
- **I1 Minimalidad**: Necesario porque governance normal es insuficiente para crisis (decision latency incompatible con urgencia)

---

## §2. ACTIVATION TRIGGERS (CUÁNDO ACTIVAR)

### Thresholds Automáticos

```yaml
Crisis_Threshold_Primary:
  H_Score < 45 for 1 month
  → Activate Crisis Governance (P52)
  → Transition governance normal → emergency protocols

Crisis_Threshold_Observable_Based:
  ANY(O1-O8, IN1-IN3) < 30 for 2 weeks consecutive
  → Evaluate activation
  → Multiple observables < 30 → Mandatory activation

Existential_Threshold:
  H_Score < 15 OR
  O3_Capacidad < 15 (cash runway < 7 días) OR
  O2_Valor < 15 (mass customer defection) OR
  IN2_Salud_Talento < 15 (organizational knowledge collapse)
  → IMMEDIATE emergency triage (Path 1)
```

---

### Indicadores por Tipo de Crisis

#### Financial Crisis

```yaml
Activación_Mandatoria_Si:
  - Cash runway < 90 días (O3 < 30)
  - Burn rate accelerating >20% MoM
  - Payroll at risk dentro 30 días
  - Accounts payable >90 días aging >30% total
  - Credit lines exhausted

Severity_Levels:
  Severe (O3: 30-45): 30-90 días runway
  Critical (O3: 15-30): 7-30 días runway
  Existential (O3: 0-15): <7 días runway

Señal_Emission:
  IF O3 < 30 THEN Emit(Señal: "Financial_Crisis_P52")
  IF O3 < 15 THEN Emit(Señal: "Financial_Existential_Emergency")
```

---

#### Customer/Value Crisis

```yaml
Activación_Mandatoria_Si:
  Private_Context:
    - Churn > 20% annualized (O2 < 30)
    - NPS < 0 (promoters < detractors)
    - Key account losses (top 20% revenue at risk)
    - Product-market fit loss (demand collapse)
  
  Public_Context:
    - Service delivery failures > 20% (O2 < 30)
    - Citizen satisfaction < 40%
    - Legislative hearings or investigations active
    - Media sentiment 80%+ negative
    - Legitimacy crisis (trust index < 30%)

Severity_Levels:
  Severe (O2: 30-45): Churn 15-20%, service failures 10-20%
  Critical (O2: 15-30): Churn >20%, service failures >20%
  Existential (O2: 0-15): Mass defection >30%, service collapse

Señal_Emission:
  IF O2 < 30 THEN Emit(Señal: "Customer_Defection_Crisis_P52")
  IF O2 < 15 THEN Emit(Señal: "Market_Rejection_Existential")
```

---

#### Talent Crisis

```yaml
Activación_Mandatoria_Si:
  - Attrition > 25% annualized (I2 < 30)
  - High-performer exodus > 20%
  - Leadership team departures (C-level, VPs)
  - Engagement score < 40
  - Critical vacancies > 90 días unfilled
  - Flight risk: >50% top talent actively job hunting

Severity_Levels:
  Severe (I2: 30-45): Attrition 20-25%, engagement 40-50
  Critical (I2: 15-30): Attrition >25%, engagement 30-40
  Existential (I2: 0-15): Mass exodus >30% quarterly, leadership departures

Señal_Emission:
  IF I2 < 30 THEN Emit(Señal: "Talent_Exodus_Crisis_P52")
  IF I2 < 15 THEN Emit(Señal: "Organizational_Knowledge_Collapse")
```

---

#### Operational Crisis

```yaml
Activación_Recomendada_Si:
  - Incident rate spike 3× vs baseline
  - MTTR > 8 hours avg (vs <1 hr target)
  - Deployment frequency collapse (1/mes vs daily target)
  - Tech debt score > 70 (vs <30 target)
  - Velocity drop > 60% sustained

Severity: Típicamente correlaciona con IN3 (Eficiencia Flujo)
  
Nota: Operational crisis RARA VEZ es standalone
      Usualmente es CONSECUENCIA de otra crisis (financial, talent)
      Tratar síntoma operacional sin addressar root cause falla
```

---

## §3. P52 CRISIS GOVERNANCE PATTERN

### Structure: Crisis Team

```yaml
Team_Size: 5-7 personas (optimal span crisis decision-making)

Roles_Core:
  
  1. Executive_Sponsor:
     Authority: Overall accountability, single point decision final
     Skills: Leadership, strategic thinking, stakeholder management
     Time_Commitment: 60-80% durante crisis (daily participation)
     Selection: CEO, COO, o C-level con mandate board
  
  2. Operations_Lead:
     Authority: Service delivery continuity, customer/citizen satisfaction
     Skills: Operations expertise (BB2 Service Providers)
     Time_Commitment: 80%+ (operational decisions daily)
     Selection: COO, VP Operations, Service Delivery Lead
  
  3. Financial_Lead:
     Authority: Cash management, budget reallocation, cost controls
     Skills: Financial planning, treasury management
     Time_Commitment: 60-80%
     Selection: CFO, Finance Director
  
  4. Customer_Lead:
     Authority: Retention strategy, satisfaction recovery
     Skills: Customer success, account management (BB4 Sales/Relations)
     Time_Commitment: 60%+
     Selection: CCO, VP Customer Success, Head of Sales
  
  5. People_Lead:
     Authority: Talent retention, engagement interventions
     Skills: HR, organizational development
     Time_Commitment: 60%+
     Selection: CHRO, VP People, Talent Director
  
  6. Communications_Lead:
     Authority: Internal/external messaging, stakeholder updates
     Skills: Communications, PR, change management
     Time_Commitment: 40-60%
     Selection: CCO, Comms Director
  
  7. Legal/Compliance_Lead (as needed):
     Authority: Regulatory compliance, legal risk mitigation (BB5 Audit)
     Skills: Legal counsel, compliance
     Time_Commitment: 20-40% (on-call)
     Selection: General Counsel, Chief Compliance Officer

Selection_Criteria_All:
  - Authority real para tomar decisiones sin escalate (P1 Authority)
  - Domain expertise en su área
  - Disponibilidad daily (crisis requiere presencia continua)
  - Action orientation (bias towards decision, not analysis paralysis)
  - Credibility con stakeholders (pueden influir, persuadir)
  - Track record delivery bajo presión
```

---

### Dynamics: Ritmos Acelerados

#### Daily Morning Situation Meeting

```yaml
Timing: Same time every day (ej: 9:00am), non-negotiable attendance
Duration: 30-60 min (strict time-box, no overruns)

Agenda_Standard:
  
  1. Overnight_Developments (5 min):
     - Qué cambió desde evening meeting
     - Incidents, escalations, external events
  
  2. Vital_Signs_Update (10 min):
     - Observable readings (O1-O8, IN1-IN3)
     - H_Score trend (daily calculation crisis mode)
     - Key metrics: Cash runway, churn rate, attrition
     - Color coding: Green (stable), Yellow (concern), Red (critical)
  
  3. Priority_Actions_Today (20 min):
     - Top 3-5 actions must happen today
     - Owner assigned per action (DRI - Directly Responsible Individual)
     - Resources allocated
     - Blockers surfaced immediately
  
  4. Blockers_Escalations (15 min):
     - Issues requiring executive intervention
     - External dependencies blocking progress
     - Decisions needed from team
     - Protocol: <4 hrs for critical decisions
  
  5. Communication_Priorities (10 min):
     - What to communicate internally (staff)
     - What to communicate externally (customers, board, media)
     - Messaging consistency check

Output:
  - Action list published (Slack, email) within 15 min meeting end
  - Owners clear, deadlines today
  - Decision log updated (trazabilidad)
```

---

#### Daily Evening Progress Meeting

```yaml
Timing: End of day (ej: 5:00pm o 6:00pm)
Duration: 30 min strict

Agenda_Standard:
  
  1. Accomplishments_Today (10 min):
     - Actions completed from morning list
     - Wins (celebrate small progress, morale critical)
  
  2. Issues_Encountered (10 min):
     - Blockers not resolved
     - Surprises (negative developments)
     - Adjustments needed tomorrow
  
  3. Tomorrow_Priorities (5 min):
     - Top 3-5 actions for tomorrow (preview next morning)
  
  4. Overnight_Watch_Items (5 min):
     - Monitoring: What could go wrong overnight?
     - On-call: Who handles escalations?
     - Prepare: Data needed for morning meeting

Output:
  - Daily summary email (entire org transparency)
  - Tomorrow's draft agenda
  - Overnight monitoring activated
```

---

#### Weekly Deep Dive

```yaml
Timing: Mid-week (ej: Miércoles 2-5pm)
Duration: 2-3 hrs (longer horizon reflection)

Agenda_Standard:
  
  1. Week-over-Week_Vital_Signs (30 min):
     - Trend analysis 4 weeks (did we stabilize?)
     - Observable trajectories (improving, stable, degrading)
     - H_Score projection: When will we cross H>45?
  
  2. Progress_Stabilization_Plan (30 min):
     - 30-day stabilization plan review
     - % milestones completed
     - Adjustments needed
  
  3. Deep_Dive_Critical_Issue (60 min):
     - Pick 1 critical problem (rotating focus)
     - Root cause analysis (5 whys)
     - Options generation
     - Decision + action plan
  
  4. Next_Week_Priorities (30 min):
     - Strategic actions próxima semana
     - Resource reallocation if needed
     - Communication plan

Output:
  - Weekly report (board, investors if applicable)
  - Stabilization plan updated
  - Deep-dive RCA documented
```

---

### Decision Rights Crisis Mode

```yaml
Authority_Allocation:
  
  Executive_Sponsor (CEO/COO):
    Decisions:
      - Strategic direction crisis response
      - Major resources (>$100K or >10% budget)
      - Executive appointments/removals (if leadership issue)
      - Board/investor/political stakeholder communication
      - Media strategy (if public crisis)
    
    Time_Commitment: <4 hrs critical decisions, <24 hrs tactical
  
  Functional_Leads (CFO, CHRO, etc.):
    Decisions:
      - Within domain, up to thresholds ($10K-$50K typical)
      - Daily operational decisions (non-strategic)
      - Tactical resource shifts within budget
      - Team-level actions (hiring freeze, cost cuts)
    
    Time_Commitment: <2 hrs tactical, <8 hrs operational
  
  Team_Consensus (5-7 crisis team):
    Decisions:
      - Cross-functional issues (no clear owner)
      - Major policy changes (affect multiple domains)
      - Restructuring decisions (if needed post-stabilization)
      - Trade-offs (ej: cut costs vs maintain service quality)
    
    Process: Majority vote if consensus impossible (Sponsor breaks tie)
  
  Escalate_to_Board:
    Decisions:
      - Beyond crisis team authority (legal, fiduciary)
      - Capital structure changes (equity, debt)
      - Liquidation, bankruptcy, M&A distressed
      - CEO removal (if sponsor IS CEO, board takes over)

Delegation_Normal_to_Crisis:
  Normal: Decisions escalate up slowly (days-weeks)
  Crisis: Decisions de-escalate down rapidly (hours)
  
  Ejemplo:
    Normal: $50K purchase → VP approval (2 días)
    Crisis: $50K critical (cash flow) → CFO approval (2 hrs)
```

---

### Communication Protocols

```yaml
Internal_Communication:
  
  Frequency: Daily updates mandatory
  
  Channels:
    - Email: Daily summary post evening meeting (entire org)
    - Slack: #crisis-updates channel (real-time, critical only)
    - Town Halls: Weekly (30 min, Q&A)
    - Manager cascade: Talking points provided daily
  
  Messaging_Principles:
    - Transparency: Honest about severity, no sugar-coating
    - Actionable: What staff should/shouldn't do
    - Hope: Progress visible, light at end of tunnel
    - Consistency: All leaders tell same story
  
  Avoid:
    - Panic-inducing language ("we might not survive")
    - Blame individuals publicly
    - Overpromising ("everything will be fine")
    - Information vacuum (silence generates rumors)

External_Communication:
  
  Stakeholders:
    - Customers: Service continuity assurance
    - Investors: Financial transparency
    - Partners: Commitment to obligations
    - Regulators: Compliance status
    - Media: Controlled messaging (if public)
  
  Frequency: As needed, but proactive (don't wait for questions)
  
  Spokesperson: Executive Sponsor (single voice)
```

---

## §4. EXIT CRITERIA (CUÁNDO DESACTIVAR)

### Transition Normal Governance

```yaml
Required_Conditions (ALL must be met):
  
  1. H_Score_Stability:
     - H_Score > 45 for 3 consecutive months
     - Trend: Improving or stable (not volatile)
  
  2. Observable_Recovery:
     - All observables O1-O8, IN1-IN3 > 30
     - No crisis thresholds active
  
  3. Financial_Stability:
     - Cash runway > 180 días (O3 > 60)
     - Burn rate under control (declining or stable)
     - Payroll secured 6+ months
  
  4. Customer_Stability:
     - Churn stabilized or declining (not accelerating)
     - NPS > 20 (neutral, not negative)
     - Service delivery > 85% (if public)
  
  5. Talent_Stability:
     - Attrition < 20% annualized (IN2 > 45)
     - Engagement score > 50
     - Leadership team complete (no critical vacancies)
     - Flight risk reduced (<30% top talent job hunting)
  
  6. Operational_Stability:
     - Incident rate back to baseline (not 3× spike)
     - Velocity recovering (>50% of pre-crisis)
     - No firefighting mode (planned work >50%)

Validation: CFO, CHRO, COO confirm their domains stable
```

---

### Transition Process

```yaml
Week_1-2: Design Normal Governance
  - Define post-crisis structure (org chart if changed)
  - Establish normal cadence (weekly/monthly vs daily)
  - Assign ownership BAU (business-as-usual)
  - Document lessons learned (retrospectiva crisis)

Week_3-4: Pilot Normal Cadence
  - Reduce meetings: Daily → Weekly
  - Crisis team: Daily → Weekly check-ins
  - Test if organization can sustain without daily oversight

Week_5-8: Full Transition
  - Crisis team disbands (roles return to normal)
  - Monitoring continues (H_Score monthly)
  - Governance BAU (QBR quarterly)

Month_3+: Vigilance
  - Monitor for regression (H_Score tracking)
  - IF H_Score drops < 45 again → Reactivate P52
  - Post-crisis retrospectiva (6 months after exit)

Fallback_Protocol:
  IF during transition H_Score drops < 40:
    → Pause transition
    → Re-activate crisis governance
    → Diagnosis: Why regression?
```

---

## §5. ANTIPATRONES CRISIS (AP31-AP33)

### AP31: Crisis Theater

```yaml
ID: AP31
Nombre: Crisis Theater
Severidad: 🔴 Crítico

Síntoma:
  - Leadership declara "crisis" públicamente
  - PERO governance no cambia (meetings still weekly)
  - PERO decision rights no cambian
  - PERO no crisis team formado
  - Staff trabaja overtime sin emergency structure

Causa_Raíz:
  - Leadership quiere urgency sin accountability
  - Motivación política ("create burning platform")
  - H_Score típicamente 50-65 (NO es crisis real)

Consecuencia (12 meses):
  - Burnout rate +40%
  - Attrition +15% (IN2 collapse)
  - "Crisis fatigue" - next real crisis not taken seriously
  - Credibility leadership destroyed
  - Staff cynicism ("boy who cried wolf")

Diagnóstico:
  Check_Real_Crisis:
    IF H_Score < 45 AND (O3<30 OR O2<30 OR IN2<30):
      → Real crisis, activate P52 justified
    ELSE:
      → Not crisis, don't declare crisis
      → Use normal urgency mechanisms (OKRs, prioritization)

Fix:
  If_Crisis_Real:
    - Activate P52 genuinely (daily meetings, decision protocols)
    - Walk the talk (structure matches rhetoric)
  
  If_Not_Crisis:
    - Retract "crisis" declaration
    - Communicate honest urgency level
    - Use normal governance with higher priority
    - Damage control (apologize for overreaction)

Prevention:
  - Objective threshold (H<45) before declare crisis
  - Crisis team pre-identified (don't improvise)
  - Board approval before public crisis declaration
```

---

### AP32: Forcing Transformation Unprepared

```yaml
ID: AP32
Nombre: Forcing Transformation Unprepared
Severidad: 🔴 Crítico

Síntoma:
  - Transformation kicked off sin readiness assessment (R1-R5)
  - Leadership fragmented (algunos support, otros resist)
  - No resources allocated (team at 95% utilization)
  - No skills in-house, no budget consultants
  - Urgency artificial ("competitors doing it, we must too")

Causa_Raíz:
  - Executive impatience
  - Ignoring prerequisites (momentum, capabilities, forces)
  - FOMO (Fear Of Missing Out) technology/methodology
  - Pressure board/investors ("show progress")

Readiness_Dimensions (rate 1-5 each):
  1. Leadership_Alignment: 100% exec team buy-in
  2. Urgency_Level: Compelling case for change NOW
  3. Resource_Availability: Time, money, people allocated
  4. Capability: Skills to execute (in-house or consultants)
  5. Org_Bandwidth: Can absorb change while operating

Decision_Matrix:
  IF ANY dimension < 3:
    → BUILD READINESS first, don't force transformation
    → 70% failure rate if proceed anyway
  
  IF ALL dimensions >= 3:
    → Proceed with pilot/phased approach
    → Monitor readiness continuously

Consecuencia (24 meses):
  - 70% probability complete failure
  - $500K-$2M wasted (consulting, tools, opportunity cost)
  - Morale damage (cynicism future transformations)
  - Competitive position worsens (distraction from core)

Fix:
  Stop_Transformation:
    - Pause or cancel if in first 3 months
    - Honest admission "not ready, regrouping"
  
  Build_Prerequisites:
    1. Leadership_Alignment: Workshops, get 100% buy-in
    2. Resource_Availability: Free up 20% capacity, allocate budget
    3. Capability: Hire expertise or engage consultants
    
    Re-Assess: 3-6 months, verify all dimensions >= 3
  
  Then_Proceed: With confidence, proper foundation

Prevention:
  - Mandatory R1-R5 assessment before any transformation >$500K or >6 months
  - Go/No-Go gate based on readiness score
  - Board approval requires readiness documentation
```

---

### AP33: Transforming During Crisis

```yaml
ID: AP33
Nombre: Transforming During Crisis
Severidad: 🔴 Crítico

Síntoma:
  - H_Score 20-40 (crisis mode active)
  - Cash runway < 60 días OR Churn > 25% OR Attrition > 25%
  - Executive decides "now is time to restructure"
  - Major organizational changes while firefighting
  - Belief: "Never waste a crisis" (misunderstood)

Causa_Raíz:
  - Confusion: Crisis = opportunity for change
  - Reality: Crisis needs STABILIZATION first, transformation second
  - Impatience: "Fix everything at once"
  - Overconfidence: "We can handle both"

Dual_Disruption_Effect:
  Crisis_Impact:
    - Staff already stressed (60-80% utilization emergency work)
    - Cognitive load high (survival mode)
    - Resistance elevated (fear, uncertainty)
  
  Transformation_Impact:
    - Requires 20-40% capacity (learning, transition)
    - Adds uncertainty (new roles, processes)
    - Attention diverted from stabilization
  
  Combined:
    - Crisis worsens (bleeding not stopped)
    - Transformation fails (org too stressed to absorb)
    - H_Score drops further: 35 → 22 (existential)
    - Talent exodus accelerates (uncertainty × stress)

Consecuencia (6 months):
  - Crisis deepens instead of stabilizing
  - Transformation abandoned (too much chaos)
  - Leadership turnover (board loses confidence)
  - Organization death spiral (hard to recover)

Correct_Sequence:
  
  Phase_1_Stabilization (Week 1-4):
    - Activate P52 Crisis Governance
    - Stop bleeding: Cash, customers, talent
    - Daily meetings, emergency protocols
    - NO structural changes (freeze org chart)
  
  Phase_2_Diagnosis (Week 5-12):
    - Root cause analysis (why crisis occurred)
    - Energy dissipation mapping
    - Conflict topology
    - Building blocks completeness
    - Identify structural vs dynamic issues
  
  Phase_3_Check_Exit_Criteria (Month 4):
    IF H_Score > 45 for 3 months consecutive:
      → NOW safe to transform
      → Follow normal transformation playbook (A4 §1-§6)
    ELSE:
      → Continue stabilization
      → Delay transformation
  
  Phase_4_Transform (Month 6+):
    - Only after sustained H>45
    - Normal readiness assessment (R1-R5)
    - Phased rollout (pilot first)

Fix_If_Caught_Mid-Stream:
  - Pause transformation immediately
  - Return focus to stabilization
  - Communicate honestly: "We tried to do too much"
  - Resume transformation only after H>45 stable

Prevention:
  - Explicit protocol: "No major reorg if H<45"
  - Board approval required transformation during H<60
  - Crisis governance (P52) prohibits structural changes explicitly
```

---

## §6. STABILIZATION ACTIONS BY CRISIS TYPE

### Financial Crisis (O3 < 30)

```yaml
Week_1_Emergency:
  Priority_1: Extend Cash Runway
    - Secure bridge financing (line of credit, investors)
    - Delay payables (negotiate with vendors)
    - Accelerate receivables (payment terms)
    - Cut non-essential spend immediately
  
  Priority_2: Reduce Burn Rate
    - Hiring freeze (except critical)
    - Discretionary spend freeze (travel, marketing, etc.)
    - Renegotiate contracts (SaaS, vendors)
    - Defer non-critical projects
  
  Priority_3: Scenario Planning
    - Best case: Runway extended to 180 días
    - Base case: Runway extended to 120 días
    - Worst case: Layoffs required (size, timing)

Week_2-4_Stabilization:
  - Execute scenario plan
  - IF layoffs needed: Execute humanely, quickly (don't drag)
  - Communicate financial status weekly (transparency)
  - Target: O3 > 30 (runway > 90 días) before exit crisis mode

Prevention_Future:
  - Monthly cash flow forecasting (12 months rolling)
  - Alert thresholds: Runway < 180d → Yellow, < 90d → Red
  - Burn rate monitoring weekly
```

---

### Customer Crisis (O2 < 30)

```yaml
Week_1_Emergency:
  Priority_1: Stop Defection
    - Identify at-risk accounts (top 20% revenue)
    - Executive outreach (C-level calls)
    - Retention offers (discounts, features, support)
    - Win-back campaigns (churned customers)
  
  Priority_2: Service Recovery
    - Fix critical bugs/incidents causing churn
    - Increase support capacity (temporary contractors)
    - Daily customer sentiment monitoring
  
  Priority_3: Root Cause Understanding
    - Why are customers leaving? (surveys, interviews)
    - Competitor analysis (what are they offering?)
    - Product gaps (feature parity analysis)

Week_2-4_Stabilization:
  - Deploy quick wins (high-impact features)
  - Service quality improvements visible
  - NPS tracking weekly (target: stop decline, then improve)
  - Target: O2 > 30 (churn < 20%, NPS > 0) before exit

Prevention_Future:
  - Churn prediction ML (M2-M3 mode)
  - Proactive customer success (outreach before churn)
  - NPS monitoring monthly (alert < 30)
```

---

### Talent Crisis (IN2 < 30)

```yaml
Week_1_Emergency:
  Priority_1: Stop Exodus
    - Identify flight risk (top performers actively looking)
    - Retention conversations (1:1s with CFO, CEO)
    - Retention packages (equity, bonus, flexibility)
    - Address grievances immediately (toxic manager? remove)
  
  Priority_2: Stabilize Leadership
    - If C-level departures: Interim appointments rapid
    - Communicate succession plan (reduce uncertainty)
    - Board support visible (confidence signal)
  
  Priority_3: Culture Triage
    - Exit interviews: Why are people leaving?
    - Engagement pulse survey (weekly during crisis)
    - Address top 3 issues (work conditions, leadership, uncertainty)

Week_2-4_Stabilization:
  - Implement quick wins culture (flexibility, tools, recognition)
  - Communication transparency (honesty about challenges)
  - Celebrate small wins (morale critical)
  - Target: IN2 > 30 (attrition < 25%, engagement > 40) before exit

Prevention_Future:
  - Engagement surveys quarterly
  - Attrition monitoring monthly (alert > 15%)
  - Stay interviews (not just exit interviews)
  - 1:1s mandatory monthly (manager-report)
```

---

## §7. CONEXIÓN PRIMITIVOS KERNEL

### Crisis Governance como Composición

```yaml
Pattern_Composition (ver CORE/01 §7):

Crisis_Governance_Unidad_Trabajo:
  
  # Actores
  actores: {Crisis_Team: Set(Actor)} 
    - 5-7 personas con authorities específicas
    - Actor type: Humano (crisis decisions requiere juicio, P8)
  
  # Flujos
  flujos: {Daily_Morning_Situation, Daily_Evening_Progress, Weekly_Deep_Dive}
    - Secuencias ordenadas de decisión + comunicación
  
  # Señales Input
  señales_input: {Vital_Signs_Alerts, Blocker_Escalations, Overnight_Incidents}
    - Triggers que inician daily meetings
    - H_Score < 45 activa todo el pattern
  
  # Datos Input
  datos_input: {Observable_Readings, Financial_Reports, Sentiment_Data}
    - Información estructurada para decisiones
  
  # Productos/Servicios (outputs)
  productos_servicios: {Stabilization, Decision_Velocity, Communication_Clarity}
    - Output: Org estabilizada (H>45)
  
  # Destinatarios
  destinatarios: {Board, Staff, Customers, Stakeholders}
    - Quién consume outputs crisis governance
  
  # Límites
  limites:
    - Temporal: Max 12 semanas crisis mode (fatigue if longer)
    - Authority: Bounded by board mandate
    - Financial: Budget emergency allocated
    - Decisional: <4hrs critical, <24hrs tactical (speed limits)
  
  # Estado
  estados:
    - Estado(t0): Crisis detected (H<45)
    - Estado(t1-t12): Crisis mode active (P52 operating)
    - Estado(t13+): Post-crisis, normal governance restored

Conexión_Ciclo_SDA:
  Sense (D2): Vital signs daily (11 observables)
  Decide (D3): Crisis team decisions (<4hrs critical)
  Act (D4): Emergency actions executed
  → Loop: Daily (vs normal weekly/monthly)
```

---

## §8. VALIDATION & BOUNDARIES

### Cuándo NO Activar P52

```yaml
False_Alarms:
  - H_Score 50-60 (attention needed, not crisis)
  - Single observable < 30 temporarily (spike, not trend)
  - Political pressure without objective thresholds
  - "Manufactured crisis" for urgency theater

Risk_Over-Activation:
  - Fatigue: Daily meetings unsustainable >12 weeks
  - Normalization: Crisis becomes "new normal" (lose urgency)
  - Credibility: If activate unnecessarily, future real crisis ignored

Decision:
  IF H_Score >= 45 AND no observable <30 sustained:
    → Use normal governance with increased priority
    → Weekly monitoring instead of daily
    → Don't declare crisis (AP31 Crisis Theater)
```

---

### Cuándo Activar Parcialmente

```yaml
Modified_P52 (Single Domain Crisis):
  
  Scenario: O3 < 30 (financial) pero O2, IN2 > 45 (customer, talent OK)
  
  Approach: Crisis governance SOLO financial domain
    - Daily financial check-ins (CFO + CEO)
    - Weekly crisis team (not daily, solo financial focus)
    - Other domains continue normal governance
  
  Benefit: Avoid over-disruption
  Risk: Domains interdependent (financial crisis → talent crisis lag 2-3 months)

Recommendation: Partial activation only if:
  - Single observable < 30
  - High confidence isolation (crisis won't spread)
  - Duration expected < 4 weeks
```

---

## §9. CASE STUDY: FINANCIAL CRISIS STABILIZATION

### Context

```yaml
Org: SaaS Startup (80 personas, 50 eng)
Situation: Series A runway agotándose
H_Score: 28 (Critical)
Observables:
  O3_Capacidad: 18 (cash runway 22 días)
  O2_Valor: 62 (churn OK, pero ingresos no crecen suficiente)
  IN2_Talent: 48 (attrition normal, pero riesgo si layoffs)
```

---

### Week 1-4: Emergency Stabilization

```yaml
Day_1: P52 Activation
  - Crisis team formed (CEO, CFO, COO, VP Eng, VP Sales, CHRO)
  - Daily meetings scheduled (9am, 5pm)
  - Communication: Honest all-hands (cash situation critical)

Day_2-7: Stop Bleeding
  Actions:
    - CFO: Secured $500K bridge loan (3 weeks close)
    - CEO: Froze hiring (15 open positions paused)
    - COO: Cut SaaS spend 30% ($40K/mes savings)
    - VP Sales: Accelerated collections (net-30 → net-15 ask)
  
  Result Week 1:
    - Cash runway: 22 → 35 días (bridge loan committed)
    - Burn: $280K/mes → $240K/mes (cuts effective)

Week_2: Scenario Planning
  Best_Case: Bridge loan + revenue growth → 120 días runway
  Base_Case: Bridge loan + flat revenue → 90 días runway
  Worst_Case: No bridge, flat revenue → Layoffs 15 personas (extend to 150 días)
  
  Decision: Execute base case, prepare worst case

Week_3-4: Execution
  - Bridge loan closed (runway: 35 → 90 días)
  - Revenue sprint (sales focused on close deals Q4)
  - Cost discipline maintained
  
  Result Week 4:
    - Cash runway: 90 días
    - O3_Capacidad: 18 → 42 (crisis threshold crossed)
    - H_Score: 28 → 48 (exited crisis zone)
```

---

### Month 2-3: Diagnosis & Sustain

```yaml
Crisis_Team_Transition:
  - Meetings: Daily → 3×/week (reduced intensity)
  - Focus: Why did we reach crisis? (root causes)

Root_Cause_Analysis:
  1. Por qué cash crisis? → Burn rate > revenue growth
  2. Por qué burn > revenue? → Hiring aggressive, sales lagging
  3. Por qué sales lag? → Product-market fit incomplete
  4. Por qué PMF incomplete? → Feature bloat, no focus
  5. Root: Strategy diffuse, no clear ICP (Ideal Customer Profile)

Sustained_Improvements:
  - Define ICP narrow (SMB SaaS $100K-$500K ARR)
  - Focus product on ICP (remove 30% features unused)
  - Hiring discipline (only when runway > 18 meses)
  
  Result Month 3:
    - Revenue growth +15% (ICP focus)
    - Burn under control ($220K/mes)
    - Runway: 150 días
    - H_Score: 58 (stable >45 for 3 months)

Exit_Criteria_Met: Month 4
  - H_Score > 45 for 3 months ✓
  - O3 > 60 ✓
  - All observables > 30 ✓
  - Transition to normal governance approved
```

---

## §10. INTEGRATION DOMINIOS

### Arquitectura (D1) During Crisis

```yaml
Changes_Allowed:
  - Minor: Role clarifications, decision rights adjustments
  - Tactical: Task force formations (temporary)

Changes_PROHIBITED:
  - Major reorgs (department restructures)
  - Leadership changes (unless cause of crisis)
  - New governance models (matrix, federated, etc.)

Rationale:
  - Crisis requires stability, not disruption
  - Structure changes during crisis = AP33 (violates)
  - Wait until H>45 stable, THEN transform
```

---

### Percepción (D2) During Crisis

```yaml
Sensing_Intensified:
  - Observable tracking: Monthly → Daily
  - H_Score calculation: Monthly → Daily
  - Alerting: Proactive (predict thresholds crossing)
  - Dashboards: Real-time, crisis team access 24/7

Awareness_Levels:
  - L1 Detect: Automated, comprehensive (all systems)
  - L2 Comprehend: Daily synthesis (morning meeting input)
  - L3 Project: Weekly deep-dive (trend analysis, exit criteria forecast)
```

---

### Decisión (D3) During Crisis

```yaml
Decision_Speed_Accelerated:
  Normal: Type 1 <14 días, Type 2 <7 días
  Crisis: Critical <4 hrs, Tactical <24 hrs, Strategic <7 días

Decision_Modes_Shift:
  - More Mode 1-2 (Direct, Rule-based): Fast decisions
  - Less Mode 4 (Knowledge-based): No time for deep analysis
  - Exception: Weekly deep-dive permite Mode 4 focused

OKRs_Suspended:
  - Normal OKRs paused (focus survival)
  - Crisis OKRs: "Achieve H>45", "Extend runway >180d", "Stop churn"
  - Resume normal OKRs post-exit
```

---

### Operación (D4) During Crisis

```yaml
Work_Mix_Changed:
  Normal: 70% planned, 20% reactive, 10% innovation
  Crisis: 20% planned, 70% emergency, 10% critical tech debt
  
  Rationale: Shift to firefighting mode temporarily

Ceremonies_Adjusted:
  - Daily standups: Continue (but brief, 10 min)
  - Sprint planning: Simplified (top priorities only)
  - Retrospectives: Weekly (accelerated learning)
  - Sprint reviews: Paused (no stakeholder demos, survival focus)

Tech_Debt:
  - 20% rule suspended temporarily
  - Only critical tech debt (blocks stabilization)
  - Resume 20% rule post-exit
```

---

## Referencias Cruzadas

- **H_Score calculation:** `DOMINIOS/D2_Percepcion.md` §4
- **Observables thresholds:** `DOMINIOS/D2_Percepcion.md` §2 (O1-O8), §3 (IN1-IN3)
- **Readiness R1-R5:** `DOMINIOS/D3_Decision.md` §3
- **Implementation playbook:** `APLICACION/A4_Implementacion.md` §0 (Triage Paths)
- **Antipatrones consolidados:** Este documento §5 (AP31-AP33)
- **Primitivos composición:** `CORE/01_Primitivos.md` §7
- **Principio P8:** `CORE/00_Manifiesto.md` §3 (Herramienta no Oráculo)
- **Building Blocks:** `DOMINIOS/D1_Arquitectura.md` §4
- **Pattern P52 original:** Este documento §3 (ahora single source of truth)

---

**Fin de Crisis Management**
