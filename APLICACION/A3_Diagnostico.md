# A3_Diagnostico

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Consultores, Arquitectos Empresariales, Líderes

---

## §1. OVERVIEW FRAMEWORK DIAGNÓSTICO

### Propósito

```yaml
Objetivo: Evaluar health organizacional end-to-end mediante KERNEL
Salida: H_Score (0-100) + recomendaciones priorizadas
Duración: 2-4 semanas típico (depende org size)
Audiencia_Reporte: C-level, Board (strategic), Managers (tactical)
```

---

### 5 Fases

```
1. PREPARACIÓN (3-5 días)
   - Definir scope, stakeholders clave, access datos
   
2. RECOLECCIÓN_DATOS (5-10 días)
   - 11 observables (O1-O8, I1-I3)
   - Entrevistas (20-30 personas)
   - Métricas sistemas

3. ANÁLISIS (3-5 días)
   - Calcular H_Score
   - Identificar antipatrones (AP01-AP35: 30 base + 5 crisis/orchestration)
   - Detectar patrones faltantes (P01-P53: 50 base + 3 emergentes)

4. RECOMENDACIONES (2-3 días)
   - Priorizar top 5 iniciativas
   - Roadmap 12 meses
   - Quick wins (30-90 días)

5. PRESENTACIÓN (1-2 días)
   - Executive summary (C-level)
   - Detailed report (managers)
   - Workshop actionable
```

---

## §2. PREPARACIÓN (FASE 1)

### Checklist Inicio

```yaml
Logística:
  ☐ Sponsor C-level identificado (CEO/CTO)
  ☐ Budget aprobado ($X para consultoría si externa)
  ☐ Timeline acordado (2-4 semanas)
  ☐ NDA firmado si datos sensibles

Access:
  ☐ Acceso sistemas métricas (Jira, Git, CI/CD, etc.)
  ☐ Calendario 20-30 entrevistas bloqueado
  ☐ Docs internos (org chart, OKRs, roadmaps)
  ☐ Financials si relevante (revenue, churn, etc.)

Scope:
  ☐ Boundary org (¿toda empresa o solo Engineering?)
  ☐ Profundidad (high-level o deep-dive por dominio)
  ☐ Focus areas si dirigido (ej: solo Operación, solo IA)
```

---

### Template Kick-Off

```yaml
Meeting_Duration: 90 min
Attendees: Sponsor, stakeholders clave (5-8 personas)

Agenda:
  1. Intro KERNEL framework (15 min)
  2. Objetivos diagnóstico (10 min)
  3. Metodología (11 observables, H_Score) (20 min)
  4. Timeline & logistics (10 min)
  5. Q&A (20 min)
  6. Next steps (15 min)

Outputs:
  - Lista entrevistados (roles, fechas)
  - Accesos sistemas confirmados
  - Questions específicas sponsor quiere responder
```

---

## §3. RECOLECCIÓN DATOS (FASE 2)

### 11 Observables: Data Sources

| Observable | Source Primaria | Source Secundaria | Tooling Típico |
|-----------|-----------------|-------------------|----------------|
| **O1 (Demanda)** | Jira backlog, sales pipeline | Entrevistas PMs | Jira, Salesforce |
| **O2 (Valor)** | NPS, CSAT, churn metrics | Customer interviews | Qualtrics, Mixpanel |
| **O3 (Capacidad)** | Headcount, utilization | Entrevistas managers | HR system, Jira |
| **O4 (Eventos)** | Incident logs, regulatory changes | Entrevistas CTO | PagerDuty, legal |
| **O5 (Restricciones)** | Compliance audits, SLA breaches | Entrevistas compliance | SOC2 reports |
| **O6 (Competencia)** | Market research, win/loss data | Entrevistas sales | G2, Crunchbase |
| **O7 (Dependencias)** | Vendor contracts, integration logs | Entrevistas architects | Contract mgmt |
| **O8 (Calidad Info)** | Data quality reports, trust surveys | Entrevistas data team | DBT, Alation |
| **I1 (Velocidad Decisional)** | Decision log, escalations | Entrevistas managers | Custom tracking |
| **I2 (Salud Talento)** | Engagement surveys, turnover | Entrevistas HR | Culture Amp, Lattice |
| **I3 (Eficiencia Flujo)** | Cycle time, throughput, WIP | Git, Jira | LinearB, Jellyfish |

---

### Template Entrevista

```yaml
Duración: 45-60 min
Formato: Semi-estructurado (preguntas guía + follow-up)

Secciones:
  1. Contexto (5 min):
     - Rol, tenure, team size
  
  2. Estado actual (15 min):
     - "¿Cuáles son tus top 3 challenges hoy?"
     - "¿Qué funciona bien?"
  
  3. Por dominio (20 min):
     - Arquitectura: "¿Es clara la estructura org? ¿Quién decide qué?"
     - Percepción: "¿Tienes datos confiables para decisiones?"
     - Decisión: "¿Cómo priorizas? ¿Qué tan rápido decides?"
     - Operación: "¿Cómo mides velocity? ¿Tech debt es manejable?"
  
  4. IA (si aplica) (10 min):
     - "¿Usan IA/ML? ¿En qué modo (M1-M6)?"
     - "¿Confían en outputs IA?"
  
  5. Cierre (10 min):
     - "Si tuvieras varita mágica, ¿qué cambiarías?"
     - "¿Algo más importante mencionar?"

Notas:
  - Grabar (con permiso) para accuracy
  - Confidencialidad: feedback anónimo en reporte
```

---

### Matriz Roles × Preguntas

| Rol | Focus Preguntas |
|-----|-----------------|
| **C-level** | Estrategia, OKRs, presupuesto, top risks |
| **VP/Directors** | Priorización portfolio, resource allocation, coordination cross-team |
| **Managers** | Team health, velocity, blockers, tech debt |
| **ICs (Individual Contributors)** | Herramientas, process pain points, autonomy |
| **Product** | Roadmap, discovery, customer feedback |
| **Data/Analytics** | Data quality, lineage, trust |

---

## §4. ANÁLISIS (FASE 3)

### Cálculo H_Score

**Ver fórmula completa:** `DOMINIOS/D2_Percepcion.md` §4

```yaml
Paso_1: Score cada observable 0-100
Paso_2: Aplicar ponderaciones
  H = 0.12*O1 + 0.15*O2 + 0.10*O3 + 0.08*O4 + 
      0.10*O5 + 0.10*O6 + 0.08*O7 + 0.07*O8 +
      0.08*I1 + 0.08*I2 + 0.04*I3

Paso_3: Interpretación
  90-100: Excelente
  75-89: Bueno
  60-74: Atención requerida
  <60: Crítico
```

---

### Detección Antipatrones

```yaml
Por_Cada_Antipatrón (AP01-AP35):
  1. Check síntomas (métricas + entrevistas)
  2. Si 2+ síntomas presentes → AP confirmado
  3. Severity: 🔴 Crítico / 🟡 Alto / 🟢 Moderado
  
  Antipatrones_v1.3_Nuevos:
    - AP31 (Crisis Theater): Declarar crisis sin cambiar governance
    - AP32 (Forcing Transformation Unprepared): Transform sin readiness R1-R5
    - AP33 (Transforming During Crisis): Transform cuando H_Score<45
    - AP34 (No Orchestration): N agents compiten, conflicts sin coordinator
    - AP35 (Over-Orchestration): Orchestrator bottleneck, agents await approval

Priorización:
  - Críticos first (AP con severidad 🔴)
  - Ordenar por impact (Cost of Delay × Probability)

Ejemplo:
  AP14 (Tech Debt Perpetuo):
    ✅ Síntoma 1: Tech debt score 68 (threshold <30)
    ✅ Síntoma 2: Velocity -62% vs baseline
    ✅ Síntoma 3: Incident rate +200%
    → AP14 confirmado, Severity 🔴
    → Cost of Delay: $250K/mes (per 100 eng)
    → Top priority remediation
```

---

### Patrones Faltantes

```yaml
Por_Cada_Patrón (P01-P53):
  1. ¿Está implementado?
  2. Si NO y contexto aplica → Gap identificado
  3. ROI_Estimado patrón (Ver §8 A1_Patrones)

Ejemplo:
  P23 (Feature Flags):
    Estado: No implementado
    Contexto: Deploy frequency <1/mes, rollback 30+ min
    → Patrón aplica
    ROI: Deploy frequency 2×/día, rollback <1 min
    → Recomendar implementar (quick win)
```

---

### Evaluación Awareness Levels (S1-S3)

```yaml
Objetivo:
  Diagnosticar madurez percepción en 3 niveles cognitivos (CORE/02 §2, D2 §5)

Checklist_Por_Level:

S1_DETECT (Percibir):
  ☐ ¿Org captura metrics raw de systems críticos?
  ☐ ¿Dashboards disponibles para observables O1-O8, I1-I3?
  ☐ ¿Telemetry real-time o near-real-time?
  ☐ ¿Logs aggregated y searchable (ELK, Splunk)?
  
  Score_S1 (0-100):
    = (% systems_monitored + dashboard_coverage + telemetry_quality) / 3
  
  Target: >80
  Gap_Típico: M1 agents faltantes (monitoring automated)

S2_COMPREHEND (Comprender):
  ☐ ¿H_Score calculado automáticamente? (11 observables → 1 metric)
  ☐ ¿Alerting context-aware? (no solo raw thresholds)
  ☐ ¿Observables interpretados con contexto business?
  ☐ ¿Pattern recognition automated? (anomaly detection)
  
  Score_S2 (0-100):
    = (h_score_automated + alerting_quality + pattern_detection) / 3
  
  Target: >70
  Gap_Típico: M2 agents faltantes (intelligent alerting, synthesis)

S3_PROJECT (Proyectar):
  ☐ ¿Forecasting trends implementado? (revenue, churn, capacity)
  ☐ ¿Crisis thresholds monitoreados? (H_Score<45 trigger alerts)
  ☐ ¿Scenario planning tools available? (Monte Carlo, what-if)
  ☐ ¿Predictive models en producción? (churn, demand, failures)
  
  Score_S3 (0-100):
    = (forecasting + crisis_monitoring + scenarios + predictive_models) / 4
  
  Target: >60
  Gap_Típico: M3 agents faltantes (predictive analytics, simulation)

Awareness_Maturity_Overall:
  Score = (S1 × 0.4) + (S2 × 0.35) + (S3 × 0.25)
  
  Interpretación:
    >80: Excelente - Full spectrum awareness
    60-80: Bueno - S1+S2 strong, S3 emergente
    40-60: Atención - Solo S1, gaps S2-S3
    <40: Crítico - Awareness básica insuficiente
```

---

### Evaluación Decision Modes (D1-D4)

```yaml
Objetivo:
  Diagnosticar madurez decisional en 4 modos complejidad (CORE/02 §3, D3 §6)

Checklist_Por_Mode:

D1_DIRECT_FEEDBACK (Automática):
  ☐ ¿Qué decisiones automáticas existen? (list 10+)
  ☐ Ejemplos: Autoscaling, circuit breakers, fraud rules simple
  ☐ ¿Bounded autonomy clara? (M6 con limits explícitos)
  
  Automation_D1_Rate:
    = # decisiones_D1_automated / # decisiones_D1_posibles
    Target: >60%
  
  Gap: Opportunities para M6 automation (thermostat-style loops)

D2_RULE_BASED (Condicional):
  ☐ ¿Business rules explícitas? ¿Documentadas?
  ☐ ¿Approval workflows automated? (>$10K require VP)
  ☐ ¿Rules engine en uso? (Drools, decision tables)
  
  Rules_Coverage_D2:
    = # business_rules_documented / # critical_decision_types
    Target: >90%
  
  Gap: Rules engines faltantes, rules tribal knowledge (M4-M5)

D3_ASSOCIATIVE (Expertise-based):
  ☐ ¿ML models en producción? ¿Qué deciden?
  ☐ ¿Human validation required? (M4 control)
  ☐ ¿Model monitoring? (drift, accuracy, fairness)
  
  ML_Production_D3:
    = # ML_models_serving_decisions
    Target: 5-10 models (depends on org size)
  
  Gap: ML/AI underutilized, no human-in-loop validation

D4_KNOWLEDGE_BASED (Analítica):
  ☐ ¿Strategic planning structured? (OKRs, roadmaps)
  ☐ ¿Simulation tools available? (Monte Carlo, scenarios)
  ☐ ¿Decision latency acceptable? (<7 days strategic)
  
  Decision_Latency_D4:
    = Avg time desde problem identified → decision made
    Target: <7 days (strategic), <24hrs (tactical)
  
  Gap: Decision support tools (M2-M3 enable), analysis paralysis

Decision_Maturity_Overall:
  Automation_Score = % decisiones repeatables que están automated
  
  Benchmark:
    >50%: Excelente - Alta automation apropiada
    30-50%: Bueno - Balance automation/human
    15-30%: Atención - Underautomated
    <15%: Crítico - Manual decision overload
```

---

## §5. RECOMENDACIONES (FASE 4)

### Framework Priorización

```yaml
Score_Iniciativa = (
  0.40 × Impact_Estimado +
  0.25 × Urgencia +
  0.20 × Feasibility +
  0.15 × Strategic_Fit
)

Impact_Estimado:
  - H_Score mejora esperada (ej: +15 pts)
  - ROI financiero ($ savings o revenue)

Urgencia:
  - Severity antipatrón (🔴=100, 🟡=60, 🟢=30)
  - Deadline externo (regulación, competitor)

Feasibility:
  - R1-R5 preparación score (Ver DOMINIOS/D3)
  - Complejidad técnica

Strategic_Fit:
  - Alignment OKRs existentes
  - Sponsor C-level disponible
```

---

### Template Recomendación

```yaml
Iniciativa_ID: REC-XX
Título: [Nombre descriptivo]
Antipatrón_Mitigado: [APXX] O Patrón_Implementado: [PXX]

Problema_Actual:
  - [Síntomas observados]
  - [Métricas actuales vs target]

Solución_Propuesta:
  - [Patrón a implementar]
  - [Cambios específicos org/tech/process]

Beneficios_Esperados:
  - H_Score: +X puntos (Y → Z)
  - Métricas específicas: [ej: cycle time 14d → 5d]
  - ROI: $X ahorros/año

Effort_Estimado:
  - Duración: X semanas/meses
  - Headcount: Y personas
  - Budget: $Z

Riesgos:
  - [Riesgo 1 + mitigación]
  - [Riesgo 2 + mitigación]

Preparación_R1-R5:
  - R1 (Momentum): XX/100
  - R2 (Capabilities): YY/100
  - R3 (Forces): ZZ/100
  - R4 (Drivers): AA/100
  - R5 (Catalysts): BB/100
  - Score Total: CC/100 (GO / GO CONDITIONAL / NO-GO)

Prioridad: Alta / Media / Baja
Timeline: Q1 2025 / Q2 2025 / etc.
Owner_Propuesto: [Rol]
```

---

### Top 5 Iniciativas Típicas

```yaml
1. Remediar_Tech_Debt (si AP14 presente):
   - Implementar 20% rule capacity health
   - Quick win visible (velocity +40% en 8 semanas)

2. Implementar_Feature_Flags (si AP18):
   - Deploy ≠ Release
   - ROI: Deploy frequency 10×, rollback <1min

3. OKRs_Bottom-Up (si AP19, AP20):
   - Outcomes no outputs
   - Alignment strategy ↔ execution

4. Cross-Functional_Teams (si AP03):
   - Eliminar silos
   - Cycle time -50%

5. Anomaly_Detection_IA (si O8 bajo):
   - M2 mode alertas automáticas
   - Proactive vs reactive
```

---

## §6. PRESENTACIÓN (FASE 5)

### Executive Summary (C-level, 30 min)

```yaml
Slide_1: H_Score Overall
  - Score: XX/100 (Bueno/Atención/Crítico)
  - Trend: vs Q anterior si disponible
  - Top 3 fortalezas
  - Top 3 gaps

Slide_2: Observables Breakdown
  - 11 observables visual (radar chart)
  - Rojos: [OX, IY] críticos
  - Verdes: [OZ] excelentes

Slide_3: Antipatrones Críticos
  - APXX: [Nombre], Cost $X/mes, Severity 🔴
  - APYY: [Nombre], Cost $Y/mes, Severity 🔴
  - Total: Z antipatrones, $W/mes cost

Slide_4: Top 5 Recomendaciones
  - REC-01: [Título], Impact +X pts H_Score, ROI $Y
  - REC-02: ...
  - REC-03: ...
  - REC-04: ...
  - REC-05: ...

Slide_5: Roadmap 12 Meses
  - Q1: Quick wins (REC-01, REC-03)
  - Q2: Foundations (REC-02)
  - Q3-Q4: Transformational (REC-04, REC-05)

Slide_6: Investment Requerido
  - Budget: $X total
  - Headcount: Y personas dedicated
  - Timeline: Z meses
  - ROI: A× en año 1

Slide_7: Next Steps
  - Aprobar budget
  - Asignar owners iniciativas
  - Kick-off REC-01 (quick win)
```

---

### Detailed Report (Managers, 50-80 páginas)

```yaml
Estructura:
  1. Executive Summary (5 pgs)
  2. Metodología (3 pgs)
  3. Findings (30 pgs)
     - Por dominio (Arquitectura, Percepción, Decisión, Operación)
     - 11 observables detallados
     - Antipatrones identificados
  4. Recomendaciones (20 pgs)
     - Top 5 detalladas
     - Otras 10 priorizadas
  5. Appendix (20 pgs)
     - Raw data
     - Interview quotes (anónimos)
     - Benchmarks industry

Formato:
  - PDF + Excel (datos raw para analysis)
  - Confidencial (no share fuera org sin approval)
```

---

## §7. EJEMPLO COMPLETO: CASO FICTICIO "TechCorp"

### Contexto

```yaml
Org: TechCorp (B2B SaaS, 150 personas, 80 eng)
Duración_Diagnóstico: 3 semanas
Sponsor: CTO
Objetivo: Entender por qué velocity cayó 40% último año
```

---

### H_Score Calculado

```yaml
Observables:
  O1_Demanda: 75 (backlog creciendo sano)
  O2_Valor: 55 (NPS 28, churn 12% - CRÍTICO)
  O3_Capacidad: 65 (utilization 92%, capacity free 8% - límite)
  O4_Eventos: 85 (sin disrupciones mayores)
  O5_Restricciones: 90 (compliance OK)
  O6_Competencia: 60 (perdiendo vs competitor X)
  O7_Dependencias: 80 (vendors estables)
  O8_Calidad_Info: 70 (data quality 75%, OK)
  I1_Velocidad_Decisional: 45 (TTD 18 días - CRÍTICO)
  I2_Salud_Talento: 50 (turnover 22%, engagement 55 - CRÍTICO)
  I3_Eficiencia_Flujo: 40 (cycle time 16 días, efficiency 18% - CRÍTICO)

H_Score = 0.12*75 + 0.15*55 + 0.10*65 + 0.08*85 + 
          0.10*90 + 0.10*60 + 0.08*80 + 0.07*70 +
          0.08*45 + 0.08*50 + 0.04*40
        = 9 + 8.25 + 6.5 + 6.8 + 9 + 6 + 6.4 + 4.9 + 3.6 + 4 + 1.6
        = 66.05/100 → ATENCIÓN REQUERIDA
```

---

### Antipatrones Detectados

```yaml
Críticos (🔴):
  - AP14 (Tech Debt Perpetuo):
      Síntomas: Velocity -40%, tech debt score 72, incident rate +180%
      Cost: $200K/mes
  
  - AP09 (Handoff Hell):
      Síntomas: 9 handoffs deploy process, cycle time 16 días, efficiency 18%
      Cost: $120K/mes

Altos (🟡):
  - AP03 (Silos Profundos):
      Síntomas: Frontend/Backend/QA teams separados, "not my job" culture
  
  - AP08 (WIP Sin Límite):
      Síntomas: WIP 42 items (team 20 eng), context switching alto
  
  - AP19 (Output Disguised):
      Síntomas: OKRs "Launch 8 features", no outcomes medibles

Total_Cost_of_Delay: ~$320K/mes + opportunity cost churn alto
```

---

### Top 5 Recomendaciones

```yaml
REC-01 (Prioridad ALTA):
  Título: "Implementar 20% Rule Tech Debt"
  Antipatrón: AP14
  Impact: H_Score +8 pts, Velocity +35%
  Effort: 2 sprints setup
  ROI: $150K/mes (velocity recovery)
  Timeline: Inicio inmediato
  Owner: VP Engineering

REC-02 (Prioridad ALTA):
  Título: "Cross-Functional Feature Teams"
  Antipatrón: AP03, AP09
  Patrón: P01 (Feature Teams)
  Impact: H_Score +12 pts, Cycle time 16d → 6d
  Effort: 8 semanas reorg
  ROI: $180K/mes
  Timeline: Q1 2025
  Owner: CTO
  Preparación_R1-R5: 72/100 (GO CONDITIONAL - need address forces)

REC-03 (Prioridad ALTA):
  Título: "WIP Limits Kanban"
  Antipatrón: AP08
  Patrón: P15
  Impact: H_Score +5 pts, Cycle time -30%
  Effort: 2 semanas
  ROI: $60K/mes
  Timeline: Quick win (30 días)
  Owner: Eng Managers

REC-04 (Prioridad MEDIA):
  Título: "OKRs Bottom-Up Outcomes"
  Antipatrón: AP19
  Patrón: P29
  Impact: H_Score +4 pts, Alignment strategy ↔ execution
  Effort: 1 quarter rollout
  ROI: Qualitativo (mejor priorización)
  Timeline: Q2 2025
  Owner: CPO

REC-05 (Prioridad MEDIA):
  Título: "Churn Prediction ML (M2)"
  Observable: O2 bajo (churn 12%)
  Patrón: P39
  Impact: H_Score +6 pts (O2: 55 → 75), Churn 12% → 7%
  Effort: 4 meses (hire DS, build model)
  ROI: $200K/año (churn reduction)
  Timeline: Q2-Q3 2025
  Owner: Head of Data
```

---

### Roadmap 12 Meses

```
Q1_2025 (Meses 1-3):
  - REC-01: 20% rule tech debt (quick win)
  - REC-03: WIP limits (quick win)
  - REC-02: Pilot cross-functional 2 teams

Q2_2025 (Meses 4-6):
  - REC-02: Rollout cross-functional 8 teams total
  - REC-04: OKRs bottom-up Q3 planning
  - REC-05: Start churn prediction (hire, data prep)

Q3_2025 (Meses 7-9):
  - REC-05: Deploy churn prediction M2 pilot
  - Consolidate gains REC-01,02,03
  - Measure H_Score (esperado: 66 → 78+)

Q4_2025 (Meses 10-12):
  - REC-05: Scale churn prediction all customers
  - Retrospectiva año, plan 2026
  - Target H_Score >80 EOY
```

---

## §8. HERRAMIENTAS & TEMPLATES

### Plantillas Disponibles

```yaml
Templates_Disponibles:
  - Kick-off deck (PPT)
  - Interview guide (Word)
  - Data collection spreadsheet (Excel)
  - H_Score calculator (Excel con fórmulas)
  - Recommendation template (Word)
  - Executive summary deck (PPT)
  - Detailed report outline (Word)

Ubicación: REFERENCIA/Templates/
```

---

## §9. ENERGY FLOW ANALYSIS

### Concepto

```yaml
Definición:
  Energy = tiempo, atención, esfuerzo invertido por staff
  
  Productive_Energy: Invertida en value creation para clientes
  Dissipated_Energy: Invertida en fricción interna, rework, política
  
Fundamento:
  Organizaciones sanas minimizan dissipation
  Organizaciones enfermas gastan >50% energy en fricción interna
```

---

### Framework Diagnóstico

```yaml
Proceso:
  1. Map_Time_Investment: ¿Dónde staff realmente gasta tiempo?
  2. Categorize_Activities:
     - Value_Creation: Trabajo directo para clientes/productos
     - Necessary_Coordination: Meetings/sync esenciales
     - Waste: Fricción, rework, política, handoffs innecesarios
  3. Identify_Bottlenecks: Dónde energy se acumula (waiting)
  4. Identify_Friction_Points: Dónde energy se disipa (waste)
  5. Trace_to_Root_Causes: Estructura o dynamics causantes

Métrica_Clave:
  Energy_Efficiency = Productive_Energy / Total_Energy
  Target: >60% (healthy), 40-60% (medio), <40% (crítico)
```

---

### Indicadores Energy Dissipation

```yaml
1. Excessive_Coordination_Meetings:
   Síntoma: >30% tiempo semanal en meetings coordinación
   Causa_Root: Boundaries difusos (viola P2 D1), silos sin interfaces
   
2. Repeated_Discussions_Without_Resolution:
   Síntoma: Mismo issue discutido 3+ veces sin decisión
   Causa_Root: Decision rights unclear (viola P1 D1)
   
3. Escalations_for_Routine_Decisions:
   Síntoma: >20 escalaciones/semana a C-level
   Causa_Root: Centralización excesiva (viola P7 D1, P6 Autonomy)
   
4. Rework_Due_to_Unclear_Requirements:
   Síntoma: >25% trabajo re-hecho post feedback
   Causa_Root: Handoff hell (viola P5 D1), communication breakdown
   
5. Conflict_Resolution_Consuming_Mgmt_Time:
   Síntoma: Managers gastan >20% tiempo resolviendo conflictos
   Causa_Root: Domain overlaps (viola P2 D1), conflictos interés (viola P9 D1)
   
6. Politics_and_Relationship_Management:
   Síntoma: Staff gastan tiempo "managing up" vs executing
   Causa_Root: Blame culture (no P10), misaligned incentivos
```

---

### Energy Flow Map (Template)

```yaml
Activity_Categories:
  
  Value_Creation (Target >60%):
    - Coding/designing/building productos
    - Customer support directo
    - Sales/marketing a clientes
    - Research/innovation
  
  Necessary_Coordination (Target 20-30%):
    - Sprint planning, standups, retros (si aportan valor)
    - Cross-team sync esencial
    - 1:1s manager-report
    - Architecture reviews necesarios
  
  Waste_Friction (Target <10%):
    - Meetings sin agenda/outcomes
    - Rework evitable
    - Waiting for approvals/handoffs
    - Resolving conflicts estructurales
    - Búsqueda información (tribal knowledge)
    - Politics/CYA behaviors

Ejemplo_Healthy:
  Value: 65% | Coordination: 25% | Waste: 10%
  → Energy efficiency 65%

Ejemplo_Unhealthy:
  Value: 35% | Coordination: 35% | Waste: 30%
  → Energy efficiency 35%, friction crítica
```

---

### Conexión Observables

```yaml
Energy_Dissipation conecta con:
  - I3 (Eficiencia Flujo): Flow efficiency = productive energy / cycle time
  - I1 (Velocidad Decisional): Decision delays = energy waiting
  - O7 (Dependencias): External dependencies = coordination overhead
  
Uso_Diagnóstico:
  Si I3 <50 → Ejecutar Energy Flow Analysis
  → Identificar categorías waste específicas
  → Trace to structural root causes (P1-P10 violations)
```

---

## §10. CONFLICT PATTERN ANALYSIS

### Concepto

```yaml
Premisa:
  Conflict NO inherentemente malo
  Conflict = información sobre problemas estructurales/dinámicos
  
Tipos_Conflict:
  
  Healthy_Conflict:
    - Disagreement sobre mejor approach a shared goal
    - Task conflict (cómo hacer X mejor)
    - Constructive debate
    - Resuelto colaborativamente
  
  Unhealthy_Conflict:
    - Competition por recursos, territorio, crédito
    - Relationship conflict (personal)
    - Political maneuvering
    - Resuelto por power, no merit
  
  Toxic_Conflict:
    - Unresolved conflicts que festeran
    - Passive-aggressive behaviors
    - Sabotage, blame, CYA
    - Spreads y contamina org culture
```

---

### Conflict Topology Mapping

```yaml
Proceso:
  1. Map_Recurring_Conflicts:
     - Quién conflicts con quién
     - Sobre qué (resources, decisions, territory, credit)
     - Frecuencia (semanal, mensual, ocasional)
  
  2. Identify_Conflict_Clusters:
     - Groups que frecuentemente conflict
     - Departments con alta tensión
     - Interfaces problemáticas
  
  3. Analyze_Conflict_Causes:
     - Domain overlap (P2 D1 violation)
     - Resource competition (governance weakness)
     - Misaligned incentivos (individual vs team metrics)
     - Authority-accountability mismatch (P1 D1 violation)
     - Conflicts of interest (P9 D1 violation)
  
  4. Trace_to_Structural_Problems:
     - Boundaries unclear → Redefinir domains
     - Shared resources → Governance process
     - Misaligned goals → Restructure OKRs
```

---

### Conflict Resolution Patterns

```yaml
Healthy_Pattern:
  - Conflicts resolved at lowest level
  - Parties involucradas resuelven directamente
  - Manager facilita, no decide
  - Process: Identify shared goal → Explore options → Consensus
  - Timeframe: Días, no semanas
  
Unhealthy_Pattern:
  - Conflicts escalated immediately
  - Executives become bottleneck (decide todo)
  - Parties evitan confrontation, esperan escalation
  - Process: Complain to boss → Boss decides → Resentment
  - Timeframe: Semanas, meses
  
Toxic_Pattern:
  - Conflicts not resolved, fester
  - Passive-aggressive behavior
  - Work-arounds en lugar de resolution
  - Trust erodes, collaboration stops
  - Culture contamination spreads
```

---

### Conflict Diagnosis Template

```yaml
Conflict_ID: [Unique identifier]
Parties: [Who vs Who]
Subject: [What about - resources, decision, territory, etc.]
Frequency: [Weekly, Monthly, Once]
Type: [Healthy, Unhealthy, Toxic]

Root_Cause_Hypothesis:
  Structural:
    - [ ] Domain overlap (P2 D1)
    - [ ] Authority mismatch (P1 D1)
    - [ ] Conflict of interest (P9 D1)
    - [ ] Conway mismatch (P4 D1)
  
  Dynamic:
    - [ ] Misaligned incentivos
    - [ ] Resource competition
    - [ ] Information hoarding
    - [ ] Blame culture (violates P10)

Resolution_Pattern: [Healthy/Unhealthy/Toxic]

Recommended_Fix:
  If_Structural: [Reorg, clarify boundaries, split roles]
  If_Dynamic: [Governance process, shared OKRs, blameless postmortems]

Ejemplo:
  Conflict_ID: C-2024-015
  Parties: Product Team A vs Platform Team
  Subject: Platform changes breaking Product features sin notice
  Frequency: Weekly
  Type: Unhealthy
  
  Root_Cause: Boundary unclear (P2 D1) + No interface contract
  Resolution_Pattern: Unhealthy (escalated a CTO cada vez)
  
  Fix: 
    - Structural: Definir API contract formal (SLA, versioning)
    - Dynamic: Platform → Product notification 2 weeks antes breaking changes
    - Governance: Monthly sync Product-Platform roadmaps
```

---

### Conexión Principios

```yaml
Conflict_Patterns revelan violaciones:
  
  Territorial_Disputes → P2 D1 (Boundaries claros) violation
  Finger_Pointing → P1 D1 (Authority-Accountability match) violation
  "Not_My_Job" → P5 D1 (Minimize Handoffs) violation
  Innovation_Blocked → P9 D1 (Avoid Conflicts Interest) violation
  Silos → P10 (Culture Emergence) - estructura genera cultura silo
  
Uso_Diagnóstico:
  Map conflicts → Identify patterns → Trace to principle violations
  → Structural fix (reorg) or Dynamic fix (governance)
```

---

## Referencias Cruzadas

- **11 Observables:** `DOMINIOS/D2_Percepcion.md`
- **H_Score calculation:** `DOMINIOS/D2_Percepcion.md` §4
- **10 Principios Estructurales:** `DOMINIOS/D1_Arquitectura.md` §1
- **Culture Emergence (P10):** `CORE/00_Manifiesto.md` §3
- **Antipatrones:** `APLICACION/A2_Antipatrones.md`
- **Patrones:** `APLICACION/A1_Patrones.md`
- **Preparación R1-R5:** `DOMINIOS/D3_Decision.md` §3
- **Implementación roadmap:** `APLICACION/A4_Implementacion.md`
- **Medición:** `APLICACION/A5_Medicion.md`
