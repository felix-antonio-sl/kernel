# D3_Decision

**Versión:** 3.0.0 | **Estado:** Definitivo | **Audiencia:** Product Managers, Strategy Leaders

## INVARIANTE DOMINIO

**Decisión = Aplicación sistemática de Decide (D1-D4) sobre inputs D2 (observables) → Priorización + Roadmap + Portfolio.**

**Propiedad:** D3 NO ejecuta (eso es D4), solo planifica QUÉ hacer y EN QUÉ ORDEN.

## REFERENCIAS RÁPIDAS

```yaml
Frameworks_Core_3:
  OKRs: §1 - Objectives & Key Results (outcomes not outputs, 70% target)
  Time-Value: §2 - SPIKE/STEP/GROWTH/DELAYED (cuándo capturar valor)
  Probabilistic: §3 - Ranges not points (50%/80%/95% confidence)

Frameworks_Advanced_3:
  Cost_of_Delay: §2.1 - Priorizar valor/tiempo sin estimar effort
  R1-R5_Readiness: §4 - Go/No-Go transformaciones (>60% proceed)
  Portfolio_Optimization: §5 - Multi-objetivo bajo constraints

Métricas:
  D_Score: §6 - Calidad decisional (0-100)
  Crisis: IN1_Velocidad_Decisional <50 (D2 observable)
  Típico_MVD: 65-75 (post-implementación básica)

Decision_Modes (CORE/02 §3):
  D1_Directa: Loops automáticos (<1s, M6)
  D2_Reglas: Condicional (min-hrs, M5)
  D3_Asociativa: Pattern fuzzy (hrs-días, M4)
  D4_Analítica: Iterativo problem-solving (días-semanas, M2-M3)

Type_1_vs_Type_2:
  Type_1: Irreversible (M&A, reorg) → C-level, <14d, slow OK
  Type_2: Reversible (features, tech) → Delegate, <3d, fast

Cross-References:
  CORE/02_Ciclo_Fundamental.md §3: Decide phase (D1-D4 formal)
  D2_Percepcion.md §4.3: S3 Proyectar provee forecasts
  D2_Percepcion.md §3.1: IN1 Velocidad Decisional observable
  D1_Arquitectura.md §1.7: PE7 Reversible Decisions Fast
  D4_Operacion.md §1: Execution consume roadmap D3
```

## Responsabilidad

**DECISIÓN planifica EVOLUCIÓN organizacional mediante análisis D2 (state) → estrategia (qué) → priorización (orden).**

**Pregunta clave:** ¿Qué construir/cambiar y en qué orden para maximizar valor?

**NO pregunta:** ¿Cómo ejecutamos? (eso es D4 Operación)

## §0. QUICK START: DECISIÓN MÍNIMA VIABLE (MVD)

**Objetivo**: Planning framework operando en 4-6 semanas.

### MVD Checklist

```yaml
Week_1-2: OKRs Fundacionales
  ☐ Company-level: 1-2 OKRs (NO 5+)
  ☐ Format: Objective + 3 Key Results SMART
  ☐ Outcome-focused (NO "launch X features", SÍ "increase retention 15%")
  ☐ Transparent: Publicado donde toda org ve

Week_3-4: Time-Value Classification
  ☐ Top 10 backlog items → classify:
    - SPIKE (20%): Deadline-driven
    - STEP (50%): Immediate value
    - GROWTH (20%): Valor crece
    - DELAYED (10%): Long-term
  ☐ Priorizar SPIKEs primero

Week_5: Forecasting Básico
  ☐ Velocity últimos 4 sprints: avg ± std dev
  ☐ Forecast próximos 3 items con ranges:
    - Best: velocity high
    - Expected: velocity avg
    - Worst: velocity low
  ☐ Comunicar ranges, NO points

Week_6: Roadmap Simple
  ☐ H1 (0-3M): Features específicas
  ☐ H2 (3-12M): Capabilities target
  ☐ Link: Feature → OKR (alignment)

Output_MVD:
  - Clarity estratégica (OKRs)
  - Priorización táctica (time-value)
  - Predictibilidad (ranges)
  - D_Score típico: 65-75

Saltar_MVD_Si:
  - OKRs existentes + tracked
  - Roadmap <1 mes old
  - Forecasts con ranges
  → Ir directo §1-§6 completo
```

## §1. OKRs (OBJECTIVES & KEY RESULTS)

### Filosofía Kelly

```yaml
Principios:
  - Bottom-up: Teams proponen (NO top-down dictado)
  - Outcomes: Resultados (NO outputs/actividades)
  - Aspiracional: 70% target (NO 100%)
  - Transparent: Todos ven OKRs de todos
  - Time-boxed: Trimestre típico

Estructura:
  Objective: Declaración cualitativa inspiradora
  Key Results (3-5): Métricas SMART cuantitativas

SMART:
  S: Specific (preciso "NPS 45→65")
  M: Measurable (0-100%)
  A: Achievable (posible pero stretch)
  R: Relevant (alineado OKRs superiores)
  T: Time-bound (31-Dic-2025)

Scoring:
  70-80%: Sweet spot (ambicioso alcanzable)
  >90%: Demasiado conservador (incrementar ambición)
  <50%: Demasiado ambicioso o mal ejecutado (ajustar)
```

### Anti-Patrones (Críticos)

```yaml
AP1_Output_Disguised:
  ❌ "Lanzar 10 features"
  ✅ "Aumentar retention 12%"
  Razón: Output ≠ Outcome

AP6_Top_Down_Imposition:
  ❌ Manager dicta OKRs completos
  ✅ Leader define objetivo, team propone cómo
  Efecto: Imposición destruye ownership

AP7_Linked_to_Compensation:
  ❌ Bonus = 10% si 100% OKRs
  ✅ OKRs desacoplados de bonos
  Efectos: Sandbagging, gaming, no learning

AP8_Estimating_OKRs:
  ❌ "¿Cuánto esfuerzo este OKR?"
  ✅ "OKR ambicioso, aprendemos ejecutando"
  Razón: OKRs son hypothesis valor, NO backlog estimable

Ver_Completo: APLICACION/A2_Antipatrones.md §10 para 9 antipatrones + remediation
```

## §2. PERFILES TIEMPO-VALOR

### 4 Perfiles (Kelly)

```yaml
Concepto: Valor NO se captura siempre al deploy
         Timing afecta captura total

SPIKE (20% portfolio):
  - Valor inmediato, luego decae
  - Ejemplo: Campaña Black Friday
  - Gráfico: ▲ pico rápido → caída
  - Prioridad: Alta (deadline-driven)

STEP (50% portfolio):
  - Valor instantáneo, se mantiene
  - Ejemplo: Bug fix crítico, feature core
  - Gráfico: ┗━━ salto → plateau
  - Prioridad: Media-Alta (ASAP)

GROWTH (20% portfolio):
  - Valor crece gradual en tiempo
  - Ejemplo: Viralidad, SEO, network effects
  - Gráfico: ╱ crecimiento exponencial
  - Prioridad: Media (deploy pronto, optimizar durante)

DELAYED (10% portfolio):
  - Valor tras período incubación
  - Ejemplo: Platform nueva (necesita ecosystem)
  - Gráfico: ___╱ flat → crece
  - Prioridad: Baja (apuesta long-term)

Portfolio_Balance_Óptimo:
  50% STEP, 20% SPIKE, 20% GROWTH, 10% DELAYED
  Desbalance típico: 80% STEP, 5% GROWTH (no investment futuro)
```

### §2.1. Cost of Delay

```yaml
Fórmula:
  CoD = Valor/Tiempo
  CD3 = CoD / Duration (priorizar sin estimar effort)

Ejemplo_Secuencia_Contraintuitiva:
  I1_Halloween_Campaign: Valor $100K, window 2 semanas antes Halloween
  I2_Santa_Campaign: Valor $200K, window 4 semanas antes Navidad
  
  Secuencia_Naive: I2 primero (mayor valor)
  → Miss Halloween window ($100K perdidos)
  → Captura Santa ($200K)
  → Total: $200K
  
  Secuencia_Optimal: I1 primero (menor valor pero deadline)
  → Captura Halloween ($100K)
  → Captura Santa ($200K)
  → Total: $300K
  
  Insight: Timing > Valor absoluto

Antipatrón_I_Need_It_Yesterday:
  Cliente: "Urgente para mañana"
  Investigar: ¿Ventana real captura valor?
  Típico: "Urgencia" emocional, ventana real 3-6 meses
```

## §3. FORECASTING PROBABILÍSTICO

### Filosofía (Manifiesto P6)

```yaml
Principio: Estimación ≠ Compromiso
          Comunicar incertidumbre explícita

Ranges_Not_Points:
  ❌ "Entregaremos 15-May"
  ✅ "50% prob: 10-20 May, 80% prob: 5-25 May"

Planning_Fallacy:
  Humanos subestiman 2-3× tiempo real
  Mitigar: Usar velocity histórica, NO intuición

Forecasting_Hygiene:
  - NO penalizar forecasts incorrectos (destruye honestidad)
  - Actualizar semanalmente con nueva data
  - Track accuracy histórica (learn, improve)
```

### §3.1. Monte Carlo Simulation

```yaml
Input:
  - Velocity histórica (últimos 8-12 sprints)
  - Backlog items (esfuerzo estimado rough)
  - Variabilidad típica (std dev velocity)

Output_Distribución:
  - 50% confidence: 8-12 semanas
  - 80% confidence: 6-16 semanas
  - 95% confidence: 4-20 semanas

Comunicación_Stakeholder:
  "Tenemos 80% probabilidad entregar entre 6-16 semanas.
   Expected case (50%) es 10 semanas.
   Si necesitas >95% certeza, plan 20 semanas."

Delegación: M3-M4 (IA simula, humano interpreta)
```

## §4. READINESS (R1-R5)

### Framework Go/No-Go

```yaml
Uso: Transformaciones >$500K, >6 meses, >30% org impactada

R1_Momentum (20%):
  ¿Existe burning platform o opportunity irresistible?
  Score: 0-100 (pain actual, upside potencial)

R2_Capabilities (30%):
  ¿Tenemos skills, tools, budget?
  Score: 0-100 (gap analysis)

R3_Forces (20%):
  ¿Stakeholders apoyan o resisten?
  Score: 0-100 (coalición + resistencia)

R4_Drivers (15%):
  ¿Líderes comprometidos drive change?
  Score: 0-100 (bandwidth, credibility)

R5_Catalysts (15%):
  ¿Quick wins posibles early?
  Score: 0-100 (visible success factible)

Readiness_Score = 0.20*R1 + 0.30*R2 + 0.20*R3 + 0.15*R4 + 0.15*R5

Decision:
  >70: GO (alta probabilidad éxito)
  60-70: CONDITIONAL (address gaps primero)
  <60: NO-GO (defer hasta readiness mejora)

Ejemplo:
  Transformación_Cloud_Migration:
    R1: 85 (on-prem caro, scaling imposible)
    R2: 60 (team sabe Docker, no Kubernetes)
    R3: 70 (CTO apoya, CFO neutral, Ops resiste)
    R4: 75 (CTO dedicado 40% tiempo)
    R5: 65 (POC factible en 4 semanas)
    → Readiness = 0.20*85 + 0.30*60 + 0.20*70 + 0.15*75 + 0.15*65 = 69
    → CONDITIONAL GO (upskill Kubernetes primero)
```

## §5. PORTFOLIO OPTIMIZATION

### Multi-Objetivo

```yaml
Inputs:
  - N initiatives candidatas
  - Constraints: Budget, Time, Headcount
  - Scores: Valor, Riesgo, Costo, OKR_Fit

Función_Objetivo:
  Maximize: Σ(Valor_i * OKR_Fit_i * (1 - Riesgo_i))
  Subject_to:
    Σ Budget_i ≤ Budget_total
    Σ Headcount_i ≤ Headcount_available
    Σ Duration_i overlaps viable

Output:
  - Portfolio óptimo (subset initiatives)
  - ROI esperado
  - Risk profile agregado

Delegación: M2-M3 (IA optimiza, humano valida trade-offs)

Ver: APLICACION/A3_Optimization.md para algoritmos detallados
```

## §6. D_SCORE (0-100)

### Fórmula Decisión

```yaml
D_Score: Métrica agregada calidad decisional

Fórmula:
  D_Score = (
    0.40 * OKRs_Quality +
    0.30 * Forecasting_Hygiene +
    0.20 * Roadmap_Clarity +
    0.10 * Readiness_Assessment
  )

Componentes:

  OKRs_Quality (0-100):
    - Outcome-focused (NO output disguised): 25%
    - Transparent (todos ven): 25%
    - Aligned (team → company): 25%
    - Time-boxed + actualizado: 25%
  
  Forecasting_Hygiene (0-100):
    - Probabilístico (ranges not points): 30%
    - Actualizado semanalmente: 25%
    - Accuracy histórica >70%: 25%
    - NO penalización forecasts incorrectos: 20%
  
  Roadmap_Clarity (0-100):
    - H1 (0-3M) detallado: 40%
    - H2 (3-12M) visible: 35%
    - Features → OKRs linked: 25%
  
  Readiness_Assessment (0-100):
    - R1-R5 evaluado pre-transformación: 50%
    - Go/No-Go data-driven: 50%

Interpretación:
  >75: Decisión excelente (predictable, aligned, data-driven)
  60-75: Decisión funcional (gaps menores)
  <60: Decisión débil (ad-hoc, reactive)

Típico_post-MVD: 65-75
Típico_excelencia: 80-90

Vinculación_D2:
  D_Score consume IN1_Velocidad_Decisional (D2 §3.1)
  IF D_Score <60 AND IN1 <50 → Crisis decisional, escalate
```

## §7. MODOS DECISIONALES (CORE/02 §3)

### Espectro Complejidad

```yaml
Conexión_Ciclo_SDA:
  Decide phase opera en 4 modos (CORE/02_Ciclo_Fundamental.md §3):

D1_DIRECTA (Mode 1):
  - Loops automáticos (<1s)
  - Ejemplo: Autoscaling CPU >80% → add instance
  - Delegación: M6 Execute (bounded autonomy)
  - Awareness: S1 Detectar

D2_REGLAS (Mode 2):
  - Condicional (min-hrs)
  - Ejemplo: H_Score <45 → activate Crisis Governance
  - Delegación: M5 Co-produce (automated con oversight)
  - Awareness: S2 Comprender

D3_ASOCIATIVA (Mode 3):
  - Pattern fuzzy (hrs-días)
  - Ejemplo: ML churn prediction → retention offer
  - Delegación: M4 Control (IA sugiere, humano valida)
  - Awareness: S3 Proyectar

D4_ANALÍTICA (Mode 4):
  - Iterativo problem-solving (días-semanas)
  - Ejemplo: Market entry strategy, M&A due diligence
  - Delegación: M2-M3 Enable (humano-led, IA augmenta)
  - Awareness: S3 Proyectar + causal

Decision_Mode_Selection:
  IF problema SIMPLE AND rules EXHAUSTIVE:
    → D1-D2 (automate M5-M6)
  
  ELSE IF problema KNOWN AND pattern RECOGNIZED:
    → D3 (IA suggests, humano valida M4)
  
  ELSE IF problema COMPLEX OR strategic:
    → D4 (humano-led, IA augments M2-M3)

Evolution_Path:
  D4 (humano resuelve) → codify heuristics
  D3 (IA aprende patterns) → validate suggestions
  D2 (convert to explicit rules) → automate con oversight
  D1 (full automation bounded)
```

## §8. ANTI-PATRONES DECISIONALES

```yaml
AP_D3_1_Analysis_Paralysis:
  Síntoma: Forecasting perfecto, pero NO decisiones
  Causa: D3 viola ortogonalidad (debe Decidir, no solo analizar)
  Fix: Time-box analysis, decide con data imperfecta

AP_D3_2_HiPPO_Decisions:
  Síntoma: Highest Paid Person's Opinion gana siempre
  Causa: NO data-driven, autoridad trumps evidence
  Fix: OKRs + observables transparent, escalate con data

AP_D3_3_Sunk_Cost_Fallacy:
  Síntoma: "Ya invertimos $2M, debemos continuar"
  Causa: Confundir costos hundidos con valor futuro
  Fix: Evaluar solo valor futuro esperado vs costo futuro

AP_D3_4_Recency_Bias:
  Síntoma: Última crisis domina roadmap (reactive)
  Causa: NO balance portfolio (todo SPIKE, no GROWTH/DELAYED)
  Fix: Portfolio mix 50/20/20/10, resist reactive pivots

AP_D3_5_Feature_Factory:
  Síntoma: Medir outputs (features shipped), NO outcomes (valor)
  Causa: OKRs son outputs disguised (AP1)
  Fix: Manifiesto P5 (Outcomes > Outputs), track O2_Valor

Ver: APLICACION/A2_Antipatrones.md §10 para 15+ decisionales
```

## §9. COALICIONES & RESISTENCIA

### Building Coalitions (Kotter)

```yaml
Tamaño_Mínimo:
  - Org <50: 3-5 personas (1 C-level)
  - Org 50-200: 8-12 personas (2-3 executives)
  - Org 200-1000: 15-25 personas (functional heads)

Composición:
  - Power: Autoridad formal (CTO, VPs)
  - Expertise: Conocimiento técnico (Architects)
  - Credibility: Respeto peers (Tech leads)
  - Leadership: Influencia natural (Change agents)

Resistencia_Como_Señal:
  NO "malas personas", ES información

Tipos:
  Cognitiva: No entienden why (fix: comunicar urgencia R1)
  Emocional: Miedo pérdida (fix: address fears 1:1)
  Política: Cambio reduce poder (fix: negotiate win-win)
  Legítima: Concerns técnicos válidos (fix: ESCUCHAR, ajustar)
```

## §10. VALIDACIÓN DOMINIO

**Validación Formal:** Ver `CORE/07_Validacion.md` para pruebas completas de Invariantes I1-I3, Completitud y Consistencia.

**Checklist Rápido D3 (5 min):**

```yaml
✓ Ortogonalidad: D3 ∩ {D1, D2, D4} = ∅
  - D3 decide/planifica, D2 detecta, D1 organiza, D4 ejecuta
  - Sin solapamiento: D3 consume información D2, produce roadmap para D4

✓ Trazabilidad: Flujo causal verificable
  - D2 observables → D3 OKRs/roadmap → D4 execution → D2 outcomes (loop)
  - Ejemplo: O2_Valor↓ → D3 prioriza CX OKR → D4 fixes bugs → O2↑

✓ Completitud: Frameworks suficientes
  - Estratégica: OKRs, Readiness (R1-R5)
  - Táctica: Time-Value, Cost of Delay
  - Portfolio: Optimization multi-objetivo

✓ Parsimonia: Elementos mínimos
  - OKRs: Necesario para alignment estratégico
  - Time-Value: Necesario para priorización
  - Forecasting probabilístico: Necesario para predictibilidad

✓ Alineamiento CORE:
  - A4 (Ciclo SDA) → D1-D4 es el Decide del ciclo
  - P3 (Outside-In) → OKRs driven por outcomes externos
  - P5 (Outcomes > Outputs) → OKRs miden valor, no features
  - P6 (Probabilístico) → Forecasting bajo incertidumbre
```

**Para revisión formal:** Aplicar pruebas de `CORE/07_Validacion.md` §2 (Ortogonalidad), §3 (Trazabilidad)

## Referencias Cruzadas

- **Ciclo SDA Decide:** `CORE/02_Ciclo_Fundamental.md` §3 (D1-D4 formal)
- **Manifiesto P5:** `CORE/00_Manifiesto.md` §3.5 (Outcomes > Outputs)
- **Manifiesto P6:** `CORE/00_Manifiesto.md` §3.6 (Probabilístico)
- **Observables decisión:** `D2_Percepcion.md` (O1-O8, IN1)
- **S3 Proyectar:** `D2_Percepcion.md` §4.3 (forecasts input D3)
- **IN1 Velocidad:** `D2_Percepcion.md` §3.1 (observable vinculado)
- **PE7 Reversible:** `D1_Arquitectura.md` §1.7 (Type 1 vs Type 2)
- **Execution:** `D4_Operacion.md` §1 (consume roadmap D3)
- **Delegación:** `CORE/04_Delegacion.md` (M2-M6)
- **Smartness D3:** `CORE/05_Smartness.md` matriz D3 row
- **Trazabilidad:** `CORE/06_Trazabilidad.md` §3 (Objetivos→Valor)
- **Implementación:** `APLICACION/A4_Implementacion.md`

**Fin D3_Decision v3.0.0**