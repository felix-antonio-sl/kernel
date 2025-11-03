# A3_Diagnostico

**Versión:** 2.2.0 | **Estado:** Definitivo | **Audiencia:** Consultores, Arquitectos, Líderes, Security, Product/UX

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
   - 11 observables (O1-O8, IN1-IN3)
   - Entrevistas (20-30 personas)
   - Métricas sistemas

3. ANÁLISIS (3-5 días)
   - Calcular H_Score
   - Identificar antipatrones (AP01-AP40)
   - Detectar patrones faltantes (P01-P64)

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
| **IN1 (Velocidad Decisional)** | Decision log, escalations | Entrevistas managers | Custom tracking |
| **IN2 (Salud Talento)** | Engagement surveys, turnover | Entrevistas HR | Culture Amp, Lattice |
| **IN3 (Eficiencia Flujo)** | Cycle time, throughput, WIP | Git, Jira | LinearB, Jellyfish |

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
      0.08*IN1 + 0.08*IN2 + 0.04*IN3

Paso_3: Interpretación
  90-100: Excelente
  75-89: Bueno
  60-74: Atención requerida
  <60: Crítico
```

---

### Detección Antipatrones

```yaml
Por_Cada_Antipatrón (AP01-AP40):
  1. Check síntomas (métricas de A5_Medicion + entrevistas)
  2. Si 2+ síntomas presentes → AP confirmado
  3. Severity: 🔴 Crítico / 🟡 Alto / 🟢 Moderado

Priorización:
  - Críticos first (AP con severidad 🔴)
  - Ordenar por impact (Cost of Delay × Probability)

Ejemplo:
  AP14 (Tech Debt Perpetuo):
    ✅ Síntoma 1: Tech debt score 68 (O9 en A5_Medicion)
    ✅ Síntoma 2: Velocity -62% vs baseline
    ✅ Síntoma 3: Incident rate +200%
    → AP14 confirmado, Severity 🔴
    → Cost of Delay: $250K/mes (per 100 eng)
    → Top priority remediation
```

---

### Patrones Faltantes

```yaml
Por_Cada_Patrón (P01-P64):
  1. ¿Está implementado?
  2. Si NO y contexto aplica → Gap identificado
  3. ROI_Estimado patrón (Ver §8 A1_Patrones)

Ejemplo:
  P23 (Feature Flags):
    Estado: No implementado
    Contexto: Deploy frequency <1/mes, rollback 30+ min
    → Patrón aplica
    ROI: Deploy frequency 10×, rollback <1 min
    → Recomendar implementar (quick win)
```

---

### Evaluación Awareness Levels (S1-S3)

```yaml
Objetivo:
  Diagnosticar madurez percepción en 3 niveles cognitivos (CORE/02 §2, D2 §5)

Proceso:
  - Usar los KPIs específicos de A5_Medicion.md §7.1 para evaluar cada nivel.
  - Calcular el score de madurez general de Awareness.

Checklist_Resumen:

S1_DETECT (Percibir):
  ☐ ¿Monitoring coverage >95%? (KPI S1_Monitoring_Coverage)
  ☐ ¿Latencia de telemetría <30s? (KPI S1_Telemetry_Latency)
  
S2_COMPREHEND (Comprender):
  ☐ ¿H_Score se calcula automáticamente? (KPI S2_H_Score_Automated)
  ☐ ¿Calidad de alertas >80%? (KPI S2_Alert_Quality)

S3_PROJECT (Proyectar):
  ☐ ¿Precisión de forecasting <15% MAPE? (KPI S3_Forecast_Accuracy)
  ☐ ¿Monitoreo de crisis activo? (KPI S3_Crisis_Monitoring)

Awareness_Maturity_Overall:
  Score = (S1_avg × 0.4) + (S2_avg × 0.35) + (S3_avg × 0.25)
  
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

Proceso:
  - Usar los KPIs específicos de A5_Medicion.md §7.2 para evaluar cada modo.
  - Calcular el score de madurez general de Decisión.

Checklist_Resumen:

D1_DIRECT_FEEDBACK (Automática):
  ☐ ¿Tasa de automatización D1 >60%? (KPI D1_Automation_Rate)
  ☐ ¿Latencia del loop <1s? (KPI D1_Loop_Latency)

D2_RULE_BASED (Condicional):
  ☐ ¿Cobertura de reglas de negocio >90%? (KPI D2_Rule_Coverage)
  ☐ ¿Automatización de workflows >75%? (KPI D2_Workflow_Automation)

D3_ASSOCIATIVE (Expertise-based):
  ☐ ¿Modelos ML en producción >5? (KPI D3_ML_Models_Production)
  ☐ ¿Tasa de validación humana >90%? (KPI D3_Human_Validation_Rate)

D4_KNOWLEDGE_BASED (Analítica):
  ☐ ¿Latencia de decisión estratégica <7 días? (KPI D4_Decision_Latency_Strategic)
  ☐ ¿Decisiones vinculadas a OKRs >80%? (KPI D4_OKR_Structure)

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
  O2_Valor: 45 (NPS 15, churn 18% - CRÍTICO)
  O3_Capacidad: 65 (utilization 92%, capacity free 8% - límite)
  O4_Eventos: 70 (MTTR 26 horas - CRÍTICO)
  O5_Restricciones: 90 (compliance OK)
  O6_Competencia: 60 (perdiendo vs competitor X)
  O7_Dependencias: 80 (vendors estables)
  O8_Calidad_Info: 70 (data quality 75%, OK)
  IN1_Velocidad_Decisional: 45 (TTD 18 días - CRÍTICO)
  IN2_Salud_Talento: 50 (turnover 22%, engagement 55 - CRÍTICO)
  IN3_Eficiencia_Flujo: 40 (cycle time 16 días, efficiency 18% - CRÍTICO)

H_Score = 0.12*75 + 0.15*45 + 0.10*65 + 0.08*70 + 
          0.10*90 + 0.10*60 + 0.08*80 + 0.07*70 +
          0.08*45 + 0.08*50 + 0.04*40
        = 9 + 6.75 + 6.5 + 5.6 + 9 + 6 + 6.4 + 4.9 + 3.6 + 4 + 1.6
        = 63.35/100 → ATENCIÓN REQUERIDA
```

---

### Antipatrones Detectados

```yaml
Críticos (🔴):
  - AP14 (Tech Debt Perpetuo): Velocity -40%, tech debt score 72.
  - AP09 (Handoff Hell): 9 handoffs, cycle time 16 días.
  - AP37 (Respuesta a Incidentes Lenta): MTTR 26 horas.
  - AP39 (Fricción del Cliente Invisible): NPS 15, churn 18% sin causa raíz clara.
  - AP40 ("Tragedia de los Comunes" en CX): Múltiples quejas sobre handoffs en el journey.

Altos (🟡):
  - AP03 (Silos Profundos): Teams Frontend/Backend/QA separados.
  - AP19 (Output Disguised): OKRs "Launch 8 features".
  - AP38 (Diseño Inside-Out): El journey del cliente refleja la estructura interna.

Total_Cost_of_Delay: ~$450K/mes (incluyendo nuevos APs)
```

---

### Top 5 Recomendaciones

```yaml
REC-01 (Prioridad ALTA):
  Título: "Implementar 20% Rule Tech Debt"
  Antipatrón: AP14
  Impact: H_Score +8 pts, Velocity +35%
  Timeline: Inicio inmediato
  Owner: VP Engineering

REC-02 (Prioridad ALTA):
  Título: "Mapeo y Ownership del Flujo de Cliente"
  Antipatrón: AP38, AP39, AP40
  Patrón: P_CX01, P_CX03
  Impact: H_Score +10 pts (O2: 45 → 65), Churn 18% → 12%
  Timeline: Q1 2025
  Owner: CPO

REC-03 (Prioridad ALTA):
  Título: "Automatizar Respuesta a Incidentes"
  Antipatrón: AP37
  Patrón: P_SEC05
  Impact: H_Score +5 pts (O4: 70 → 85), MTTR 26h → 4h
  Timeline: Q1 2025
  Owner: CTO

REC-04 (Prioridad MEDIA):
  Título: "Cross-Functional Feature Teams"
  Antipatrón: AP03, AP09
  Patrón: P01
  Impact: H_Score +7 pts, Cycle time 16d → 8d
  Timeline: Q2 2025
  Owner: CTO

REC-05 (Prioridad MEDIA):
  Título: "OKRs Basados en Outcomes"
  Antipatrón: AP19
  Patrón: P29
  Impact: H_Score +4 pts, Alignment strategy ↔ execution
  Timeline: Q2 2025
  Owner: CPO
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
  - IN3 (Eficiencia Flujo): Flow efficiency = productive energy / cycle time
  - IN1 (Velocidad Decisional): Decision delays = energy waiting
  - O7 (Dependencias): External dependencies = coordination overhead
  
Uso_Diagnóstico:
  Si IN3 <50 → Ejecutar Energy Flow Analysis
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
- **Medición y KPIs detallados:** `APLICACION/A5_Medicion.md`
