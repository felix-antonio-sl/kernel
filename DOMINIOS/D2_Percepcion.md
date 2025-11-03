# D2_Percepcion

**Versión:** 2.1.0 | **Estado:** Definitivo | **Audiencia:** Líderes, Analistas, Data Teams, Security

---

## REFERENCIAS RÁPIDAS
```yaml
Observables_Principales:
 O1_Demanda: §2.1 - Backlog, pipeline, market size (target crecimiento 5-10%/Q)
 O2_Valor: §2.2 - NPS, CSAT, churn (crítico >45, crisis <30)
 O3_Capacidad: §2.3 - Headcount, utilization, cash runway (crisis <30d)
 IN1_Velocidad_Decisional: §3.1 - Cycle time decisiones, Type 1 vs Type 2
 IN2_Salud_Talento: §3.2 - Engagement, turnover, regretted attrition
 IN3_Eficiencia_Flujo: §3.3 - Cycle time, WIP, throughput, flow efficiency
 SO1-SO5_Security: §8 - Vulnerabilidades, secretos, acceso, compliance, incidents
Métricas_Clave:
 H_Score: §4 - Health organizacional agregado (0-100, promedio ponderado 16 obs)
 H_Score_Extended: §8 - Incluye SO1-SO5 security (90% base + 10% security)
 Crisis_Threshold: H<45 (emergency mode), H<30 (existential threat)
 Typical_Ranges: 90-100 excelente, 75-89 bueno, 60-74 atención, <60 crítico
Conceptos_Core:
 Type_1_Decisions: Irreversibles, C-level, <14d target (M&A, reorg mayor)
 Type_2_Decisions: Reversibles, delegadas, <3d target (features, tech stack)
 ARB: Architecture Review Board (decision governance body)
 Flow_Efficiency: % tiempo value-add vs wait (target >25%, world-class >40%)
 Drift_Detection: H_Score cae >5 pts/trimestre → escalate C-level
Niveles_Awareness:
 Level_1_Detect (S1): Capturar facts crudos (M1 Monitor)
 Level_2_Comprehend (S2): Sintetizar en información meaningful (M2 Inform)
 Level_3_Project (S3): Predecir estados futuros (M3 Enable)
Cross-References:
 CORE/02_Ciclo_Fundamental.md §2: Fase Sense (S1-S3 Detectar/Comprender/Proyectar)
 CORE/01_Primitivos.md §3A: Primitivo Señal (cómo emitir alertas)
 D1_Arquitectura.md §5: A_Score, IN1, IN2 componentes
 D3_Decision.md §1: OKRs vinculados a observables
 D4_Operacion.md §2: Métricas flujo (IN3 detallado)
 APLICACION/A5_Medicion.md: Implementación práctica dashboards
```

---

## Responsabilidad

**PERCEPCIÓN detecta ESTADO interno/externo:** Sensado continuo de 16 observables (11 base + 5 security), health monitoring, drift detection.

**Pregunta clave:** ¿Cuál es nuestro estado actual y hacia dónde vamos?

---

## §0. QUICK START: PERCEPCIÓN MÍNIMA VIABLE (MVP)

**Objetivo**: Health monitoring básico funcionando en 2-4 semanas.

### MVP Checklist (2-4 semanas)

```yaml
Week_1: Observables Críticos (3 de 11)
  ☐ O2_Valor: NPS o CSAT (customer satisfaction)
    - Tool: Qualtrics, Typeform, o Google Forms
    - Frecuencia: Mensual minimum
  
  ☐ IN2_Salud_Talento: Turnover rate
    - Data: HR system (attrition last 12 months)
    - Alert: Si >15% annualized
  
  ☐ IN3_Eficiencia_Flujo: Cycle time
    - Data: Jira or Linear (start date → done date)
    - Target: <7 días avg

Week_2: Dashboard Básico
  ☐ Spreadsheet o dashboard simple (Tableau, Metabase, o Excel)
  ☐ 3 observables visualizados (valores + trend últimos 3 meses)
  ☐ Color coding: Verde >target, Amarillo borderline, Rojo crítico

Week_3: H_Score Simplificado
  ☐ Calcular H_Score con solo 3 observables (extrapolate otros a 75)
  ☐ Interpretación: >70 OK, 60-70 atención, <60 crítico
  ☐ Share con C-level (primera baseline)

Week_4: Plan Expansión
  ☐ Identificar próximos 3 observables agregar (typically O1, O3, I1)
  ☐ Timeline: 1 observable nuevo cada 2-4 semanas
  ☐ Target: 11 observables completos en 6 meses

Output_MVP:
  - Health visibility básica (3 observables críticos)
  - Baseline H_Score (~aproximado, útil para decisions)
  - Momentum: Quick win visible (2 semanas → dashboard live)

Next_Steps_Post_MVP:
  - Expand a 11 observables (6 meses rolling)
  - Automate data collection (ETL pipelines)
  - Add anomaly detection (M2 agents)
```

---

### Observables Priority Order

```yaml
Tier_1_Críticos (Week 1-2):
  - O2_Valor: Customer satisfaction (NPS, churn)
  - IN2_Salud_Talento: Employee retention (attrition, engagement)
  - IN3_Eficiencia_Flujo: Delivery speed (cycle time)
  
  Rationale: Estos 3 predicen viabilidad org mejor (Pareto 80/20)

Tier_2_Importantes (Week 3-8):
  - O1_Demanda: Pipeline health
  - O3_Capacidad: Resource availability (utilization, runway)
  - IN1_Velocidad_Decisional: Decision speed
  
  Rationale: Necessary para H_Score representativo

Tier_3_Completos (Week 9-24):
  - O4_Eventos: Incidents tracking
  - O5_Restricciones: Compliance status
  - O6_Competencia: Market position
  - O7_Dependencias: Vendor health
  - O8_Calidad_Info: Data quality
  
  Rationale: Important pero org funciona sin estos short-term

Pragmatic_Approach:
  - Start Tier 1: Actionable inmediato
  - Add Tier 2: H_Score más preciso
  - Complete Tier 3: Full observability
  
  No esperar 11 observables para actuar
  3 observables suficiente para decisions 70% casos
```

---

### Cuando Skip MVP

```yaml
Ya_Tienes_MVP_Si:
  - Dashboards existentes tracking KPIs key
  - H_Score >60 (aunque no perfect)
  - Data collection automated (no manual)
  
  → Skip to full implementation (§1-§7 completo)

MVP_No_Suficiente_Si:
  - Crisis mode (H<45): Need all 11 observables immediately
  - Audit/compliance: Regulators requieren comprehensive metrics
  - Board pressure: Investors demand full transparency
  
  → Accelerate to full observability (3-4 semanas vs 6 meses)
```

---

## §1. MODELO SENSORIAL (16 OBSERVABLES)

### Arquitectura Sensing

```
┌─────────────────────────────────────────┐
│        ENTORNO EXTERNO                  │
├─────────────────────────────────────────┤
│ O1: Demanda                             │
│ O2: Valor                               │
│ O3: Capacidad                           │
│ O4: Eventos                             │
│ O5: Restricciones                       │
│ O6: Competencia                         │
│ O7: Dependencias                        │
│ O8: Calidad Información                 │
└─────────────────────────────────────────┘
             ↓
┌─────────────────────────────────────────┐
│        ORGANIZACIÓN INTERNA             │
├─────────────────────────────────────────┤
│ IN1: Velocidad Decisional                │
│ IN2: Salud Talento                       │
│ IN3: Eficiencia Flujo                    │
└─────────────────────────────────────────┘
             ↓
┌─────────────────────────────────────────┐
│        SEGURIDAD TRANSVERSAL            │
├─────────────────────────────────────────┤
│ SO1: Vulnerabilidades                   │
│ SO2: Gestión Secretos                   │
│ SO3: Control Acceso                     │
│ SO4: Cumplimiento Normativo             │
│ SO5: Respuesta Incidentes               │
└─────────────────────────────────────────┘
             ↓
        H_Score (0-100)
```

---

## §2. OBSERVABLES EXTERNOS (O1-O8)

### O1. DEMANDA

```yaml
Definición: Necesidad del mercado/clientes por productos/servicios

Indicadores:
  - Backlog de features solicitadas (#, prioridad)
  - Tickets soporte inbound (# por día, categorías)
  - Sales pipeline ($ oportunidades, conversion rate)
  - Market size TAM/SAM/SOM
  - Search volume keywords (Google Trends, SEO)

Score_Cálculo (0-100):
  - Backlog saludable (creciendo 5-10%/trimestre): 80-100
  - Backlog estancado: 50-70
  - Backlog cayendo >15%/trimestre: 0-40

Ejemplo_Bueno (Score 90):
  - Backlog: 150 features (vs 130 Q anterior, +15%)
  - Support tickets: 200/día estable
  - Pipeline: $5M (vs $4M Q anterior, +25%)
  → Demanda sana y creciendo

Ejemplo_Malo (Score 30):
  - Backlog: 40 features (vs 80 Q anterior, -50%)
  - Support tickets: 80/día (vs 150 previo, -47%)
  - Pipeline: $1M (vs $3M Q anterior, -67%)
  → Demanda colapsando, producto no fit mercado
```

**Nota:** Demanda se mide sobre **productos_servicios** específicos entregados a **destinatarios** identificados. Para formalizar qué productos entrega cada Unidad_Trabajo y a quién, ver composición Outside-In en `CORE/01_Primitivos.md` §7.

---

### O2. VALOR ENTREGADO

```yaml
Definición: Percepción de valor por customers/stakeholders

Indicadores_Private_Context:
  - NPS (Net Promoter Score)
  - CSAT (Customer Satisfaction)
  - Churn rate (% customers lost)
  - Customer retention rate
  - Revenue per customer (proxy de valor)
  - Key account losses (top 20% revenue)

Indicadores_Public_Context:
  - Citizen satisfaction scores
  - Service delivery performance rates
  - Trust and legitimacy indices
  - Stakeholder feedback (legislators, partners)
  - Compliance/participation rates
  - Media sentiment analysis

Score_Cálculo_Normal (45-100):
  Private: NPS >30, Churn <10%, CSAT >75
  Public: Citizen Sat >60%, Service >85%, Trust >50
  
Score_Cálculo_Crisis (0-45):
  Severe (30-45):
    Private: Churn 15-20%, NPS 0-20, key accounts at risk
    Public: Service failures 10-20%, declining satisfaction, media criticism
  
  Critical (15-30):
    Private: Churn >20%, NPS <0, key account losses
    Public: Service failures >20%, legislative investigation, public crisis
  
  Existential (0-15):
    Private: Mass defection (>30% churn), NPS <-20, market rejection
    Public: Legitimacy crisis, widespread service collapse, political crisis

Señal_Emergency:
  IF O2 < 30 THEN Emit(Señal: "Customer_Defection_Crisis")
  IF O2 < 15 THEN Emit(Señal: "Market_Rejection_Threat")

Ejemplo_Healthy_Private (Score 95):
  - NPS: 65 (promoters dominant)
  - CSAT: 88/100
  - Churn: 3%/año
  - Revenue/customer: $15K/año (growing)
  → Valor entregado excelente

Ejemplo_Crisis_Public (Score 20):
  - Citizen satisfaction: 35% (plummeting)
  - Service delivery: 62% on-time (critical failures)
  - Legislative hearings: 3 in progress
  - Media sentiment: 80% negative
  - Trust index: 28% (legitimacy crisis)
  → Public value collapse, political intervention imminent
```

**Nota:** Valor se mide como outcomes que **productos_servicios** entregan a **destinatarios**. La composición formal Unidad_Trabajo especifica qué outputs se entregan, a quién, y cómo se miden (métricas_valor). Ver `CORE/01_Primitivos.md` §7 para estructura completa Outside-In.

---

### O3. CAPACIDAD

```yaml
Definición: Recursos disponibles vs demanda (workforce, financial, infrastructure)

Indicadores_Primarios:
  - Headcount vs backlog
  - Utilization rate (óptimo 70-85%)
  - Time-to-hire
  - Skill gaps
  - Infrastructure capacity

Indicadores_Financial_Crisis:
  Private_Context:
    - Cash runway (días operating cash disponible)
    - Burn rate (monthly cash consumption)
    - Accounts payable aging
    - Credit availability
  
  Public_Context:
    - Budget execution rate (% obligated)
    - Appropriations status (full-year vs continuing resolution)
    - Fiscal health (cost per service unit)
    - Unfunded mandates impact

Score_Cálculo_Normal (45-100):
  - Capacity surplus >15%, utilization 70-85%, cash >180d: 90-100
  - Capacity matches demand, utilization 70-85%, cash 90-180d: 70-85
  - Capacity deficit <15%, utilization >85%, cash 30-90d: 50-65
  - Capacity deficit 15-30%, utilization >90%, cash 15-30d: 45-50

Score_Cálculo_Crisis (0-45):
  Severe (30-45):
    - Capacity deficit >30%, utilization >95%
    - Cash runway 15-30 días OR Budget execution critical
    - Layoffs inminentes o hiring freeze total
  
  Critical (15-30):
    - Capacity deficit >50%, utilization >98%
    - Cash runway 7-15 días OR Service shutdown imminent
    - Talent exodus comenzando (attrition >20%)
  
  Existential (0-15):
    - Capacity collapse, utilization unsustainable
    - Cash runway < 7 días OR Payroll at risk
    - Massive talent exodus (>30% quarterly)

Señal_Emergency:
  IF O3 < 30 THEN Emit(Señal: "Capacity_Crisis_Protocol")
  IF O3 < 15 THEN Emit(Señal: "Existential_Capacity_Threat")

Ejemplo_Healthy (Score 85):
  - Team size: 50 engineers, backlog 6 weeks
  - Utilization: 78% (sustainable)
  - Cash runway: 240 días (private) OR Full appropriation (public)
  - Time-to-hire: 45 días
  → Capacity adecuada, operaciones sostenibles

Ejemplo_Crisis (Score 25):
  - Team size: 20 engineers (post-layoffs), backlog 26 weeks
  - Utilization: 98% (burnout zone)
  - Cash runway: 12 días (private) OR Shutdown imminent (public)
  - Attrition: 25% quarterly (exodus)
  - Time-to-hire: irrelevant (hiring freeze)
  → Capacity existencial, emergency stabilization required
```

---

### O4. EVENTOS

```yaml
Definición: Disrupciones o oportunidades externas no planificadas

Indicadores:
  - Incidents críticos (# y severidad)
  - Regulación nueva (leyes, compliance)
  - Tech breakthrough (nueva tech available)
  - Competitor move (lanzamiento, adquisición)
  - Market shift (cambio demanda súbito)

Score_Cálculo (0-100):
  - Sin eventos críticos últimos 3 meses: 90-100
  - 1-2 eventos menores gestionados: 70-85
  - 3+ eventos o 1 catastrófico no resuelto: 0-65

Ejemplo_Bueno (Score 92):
  - Incidents: 0 críticos, 2 menores resueltos <1hr
  - Regulación: GDPR compliance al día
  - Tech: Adopción Kubernetes planificada
  - Competencia: Sin disrupciones mayores
  → Entorno estable

Ejemplo_Malo (Score 25):
  - Incidents: 1 catastrófico (outage 8 hrs, $2M pérdida)
  - Regulación: Nueva ley requiere cambios arquitectura (6 meses trabajo)
  - Competencia: Competitor lanzó feature clave que no tenemos
  → Entorno disruptivo, reactive mode
```

---

### O5. RESTRICCIONES

```yaml
Definición: Límites regulatorios, legales, contractuales

Indicadores:
  - Compliance status (% controls cumplidos)
  - Findings abiertas (auditorías)
  - SLA breaches (violaciones contratos)
  - Legal risks (demandas, litigios)
  - Regulatory fines (multas pagadas)

Score_Cálculo (0-100):
  - 100% compliance, 0 findings críticos, 0 breaches: 95-100
  - >95% compliance, <5 findings menores: 80-90
  - <95% compliance, findings críticos, breaches: 0-75

Ejemplo_Bueno (Score 98):
  - SOC2: 100% controles compliant
  - GDPR: 100% compliant
  - SLA: 0 breaches últimos 12 meses
  - Findings: 2 low-priority (cosmético)
  → Restricciones under control

Ejemplo_Malo (Score 40):
  - SOC2: 85% compliant (falta encryption 15% datos)
  - GDPR: Violation (data residency incorrecta)
  - SLA: 8 breaches últimos 6 meses
  - Multa: €500K GDPR pendiente
  → Alto riesgo regulatorio
```

---

### O6. COMPETENCIA

```yaml
Definición: Alternativas disponibles para clientes

Indicadores:
  - Market share (% vs competitors)
  - Feature parity (% features competitor tienen que no tenemos)
  - Pricing position ($ vs competitors)
  - Win/loss rate (% deals ganados vs perdidos)
  - Churn to competitor (% clientes que migran)

Score_Cálculo (0-100):
  - Market leader, feature parity >90%, Win rate >60%: 85-100
  - Market follower, feature parity 70-90%, Win rate 40-60%: 60-80
  - Laggard, feature parity <70%, Win rate <40%: 0-55

Ejemplo_Bueno (Score 90):
  - Market share: 35% (líder en nicho)
  - Feature parity: 95% (casi todas features competitors)
  - Win rate: 65%
  - Churn to competitor: 1%
  → Posición competitiva fuerte

Ejemplo_Malo (Score 35):
  - Market share: 8% (distant follower)
  - Feature parity: 60% (missing key features)
  - Win rate: 28%
  - Churn to competitor: 12%
  → Posición competitiva débil, riesgo disruption
```

---

### O7. DEPENDENCIAS

```yaml
Definición: Proveedores, partners, integraciones críticas

Indicadores:
  - Vendor health (financial stability proveedores)
  - SLA compliance vendors (% uptime proveedores)
  - Single points of failure (# dependencias sin alternativa)
  - Integration failures (# fallos APIs/integraciones)
  - Switching cost ($ y tiempo migrar a alternativa)

Score_Cálculo (0-100):
  - Vendors estables, <2 SPOFs, <1% integration failures: 90-100
  - Vendors OK, 2-5 SPOFs, 1-3% failures: 70-85
  - Vendor risk alto, >5 SPOFs, >3% failures: 0-65

Ejemplo_Bueno (Score 92):
  - Vendors: AWS (AAA rating), Stripe (estable)
  - SPOFs: 1 (payment gateway, pero con backup)
  - Integration failures: 0.5% (excelente)
  - Switching cost: Moderado (3 meses migración)
  → Dependencias gestionadas

Ejemplo_Malo (Score 30):
  - Vendors: 1 proveedor small startup (funding issues)
  - SPOFs: 8 (core business depende de todos)
  - Integration failures: 8% (frecuentes outages)
  - Switching cost: Prohibitivo (12 meses + $2M)
  → Alto riesgo dependency
```

---

### O8. CALIDAD INFORMACIÓN

```yaml
Definición: Confiabilidad y disponibilidad de datos para decisiones

Indicadores:
  - Data quality score (completitud, precisión, consistencia)
  - Data latency (tiempo dato generado → disponible)
  - Data coverage (% procesos con datos)
  - Data lineage (% datos con trazabilidad)
  - Trust score (% personas confían en datos)

Score_Cálculo (0-100):
  - Quality >90%, Latency <1hr, Coverage >95%, Trust >80%: 90-100
  - Quality 70-90%, Latency 1-24hrs, Coverage 80-95%: 70-85
  - Quality <70%, Latency >24hrs, Coverage <80%: 0-65

Ejemplo_Bueno (Score 95):
  - Quality: 94% (DAMA framework)
  - Latency: Real-time para críticos, <15min otros
  - Coverage: 98% procesos
  - Lineage: 100% datos críticos trazables
  - Trust: 88% (surveys)
  → Datos confiables para decisiones

Ejemplo_Malo (Score 40):
  - Quality: 62% (inconsistencies frecuentes)
  - Latency: 48 hrs promedio
  - Coverage: 65% procesos (35% blind spots)
  - Lineage: 30% (majority unknown origin)
  - Trust: 45% (low confidence)
  → Decisiones basadas en datos dudosos
```

---

### IN1. VELOCIDAD DECISIONAL

```yaml
Definición: Rapidez, calidad y distribución con la que organización toma e implementa decisiones

Indicadores_Primarios:
  - Cycle time promedio decisiones (días)
  - % decisiones delegadas vs escaladas
  - Backlog decisiones pendientes
  - Bottlenecks decisionales (quién/dónde)

Indicadores_Vital_Signs:
  1. Decision_Velocity_by_Type:
     - Type 1 (irreversible): Cycle time mediana
     - Type 2 (reversible): Cycle time mediana
     - Target: Type 1 <14 días, Type 2 <3 días
  
    Definición_Types (Bezos-style):
     - Type 1: Decisiones irreversibles / alto impacto (ej: M&A, reorg mayor)
     - Requieren análisis profundo, C-level approval, lento es aceptable
     - Type 2: Decisiones reversibles / bajo impacto (ej: tech stack, feature)
     - Delegar a teams, decidir rápido, ajustar si falla
     - Ver: D1_Arquitectura.md P7 y D3_Decision.md §3.1 para framework completo
 
  2. Decision_Quality:
     - % decisiones correctas en retrospectiva (6 meses vista)
     - % decisiones requieren reversal mayor
     - Target: >70% correctas, <15% reversal
  
  3. Decision_Distribution:
     - Where made: C-level vs VP vs Manager vs IC
     - Healthy: 80% decisions at lowest competent level
     - Unhealthy: >50% decisions escalated to C-level

Score_Cálculo (0-100):
  - Cycle time <7 días, >80% delegadas, quality >70%: 80-100
  - Cycle time 7-14 días, 60-80% delegadas, quality 50-70%: 60-80
  - Cycle time >14 días, <60% delegadas, quality <50%: 0-50

Ejemplo_Bueno (Score 85):
  - Cycle time promedio: 4 días (Type 2: 2d, Type 1: 10d)
  - Decisiones Type 2 delegadas: 85%
  - Decision quality: 78% correctas retrospectively
  - Distribution: 75% at manager level o below
  - Decision backlog (ARB): 5 decisiones (manejable)
  → Velocidad alta, empowerment claro, calidad sostenible
  
  Nota_ARB: Architecture Review Board o decision governance body equivalente

Ejemplo_Malo (Score 35):
  - Cycle time promedio: 18 días (Type 2: 12d, Type 1: 30d)
  - Decisiones Type 2 escaladas: 70%
  - Decision quality: 45% correctas (muchos reversals)
  - Distribution: 60% at C-level (bottleneck)
  - Decision backlog (ARB): 45 decisiones (bottleneck crítico)
  → Paralysis decisional, centralización excesiva, quality pobre
```

---

### IN2. SALUD TALENTO

```yaml
Definición: Bienestar, engagement, retención de personas

Indicadores:
  - Engagement score (surveys, 0-100)
  - Turnover rate (% personas que dejan org por año)
  - Regretted attrition (% desvinculaciones de high-performers)
  - Time-to-fill (días promedio llenar vacante)
  - Flight risk (critical individuals actively looking)
  - Internal promotions (% posiciones llenadas internamente)

Score_Cálculo_Normal (45-100):
  - Engagement >75, Turnover <10%, Regretted <5%: 85-100
  - Engagement 60-75, Turnover 10-20%, Regretted 5-10%: 65-80
  - Engagement 50-60, Turnover 15-20%, Regretted 10-15%: 45-60

Score_Cálculo_Crisis (0-45):
  Severe (30-45):
    - Turnover 20-25% OR Regretted 15-20%
    - Engagement 40-50
    - Critical roles vacant >90 days
    - Flight risk: 30% top talent actively looking
  
  Critical (15-30):
    - Turnover >25% OR Regretted >20%
    - Engagement 30-40
    - Multiple critical departures in progress
    - Flight risk: >50% top talent actively looking
  
  Existential (0-15):
    - Turnover >30% quarterly (mass exodus)
    - Engagement <30
    - Leadership team departures
    - Organizational knowledge hemorrhaging

Señal_Emergency:
  IF IN2 < 30 THEN Emit(Señal: "Talent_Exodus_Crisis")
  IF IN2 < 15 THEN Emit(Señal: "Organizational_Knowledge_Collapse")

Ejemplo_Bueno (Score 92):
  - Engagement: 82/100
  - Turnover: 8%/año (industry avg 12%)
  - Regretted attrition: 3%
  - Time-to-fill: 35 días
  - Internal promotions: 60%
  → Talento sano

Ejemplo_Crisis (Score 22):
  - Engagement: 35/100 (collapse)
  - Turnover: 32%/año (mass exodus)
  - Regretted attrition: 28% (brain drain)
  - Critical vacancies: 8 positions >120 días
  - Flight risk: 65% top talent job hunting
  - Internal promotions: 10% (no succession)
  → Talent emergency, retention interventions critical
```

---

### IN3. EFICIENCIA FLUJO

```yaml
Definición: Rapidez con la que work e información fluyen desde idea hasta valor entregado

Indicadores_Primarios:
  - Cycle time (días desde idea → producción)
  - Flow efficiency (% tiempo value-adding vs wait)
  - WIP (Work in Progress items simultáneos)
  - Throughput (items completados/semana)

Indicadores_Vital_Signs_Information_Flow:
  1. Information_Velocity:
     - Time from creation to consumption (hours)
     - Healthy: Critical info reaches parties <4 hrs
     - Unhealthy: Info delayed >24 hrs, filtered, hoarded
  
  2. Information_Accuracy:
     - Fidelity through organization (% distortion)
     - Healthy: <10% distortion, context preserved
     - Unhealthy: >30% distortion, telephone game effect
  
  3. Information_Accessibility:
     - Time to find needed info (minutes)
     - % decisions delayed by info unavailability
     - Healthy: Find in <10 min, <5% delays
     - Unhealthy: Search >30 min, >20% delays, tribal knowledge

Score_Cálculo (0-100):
  - Cycle time <7d, flow eff >40%, info velocity <4hrs: 80-100
  - Cycle time 7-21d, flow eff 20-40%, info velocity 4-24hrs: 60-80
  - Cycle time >21d, flow eff <20%, info velocity >24hrs: 0-50

Ejemplo_Bueno (Score 90):
  - Cycle time: 5 días promedio
  - Flow efficiency: 45% (55% wait/handoff)
  - WIP: 12 items (team 8 personas, 1.5× size)
  - Throughput: 8 items/semana
  - Info velocity: 2 hrs promedio (Slack, docs updated)
  - Info accuracy: 92% fidelity
  - Info accessibility: 5 min average search
  → Flow excelente, bottlenecks mínimos, información fluye bien

Ejemplo_Malo (Score 30):
  - Cycle time: 28 días promedio
  - Flow efficiency: 15% (85% wait/handoff hell)
  - WIP: 45 items (team 8 personas, 5.6× size - overload)
  - Throughput: 2 items/semana (bajo throughput pese alto WIP)
  - Info velocity: 36 hrs promedio (emails perdidos, silos)
  - Info accuracy: 55% fidelity (distorsión alta)
  - Info accessibility: 35 min search (tribal knowledge, docs obsoletos)
  → Flow bloqueado, waste alto, información disfuncional
```

---

## §4. HEALTH SCORE (H)

### Fórmula Agregada

```yaml
H_Score = (
  0.12 * O1_Demanda +
  0.15 * O2_Valor +
  0.10 * O3_Capacidad +
  0.08 * O4_Eventos +
  0.10 * O5_Restricciones +
  0.10 * O6_Competencia +
  0.08 * O7_Dependencias +
  0.07 * O8_Calidad_Info +
  0.08 * IN1_Velocidad_Decisional +
  0.08 * IN2_Salud_Talento +
  0.04 * IN3_Eficiencia_Flujo
)

Nota_Security_Extended:
  Esta es fórmula BASE (11 observables).
  Para enterprise security-critical, ver §8 que agrega SO1-SO5.
  Fórmula extended: 70% O1-O8 + 20% IN1-IN3 + 10% SO1-SO5.

Ponderaciones justificadas (rationale):
  - O2 (Valor) mayor peso 15%: Es outcome final, customer-facing
  - O1 (Demanda) alto 12%: Sin demanda, no hay negocio viable
  - I3 (Eficiencia) menor 4%: Puedes ser ineficiente pero entregar valor temporalmente
  - Otros balanceados: Importancia similar (7-10% range)

Disclaimer_Calibración:
  Estado: Ponderaciones propuestas basadas en juicio experto y literature review
  
  Fuentes_Informan:
    - McKinsey OHI (weighting employee engagement, leadership)
    - Balanced Scorecard (Kaplan & Norton) weights
    - DevOps metrics research (correlation with business outcomes)
  
  Validación_Empírica:
    - Calibración con N=10 casos R1_Casos.md
    - Pendiente: Validación estadística rigurosa (N=50+ orgs)
    - Research ongoing para optimize weights via regression
  
  Recomendación_Uso:
    - Use ponderaciones como starting point
    - Organizaciones DEBEN calibrar según contexto:
        * B2B vs B2C: O1/O2 weights pueden invertirse
        * Startup vs Enterprise: O3 (Capacidad) weight mayor en startup
        * Regulated vs Unregulated: O5 (Restricciones) weight mayor
    
    - Método calibración local:
        1. Medir H_Score con weights propuestos (baseline)
        2. Después 6-12 meses: Correlacionar H_Score con outcomes reales
        3. Ajustar weights para maximize predictive power
        4. Iterar trimestral

Transparencia:
  Ponderaciones NO son "verdad absoluta" matemática
  SON heurística informada para organizaciones estándar
  Customización esperada y encouraged
```

### Interpretación H_Score

```yaml
90-100: EXCELENTE
  - Org saludable, todas dimensiones verdes
  - Mantener momentum
  - Optimizar marginal

75-89: BUENO
  - Org funcional, algunos gaps menores
  - Addressed proactivamente
  - 1-2 iniciativas mejora

60-74: ATENCIÓN REQUERIDA
  - Org con issues moderados
  - Diagnóstico profundo (§2 DOMINIOS/D1_Arquitectura)
  - 3-5 iniciativas críticas

<60: CRÍTICO
  - Org en riesgo
  - Transformación urgente
  - Roadmap remediation 6-12 meses
```

---

## §5. VECTORES DE DERIVA

### Definición

**Vector de deriva:** Tendencia observable que indica dirección cambio organizacional.

```
Deriva_Positiva: H_Score mejorando >2 puntos/trimestre consistente
Deriva_Negativa: H_Score cayendo >2 puntos/trimestre
Deriva_Estable: H_Score oscila ±2 puntos
```

### Detección Temprana

```yaml
Alertas_Proactivas:
  - Si 3 observables caen >10 puntos en 1 trimestre → Alerta Yellow
  - Si 2 observables caen >20 puntos en 1 trimestre → Alerta Red
  - Si H_Score cae >5 puntos vs trimestre anterior → Escalate C-level

Ejemplo_Alerta:
  Q1: H=78, O2=82, I2=75, I3=80
  Q2: H=72, O2=68 (-14), I2=62 (-13), I3=72 (-8)
  
  → Alerta Yellow: O2 (Valor) y I2 (Talento) cayendo >10
  → Root cause: NPS bajó 15 puntos, turnover subió de 10% a 18%
  → Acción: Diagnóstico urgente, plan remediation
```

---

## §6. AGENTES SENSORIALES IA

### Tipos de Agentes Sensing

```yaml
Tipo_1_Passive_Monitors (M1):
  Función: Capturan métricas 24/7, no interpretan
  Ejemplos:
    - Datadog APM (uptime, latency, errors)
    - Google Analytics (tráfico, conversions)
    - Jira (WIP, cycle time, throughput)
  Modo_Delegación: M1 (Monitorear)

Tipo_2_Anomaly_Detectors (M2):
  Función: Identifican patterns anómalos, alertan
  Ejemplos:
    - ML anomaly detection (O4: Eventos - detecta spike tráfico inusual)
    - Sentiment analysis (O2: Valor - analiza NPS comments)
    - Drift detection (I3: Eficiencia - detecta cycle time creciendo)
  Modo_Delegación: M2 (Informar)

Tipo_3_Predictive_Forecasters (M2):
  Función: Proyectan tendencias futuras
  Ejemplos:
    - Churn prediction (O2: Valor - forecast clientes en riesgo)
    - Capacity forecasting (O3: Capacidad - predict cuándo necesitas más eng)
    - Demand forecasting (O1: Demanda - ML sobre pipeline sales)
  Modo_Delegación: M2 (Informar)

Tipo_4_Insight_Generators (M2-M3):
  Función: Generan narrativas desde datos
  Ejemplos:
    - LLM que lee dashboards y escribe "Executive summary" semanal
    - Root cause analysis automático (ej: "I2 cayó porque 3 seniors left")
  Modo_Delegación: M2-M3 (Informar/Habilitar)
```

---

## §7. DASHBOARD HEALTH

### Estructura Recomendada

```yaml
Vista_Ejecutiva (C-level):
  - H_Score (grande, prominente): 73/100
  - Trend últimos 4 trimestres: 78 → 75 → 72 → 73 (↓ luego ↑)
  - Top 3 issues: O2 bajo (65), I2 bajo (68), I1 bajo (62)
  - Top 3 fortalezas: O5 alto (98), O8 alto (92), O4 estable (90)
  - Alerta activa: 1 Red (I2 churn crítico)

Vista_Detalle (Managers):
  - 11 observables con score + trend
  - Drill-down por observable (gráficos históricos)
  - Root cause hints (ej: I2 bajo → "5 engineers left Q2, 3 fueron seniors")

Vista_Operacional (Teams):
  - Métricas específicas team (cycle time, throughput, quality)
  - Comparación vs org avg
  - Actionable recommendations
```

---

## §8. OUTSIDE-IN METHODOLOGY

### Principio P3 Aplicado

```yaml
Flujo_Outside_In:
  1. SENSE External (O1-O8)
  2. SENSE Internal (I1-I3)
  3. COMPARE External vs Internal
  4. DECIDE basado en gaps
  5. ACT para cerrar gaps

Ejemplo:
  External_Sense:
    - O1 (Demanda): Alta (backlog creciendo)
    - O2 (Valor): Decayendo (NPS cayendo)
    - O6 (Competencia): Fuerte (competitor lanzó feature X)
  
  Internal_Sense:
    - I3 (Eficiencia): Baja (cycle time 12 días)
    - O3 (Capacidad): Insuficiente (utilization 98%)
  
  Gap_Analysis:
    - Demanda alta PERO capacidad insuficiente → No podemos capturar demanda
    - Competitor tiene feature X PERO nosotros tardamos 12 días/feature → Losing competitively
  
  Decision:
    - Priorizar: Hiring 5 engineers (aumentar O3)
    - Priorizar: Feature X en roadmap (cerrar gap O6)
    - Optimizar: Flow efficiency (reducir cycle time, mejorar I3)
```

---

## §9. NIVELES AWARENESS COGNITIVA

### Estratificación Percepción

```yaml
Concepto:
  Percepción NO es monolítica
  Opera en 3 niveles cognitivos de complejidad creciente
  Cada nivel requiere capacidades distintas (humano o algorítmico)

Conexión_Ciclo_SDA:
  Sense phase (CORE/02 §2) se subdivide en:
    Level 1 = S1 DETECTAR → Captura facts crudos
    Level 2 = S2 COMPRENDER → Sintetiza en información meaningful
    Level 3 = S3 PROYECTAR → Predice estados futuros

Nomenclatura:
  Este documento usa "Level 1-3" (perspectiva dominio específico)
  02_Ciclo_Fundamental.md usa "S1-S3" (perspectiva framework general)
  Ambas notaciones son equivalentes y se usan intercambiablemente
```

---

### §9.1. Level 1: Detect (Percibir) = S1

```yaml
Referencia: S1 DETECTAR en CORE/02_Ciclo_Fundamental.md §2

Definición: Capturar facts, eventos, señales del entorno sin interpretación

Función_Cognitiva: Sensorial (minimal processing)

Ejemplos_Concretos:
  Observable_Raw:
    - Sensor: Temperatura = 85°C (fact crudo)
    - Log: HTTP 500 error occurred at 14:32:05
    - Métrica: Response time = 3.2 seconds
    - Señal: Customer submitted complaint ticket
  
  NO_Es_Detect:
    - "Motor sobrecalentando" (esto es comprehension)
    - "Service degradado" (esto es comprehension)
    - "Churn risk alto" (esto es comprehension)

Agentes_Típicos:
  - M1 Monitor: Dashboards que muestran raw metrics
  - Sensores IoT: Temperatura, presión, vibración
  - Log aggregators: Capture events sin analysis
  - Telemetry systems: Collect data points

Complejidad: O(1) - Captura directa sin procesamiento
```

---

### §9.2. Level 2: Comprehend (Comprender) = S2

```yaml
Referencia: S2 COMPRENDER en CORE/02_Ciclo_Fundamental.md §2

Definición: Sintetizar facts en información meaningful con contexto

Función_Cognitiva: Interpretación, pattern recognition, clasificación

Ejemplos_Concretos:
  Observable_Synthesized:
    - Temperatura 85°C + threshold 80°C + contexto motor → "Motor sobrecalentando"
    - HTTP 500 rate 15% + duration 30min → "Service degradado"
    - NPS -15 + Churn 32% + Attrition 40% → "Triple crisis (customer, talent, value)"
    - Backlog growth -8% + competitor launch → "Demanda shift to competitor"
  
  Observables_O1_O8_IN1_IN3:
    TODOS operan en Level 2 (comprehension)
    - O2 Valor: NPS score es synthesis de customer responses
    - I2 Talent: Engagement score es synthesis de survey + retention
    - I3 Flow: Cycle time es synthesis de timestamps + WIP
  
  H_Score:
    Opera en Level 2 (síntesis de 11 observables en single metric)

Agentes_Típicos:
  - M2 Inform: Alerting systems con context awareness
  - Analytics platforms: Dashboards con KPIs interpretados
  - Observability tools: Service health synthesis
  - Diagnosis tools: A3 Energy Flow, Conflict Topology

Complejidad: O(n) - Procesamiento de múltiples inputs
```

---

### Level 3: Project (Proyectar) = S3

```yaml
Referencia: S3 PROYECTAR en CORE/02_Ciclo_Fundamental.md §2

Definición: Predecir estado futuro basado en trends, causality, simulation

Función_Cognitiva: Forecasting, anticipación, scenario planning

Ejemplos_Concretos:
  Observable_Predictive:
    - Temperatura trend +5°C/hr → "Falla motor en 2 horas"
    - Error rate creciendo exponentially → "Total outage en 30 minutos"
    - Churn acelerando 28% → 35% MoM → "ARR -$2M en Q4"
    - H_Score 58 → 52 → 48 (trend -3 pts/mes) → "Crisis threshold Q2"
  
  Crisis_Thresholds:
    Projection activa cuando:
      - H_Score < 45: Proyectar deterioro futuro (stabilize o collapse?)
      - Observable < 30: Proyectar tiempo hasta falla crítica
      - Trend negativo sostenido: Proyectar cuando cruzará thresholds
  
  Readiness_Assessment (A4 §0):
    Path selection requiere Level 3:
      - "Si no actuamos, ¿H_Score en 3 meses?"
      - "Si activamos P52, ¿cuándo H>45?"

Agentes_Típicos:
  - M3 Enable: Predictive analytics, forecasting models
  - Simulation tools: Monte Carlo, scenario planning
  - Early warning systems: Detect trends before crisis
  - Strategic planning: D3 roadmaps con forecasts

Complejidad: O(n²) - Simulation, causal modeling
```

---

### Progresión Awareness & Delegación

```yaml
Mapping_to_M1_M6:
  
  Level_1_Detect → M1 Monitor:
    Agente captura facts, humano interpreta
    Ejemplo: Dashboard muestra metrics, PM analiza
  
  Level_2_Comprehend → M2 Inform:
    Agente sintetiza + alerta, humano decide
    Ejemplo: Alerting system notifica "Service degraded"
  
  Level_3_Project → M3 Enable:
    Agente predice + sugiere, humano planifica
    Ejemplo: Forecasting tool: "Outage probable en 30min, suggest scale up"
  
  Autonomous_Loops:
    M5-M6 pueden operar cross-levels:
      - Detect anomaly (L1) → Comprehend as threat (L2) → Project impact (L3) → Act
      - Ejemplo: Fraud detection end-to-end

Design_Principle:
  Al asignar agente a observable, especificar level:
    - "Monitor O3 Capacity" (L1) vs
    - "Alert when O3<30" (L2) vs
    - "Forecast O3 trend, warn if <45 in 60d" (L3)
```

---

### Uso Practical en Diagnóstico

```yaml
Energy_Flow_Analysis (A3 §9):
  - Level 1: Detect time spent (calendar entries, time tracking)
  - Level 2: Comprehend as waste/value (categorize activities)
  - Level 3: Project efficiency gains (simulate reduction friction)

Conflict_Pattern_Analysis (A3 §10):
  - Level 1: Detect conflicts (reported incidents)
  - Level 2: Comprehend patterns (recurring parties, topics)
  - Level 3: Project escalation (if unresolved, predict impact)

Crisis_Triage (A4 §0):
  - Level 1: Detect indicators (cash runway, churn, attrition raw)
  - Level 2: Comprehend as crisis (H_Score<45, observables<30)
  - Level 3: Project path (stabilization timeline, exit criteria)
```

---

## §8. OBSERVABLES SEGURIDAD (SO1-SO5)

**Propósito**: Extender modelo sensorial con observables específicos security, críticos para enterprise compliance y risk management.

**Integración H_Score**: Estos observables complementan O1-O8, I1-I3. Peso sugerido: SO1-SO5 (10% total H_Score) ajustable según industry regulated.

---

### SO1. VULNERABILIDADES

```yaml
Definición: Exposición a exploits conocidos en stack tecnológico

Indicadores:
  - CVE count por severidad (critical, high, medium, low)
  - Mean Time to Patch (MTTP) vulnerabilidades críticas
  - % sistemas con patches actualizados (< 30 días)
  - Zero-day exposure (días desde disclosure hasta patch)
  - Vulnerability backlog (# pendientes >90 días)

Score_Cálculo (0-100):
  - 0 CVE critical unpatched, MTTP <7 días, >95% updated: 90-100
  - 1-5 CVE critical, MTTP 7-30 días, 80-95% updated: 70-85
  - >5 CVE critical, MTTP >30 días, <80% updated: 0-65

Ejemplo_Bueno (Score 95):
  - CVE critical: 0 (patched within 48hrs discovery)
  - MTTP: 3 días promedio
  - Systems updated: 98% (automation Ansible)
  - Vulnerability backlog: 12 low-severity items
  → Security hygiene excelente

Ejemplo_Malo (Score 35):
  - CVE critical: 8 unpatched (oldest 4 months)
  - MTTP: 45 días promedio
  - Systems updated: 62% (manual process)
  - Zero-day exposure: 15 días Log4Shell sin patch
  → Alto riesgo exploitation
```

---

### SO2. GESTIÓN SECRETOS

```yaml
Definición: Protección credenciales, API keys, certificates, tokens

Indicadores:
  - Secrets hardcoded en código (# detectados scans)
  - Secrets rotation rate (% rotados <90 días)
  - Secrets vault adoption (% apps usando Vault/KMS)
  - Certificate expiration incidents (# vencidos últimos 12M)
  - Leaked secrets (# detectados GitHub/logs)

Score_Cálculo (0-100):
  - 0 secrets hardcoded, >90% vault, rotation <90d: 90-100
  - 1-10 secrets hardcoded, 70-90% vault, rotation 90-180d: 70-85
  - >10 secrets hardcoded, <70% vault, rotation >180d: 0-65

Ejemplo_Bueno (Score 92):
  - Secrets hardcoded: 0 (GitGuardian pre-commit hooks)
  - Vault adoption: 95% apps (HashiCorp Vault)
  - Rotation: 100% credentials <60 días
  - Certificate expirations: 0 incidents (automated renewal)
  → Secrets management robusto

Ejemplo_Malo (Score 40):
  - Secrets hardcoded: 23 encontrados (DB passwords, API keys)
  - Vault adoption: 45% apps (mayoría env vars plaintext)
  - Rotation: Passwords never rotated (algunos 3+ años)
  - Leaked secrets: 2 AWS keys found GitHub public repos
  → Alto riesgo credential compromise
```

---

### SO3. CONTROL ACCESO

```yaml
Definición: Gobernanza identities, autenticación, autorización

Indicadores:
  - MFA adoption rate (% usuarios con 2FA enabled)
  - Privileged accounts (# con sudo/admin sin justificación)
  - Access reviews completed (% scheduled reviews on-time)
  - Over-provisioned permissions (% usuarios con more than needed)
  - Orphaned accounts (# accounts ex-employees >30 días)

Score_Cálculo (0-100):
  - MFA >95%, 0 orphaned, access reviews 100%, least-privilege: 90-100
  - MFA 80-95%, <5 orphaned, reviews >80%: 70-85
  - MFA <80%, >10 orphaned, reviews <80%, over-provisioning >30%: 0-65

Ejemplo_Bueno (Score 94):
  - MFA: 98% usuarios (enforced policies)
  - Privileged accounts: 8 justified (exec + security team)
  - Access reviews: 100% quarterly reviews completed
  - Least-privilege: 92% compliance (automated RBAC)
  - Orphaned accounts: 0 (auto-deprovisioning HR integration)
  → Identity governance excelente

Ejemplo_Malo (Score 38):
  - MFA: 45% usuarios (voluntary, not enforced)
  - Privileged accounts: 87 con sudo (developers, contractors, legacy)
  - Access reviews: 32% overdue (última review 18 meses ago)
  - Over-provisioning: 68% usuarios admin rights unnecessary
  - Orphaned accounts: 34 ex-employees (oldest 2 años)
  → Access control disfuncional, alto riesgo insider/external threat
```

---

### SO4. CUMPLIMIENTO NORMATIVO

```yaml
Definición: Adherencia a regulaciones security/privacy (SOC2, ISO27001, GDPR, etc.)

Indicadores:
  - Compliance frameworks certificados (# activos)
  - Controls compliance rate (% controles implemented)
  - Audit findings (# high/critical open)
  - Policy exceptions granted (# no revisadas >180 días)
  - Regulatory fines ($ pagados últimos 24M)

Score_Cálculo (0-100):
  - ≥2 certifications, >95% controls, 0 findings críticos, 0 fines: 90-100
  - 1 certification, 80-95% controls, <5 findings críticos: 70-85
  - 0 certifications, <80% controls, >5 findings críticos, fines: 0-65

Ejemplo_Bueno (Score 96):
  - Certifications: SOC2 Type II, ISO27001 (ambos current)
  - Controls: 98% implemented (automated compliance checks)
  - Audit findings: 3 low-priority open (en remediation)
  - Policy exceptions: 2 active, reviewed quarterly
  - Fines: $0 (100% compliant)
  → Compliance excellence

Ejemplo_Malo (Score 30):
  - Certifications: 0 (SOC2 failed audit 2× attempts)
  - Controls: 68% implemented (manual processes unreliable)
  - Audit findings: 18 high-critical open (backlog 14 meses)
  - Policy exceptions: 47 no revisadas (majority >2 años)
  - Fines: $850K GDPR (data residency violations)
  → Compliance crisis, regulatory risk alto
```

---

### SO5. RESPUESTA INCIDENTES SECURITY

```yaml
Definición: Capacidad detectar, contener, remediar security incidents

Indicadores:
  - Mean Time to Detect (MTTD) security incident
  - Mean Time to Contain (MTTC) post-detection
  - Incident response plan tested (# drills/año)
  - Security incidents last 12M (# y severidad)
  - Post-incident actions completed (% dentro 30 días)

Score_Cálculo (0-100):
  - MTTD <1hr, MTTC <4hrs, ≥4 drills/año, actions 100%: 90-100
  - MTTD 1-24hrs, MTTC 4-24hrs, 2-3 drills/año, actions >80%: 70-85
  - MTTD >24hrs, MTTC >24hrs, <2 drills/año, actions <80%: 0-65

Ejemplo_Bueno (Score 93):
  - MTTD: 35 minutos promedio (SIEM + EDR alerts)
  - MTTC: 2.5 horas promedio (runbooks automated)
  - IR drills: 6/año (quarterly + 2 surprise)
  - Incidents: 3 minor (phishing attempts contained), 0 breaches
  - Post-incident actions: 100% completed <30 días
  → Incident response maduro

Ejemplo_Malo (Score 25):
  - MTTD: 45 días promedio (discovered by customer!)
  - MTTC: 12 días promedio (manual investigation, no playbooks)
  - IR drills: 0 últimos 3 años (plan obsoleto)
  - Incidents: 2 breaches (customer data exfiltrated, ransomware)
  - Post-incident actions: 28% completed (majority abandoned)
  → Incident response inexistente, alto impacto breaches
```

---

### Integración H_Score Extended

```yaml
H_Score_Security_Adjusted:
  Base: 11 observables (O1-O8, IN1-IN3) con pesos §4
  Extended: Agrega SO1-SO5 (security observables)
  
  Fórmula_Extended_Detallada:
    # Renormalizar pesos base a 90% (para dejar 10% a security)
    H_Score = (
      0.90 * (
        0.12 * O1_Demanda +
        0.15 * O2_Valor +
        0.10 * O3_Capacidad +
        0.08 * O4_Eventos +
        0.10 * O5_Restricciones +
        0.10 * O6_Competencia +
        0.08 * O7_Dependencias +
        0.07 * O8_Calidad_Info +
        0.08 * IN1_Velocidad_Decisional +
        0.08 * IN2_Salud_Talento +
        0.04 * IN3_Eficiencia_Flujo
      ) +
      0.10 * avg(SO1, SO2, SO3, SO4, SO5)
    )
  
  Fórmula_Extended_Simplificada (aproximación):
    # Para cálculos rápidos, usar promedios categoría
    # NOTA: Aproximación, no exacta. Usar detallada si precisión crítica.
    H_Score ≈ 0.63 * avg(O1-O8) + 0.18 * avg(IN1-IN3) + 0.10 * avg(SO1-SO5)
    # Adjustados: 0.70*0.90=0.63, 0.20*0.90=0.18
  
  Ponderación_Industry_Specific:
    - Financial/Healthcare (regulated): SO weight 15-20% (ajustar base a 80-85%)
    - SaaS B2B (security-critical): SO weight 12-15% (ajustar base a 85-88%)
    - B2C low-sensitivity: SO weight 5-8% (ajustar base a 92-95%)
    - Default standard: SO weight 10% (base 90%)
  
  Nota_Implementación:
    Use fórmula detallada si implementando desde cero.
    Use fórmula simplificada solo para estimaciones rápidas.
    Diferencia típica: <2 puntos H_Score en mayoría casos.
  
  Crisis_Threshold:
    IF avg(SO1-SO5) < 30 OR any(SO1, SO2, SO3, SO4, SO5) < 20:
      → Security crisis mode (emergency response P_SEC patterns)
```

---

## Referencias Cruzadas

- **Ciclo SDA (Sense):** `CORE/02_Ciclo_Fundamental.md` §2
- **Niveles awareness:** Este documento §5
- **Primitivo Señal:** `CORE/01_Primitivos.md` §3A
- **16 Observables H_Score:** Este documento §2-§4 (O1-O8, I1-I3), §8 (SO1-SO5 security)
- **Security Patterns:** `APLICACION/A1_Patrones.md` §6.5 P_SEC01-P_SEC05 (implementación observables security)
- **Modos decisionales:** `DOMINIOS/D3_Decision.md` §6 (conecta Level 3 Project con Decision)
- **OKRs vinculados:** `DOMINIOS/D3_Decision.md` §1
- **Medición detallada:** `APLICACION/A5_Medicion.md`
- **Security E7:** `DOMINIOS_ESPECIALIZADOS/E7_Enterprise_Technology.md` §6 (security practices detalladas)
