# 08_Crisis_Management v2.0.0

## §0. PROPÓSITO Y SCOPE

**Definición:** Crisis Management es el conjunto de estructuras, procesos y decisiones para **estabilizar organización** cuando indicadores críticos caen bajo umbrales viabilidad (H_Score <45 o cualquier observable <30).

**Consolida:**

- P52 Crisis Governance Pattern (estructura, ritmos, roles)
- AP31-AP33 (antipatrones crisis)
- Path 1-2 Implementation (triage emergency)
- Activation triggers (thresholds automáticos)

**Relación Invariantes:**

- **I3 Trazabilidad:** Crisis Management conecta H_Score (D2) → Decisión activar (D3) → Governance (D1) → Actions (D4) → Outcomes
- **I2 Ortogonalidad:** Crisis es **estado temporal** operación, no dominio separado
- **I1 Minimalidad:** Necesario porque governance normal insuficiente para crisis (latency incompatible con urgencia)

## §1. ACTIVATION TRIGGERS

### Thresholds Automáticos

| Nivel | Condición | Acción | Path |
|-------|-----------|--------|------|
| **Crisis** | H_Score <45 por 1 mes | Activate P52 Crisis Governance | §2 |
| **Crisis Observable** | ANY(O1-O8, IN1-IN3) <30 por 2 semanas | Evaluate activation; múltiples <30 → mandatory | §2 |
| **Existential** | H_Score <15 OR O3<15 OR O2<15 OR IN2<15 | IMMEDIATE emergency triage | A4 §0 Path 1 |

### Triggers por Tipo de Crisis

| Tipo | Activación Mandatoria Si | Severity Levels | Señal Emission |
|------|-------------------------|-----------------|----------------|
| **Financial** | Cash runway <90d (O3<30)<br>Burn rate +20% MoM<br>Payroll at risk <30d | Severe (O3:30-45): 30-90d runway<br>Critical (O3:15-30): 7-30d<br>Existential (O3:0-15): <7d | O3<30 → "Financial_Crisis_P52"<br>O3<15 → "Financial_Existential" |
| **Customer/Value** | Churn >20% (O2<30)<br>NPS <0<br>Key account losses<br>Service failures >20% | Severe (O2:30-45): Churn 15-20%<br>Critical (O2:15-30): Churn >20%<br>Existential (O2:0-15): Mass defection >30% | O2<30 → "Customer_Defection_P52"<br>O2<15 → "Market_Rejection" |
| **Talent** | Attrition >25% (IN2<30)<br>High-performer exodus >20%<br>Leadership departures<br>Engagement <40 | Severe (IN2:30-45): Attrition 20-25%<br>Critical (IN2:15-30): Attrition >25%<br>Existential (IN2:0-15): Mass exodus >30% | IN2<30 → "Talent_Exodus_P52"<br>IN2<15 → "Knowledge_Collapse" |
| **Operational** | Incident rate spike 3×<br>MTTR >8h avg<br>Deploy freq collapse<br>Tech debt >70 | Típicamente correlaciona IN3<br>**Rara vez standalone**<br>Usualmente consecuencia otra crisis | Treat root cause, no solo síntoma |

## §2. P52 CRISIS GOVERNANCE PATTERN

### Structure: Crisis Team (5-7 personas)

| Rol | Authority | Time Commitment | Selection |
|-----|-----------|-----------------|-----------|
| **Executive Sponsor** | Overall accountability, single point decision final | 60-80% (daily participation) | CEO, COO, C-level con mandate board |
| **Operations Lead** | Service delivery, customer satisfaction | 80%+ (daily operational) | COO, VP Operations, Service Lead |
| **Financial Lead** | Cash management, budget reallocation | 60-80% | CFO, Finance Director |
| **Customer Lead** | Retention strategy, satisfaction recovery | 60%+ | CCO, VP Customer Success, Head Sales |
| **People Lead** | Talent retention, engagement interventions | 60%+ | CHRO, VP People, Talent Director |
| **Communications Lead** | Internal/external messaging | 40-60% | CCO, Comms Director |
| **Legal/Compliance** (as needed) | Regulatory compliance, legal risk | 20-40% (on-call) | General Counsel, Chief Compliance |

**Selection Criteria:** Authority real sin escalate, domain expertise, disponibilidad daily, action orientation, credibility stakeholders, track record bajo presión.

### Ritmos Acelerados

| Ceremony | Timing | Duration | Agenda |
|----------|--------|----------|---------|
| **Daily Morning Situation** | Same time daily (ej: 9am) | 30-60 min strict | 1. Overnight developments (5min)<br>2. Vital signs update (10min)<br>3. Priority actions today (20min)<br>4. Blockers escalations (15min)<br>5. Communication priorities (10min) |
| **Daily Evening Progress** | End of day (ej: 5-6pm) | 30 min strict | 1. Accomplishments today (10min)<br>2. Issues encountered (10min)<br>3. Tomorrow priorities (5min)<br>4. Overnight watch items (5min) |
| **Weekly Deep Dive** | Mid-week (ej: Miércoles 2-5pm) | 2-3 hrs | 1. Week-over-week vital signs (30min)<br>2. Stabilization plan progress (30min)<br>3. Deep-dive critical issue (60min)<br>4. Next week priorities (30min) |

**Outputs:**

- Action list published <15min meeting end
- Daily summary email (entire org transparency)
- Weekly report (board, investors)

### Decision Rights Crisis Mode

| Authority Level | Decisions | Time Commitment |
|-----------------|-----------|-----------------|
| **Executive Sponsor** | Strategic direction, major resources (>$100K), executive appointments, board/investor comms | <4hrs critical, <24hrs tactical |
| **Functional Leads** | Within domain up to $10K-$50K, daily operational, tactical resource shifts | <2hrs tactical, <8hrs operational |
| **Team Consensus** | Cross-functional issues, major policy changes, restructuring, trade-offs | Majority vote (Sponsor breaks tie) |
| **Escalate to Board** | Beyond team authority, capital structure, liquidation/bankruptcy/M&A, CEO removal | Per board cadence |

**Shift Normal→Crisis:** Normal escalates UP slowly (days-weeks), Crisis de-escalates DOWN rapidly (hours).

### Communication Protocols

```yaml
Internal:
  Frequency: Daily updates mandatory
  Channels: Email (daily summary), Slack (#crisis-updates), Town halls (weekly 30min)
  Principles: Transparency, Actionable, Hope, Consistency
  Avoid: Panic language, Blame publicly, Overpromising, Information vacuum

External:
  Stakeholders: Customers (continuity), Investors (financial), Partners, Regulators, Media
  Frequency: Proactive (don't wait questions)
  Spokesperson: Executive Sponsor (single voice)
```

## §3. EXIT CRITERIA

### Transition Normal Governance (ALL required)

```yaml
Required_Conditions:
  1. H_Score >45 for 3 consecutive months (trend improving/stable)
  2. All observables O1-O8, IN1-IN3 >30
  3. Cash runway >180 días (O3>60), burn rate controlled
  4. Churn stabilized/declining, NPS >20, service delivery >85%
  5. Attrition <20% (IN2>45), engagement >50, leadership team complete
  6. Incident rate baseline, velocity recovering >50% pre-crisis

Validation: CFO, CHRO, COO confirm domains stable
```

### Transition Process

| Timeline | Activities | Output |
|----------|-----------|---------|
| **Week 1-2** | Design normal governance, define post-crisis structure, assign ownership BAU, lessons learned | Retrospectiva documentada |
| **Week 3-4** | Reduce meetings daily→weekly, crisis team daily→weekly check-ins, test sustainability | Pilot normal cadence |
| **Week 5-8** | Crisis team disbands, monitoring H_Score monthly, governance BAU (QBR quarterly) | Full transition |
| **Month 3+** | Monitor regression, IF H_Score <45 → reactivate P52, post-crisis retrospectiva 6 meses | Vigilance sustained |

**Fallback:** IF H_Score drops <40 during transition → Pause, re-activate crisis governance, diagnose regression.

## §4. ANTIPATRONES CRISIS (AP31-AP33)

| Anti-Pattern | Síntoma | Causa Raíz | Consecuencia (12 meses) | Fix |
|--------------|---------|------------|------------------------|-----|
| **AP31: Crisis Theater** | Leadership declara "crisis" pero governance no cambia, meetings still weekly, no crisis team, H_Score 50-65 | Leadership wants urgency sin accountability, motivación política | Burnout +40%, Attrition +15%, Crisis fatigue, Credibility destroyed | IF H<45 → Activate P52 genuinely<br>IF H≥45 → Retract "crisis", use normal urgency |
| **AP32: Forcing Transformation Unprepared** | Transformation sin R1-R5 assessment, leadership fragmented, no resources, no skills, urgencia artificial | Executive impatience, ignoring prerequisites, FOMO | 70% failure rate, $500K-$2M wasted, Morale damage, Competitive position worsens | Stop transformation, build prerequisites (alignment, resources, capability), re-assess 3-6 meses |
| **AP33: Transforming During Crisis** | H_Score 20-40, major org changes while firefighting, "never waste crisis" misunderstood | Confusion crisis=opportunity, impatience, overconfidence | Crisis deepens (H 35→22), Transformation fails, Leadership turnover, Death spiral | Sequence: 1) Stabilize (P52, no reorg), 2) Diagnose, 3) Check exit (H>45), 4) THEN transform |

## §5. STABILIZATION ACTIONS BY TYPE

### Financial Crisis (O3 <30)

```yaml
Week_1_Emergency:
  Priority_1_Extend_Runway: Bridge financing, delay payables, accelerate receivables, cut non-essential
  Priority_2_Reduce_Burn: Hiring freeze, discretionary spend freeze, renegotiate contracts, defer projects
  Priority_3_Scenarios: Best (runway 180d), Base (120d), Worst (layoffs required)

Week_2-4_Stabilization:
  Execute scenario, layoffs if needed (humane, quick), communicate weekly, Target: O3>30 (runway>90d)

Prevention: Monthly cash flow forecasting (12mo rolling), alert thresholds runway <180d (Yellow), <90d (Red)
```

### Customer Crisis (O2 <30)

```yaml
Week_1_Emergency:
  Priority_1_Stop_Defection: Identify at-risk top 20%, executive outreach, retention offers, win-back
  Priority_2_Service_Recovery: Fix critical bugs, increase support capacity, daily sentiment monitoring
  Priority_3_Root_Cause: Why leaving? Competitor analysis, product gaps

Week_2-4_Stabilization:
  Deploy quick wins, service quality improvements, NPS weekly tracking, Target: O2>30 (churn<20%, NPS>0)

Prevention: Churn prediction ML (M2-M3), proactive customer success, NPS monthly (alert<30)
```

### Talent Crisis (IN2 <30)

```yaml
Week_1_Emergency:
  Priority_1_Stop_Exodus: Identify flight risk, retention conversations (CEO/CFO), retention packages, address grievances
  Priority_2_Stabilize_Leadership: Interim appointments if C-level departures, succession plan, board support visible
  Priority_3_Culture_Triage: Exit interviews, engagement pulse weekly, address top 3 issues

Week_2-4_Stabilization:
  Quick wins culture (flexibility, tools), transparency communication, celebrate wins, Target: IN2>30 (attrition<25%)

Prevention: Engagement quarterly, attrition monthly (alert>15%), stay interviews, 1:1s mandatory monthly
```

## §6. CASE STUDY: FINANCIAL CRISIS

```yaml
Context:
  Org: SaaS Startup (80 personas, 50 eng)
  H_Score: 28 (Critical)
  O3: 18 (cash runway 22 días)

Week_1-4_Emergency:
  Day_1: P52 activated, crisis team formed, honest all-hands
  Day_2-7: CFO secured $500K bridge (3wk close), hiring freeze, SaaS cuts 30% ($40K/mes), accelerated collections
  Result_Week_1: Runway 22→35d, Burn $280K→$240K/mes
  Week_2: Scenario planning (best/base/worst), execute base case
  Week_3-4: Bridge closed (runway→90d), revenue sprint, O3: 18→42, H_Score: 28→48

Month_2-3_Diagnosis:
  Meetings: Daily→3×/week
  Root_Cause: Burn>revenue → Hiring aggressive, sales lag → PMF incomplete → Feature bloat, no ICP focus
  Improvements: Define ICP narrow (SMB SaaS $100K-$500K ARR), focus product, hiring discipline
  Result_Month_3: Revenue +15%, Burn $220K/mes, Runway 150d, H_Score: 58

Exit_Month_4: H>45 for 3 months ✓, O3>60 ✓, all observables>30 ✓, transition normal governance approved
```

## §7. INTEGRATION DOMINIOS

| Dominio | Crisis Mode Changes | Rationale |
|---------|---------------------|-----------|
| **D1 Arquitectura** | **Allowed:** Role clarifications, task forces (temporary)<br>**PROHIBITED:** Major reorgs, leadership changes (unless cause), new governance models | Crisis needs stability, not disruption<br>Wait until H>45, THEN transform (AP33) |
| **D2 Percepción** | Tracking: Monthly→Daily (observables, H_Score)<br>Alerting: Proactive (predict thresholds)<br>Dashboards: Real-time 24/7 crisis team access | Intensified sensing critical<br>L1 Detect automated, L2 Comprehend daily, L3 Project weekly |
| **D3 Decisión** | Speed: Critical <4hrs (vs 14d), Tactical <24hrs (vs 7d)<br>Modes: More D1-D2 (Direct, Rule), Less D4 (Analytic)<br>OKRs: Suspended (crisis OKRs: "H>45", "Runway>180d") | Urgency requires fast decisions<br>Weekly deep-dive permits D4 focused |
| **D4 Operación** | Work Mix: 70% planned→20% planned, 20% reactive→70% emergency<br>Ceremonies: Standups continue (10min), sprint planning simplified, retros weekly, reviews paused<br>Tech Debt: 20% rule suspended (only critical) | Shift to firefighting temporarily<br>Resume normal mix post-exit |

## §8. VALIDACIÓN

### Completitud

```
¿Crisis Management cubre todos tipos crisis? → SÍ
  Financial, Customer, Talent, Operational (4 tipos principales)
```

### Ortogonalidad

```
¿Crisis es dominio separado? → NO
  Es estado temporal que modifica operación D1-D4
```

### Conectividad

```
¿P52 conecta a observables (D2) y acciones (D4)? → SÍ
  Thresholds activación basados H_Score/observables
  Actions estabilización medidas por outcomes
```

## Referencias Cruzadas

- **H_Score calculation:** `DOMINIOS/D2_Percepcion.md` §4
- **Observables thresholds:** `DOMINIOS/D2_Percepcion.md` §2 (O1-O8), §3 (IN1-IN3)
- **Readiness R1-R5:** `DOMINIOS/D3_Decision.md` §3
- **Implementation triage:** `APLICACION/A4_Implementacion.md` §0
- **Primitivos composición:** `CORE/01_Primitivos.md` §7
- **Principio P8:** `CORE/00_Manifiesto.md` §3
- **Building Blocks:** `DOMINIOS/D1_Arquitectura.md` §4

**Fin 08_Crisis_Management v2.0.0**