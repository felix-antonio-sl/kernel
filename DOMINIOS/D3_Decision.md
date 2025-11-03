# D3_Decision

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Product Managers, Líderes Estratégicos

---

## REFERENCIAS RÁPIDAS
```yaml
Frameworks_Principales:
 OKRs: §1 - Objectives & Key Results (bottom-up, outcome-focused, 70% target)
 Time-Value_Profiles: §2 - SPIKE/STEP/GROWTH/DELAYED (cuándo se captura valor)
 R1-R5_Readiness: §3 - Momentum/Capabilities/Forces/Drivers/Catalysts (>60% go)
 Cost_of_Delay: §2.1 - Priorizar sin estimar effort (valor/tiempo)
 Probabilistic_Forecasts: §3.1 - Ranges not points (50%/80%/95% confidence)
Conceptos_Core:
 Type_1_Decisions: Irreversibles (M&A, reorg), requieren C-level, slow OK
 Type_2_Decisions: Reversibles (features, tech), delegar, fast
 Elastic_Deadlines: Deadline = ventana captura valor, no fecha fija
 Portfolio_Mix: 50% STEP, 20% SPIKE, 20% GROWTH, 10% DELAYED (balance)
 Schedules_as_Forecasts: Estimación ≠ compromiso (no commitment culture)
Antipatrones_OKRs:
 AP1_Output_Disguised: "Lanzar 10 features" (malo) vs "Aumentar retention 12%" (bueno)
 AP6_Top_Down_Imposition: Manager dicta OKRs → destruye ownership
 AP7_Linked_to_Compensation: OKRs vinculados a bonus → sandbagging, gaming
 AP8_Estimating_OKRs: Tratar OKRs como backlog estimable → conservadurismo
Métricas:
 D_Score: §6 - Calidad decisional (OKRs 40% + Forecasts 30% + Roadmap 20% + R1-R5 10%)
 Typical_MVD: 65-75 (post implementación mínima viable)
 Excellence: >75 (predictable, aligned, data-driven)
Ejemplos_Clásicos:
 Halloween_vs_Santa: §2.1 - Secuencia contraintuitiva maximiza valor capturado
 I_Need_It_Yesterday: §2.1 - Investigar ventana real vs urgencia emocional
 Planning_Fallacy: §3.1 - Humanos subestiman 2-3x tiempo real
Cross-References:
 D2_Percepcion.md §3.1: IN1 Velocidad Decisional (observable vinculado)
 D4_Operacion.md §7.1: Carry-over work (flow entre iteraciones)
 APLICACION/A1_Patrones.md: P31 RICE, P33 WSJF (priorización frameworks)
 APLICACION/A2_Antipatrones.md §10: Cost of Delay antipatrones organizacionales
 CORE/00_Manifiesto.md: Outside-In (P3), Customer-Facing Tests (P5)
```
---

## Responsabilidad

**DECISIÓN planifica EVOLUCIÓN organizacional:** Estrategia, priorización, roadmaps, portfolio management.

**Pregunta clave:** ¿Qué debemos construir/cambiar y en qué orden?

---

## §0. QUICK START: DECISIÓN MÍNIMA VIABLE (MVD)

**Objetivo**: Planning framework funcionando en 4-6 semanas.

### MVD Checklist (4-6 semanas)

```yaml
Week_1-2: OKRs Básicos
  ☐ Company-level: 1-2 OKRs (not 5+)
  ☐ Format: Objective + 3 Key Results SMART
  ☐ Outcome-focused (not "launch X features", but "increase retention 15%")
  ☐ Transparent: Published donde toda org ve (Confluence, Notion, etc.)
  
Week_3: Time-Value Awareness
  ☐ Classify top 10 backlog items:
    - SPIKE (urgent time-bound): 20%
    - STEP (immediate value): 50%
    - GROWTH (value grows): 20%
    - DELAYED (long-term bet): 10%
  
  ☐ Prioritize SPIKEs first (deadline-driven)

Week_4-5: Probabilistic Forecasting Básico
  ☐ Calculate team velocity (last 4 sprints avg ± std dev)
  ☐ Forecast próximas 3 features:
    - Best case (velocity high)
    - Expected case (velocity avg)
    - Worst case (velocity low)
  
  ☐ Communicate ranges, not points ("2-4 semanas", not "3 semanas")

Week_6: Roadmap Simple
  ☐ Horizonte 1 (now - 3 meses): Features específicas
  ☐ Horizonte 2 (3-12 meses): Capabilities target
  ☐ Link: Each feature → Company OKR (alignment explicit)

Output_MVD:
  - Strategic clarity (OKRs documented)
  - Tactical prioritization (time-value informed)
  - Predictability (probabilistic forecasts)
  - Typical D_Score post-MVD: 65-75

Next_Steps_Post_MVD:
  - Expand frameworks (R1-R5 readiness, portfolio optimization)
  - Implement patrones (P31 RICE, P33 WSJF)
  - Automate (M4 auto-prioritization backlog)
```

---

### Frameworks MVD (3 esenciales de 7)

```yaml
OKRs_Bottom-Up:
  - CRÍTICO: Outcomes not outputs, transparent, time-boxed
  - Skip complexity: Start 1-2 OKRs, not 8
  
Time-Value_Profiles:
  - IMPORTANTE: Understand WHEN value captured
  - Skip complexity: 4 types sufficient (SPIKE/STEP/GROWTH/DELAYED)
  
Probabilistic_Forecasts:
  - IMPORTANTE: Ranges not points, confidence intervals
  - Skip complexity: Velocity-based simple (no Monte Carlo yet)

Defer_Post-MVD:
  - Cost of Delay detailed analysis
  - Readiness R1-R5 (unless transformation planned)
  - Coaliciones (unless major change)
  - Portfolio optimization advanced
```

---

### Cuando Skip MVD

```yaml
Ya_Tienes_MVD_Si:
  - OKRs existentes y tracked
  - Roadmap published <1 month old
  - Forecasts con ranges (not just deadlines)
  - D_Score >70
  
  → Skip to advanced frameworks (§2-§7 completo)

MVD_No_Suficiente_Si:
  - Transformation planned (>$500K, >6 meses)
    → Need R1-R5 readiness desde inicio
  
  - Portfolio >20 initiatives active
    → Need optimization framework desde inicio
  
  - Highly regulated
    → Need compliance integration desde inicio
```

---

## §1. OKRs (OBJECTIVES & KEY RESULTS)

### Metodología Kelly

```yaml
Filosofía:
  - Bottom-up (teams proponen, no top-down impuesto)
  - Outcome-focused (resultados, no outputs/actividades)
  - Aspiracional (70% target, no 100% garantizado)
  - Transparent (todos ven OKRs de todos)
  - Time-boxed (trimestre típico, anual estratégico)

Estructura:
  Objective: Declaración cualitativa inspiradora
  Key Results (3-5): Métricas cuantitativas SMART
  
  SMART:
    S: Specific (preciso)
    M: Measurable (medible 0-100%)
    A: Achievable (posible pero ambicioso)
    R: Relevant (alineado a objetivos superiores)
    T: Time-bound (deadline claro)
```

---

### Ejemplo OKR Completo

```yaml
Nivel_Compañía (Anual):
  Objective: "Ser líder regional en satisfacción cliente ecommerce"
  KR1: NPS aumenta de 45 a 65 (+20 pts) al 31-Dic-2025
  KR2: Churn reduce de 12% a 5% (-7 pp) al 31-Dic-2025
  KR3: Time-to-resolution tickets baja de 8hrs a 2hrs al 31-Dic-2025
  
  Target: 70% (si alcanzamos 70% de cada KR, es éxito)
  Actual Q4: NPS=58 (65% progreso), Churn=7% (71%), TTR=3.5hrs (75%)
  → Score total: 70% ✅ Exitoso

Nivel_Team (Trimestral):
  Objective: "Mejorar experiencia onboarding clientes nuevos"
  KR1: Time-to-first-value reduce de 14 días a 7 días (-50%)
  KR2: Activation rate (uso feature clave) sube de 40% a 60% (+20pp)
  KR3: Support tickets onboarding bajan de 200/mes a 80/mes (-60%)
  
  Parent: Conecta a KR1 compañía (NPS, porque onboarding mejora satisfacción)
```

---

### Anti-Patrones OKRs

```yaml
AP1_Output_Disguised:
  ❌ Malo: "Lanzar 10 features nuevas"
  ✅ Bueno: "Aumentar retention 12% vía nuevas features"
  Razón: Output (10 features) ≠ Outcome (retention)

AP2_100%_Target:
  ❌ Malo: "100% uptime" (imposible, conservador)
  ✅ Bueno: "99.95% uptime" (ambicioso pero realista, 70% sería 99.97%)
  Razón: OKR debe estirar, no ser seguro

AP3_Too_Many:
  ❌ Malo: 8 OKRs por team
  ✅ Bueno: 1-2 OKRs por team (3-5 KRs cada uno)
  Razón: Focus, no dilución

AP4_No_Alignment:
  ❌ Malo: Team OKR no conecta a Company OKR
  ✅ Bueno: Cada Team OKR deriva de Company/Dept OKR
  Razón: Sin alignment, sub-optimization

AP5_Vanity_Metrics:
  ❌ Malo: "Aumentar tráfico web +50%"
  ✅ Bueno: "Aumentar conversión qualified leads +30%"
  Razón: Tráfico puede ser bots, conversión es real valor

AP6_Top_Down_Imposition:
  ❌ Malo: Manager dicta OKRs completos a team ("Harán X, Y, Z")
  ✅ Bueno: Leader define objetivo final, team propone cómo lograrlo
  Razón: Imposición top-down destruye ownership y motivación
  Ejemplo_Malo: "Team A: Implementarán chatbot, reducirán tickets 30%"
  Ejemplo_Bueno: "Necesitamos reducir carga support. ¿Cómo pueden ayudar?"
           → Team A propone: "Chatbot + knowledge base → -30% tickets"
  Consecuencia: Teams sin autonomía solo "cumplen órdenes", no innovan

AP7_Linked_to_Compensation:
  ❌ Malo: "Bonus = 10% si logran 100% OKRs, 5% si 70%"
  ✅ Bueno: OKRs desacoplados de bonos individuales
  Razón: Vincular $ a OKRs destruye seguridad psicológica
  Efectos_Perversos:
    - Teams sandbag (metas conservadoras para garantizar bonus)
    - Gaming del sistema (manipulan métricas)
    - No comparten fracasos, no aprenden
    - Colaboración cross-team se destruye (competencia por bonos)
  Alternativa: Bonos basados en company performance general, no OKR completion

AP8_Estimating_OKRs:
  ❌ Malo: "¿Cuánto esfuerzo tomará este OKR? Estimemos story points"
  ✅ Bueno: "Este OKR es ambicioso, intentaremos, aprendemos en el camino"
  Razón: OKRs NO son para estimar, son para ser ambiciosos
  Confusión_Común: Tratar OKRs como backlog estimable
  Realidad: OKRs son hypothesis de valor, no plan de ejecución detallado
  Consecuencia: Si estimas OKRs, tiendes a hacer solo lo "seguro estimable"

AP9_100%_Completion_Expected:
  ❌ Malo: "Este team solo logró 65% OKRs, fracasaron"
  ✅ Bueno: "Lograron 70%, exactamente el target. Exitoso."
  Razón: OKRs diseñados para 70% completion, no 100%
  Filosofía:
    - 100% completion → Metas muy conservadoras
    - 40-60% completion → Posiblemente demasiado ambiciosas o mal ejecutadas
    - 70-80% completion → Sweet spot (ambiciosos pero alcanzables)
  Ajuste: Si team consistentemente logra >90%, incrementar ambición
          Si consistentemente <50%, reducir ambición o mejorar capacidades
```

---

## §2. PERFILES TIEMPO-VALOR

### Time-Value Profiles (Kelly)

```yaml
Concepto: No todo valor se captura cuando feature se deploya
         Valor emerge en el tiempo según tipo de iniciativa

4_Perfiles:

1. SPIKE:
   - Valor inmediato, luego decae
   - Ejemplo: Campaña marketing evento específico
   - Gráfico: ▲ (pico rápido, caída rápida)
   - Timing crítico: Deploy antes de evento

2. STEP:
   - Valor instantáneo, se mantiene
   - Ejemplo: Fix bug crítico, nueva capability core
   - Gráfico: ┗━━ (salto, plateau)
   - Timing: Deploy ASAP

3. GROWTH:
   - Valor crece gradualmente en el tiempo
   - Ejemplo: Viralidad, network effects, SEO
   - Gráfico: ╱ (crecimiento exponencial/lineal)
   - Timing: Deploy pronto, optimizar durante crecimiento

4. DELAYED:
   - Valor después de período incubación
   - Ejemplo: Plataforma nueva (necesita ecosystem)
   - Gráfico: ___╱ (flat, luego crece)
   - Timing: Inversión largo plazo, paciencia
```

---

### Aplicación en Priorización

```yaml
Portfolio_Mix_Saludable:
  - 50% STEP (valor inmediato, mantiene momentum)
  - 20% SPIKE (oportunidades tácticas)
  - 20% GROWTH (inversión futuro cercano)
  - 10% DELAYED (inversión largo plazo, opcionalidad)

Ejemplo_Portfolio_Q4:
  STEP:
    - Fix vulnerabilidad seguridad crítica (valor: evitar breach)
    - Feature paridad competitor (valor: retain clientes)
  
  SPIKE:
    - Campaña Black Friday (valor: revenue noviembre)
  
  GROWTH:
    - Programa referidos (valor: crece mes a mes)
    - SEO optimization (valor: crece trimestre a trimestre)
  
  DELAYED:
    - Platform API pública (valor: ecosistema en 12+ meses)
```

---

### §2.1. COST OF DELAY (CoD) & ELASTIC DEADLINES

#### Cost of Delay: Priorización sin Estimaciones

```yaml
Concepto: Impacto económico de retrasar una decisión o entrega
         Puede calcularse SIN estimar esfuerzo

Fórmula_Básica:
  CoD = Valor_Perdido_por_Unidad_Tiempo
  
  Ejemplo:
    - Feature A genera $50K/mes si deployed
    - Cada mes de delay = $50K CoD
    - Si tardamos 3 meses extra → $150K perdidos

Ventaja_CoD:
  - No requiere effort estimates (solo valor temporal)
  - Revela prioridades contra-intuitivas
  - Expone costo de "analysis paralysis"
```

---

#### Elastic Deadlines: Basados en Valor

```yaml
Concepto: Deadline no es fecha fija, es ventana de captura de valor

Pregunta_Tradicional (incorrecta):
  "¿Cuándo estará listo?" → Fuerza estimación esfuerzo

Pregunta_Correcta:
  "¿Qué podemos entregar para fecha X?" → Maximiza valor capturado

Ejemplo_Clásico: Halloween vs Santa App
  Contexto:
    - Halloween app: $355K valor, 4 semanas build
    - Santa app: $1.06M valor, 6 semanas build
    - Fecha actual: Inicio septiembre
  
  Análisis_Naive:
    Opción_A: Santa first (mayor valor absoluto $1.06M)
    Opción_B: Halloween first (menor valor $355K)
  
  Time-Value_Profile_Analysis:
    Halloween_Value_Decay:
      - Deploy fin Sept: $340K captured (deadline Oct 31)
      - Deploy Nov: $0 (evento pasó)
    
    Santa_Value_Decay:
      - Deploy Oct: $1.025M captured
      - Deploy mid-Nov: $800K captured (optimal window mid-Nov → Navidad)
      - Deploy Enero: $200K (post-temporada)
  
  Opción_C: Halloween → Santa (secuencia contraintuitiva)
    - Halloween deployed fin Sept: $340K
    - Santa deployed mid-Nov: $800K
    - Total: $1.14M ✅ (ganancia $115K vs opción naive)
  
  Opción_D: Santa → Halloween (secuencia "lógica")
    - Santa deployed mid-Oct: $1.025M
    - Halloween llega Nov (demasiado tarde): $0
    - Total: $1.025M ❌ (pérdida $115K)

Lección_Clave:
  - Valor absoluto ($1.06M > $355K) engaña
  - Ventana temporal y decay rate dominan
  - Secuencia óptima emerge de análisis CoD, no de "sentido común"
```

---

#### "I Need It Yesterday" Fallacy

```yaml
Escenario_Común:
  Stakeholder: "Necesito feature X para ayer, perdimos deal $1M"

Problema:
  - Valor en el pasado = $0 (no recuperable sin time machine)
  - Demanda "para ayer" es emotional, no analítica

Respuesta_Correcta:
  1. Acknowledge: "Entiendo que hubo oportunidad perdida"
  2. Redirect: "¿Cuál es el valor FUTURO de feature X?"
  3. Investigate: "¿Cuándo hay próxima oportunidad similar?"
  4. Discover real profile: Típicamente hay ventana futura de meses, no "ayer"

Ejemplo_Real:
  Stakeholder: "Cliente noruego quería feature X hace 2 meses, deal $1M perdido"
  
  Investigación:
    - Cliente sigue interesado (no perdido permanentemente)
    - Puede dar $100K down-payment ahora con commitment
    - Necesita deployment en 4 meses (procesos internos aprobación)
    - Full value ($1M) realizable en 8 meses
  
  Resultado:
    - "Yesterday" era ilusorio
    - Real window: 4-8 meses (manejable)
    - Time-value profile: $0 (ayer) → $100K (ahora) → $1M (8 meses)
    - Priorización informada, no reactiva

Lección:
  - Nueva información (oportunidad perdida) informa priorización futura
  - NO causa disrupción inmediata ("drop everything")
  - Investigar revela ventanas reales vs urgencias emocionales
```

---

#### Análisis CoD sin Esfuerzo

```yaml
Poder_CoD: Puede priorizar portfolio SIN estimar effort

Proceso:
  1. Identificar initiatives candidatas (I1, I2, ..., I10)
  2. Estimar valor temporal ($/mes o $/semana)
  3. Identificar decay rates (cuán rápido valor decae)
  4. Calcular CoD para cada initiative
  5. Rankear por CoD (valor/tiempo)

Ejemplo:
  I1_Security_Fix:
    - Valor: Evitar breach ($500K potencial pérdida)
    - Decay: Lineal, cada semana delay +10% probabilidad breach
    - CoD: $50K/semana
    - Rank: #1 (deploy ASAP)
  
  I2_Revenue_Feature:
    - Valor: $200K/año revenue
    - Decay: Plano hasta Q4, luego competitor lanza similar
    - CoD: $16K/mes, pero spike en Q4
    - Rank: #2 (deploy antes Q4)
  
  I3_UX_Improvement:
    - Valor: $100K/año via retention
    - Decay: Muy gradual
    - CoD: $8K/mes
    - Rank: #3 (deploy cuando capacity disponible)

Decisión:
  I1 → I2 → I3 (sin nunca estimar effort)
  
  Si capacity: Hacer todos
  Si constraint: I1 obligatorio, I2 si posible, I3 postponer

Ventaja:
  - Análisis rápido (horas, no semanas)
  - No "analysis paralysis" esperando estimaciones perfectas
  - Capture cost del propio análisis (delay mientras estimamos)
```

**Ver también:** `APLICACION/A2_Antipatrones.md` §10 para estimaciones de impacto financiero (Cost of Delay) causado por antipatrones organizacionales.

---

## §3. PREPARACIÓN (R1-R5)

### Framework Preparación Transformación

```yaml
Concepto: Antes de ejecutar cambio mayor, evaluar 5 dimensiones preparación
         Si score total <60%, transformación probablemente falla

Score: 0-100 por dimensión, promedio ponderado
```

---

### R1. MOMENTUM

```yaml
Definición: Urgencia percibida y energía para cambio

Indicadores:
  - Pain actual (severity problema): ¿Crisis o molestia?
  - Tiempo en status quo: ¿Años estancados o meses?
  - Leadership commitment: ¿CEO/CTO sponsor activo?
  - Timeline pressure: ¿Deadline externo (regulación, competencia)?

Score:
  90-100: Crisis visible, CEO sponsor, deadline claro
  70-85: Pain moderado, sponsor VP-level, urgencia media
  <60: "Nice to have", no sponsor claro, sin urgencia

Ejemplo_Alto_Momentum (Score 95):
  - Pain: Sistema legacy cae 2 veces/mes, pérdida $500K/incident
  - Tiempo: 3 años sin modernizar, tech debt crítico
  - Leadership: CTO sponsor activo, budget aprobado
  - Deadline: Regulación nueva requiere cambio en 9 meses
  → Alta probabilidad éxito

Ejemplo_Bajo_Momentum (Score 35):
  - Pain: "Sería bueno tener mejor UX"
  - Tiempo: 6 meses desde idea
  - Leadership: PM interesado, no C-level sponsor
  - Deadline: Ninguno
  → Alta probabilidad fracaso, postponer hasta momentum suba
```

---

### R2. CAPABILITIES

```yaml
Definición: Skills y recursos disponibles para ejecutar

Indicadores:
  - Technical skills: ¿Team tiene expertise necesario?
  - Headcount: ¿Suficientes personas?
  - Budget: ¿$ suficiente?
  - Time: ¿Calendario realista?

Score:
  90-100: Team experto, headcount suficiente, budget holgado
  70-85: Skills OK (o trainable), headcount justo, budget tight
  <60: Gaps críticos skills, understaffed, budget insuficiente

Ejemplo_Alto_Capabilities (Score 88):
  - Skills: 8 engineers con experiencia Kubernetes
  - Headcount: 10 personas asignadas (vs 8 necesario)
  - Budget: $500K aprobado (vs $400K estimado)
  - Time: 9 meses calendario (vs 8 meses estimado)
  → Factible

Ejemplo_Bajo_Capabilities (Score 40):
  - Skills: 0 engineers con experiencia ML (necesario para proyecto)
  - Headcount: 3 personas (vs 10 necesario)
  - Budget: $100K (vs $600K estimado)
  - Time: 3 meses (vs 12 meses realista)
  → Inviable, necesita hiring o upskilling primero
```

---

### R3. FORCES

```yaml
Definición: Balance fuerzas a favor vs en contra

Indicadores:
  - Supporters (quién apoya): # y seniority
  - Blockers (quién bloquea): # y poder veto
  - Affected parties: ¿Mayoría gana o pierde?
  - Political capital: ¿Sponsor tiene influencia suficiente?

Score:
  90-100: Mayoría apoya, blockers minoritarios sin veto
  70-85: Supporters y blockers balanceados, negociable
  <60: Mayoría se opone o blockers con poder veto

Ejemplo_Alto_Forces (Score 90):
  - Supporters: CTO + 8 de 10 teams
  - Blockers: 2 managers con concerns, pero sin veto
  - Affected: 70% personas mejoran (mejor tools)
  - Political: CTO tiene mandate CEO
  → Oposición manejable

Ejemplo_Bajo_Forces (Score 30):
  - Supporters: 1 PM entusiasta
  - Blockers: CFO (dice "muy caro"), 6 de 10 teams ("no tenemos tiempo")
  - Affected: 60% personas perciben más trabajo sin beneficio claro
  - Political: PM no tiene autoridad cross-team
  → Resistencia fuerte, fracaso probable
```

---

### R4. DRIVERS

```yaml
Definición: Motivadores externos que fuerzan o incentivan cambio

Indicadores:
  - Regulatory: ¿Ley nueva obliga?
  - Competitive: ¿Competencia nos está superando?
  - Customer: ¿Clientes demandan?
  - Financial: ¿Costo status quo insostenible?

Score:
  90-100: Múltiples drivers fuertes, status quo no viable
  70-85: 1-2 drivers moderados
  <60: Sin drivers externos claros

Ejemplo_Alto_Drivers (Score 95):
  - Regulatory: GDPR requiere cambios (mandatorio)
  - Competitive: 3 competitors lanzaron feature clave
  - Customer: NPS cayó 20 pts, feedback consistente
  - Financial: Infra legacy cuesta $2M/año vs $500K moderna
  → Cambio inevitable

Ejemplo_Bajo_Drivers (Score 25):
  - Regulatory: Ninguno
  - Competitive: Sin presión
  - Customer: Satisfechos con status quo
  - Financial: Costo actual OK
  → Cambio opcional, baja prioridad
```

---

### R5. CATALYSTS

```yaml
Definición: Eventos o personas que aceleran cambio

Indicadores:
  - Quick wins disponibles: ¿Hay victorias tempranas visibles?
  - Change agents: ¿Hay champions internos con credibilidad?
  - Success stories: ¿Otras orgs han hecho esto exitosamente?
  - Tooling/enablers: ¿Existen herramientas que facilitan?

Score:
  90-100: Múltiples quick wins, champions fuertes, casos éxito probados
  70-85: 1-2 quick wins, champion moderado
  <60: Sin quick wins visibles, no champions

Ejemplo_Alto_Catalysts (Score 92):
  - Quick wins: Pilot en 1 team mostró 40% reducción cycle time en 4 semanas
  - Champions: Tech Lead senior respetado, evangeliza activamente
  - Success stories: Netflix, Google, Spotify publicaron casos similares
  - Tooling: Kubernetes maduro, muchos tutoriales/support
  → Momentum se auto-refuerza

Ejemplo_Bajo_Catalysts (Score 30):
  - Quick wins: Ninguno identificado (proyecto largo, payoff tardío)
  - Champions: Nadie con credibilidad empuja fuerte
  - Success stories: Ninguna org comparable ha hecho esto
  - Tooling: Tech bleeding-edge, inmadura
  → Uphill battle, riesgo fatiga
```

---

### Decisión Go/No-Go

```yaml
Preparación_Score = (
  0.25 * R1_Momentum +
  0.25 * R2_Capabilities +
  0.20 * R3_Forces +
  0.15 * R4_Drivers +
  0.15 * R5_Catalysts
)

Ponderaciones_Rationale:
  - R1/R2 peso igual 25%: Momentum y Capabilities son critical success factors
  - R3 Forces 20%: Resistencia puede bloquear, pero superable
  - R4/R5 menor: Drivers y Catalysts aceleran pero no son blockers absolutos

Disclaimer_Calibración:
  Estado: Ponderaciones basadas en change management research (Kotter, Prosci)
  Validación: Correlación empírica con 10 casos transformación
  Customización: Ajustar según context
    - Regulatory change (mandated): R4 weight→35%, R1→15%
    - Cultural transformation: R3 weight→30%, R5→20%
    - Technical migration: R2 weight→35%, R5→10%

Decisión:
  >75: GO - Alta probabilidad éxito, proceder
  60-75: GO CONDITIONAL - Addressar gaps primero (ej: hire, build momentum)
  <60: NO-GO - Transformación probablemente falla, postponer o rediseñar
  
Evidencia_Threshold_60:
  - Transformaciones readiness <60%: 70% failure rate (Prosci research)
  - Transformaciones readiness >75%: 80% success rate
  - Zone 60-75: Depends on addressing gaps effectively

Ejemplo_Borderline (Score 68):
  R1: 75 (momentum moderado)
  R2: 55 (capabilities gap crítico)
  R3: 70 (forces balanceadas)
  R4: 80 (drivers fuertes)
  R5: 60 (catalysts débiles)
  
  Decisión: GO CONDITIONAL
  Plan:
    1. Hire 3 engineers con skills necesarias (mejora R2: 55 → 75)
    2. Pilot 1 team para generar quick win (mejora R5: 60 → 80)
    3. Re-assess en 3 meses (esperado score: 75+)
```

---

### §3.1. SCHEDULES AS FORECASTS, NOT COMMITMENTS

#### Principio Fundamental

```yaml
Error_Común: Confundir estimación con compromiso
             "Estimamos 6 semanas" → Se convierte en "Prometemos 6 semanas"

Realidad:
  Estimate = Forecast (predicción probabilística)
  Commitment = Promise (garantía contractual)
  
  Estimate ≠ Commitment

Problema:
  Desarrollo software tiene incertidumbre inherente
  - Unknowns técnicos emergen durante implementación
  - Requerimientos cambian ~2% por mes
  - Dependencies externas fallan
  - Estimaciones humanas consistentemente optimistas (Planning Fallacy)
```

---

#### Planning Fallacy

```yaml
Concepto: Humanos sistemáticamente subestiman tiempo/esfuerzo requerido

Evidencia_Empírica:
  - Estudios: Tareas toman en promedio 2-3x tiempo estimado
  - Overconfidence: 90% personas creen sus estimaciones son "realistas"
  - Bias optimista: Ignoran evidencia histórica propia

Causa:
  - Best-case thinking: Estimamos asumiendo todo sale bien
  - Anclas mentales: Primera estimación "ancla" subsecuentes
  - Wishful thinking: Queremos creer que seremos más rápidos

Ejemplo:
  Engineer estima: "5 días"
  Asume: No bugs, no blockers, no interrupciones
  Realidad: 12 días (bugs + code review delays + production issue interrupt)
  
  → Estimación 2.4x optimista (típico)
```

---

#### Parkinson's Law & Student Syndrome

```yaml
Parkinson's_Law:
  "Work expands to fill the time available for its completion"
  
  Efecto:
    - Si das 10 días para tarea de 3 días → Tomará 10 días
    - Perfeccionismo, gold-plating, procrastinación llenan tiempo
    - Deadline fijo NO garantiza entrega temprana

Student_Syndrome:
  "Procrastination until the last possible moment before deadline"
  
  Efecto:
    - Team no empieza hasta días antes de deadline
    - Trabajo se comprime al final (stress, lower quality)
    - Si surge imprevisto → Retraso inevitable

Resultado_Perverso:
  Deadlines generosos → NO aceleran entrega
  Deadlines agresivos → Causan shortcuts, tech debt, burnout
  
  Solución: Iteraciones cortas con feedback frecuente (no deadlines largos)
```

---

#### Forecasts Probabilísticos

```yaml
Enfoque_KERNEL: Forecasts con rangos, no puntos

Malo (determinista):
  "Feature estará lista el 15 de marzo"

Bueno (probabilístico):
  "Feature tiene:
    - 50% probabilidad antes del 10 marzo
    - 80% probabilidad antes del 20 marzo
    - 95% probabilidad antes del 31 marzo"

Cómo_Generar_Probabilístico:
  1. Usar datos históricos team (velocity, cycle time)
  2. Monte Carlo simulations (1000 iteraciones)
  3. Generar distribución probabilidades
  4. Comunicar rangos, no punto único

Ejemplo_Con_Velocity:
  Team_Velocity:
    - Sprint 1: 23 points
    - Sprint 2: 28 points
    - Sprint 3: 19 points
    - Sprint 4: 26 points
    - Sprint 5: 21 points
  
  Estadísticas:
    - Media: 23.4 points/sprint
    - Std Dev: 3.5 points
    - Min: 19, Max: 28
  
  Feature_Estimate: 45 points
  
  Forecast_Probabilístico:
    - Best case (velocity 28): 1.6 sprints (50% probabilidad)
    - Expected (velocity 23.4): 1.9 sprints (70% probabilidad)
    - Worst case (velocity 19): 2.4 sprints (95% probabilidad)
  
  Comunicación_Stakeholder:
    "Feature probablemente lista en 2 sprints (4 semanas),
     con 80% confianza en 2-3 sprints (4-6 semanas)"
```

---

#### Alternativa: Time-Boxed Delivery

```yaml
Concepto: Invertir la pregunta

Pregunta_Tradicional:
  "¿Cuándo estará feature completa?"
  → Fuerza estimación, crea commitment implícito

Pregunta_Mejor:
  "¿Qué podemos entregar en X semanas?"
  → Time-box fijo, scope variable

Ventajas:
  - Elimina uncertainty sobre timing
  - Fuerza priorización ruthless (solo más valioso)
  - Permite entregar algo útil temprano
  - Scope crece incrementalmente (no big-bang)

Ejemplo:
  Stakeholder: "¿Cuándo tendremos el nuevo checkout?"
  
  Respuesta_Mala:
    "6 semanas" (commitment implícito, probablemente se rompe)
  
  Respuesta_Buena:
    "En 2 semanas: Checkout básico (pago 1 tarjeta, sin promociones)
     En 4 semanas: + múltiples métodos pago
     En 6 semanas: + códigos promocionales
     En 8 semanas: + saved payment methods
     
     ¿Cuál versión necesitas para lanzar?"
  
  → Stakeholder puede elegir trade-off tiempo/features
```

---

#### Comunicación de Forecasts

```yaml
Reglas_Comunicación:

1. NUNCA_Ocultar_Incertidumbre:
   ❌ Malo: "Estará listo el 15 de marzo" (falsa certeza)
   ✅ Bueno: "Estimamos entre 10-20 marzo con 80% confianza"

2. SIEMPRE_Probabilidades_Explícitas:
   ❌ Malo: "Probablemente en 3 semanas"
   ✅ Bueno: "70% probabilidad 3 semanas, 90% probabilidad 4 semanas"

3. ACTUALIZAR_Frecuentemente:
   - Forecast es snapshot temporal
   - Actualizar semanalmente con nuevos datos
   - Si velocity cae → Comunicar impacto inmediato

4. NO_Penalizar_Forecasts_Incorrectos:
   - Si penalizas error → Teams sandbag (estimaciones conservadoras)
   - O peor: Mienten sobre progreso para "cumplir"

Ejemplo_Actualización:
  Semana 1: "Feature lista en 4 semanas (80% confianza)"
  Semana 2: "Descubrimos complejidad extra, ahora 5 semanas (80%)"
  Semana 3: "Blocker externo resuelto, 4 semanas desde hoy (80%)"
  
  → Transparencia continua, no sorpresas finales
```

---

## §4. ROADMAPS

### Capability-Based Planning

```yaml
Concepto: Roadmap organizado por capabilities, no por proyectos
         Capabilities evolucionan continuamente (no "completadas")

Estructura:
  Capability → Initiatives → Features → Tasks

Ejemplo:
  Capability: "Customer Self-Service"
    State_Actual: 40% tickets resolvibles por clientes solos
    State_Target: 80% tickets self-service
    
    Initiatives_Q4:
      - I1: Knowledge base mejorado (contribuye +15% self-service)
      - I2: Chatbot IA FAQ (contribuye +20% self-service)
      - I3: Video tutoriales (contribuye +5% self-service)
    
    Features_I2_Chatbot:
      - F1: NLP intent recognition
      - F2: Integration con knowledge base
      - F3: Handoff a humano si no resuelve
```

---

### Horizonte Temporal

```yaml
Horizonte_1 (Now - 3 meses):
  - Detalle: Features específicas, sprints planificados
  - Commitment: Alto (70% confianza entrega)
  - Ejemplo: Q4 roadmap con 15 features priorizadas

Horizonte_2 (3-12 meses):
  - Detalle: Initiatives, capabilities target
  - Commitment: Moderado (forecast, ajustable)
  - Ejemplo: 2025 roadmap con 8 capabilities a mejorar

Horizonte_3 (1-3 años):
  - Detalle: Visión estratégica, bets grandes
  - Commitment: Bajo (dirección, no promesa)
  - Ejemplo: 2025-2027 vision: "Líderes regional IA customer experience"
```

---

## §5. OPTIMIZACIÓN PORTFOLIO

### Multi-Objective Optimization

```yaml
Variables_Decision: ¿Qué initiatives priorizar?

Objetivos (competing):
  1. Maximize Valor: Suma(valor_esperado initiatives)
  2. Minimize Riesgo: Suma(probabilidad_falla × impacto)
  3. Minimize Costo: Suma(budget initiatives)
  4. Maximize Strategic_Fit: Alineación a OKRs

Constraints:
  - Budget total: $2M
  - Headcount: 50 engineers
  - Time: 12 meses
  - Max initiatives simultáneas: 5 (capacity org)
  - Min 1 initiative por OKR crítico

Método:
  - Scoring: Cada initiative puntaje 0-100 por objetivo
  - Ponderación: Valor 40%, Riesgo 25%, Costo 20%, Fit 15%
  - Optimización: Knapsack problem (programación lineal)
```

---

### Ejemplo Optimización

```yaml
Initiatives_Candidatas (10):
  I1_ML_Churn_Prediction:
    Valor: 90 ($800K/año ahorro)
    Riesgo: 60 (tech nueva, incertidumbre alta)
    Costo: 70 ($300K)
    Fit: 100 (alineado OKR1 "Reducir churn")
    Score: 0.4*90 + 0.25*60 + 0.2*70 + 0.15*100 = 36+15+14+15 = 80

  I2_UI_Redesign:
    Valor: 70 ($400K/año via retention)
    Riesgo: 85 (bajo riesgo, design conocido)
    Costo: 50 ($150K)
    Fit: 80 (alineado OKR2 "Mejorar NPS")
    Score: 0.4*70 + 0.25*85 + 0.2*50 + 0.15*80 = 28+21.25+10+12 = 71.25

  ...

Portfolio_Óptimo (respetando constraints):
  - I1_ML_Churn (Score 80, Budget $300K, 6 meses, 8 eng)
  - I2_UI_Redesign (Score 71, Budget $150K, 4 meses, 6 eng)
  - I5_API_Platform (Score 68, Budget $400K, 10 meses, 12 eng)
  - I7_Security_Hardening (Score 65, Budget $200K, 5 meses, 5 eng)
  
  Total: Budget $1.05M (dentro de $2M), 12 meses, 31 eng peak (dentro 50)
  Valor agregado esperado: $2.1M/año
  ROI: $2.1M / $1.05M = 200% año 1
```

---

## §6. D_SCORE (0-100)

### Fórmula Decisión

```yaml
D_Score: Métrica agregada calidad decisional organizacional

Fórmula:
  D_Score = (
    0.40 * OKRs_Quality +
    0.30 * Forecasting_Hygiene +
    0.20 * Roadmap_Clarity +
    0.10 * Readiness_Assessment
  )

Componentes:

  OKRs_Quality (0-100):
    - Outcome-focused (not output disguised): 25%
    - Transparent (todos ven OKRs): 25%
    - Aligned (team → company): 25%
    - Time-boxed claro: 15%
    - Actualizado trimestral: 10%
    Cálculo: avg(completion rate 60-80% sweet spot, anti-patrones avoided)
  
  Forecasting_Hygiene (0-100):
    - Probabilístico (ranges not points): 30%
    - Actualizado semanalmente: 25%
    - Accuracy histórica >70%: 25%
    - No penalización forecasts incorrectos: 20%
  
  Roadmap_Clarity (0-100):
    - Horizonte 1 (0-3m) detallado: 40%
    - Horizonte 2 (3-12m) visible: 35%
    - Linked OKRs → Features: 25%
  
  Readiness_Assessment (0-100):
    - R1-R5 evaluado pre-transformación: 50%
    - Go/No-Go decisions data-driven: 50%

Interpretación:
  >75: Decisión excelente (predictable, aligned, data-driven)
  60-75: Decisión funcional (gaps menores)
  <60: Decisión débil (ad-hoc, reactive)

Típico post-MVD: 65-75
```

---

## §7. COALICIONES

### Building Coalitions (Kotter)

```yaml
Concepto: Cambios mayores requieren coalición suficientemente poderosa
         No basta sponsor solo, necesitas masa crítica supporters

Tamaño_Coalición_Mínimo:
  - Org <50: 3-5 personas clave (incluye 1 C-level)
  - Org 50-200: 8-12 personas (incluye 2-3 executives)
  - Org 200-1000: 15-25 personas (incluye functional heads)

Composición:
  - Power (autoridad formal): CTO, VPs
  - Expertise (conocimiento técnico): Architects, Staff Engineers
  - Credibility (respeto peers): Tech leads respetados
  - Leadership (habilidad influir): Change agents naturales

Actividades_Coalición:
  - Weekly sync (mantener alignment)
  - Messaging consistency (todos cuentan misma historia)
  - Address resistance proactivamente
  - Celebrate quick wins públicamente
```

---

## §8. RESISTENCIA COMO SEÑAL

### Interpretar Resistance

```yaml
Principio: Resistencia NO es "malas personas", es INFORMACIÓN

Tipos_Resistencia:

1. Resistencia_Cognitiva:
   - Causa: No entienden por qué cambio es necesario
   - Síntoma: "¿Por qué cambiamos si funciona actual?"
   - Fix: Comunicar pain actual, datos, urgencia (R1 Momentum)

2. Resistencia_Emocional:
   - Causa: Miedo pérdida (status, expertise, job)
   - Síntoma: "Esto no va a funcionar" (sin razón técnica)
   - Fix: Address fears directamente, 1:1s, safety nets

3. Resistencia_Política:
   - Causa: Cambio reduce su poder/influencia
   - Síntoma: Bloqueo activo, sabotaje sutil
   - Fix: Negotiate win-win, incluir en coalición, o override si necesario

4. Resistencia_Legítima:
   - Causa: Concerns técnicos válidos
   - Síntoma: Argumentos razonados con data
   - Fix: ESCUCHAR, ajustar plan, puede mejorar outcome
```

---

## §9. AGENTES DECISIONALES IA

### Modos Delegación

```yaml
M2_Recomendador_Portfolio:
  Función: Optimiza portfolio multi-objetivo
  Input: 20 initiatives candidatas, constraints (budget, time, headcount)
  Output: "Recomiendo I1, I3, I7, I9 (score agregado 78/100)"
  Humano: Revisa, ajusta ponderaciones, decide final
  Modo: M2 (Informar)

M3_Simulador_Escenarios:
  Función: "What-if" análisis bajo demanda
  Input: "¿Qué pasa si duplicamos budget I1?"
  Output: "Valor esperado sube $400K, pero ROI baja de 200% a 150%"
  Humano: Solicita múltiples escenarios, elige mejor
  Modo: M3 (Habilitar)

M4_Auto_Prioritizer_Backlog:
  Función: Rankea backlog según reglas definidas
  Input: 200 features en backlog, reglas (valor, urgencia, esfuerzo)
  Output: Top 20 priorizadas automáticamente
  Humano: Revisa solo top 20, ajusta si excepciones
  Modo: M4 (Controlar)

M5_Collaborative_Planning:
  Función: Co-crea roadmap con humano
  Input_Humano: "Necesito mejorar NPS +15 pts en Q4"
  Output_IA: "Sugiero 3 initiatives: UI redesign, Chatbot, Onboarding. ¿Cuál priorizas?"
  Input_Humano: "UI redesign"
  Output_IA: "OK, aquí 8 features para UI redesign, ¿cuáles incluimos?"
  → Iteración colaborativa
  Modo: M5 (Coproducir)
```

---

## §10. MODOS DECISIONALES POR COMPLEJIDAD COGNITIVA

### Espectro Complejidad

```yaml
Concepto:
  Decisiones NO son monolíticas
  Varían en complejidad cognitiva desde loops automáticos hasta problem-solving iterativo
  Cada modo requiere awareness level distinto y delegation approach distinto

Conexión_Ciclo_SDA:
  Decide phase (CORE/02 §3) opera en 4 modos de creciente complejidad:
    Mode 1 = D1 DIRECTA → Automático (skill-based)
    Mode 2 = D2 REGLAS → Condicional (rule matching)
    Mode 3 = D3 ASOCIATIVA → Pattern fuzzy (expertise heuristic)
    Mode 4 = D4 ANALÍTICA → Iterativo (investigation + simulation)

Nomenclatura:
  Este documento usa "Mode 1-4" (perspectiva dominio específico)
  02_Ciclo_Fundamental.md usa "D1-D4" (perspectiva framework general)
  Ambas notaciones son equivalentes y se usan intercambiablemente
```

---

### Mode 1: Direct Feedback Loops = D1

```yaml
Referencia: D1 DIRECTA en CORE/02_Ciclo_Fundamental.md §3

Definición: Sensor → Action sin decisión consciente (closed loop automático)

Características:
  - Latencia: <1 segundo
  - Awareness: Level 1 Detect (D2 §5)
  - Complejidad: Mínima (no interpretation)
  - Reversibilidad: Alta (cambios small, frecuentes)

Ejemplos:
  Infrastructure:
    - Thermostat: temp > 25°C → cooling ON
    - Autoscaling: CPU > 80% → add instance
    - Circuit breaker: error rate > 10% → open circuit
    - Load balancer: response time > 500ms → route to other server
  
  Process:
    - Inventory: stock < 100 units → trigger reorder
    - Queue: messages > 1000 → scale workers
    - Deployment: health check fail → rollback

Delegación_Típica: M6 Execute (fully autonomous, bounded)
Risk_Profile: Bajo (changes small, reversible, well-bounded)

Design_Principle:
  IF problema bien_definido AND feedback loop simple AND impact bounded:
    → Automate completamente (M6)
  
  Ejemplo_Decisión:
    "¿Automate thermostat?" → SÍ
    Bounded: Solo afecta temperatura
    Reversible: Apagar/encender cooling inmediato
    Low-impact: Comfort issue, no safety/financial risk
```

---

### Mode 2: Rule-Based Decisions = D2

```yaml
Referencia: D2 BASADA EN REGLAS en CORE/02_Ciclo_Fundamental.md §3

Definición: Condition reconocida → Rule aplicada → Action ejecutada

Características:
  - Latencia: Seconds to minutes
  - Awareness: Level 2 Comprehend (D2 §5)
  - Complejidad: Media (requires interpretation)
  - Reversibilidad: Media (depends on action type)

Ejemplos:
  Business_Rules:
    - Fraud detection: transaction pattern X → block transaction
    - Pricing: competitor price -10% → match price
    - Triage: H_Score < 45 → activate P52 Crisis Governance
    - Approval: purchase > $10K → requires VP approval
  
  Operational_Rules:
    - Incident severity: SEV1 → page on-call immediately
    - Deploy window: production change → only 2am-5am
    - Resource allocation: priority "high" → allocate premium resources

Delegación_Típica: M5 Co-produce (automated con human oversight)
Risk_Profile: Medio (depends on rule quality, edge cases)

Design_Principle:
  IF rules exhaustivas AND comprehension confiable AND impact medium:
    → Automate con human-on-loop (M5)
  
  Ejemplo_Decisión:
    "¿Automate fraud detection blocking?" → SÍ con oversight
    Rules: Bien definidas (pattern library extensive)
    Comprehension: ML model >95% accuracy
    Impact: Medio (block legit user frustration, pero protege fraud)
    Oversight: Daily review false positives, adjust rules

Anti-Pattern:
  AP_Incomplete_Rules:
    - Rule set no exhaustivo → edge cases sin handler
    - Fix: Start M4 (human validates), evolve to M5 cuando rules mature
```

---

### Mode 3: Associative Mapping (Expertise-Based) = D3

```yaml
Referencia: D3 ASOCIATIVA en CORE/02_Ciclo_Fundamental.md §3

Definición: Pattern fuzzy → Heuristic → Action (basado en experience/training)

Características:
  - Latencia: Minutes to hours
  - Awareness: Level 3 Project (D2 §5)
  - Complejidad: Alta (fuzzy matching, no explicit rules)
  - Reversibilidad: Baja (decisions significant)

Ejemplos:
  Machine_Learning:
    - Churn prediction: customer behavior pattern → churn probability → retention offer
    - Recommendation: user history + collaborative filtering → personalized suggestions
    - Diagnosis: symptom patterns → likely root causes → investigation path
    - Hiring: resume + interview patterns → hire/no-hire recommendation
  
  Human_Expertise:
    - Doctor diagnosis: symptom constellation → disease hypothesis
    - Architect design: requirements fuzzy → architectural pattern
    - Crisis response: situation pattern → playbook selection

Delegación_Típica: M4 Control (AI suggests, human validates)
Risk_Profile: Medio-Alto (explainability gap, trust dependency)

Design_Principle:
  IF uncertainty alta OR impact alto OR explainability requerida:
    → Human-in-loop with AI augmentation (M3-M4)
  
  Ejemplo_Decisión:
    "¿Automate churn prediction offers?" → NO fully, M4 instead
    Pattern: ML detects churn risk 75% accuracy
    Explainability: Model black-box, can't articulate "why"
    Impact: Alto ($500K ARR account at risk)
    Approach: AI flags risk, human analyst validates + customizes offer

Transparency_Requirement:
  - Explicar qué pattern matched (feature importance)
  - Confidence score (75% probability churn)
  - Alternative hypotheses (other possible reasons)
  - Human can override (expert intuition trumps model)
```

---

### Mode 4: Knowledge-Based Reasoning = D4

```yaml
Referencia: D4 ANALÍTICA en CORE/02_Ciclo_Fundamental.md §3

Definición: Investigation → Simulation → Planning → Decision (iterative problem-solving)

Características:
  - Latencia: Hours to days/weeks
  - Awareness: Level 3 Project + causal analysis
  - Complejidad: Máxima (uncertain, high-stakes, novel)
  - Reversibilidad: Muy baja (strategic commitments)

Ejemplos:
  Strategic:
    - Market entry: analyze market → simulate scenarios → decide strategy
    - Crisis response: diagnose root causes → option generation → mitigation plan
    - Architecture: requirements analysis → design alternatives → ADR
    - M&A: due diligence → valuation models → acquisition decision
  
  Operational_Complex:
    - Incident postmortem: timeline reconstruction → causal analysis → prevention plan
    - Capacity planning: forecast growth → model infrastructure → investment roadmap
    - Organizational design: diagnose dysfunction → simulate structures → reorg plan

Delegación_Típica: M2-M3 (human-led, AI augments with data/simulation)
Risk_Profile: Alto (complex, high-impact, irreversible)

Design_Principle:
  IF problema novel OR high uncertainty OR strategic impact:
    → Human drives, AI provides tools/insights (M2-M3)
  
  Ejemplo_Decisión:
    "¿Should we pivot to new market segment?" → Human-led decision
    Investigation: Market research, customer interviews (weeks)
    Simulation: Financial models, growth scenarios (AI-assisted)
    Planning: Go-to-market strategy, resource allocation
    Decision: CEO + board decide (M2, AI informs pero no decide)

AI_Role:
  - Provide data analysis at scale (market sizing, competitor analysis)
  - Simulate scenarios (Monte Carlo financial projections)
  - Generate options (constraint-based planning tools)
  - NOT decide (human expertise + judgment required)
```

---

### Decision Mode Selection Framework

```yaml
Decision_Tree:
  
  IF problema SIMPLE AND rules EXHAUSTIVE AND impact LOW:
    → Mode 1-2 (automate, M5-M6)
    Ejemplo: Autoscaling, fraud simple rules
  
  ELSE IF problema KNOWN AND pattern RECOGNIZED AND trust HIGH:
    → Mode 3 (AI suggests, human validates, M4)
    Ejemplo: Churn prediction, recommendation systems
  
  ELSE IF problema COMPLEX OR uncertainty HIGH OR impact STRATEGIC:
    → Mode 4 (human-led, AI augments, M2-M3)
    Ejemplo: Crisis response, strategic planning, M&A
  
  ELSE:
    → Start Mode 4, learn, potentially evolve to Mode 3 over time

Evolution_Path:
  Mode 4 (human solves repeatedly)
    → Codify heuristics
  Mode 3 (AI learns patterns from human decisions)
    → Validate AI suggestions
  Mode 2 (Convert validated patterns to explicit rules)
    → Automate with oversight
  Mode 1 (Full automation for bounded sub-decisions)
```

---

### Conexión con Awareness Levels & Delegación

```yaml
Cross-Reference_Matrix:
  
  Awareness_Level → Decision_Mode → Delegation_Mode:
    
    L1_Detect → M1_Direct_Feedback → M6_Execute:
      Ejemplo: Sensor → Actuator (thermostat)
    
    L2_Comprehend → M2_Rule_Based → M5_Co_produce:
      Ejemplo: Alerting → Rule → Action (fraud block)
    
    L3_Project → M3_Associative → M4_Control:
      Ejemplo: Forecast → ML model → Human validates
    
    L3_Project → M4_Knowledge_Based → M2-M3_Enable:
      Ejemplo: Simulation → Human decides → AI augments

Design_Implication:
  Al diseñar decision system, especificar:
    1. Awareness level requerido (L1, L2, L3)
    2. Decision mode apropiado (M1-M4)
    3. Delegation mode resultante (M1-M6)
  
  Ejemplo_Completo:
    "Design fraud detection system"
    → Awareness: L2 Comprehend (pattern recognition)
    → Decision: M2 Rule-Based (known fraud patterns)
    → Delegation: M5 Co-produce (automate con oversight)
    → Human oversight: Daily review false positives, weekly rule tuning
```

---

## Referencias Cruzadas

- **Ciclo SDA (Decide):** `CORE/02_Ciclo_Fundamental.md` §3
- **Modos decisionales:** Este documento §6
- **Awareness levels:** `DOMINIOS/D2_Percepcion.md` §5 (conecta Project con Mode 3-4)
- **Observables para decisión:** `DOMINIOS/D2_Percepcion.md` (O1-O8, IN1-IN3)
- **Trazabilidad Objetivos→Valor:** `CORE/06_Trazabilidad.md` §3,§12
- **Delegación IA decisional:** `CORE/04_Delegacion.md` (M2-M5)
- **Implementación roadmap:** `APLICACION/A4_Implementacion.md`
