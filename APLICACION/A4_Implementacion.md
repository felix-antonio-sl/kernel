# A4_Implementacion

**Versión:** 1.2.0 | **Estado:** Definitivo | **Audiencia:** Implementadores, PMO, Change Leaders

---

## §0. READINESS AND TRIAGE

### Decision Tree

```yaml
Purpose: Determinar approach correcto basado en organizational state
Input: H_Score + Observables O1-O8, IN1-IN3
Output: Go/No-Go decision + Implementation path
```

---

### Path 1: EXISTENTIAL CRISIS (H_Score < 15)

```yaml
Condition:
  - H_Score < 15 OR
  - Multiple observables < 15 OR
  - Cash runway < 7 días OR
  - Service collapse imminent

Action: EMERGENCY TRIAGE

Protocol: Ver detalles completos en CORE/08_Crisis_Management.md
  
  Week 1: Activate P52 Crisis Governance
    - Form crisis team 5-7 personas (§3 structure)
    - Daily morning/evening meetings (§3 dynamics)
    - Stop bleeding (§6 stabilization actions)
  
  Week 2-4: Stabilization
    - Execute domain-specific actions (§6)
    - Monitor H_Score daily
    - Target: H>30 minimum before transition
  
  Week 5+: IF H_Score > 30 THEN transition to Path 2
          ELSE continue emergency (seek board/investor support)

Do_NOT: Transformación estructural (AP33 - ver CORE/08 §5)
Focus: Survival primero, transformation después
```

---

### Path 2: CRISIS STABILIZATION (H_Score 15-45)

```yaml
Condition:
  - H_Score 15-45 OR
  - Any observable 15-30 (severe crisis) OR
  - Cash runway 7-90 días OR
  - Churn >20% OR Talent exodus >20%

Action: CRISIS + DIAGNOSIS

Protocol: Ver detalles completos en CORE/08_Crisis_Management.md
  
  Week 1-4: Emergency Stabilization
    - Activate P52 Crisis Governance (CORE/08 §3)
    - Crisis team + daily meetings (§3 dynamics)
    - Domain-specific stabilization (§6)
    - Target: H>45 o al menos stopping deterioration
  
  Week 5-12: Intensive Diagnosis (if stabilized)
    - Root cause analysis (A3 §9 Energy, §10 Conflict)
    - Building blocks completeness (D1 §4)
    - Identify principle violations (P1-P10)
  
  Month 4+: Check Exit Criteria (CORE/08 §4)
    IF H_Score > 45 for 3 months → Transition Path 3
    ELSE continue stabilization

Do_NOT: Major reorg during crisis (AP33 - CORE/08 §5)
Focus: Stabilize → Diagnose → Transform (sequence critical)
```

---

### Path 3: CHANGE READINESS ASSESSMENT (H_Score 45-60)

```yaml
Condition:
  - H_Score 45-60 (stable but opportunity for improvement)
  - No observables < 30 (no crisis)
  - Transformation desired

Action: ASSESS READINESS (5 Dimensions)

Dimensions (Rate 1-5 each):
  
  1. Leadership_Alignment:
     5: Executive team 100% unified on need/approach
     3: Majority support, some skeptics
     1: No alignment, fragmented leadership
  
  2. Urgency_Level:
     5: Compelling case for change NOW (market threat, opportunity window)
     3: Change desirable but no burning platform
     1: No clear urgency, status quo acceptable
  
  3. Resource_Availability:
     5: Time, money, people fully allocated to transformation
     3: Resources available but constrained
     1: No resources, org at capacity limit
  
  4. Capability:
     5: Skills to design/implement in-house OR budget for consultants
     3: Some skills, need upskilling/hiring
     1: No transformation capability, no budget to acquire
  
  5. Organizational_Bandwidth:
     5: Can absorb change while maintaining operations (utilization <80%)
     3: Tight but manageable (utilization 80-90%)
     1: Overloaded, no capacity for change (utilization >95%)

Decision_Matrix:
  
  IF ALL dimensions >= 4:
    → PROCEED full transformation (§1-§6 playbook)
  
  IF MOST dimensions >= 3:
    → PROCEED pilot/phased approach
    → Start with 1-2 teams, 3-month pilot
    → Learn and adjust before scaling
  
  IF ANY dimension < 3:
    → BUILD READINESS first
    → Address gaps (leadership alignment workshops, free up capacity, etc.)
    → Re-assess in 3-6 months
  
  IF ANY dimension = 1:
    → DELAY transformation
    → Not ready, forcing change will fail
    → Focus on prerequisite work first
```

---

### Path 4: EVOLUTIONARY IMPROVEMENT (H_Score > 60)

```yaml
Condition:
  - H_Score > 60 (healthy organization)
  - No crisis indicators
  - Continuous improvement desired

Action: STANDARD PLAYBOOK

Protocol:
  - Follow §1-§6 normal cadence
  - No urgency, take time to do it right
  - Emphasize learning and capability building
  - Low risk tolerance for disruption

Focus: Incremental excellence, not survival
```

---

### Readiness Anti-Patterns

```yaml
AP32_Forcing_Transformation_Unprepared:
  Síntoma: Iniciar transformation con readiness score <3
  Causa: Executive impatience, ignoring prerequisites
  Consecuencia: 70% failure rate transformations
  Fix: Build readiness first, patience required

AP33_Transforming_During_Crisis:
  Síntoma: Major reorg while H_Score <45
  Causa: "Never waste a crisis" mal interpretado
  Consecuencia: Crisis deepens, transformation fails
  Fix: Stabilize FIRST (P52), transform AFTER (H>45)
```

---

## §1. PLAYBOOK TRANSFORMACIÓN

### Overview 6 Fases

```yaml
Duración_Total: 12-24 meses (típico org 100-500 personas)
Fases:
  1. DIAGNÓSTICO (3-4 semanas)
  2. DISEÑO (4-6 semanas)
  3. PREPARACIÓN (4-8 semanas)
  4. PILOTO (8-12 semanas)
  5. ESCALAMIENTO (12-24 semanas)
  6. SOSTENIBILIDAD (continuo)

Objetivo: H_Score de X → >80 en 12-18 meses
```

---

## §2. FASE 1: DIAGNÓSTICO (3-4 SEMANAS)

**Ver detalle completo:** `APLICACION/A3_Diagnostico.md`

### Deliverables

```yaml
Week_1:
  ☐ Kick-off meeting completado
  ☐ Accesos sistemas obtenidos
  ☐ 10 entrevistas realizadas

Week_2:
  ☐ 20 entrevistas restantes
  ☐ Métricas 11 observables recolectadas
  ☐ Análisis preliminar

Week_3:
  ☐ H_Score calculado
  ☐ Antipatrones identificados (AP01-AP35: 30 base + 5 v1.3)
  ☐ Patrones gap analysis (P01-P53: 50 base + 3 emergentes)

Week_4:
  ☐ Top 5 recomendaciones priorizadas
  ☐ Executive summary deck preparado
  ☐ Presentación C-level realizada
  ☐ Budget aprobado para Fase 2
```

---

### Gates Críticos

```yaml
Gate_1.1_Access_Confirmado:
  Criterio: Tenemos acceso completo sistemas + calendarios entrevistas
  Si_NO: Escalate sponsor, puede delay 1-2 semanas

Gate_1.2_H_Score_Calculable:
  Criterio: 8+ de 11 observables con datos suficientes
  Si_NO: Extender recolección datos, focus observables críticos

Gate_1.3_Budget_Aprobado:
  Criterio: C-level aprueba investment Fases 2-6
  Si_NO: Reducir scope O pausar (transformación requiere funding)
```

---

## §3. FASE 2: DISEÑO (4-6 SEMANAS)

### Objetivo

```yaml
Input: Top 5 recomendaciones Fase 1
Output: Blueprint detallado target state + roadmap 12 meses
```

---

### Actividades

#### Semana 1-2: Target State Design

```yaml
Arquitectura_Target:
  - Org chart futuro (teams, roles, reporting)
  - RACI matrices nuevas
  - Governance model (ARB, decision rights)
  - Ejemplo: Si REC-02 = "Cross-functional teams"
    → Diseñar 8 teams específicos (nombres, ownership, headcount)

Tecnología_Target:
  - Architecture diagram (si cambios tech)
  - CI/CD pipeline futuro
  - Tech stack rationalization
  - Ejemplo: Si implementas P23 (Feature Flags)
    → Tool selection (LaunchDarkly, Unleash, custom)

Proceso_Target:
  - Workflows futuros (value stream maps)
  - Ceremonies (si Scrum/Kanban)
  - KPIs tracking
```

---

#### Semana 3-4: Transition Plan

```yaml
Gap_Analysis:
  Estado_Actual → Estado_Target
  Por_Cada_Gap:
    - ¿Qué debe cambiar?
    - ¿Quién afectado?
    - ¿Cuánto tiempo?
    - ¿Qué risks?

Change_Impact_Assessment:
  Por_Persona (sample 20%):
    - ¿Cambia rol? (Sí/No)
    - ¿Cambia manager? (Sí/No)
    - ¿Cambia herramientas? (Sí/No)
    - ¿Cambia ubicación física? (Sí/No)
    - Impact_Score: Alto/Medio/Bajo

Risks_Catalog:
  Risk_1:
    Descripción: "Resistance managers funcionales (pierden autoridad)"
    Probabilidad: 70%
    Impacto: Alto (puede bloquear transformación)
    Mitigación: "Include en coalición, win-win negotiation"
  
  Risk_2:
    Descripción: "Tech debt crítico impide velocity durante transition"
    Probabilidad: 50%
    Impacto: Medio (delay 4-8 semanas)
    Mitigación: "20% rule desde Week 1, freeze features 2 sprints"
```

---

#### Semana 5-6: Roadmap & Resource Planning

```yaml
Roadmap_12_Meses:
  Q1_Meses_1-3:
    - Quick wins (REC-01, REC-03)
    - Pilot preparation (REC-02)
  
  Q2_Meses_4-6:
    - Pilot execution (2 teams)
    - Learning & adjustments
  
  Q3_Meses_7-9:
    - Scale (8 teams total)
    - Consolidate gains
  
  Q4_Meses_10-12:
    - Full adoption
    - Measure H_Score improvement
    - Plan next wave

Investment_Plan:
  Headcount:
    - Transformation PMO: 2-3 personas full-time
    - Enabling teams (si P05): 1-2 personas per team helped
    - Backfill: 10-20% capacity teams durante transition
  
  Budget:
    - Tooling (ej: Feature flags, CI/CD, analytics): $50K-$200K
    - Consulting (si externa): $100K-$500K
    - Training: $20K-$50K
    - Contingency (15%): $X
  
  Timeline_Total: 12 meses
  ROI_Expected: 2-3× investment en año 1 post-implementation
```

---

### Deliverables Fase 2

```yaml
☐ Target state blueprint (org chart, RACI, processes)
☐ Gap analysis completo
☐ Risk catalog + mitigations
☐ Roadmap 12 meses detallado
☐ Investment plan aprobado
☐ Coalición guiding formada (8-12 personas key)
```

---

### Gates Críticos

```yaml
Gate_2.1_Target_State_Validated:
  Criterio: 80%+ stakeholders "esto tiene sentido"
  Validación: 5-10 entrevistas validación design
  Si_NO: Ajustar design, otra ronda feedback

Gate_2.2_Coalition_Formed:
  Criterio: 8-12 personas key committed (power+expertise+credibility)
  Si_NO: No proceder Fase 3, transformación fracasará sin coalición
```

---

## §4. FASE 3: PREPARACIÓN (4-8 SEMANAS)

### Objetivo

```yaml
Preparar org para transition: comunicar, entrenar, ajustar systems
```

---

### Actividades

#### Semana 1-2: Comunicación

```yaml
Town_Hall_Kickoff:
  Audiencia: Toda org (all-hands)
  Duración: 60 min
  Contenido:
    - Por qué transformamos (pain actual, visión futura)
    - Qué cambia (high-level)
    - Timeline (cuándo cada quien afectado)
    - FAQ (top 10 preguntas anticipadas)
    - Q&A abierto
  
  Tono: Transparente, honesto, inspirador (no "corporate BS")

Communication_Plan:
  Frecuencia: Bi-weekly updates (newsletter, Slack)
  Canales:
    - Email C-level → all company
    - Slack channel #transformation (AMA)
    - Manager cascade (talking points provistos)
  
  Mensajes_Clave:
    - "Por qué" (business case claro)
    - "Qué hay para mí" (WIIFM - What's In It For Me)
    - "Cómo participo" (feedback loops)
```

---

#### Semana 3-4: Training

```yaml
Training_Modules:
  
  Module_1_All_Hands (2 hrs):
    - Intro KERNEL framework
    - Nuevos workflows (ej: cross-functional teams cómo operan)
    - Nuevas herramientas (ej: feature flags, Kanban boards)
  
  Module_2_Managers (4 hrs):
    - Leadership en transformación
    - Managing resistance
    - Coaching teams through change
  
  Module_3_Technical (8 hrs, solo eng):
    - CI/CD nuevo pipeline
    - Feature flags hands-on
    - Pair programming IA (si aplica)

Delivery:
  - Virtual (grabado) + Live Q&A
  - Mandatory attendance tracked
  - Quiz post-training (80% pass rate target)
```

---

#### Semana 5-8: Systems & Tools Setup

```yaml
Infrastructure:
  ☐ CI/CD pipeline configurado (staging, prod, rollback)
  ☐ Feature flags platform deployed (ej: LaunchDarkly)
  ☐ Monitoring dashboards (H_Score, métricas flow)
  ☐ Data pipelines (para 11 observables automation)

Governance:
  ☐ ARB calendar establecido (weekly slot)
  ☐ Decision log template + process
  ☐ OKRs templates + timeline Q planning

Documentation:
  ☐ Runbooks actualizados
  ☐ Team charters escritos (8 teams si esa es target)
  ☐ RACI matrices publicadas (Confluence, Notion)
```

---

### Deliverables Fase 3

```yaml
☐ Town hall realizado, grabación compartida
☐ Training completado (>90% attendance)
☐ Tools & systems live en staging
☐ Pilot teams seleccionados (2 teams para Fase 4)
☐ Pilot ready checklist 100% completado
```

---

### Gates Críticos

```yaml
Gate_3.1_Communication_Reach:
  Criterio: >85% org aware of transformation (survey)
  Si_NO: Extended communication, address pockets sin info

Gate_3.2_Pilot_Teams_Ready:
  Criterio: 2 teams volunteer + trained + systems access
  Si_NO: Delay Fase 4, need better preparation
```

---

## §5. FASE 4: PILOTO (8-12 SEMANAS)

### Objetivo

```yaml
Validar target state con 2 teams, learn & adjust antes full rollout
```

---

### Pilot Team Selection

```yaml
Criterios:
  - High-performing team (no struggling team como piloto)
  - Representative work (típico org, no edge case)
  - Manager entusiasta (champion, no skeptic)
  - Headcount 5-9 personas (two-pizza team)
  - Tenure >6 meses avg (no new hires)

Ejemplo:
  Pilot_Team_A: "Payments Team" (7 personas, manager Sarah - champion)
  Pilot_Team_B: "Catalog Team" (6 personas, manager John - open-minded)
```

---

### Semana 1-4: Pilot Execution

```yaml
Week_1:
  - Pilot teams transition a target state
  - Ejemplo: Si cross-functional, reassign QA engineer a team
  - Daily check-ins con transformation PMO

Week_2-3:
  - Operate en nuevo modelo
  - Medir métricas baseline vs nuevo:
      * Cycle time
      * Throughput
      * WIP
      * Team satisfaction (survey semanal)
  
Week_4:
  - Mid-pilot retrospectiva
  - Ajustes menores (OK cambiar proceso si no funciona)
```

---

### Semana 5-8: Learning & Iteration

```yaml
Data_Collection:
  Quantitative:
    - Cycle time: Pilot vs Control teams
    - Throughput: Items/week
    - Incident rate: Bugs escaped to prod
    - Deployment frequency
  
  Qualitative:
    - Weekly surveys pilot teams (5 preguntas, 5 min)
    - Bi-weekly retrospectivas
    - Anecdotes (what surprised them, pain points)

Adjustments:
  Ejemplo_Real:
    Problema: "Daily standups 15 min no suficiente para 7 personas cross-functional"
    Ajuste: "Split en 2 standups: Backend (8 min) + Frontend (8 min)"
    Validación: Team satisfacción +15 pts
```

---

### Semana 9-12: Pilot Wrap-Up

```yaml
Success_Criteria:
  Quantitative_Gates:
    ☐ Cycle time -20%+ vs baseline (target met)
    ☐ Team satisfaction >75/100 (vs 60 baseline)
    ☐ H_Score pilot teams +10 pts
  
  Qualitative_Gates:
    ☐ Team recommends rollout a otros teams (>80% "yes")
    ☐ No blockers críticos sin solución
    ☐ Manager champions advocate publicly

Pilot_Report:
  - Executive summary (2 pgs)
  - Metrics before/after (dashboards)
  - Lessons learned (top 10)
  - Adjustments needed para rollout
  - Go/No-Go recommendation

Decision_Gate:
  Si SUCCESS → Proceder Fase 5 (Scale)
  Si MIXED → Extend pilot 4 semanas, address gaps
  Si FAILURE → Pause, diagnóstico profundo qué falló
```

---

### Deliverables Fase 4

```yaml
☐ Pilot execution completado (12 semanas)
☐ Metrics collected & analyzed
☐ Lessons learned documentadas
☐ Pilot report presentado a C-level
☐ Go decision para Fase 5
```

---

## §6. FASE 5: ESCALAMIENTO (12-24 SEMANAS)

### Objetivo

```yaml
Rollout target state a toda org, wave-by-wave
```

---

### Wave Planning

```yaml
Approach: Rollout incremental, no big-bang

Wave_1 (Semanas 1-6):
  Teams: 2-3 teams nuevos (ya tenemos 2 pilot = 4-5 total)
  Criterio: Managers entusiastas, low risk
  Support: Transformation PMO full-time con estos teams

Wave_2 (Semanas 7-12):
  Teams: 4-6 teams nuevos (total 8-11)
  Criterio: Mayoría teams, include algunos skeptics
  Support: PMO part-time, peer learning (pilot teams ayudan)

Wave_3 (Semanas 13-18):
  Teams: Restantes teams (total org)
  Criterio: Laggers, teams complejos
  Support: Self-service mayormente, PMO solo escalations

Buffer (Semanas 19-24):
  - Consolidación
  - Address edge cases
  - Full stabilization
```

---

### Execution per Wave

```yaml
Pre_Wave_Checklist (2 semanas antes):
  ☐ Teams seleccionados notificados
  ☐ Training scheduled
  ☐ 1:1s con cada persona afectada (manager hace)
  ☐ Tools access provisioned

Wave_Execution (6 semanas):
  Week_1: Transition
  Week_2-5: Operate + support intensivo
  Week_6: Retrospectiva wave, consolidate learnings

Post_Wave:
  ☐ Metrics collected
  ☐ Issues log updated
  ☐ Adjustments para next wave (si necesario)
```

---

### Resistance Management

```yaml
Tipos_Resistance (Ver DOMINIOS/D3 §7):

1. Cognitive (no entienden):
   Fix: Re-comunicar "por qué", data, case studies pilot

2. Emotional (miedo):
   Fix: 1:1s empathy, address fears, safety nets
   Ejemplo: "Si nuevo rol no funciona, puedes volver" (escape hatch)

3. Political (pierden poder):
   Fix: Negotiate win-win, include en coalición, o override si blockers
   Ejemplo: Manager funcional pierde reports → Ofrecer lead platform team

4. Legítima (concerns válidos):
   Fix: ESCUCHAR, adjust plan si hace sentido
   Ejemplo: "Edge case X no contemplado" → Address en design

Escalation_Path:
  Level_1: Team manager
  Level_2: Transformation PMO
  Level_3: Coalición guiding
  Level_4: Sponsor C-level (última instancia)
```

---

### Deliverables Fase 5

```yaml
☐ Wave 1 completado (4-5 teams total)
☐ Wave 2 completado (8-11 teams)
☐ Wave 3 completado (toda org)
☐ H_Score re-medido (esperado +15-25 pts vs baseline)
☐ Retrospectiva transformación completa
☐ Handoff a Fase 6 (sostenibilidad)
```

---

### Gates Críticos

```yaml
Gate_5.1_Wave_Success:
  Criterio: Cada wave >70% teams success criteria met
  Si_NO: Pause next wave, diagnóstico issues

Gate_5.2_H_Score_Improvement:
  Criterio: H_Score +15 pts mínimo vs baseline
  Si_NO: Deep-dive qué no funcionó, adjust antes consolidate
```

---

## §7. FASE 6: SOSTENIBILIDAD (CONTINUO)

### Objetivo

```yaml
Institucionalizar cambios, evitar "volver a old ways"
```

---

### Actividades Continuas

#### Monitoring (Mensual)

```yaml
H_Score_Tracking:
  - Calcular 11 observables mensual
  - Dashboard público (toda org ve)
  - Trend: ¿Mejorando, estable, o degradando?

Metrics_Review:
  - Cycle time, throughput, WIP por team
  - Tech debt score
  - Deployment frequency
  - Incident rate

Alerts_Proactivas:
  Si_H_Score_Cae_>5pts:
    → Alerta Yellow, diagnóstico root cause
  Si_Cae_>10pts:
    → Alerta Red, intervention inmediata
```

---

#### Governance (Trimestral)

```yaml
Quarterly_Business_Review:
  Attendees: C-level + VPs + Transformation PMO
  Agenda:
    1. H_Score trend (30 min)
    2. Top 3 wins (15 min)
    3. Top 3 challenges (15 min)
    4. Adjustments roadmap (30 min)
  
  Output:
    - OKRs ajustados si necesario
    - Budget para siguiente quarter
    - Initiatives nuevas o kill existentes

Retrospectiva_Org:
  Frecuencia: Anual
  Formato: Survey toda org (20 preguntas) + focus groups (30 personas)
  Preguntas:
    - "¿Transformación cumplió promesas?" (1-10)
    - "¿Qué mejoró más?"
    - "¿Qué aún falta?"
    - "¿Recomendarías este cambio a otra org?" (NPS)
```

---

#### Continuous Improvement

```yaml
Kaizen_Culture:
  - Retrospectivas team-level (bi-weekly)
  - Action items tracked (max 3 per retro)
  - Experiments small (<2 semanas) continuous

Pattern_Library_Update:
  - Si descubres nuevo patrón (P51), documentar
  - Si antipatrón emerge (AP31), alertar
  - Share learnings cross-org (tech talks, wikis)

Training_Refresh:
  - Onboarding new hires: KERNEL intro (2 hrs)
  - Annual refresher: "What's new in KERNEL" (1 hr)
```

---

### Handoff Transformation PMO → BAU

```yaml
Timeline: Meses 18-24 post-kick-off

PMO_Responsibilities_Decrease:
  Mes_18:
    - PMO de 3 personas → 1 persona (70% reduction)
    - Transition ownership a line managers
  
  Mes_24:
    - PMO disuelto
    - Responsibilities embedded BAU:
        * H_Score tracking → Data team
        * QBR → C-level existing meeting
        * Training → HR onboarding

Criteria_Handoff:
  ☐ H_Score stable >80 por 2 quarters consecutivos
  ☐ <5% teams reverting a old ways
  ☐ Managers confident owning continuous improvement
  ☐ No dependency en transformation PMO para operate
```

---

### Deliverables Fase 6

```yaml
☐ H_Score monitoring dashboard live
☐ QBR cadence establecida (quarterly)
☐ Continuous improvement embedded (retros, experiments)
☐ PMO handoff completado (Mes 24)
☐ Transformation declared "complete" (celebrate! 🎉)
```

---

## §8. MÉTRICAS SUCCESS TRANSFORMACIÓN

### Leading Indicators (Monitorear durante)

```yaml
Durante_Fases_1-5:
  - Participation rate training (target >90%)
  - Survey sentiment (target >70/100)
  - Escalations count (target decreasing)
  - Pilot team satisfaction (target >75/100)
```

---

### Lagging Indicators (Medir outcome)

```yaml
Al_Final_Fase_5 (Mes 12):
  - H_Score: Baseline → Target (ej: 66 → 85, +19 pts ✅)
  - Cycle time: -40% (ej: 16d → 9d)
  - Deployment frequency: +500% (ej: 1×/mes → 2×/semana)
  - Turnover: -30% (ej: 22% → 15%)
  - NPS employees: +20 pts (ej: 45 → 65)

ROI_Calculation:
  Investment: $800K (PMO + tools + training)
  Benefits_Year_1:
    - Velocity gain: $1.2M (más features, faster time-to-market)
    - Churn reduction: $400K (si O2 mejoró)
    - Incident reduction: $200K (menos downtime)
  Total_Benefits: $1.8M
  ROI: ($1.8M - $800K) / $800K = 125% año 1
```

---

## §9. PLAYBOOK POR ANTIPATRÓN

**Ejemplo:** Si AP14 (Tech Debt Perpetuo) detectado

```yaml
Fase_1_Diagnóstico:
  - Confirmar síntomas: Tech debt score >50, velocity -40%+
  - Calcular cost of delay: $250K/mes per 100 eng

Fase_2_Diseño:
  - Target: Tech debt score <30, 20% rule implementado
  - Plan: 2 sprints freeze features, refactor top 3 módulos

Fase_3_Preparación:
  - Comunicar: "Por qué freeze features" (business case)
  - Training: Refactoring patterns, test automation

Fase_4_Piloto:
  - 2 teams implementan 20% rule (4 semanas)
  - Medir: Velocity recovery, tech debt score evolution

Fase_5_Scale:
  - Rollout 20% rule a todos teams (8 semanas)
  - Quality gates CI/CD (coverage >80%)

Fase_6_Sostenibilidad:
  - Monitor tech debt score mensual
  - Alert si sube >30 (regression)
```

---

## Referencias Cruzadas

- **Crisis Management (P52):** `CORE/08_Crisis_Management.md` (activation, structure, exit criteria)
- **Diagnóstico:** `APLICACION/A3_Diagnostico.md`
- **Patrones implementar:** `APLICACION/A1_Patrones.md`
- **Antipatrones remediar:** `APLICACION/A2_Antipatrones.md`
- **Preparación R1-R5:** `DOMINIOS/D3_Decision.md` §3
- **Métricas tracking:** `APLICACION/A5_Medicion.md`
