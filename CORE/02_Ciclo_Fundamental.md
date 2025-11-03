# 02_Ciclo_Fundamental

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Todos

---

## Invariante

**Toda acción organizacional atraviesa el ciclo Sense-Decide-Act, y toda unidad de trabajo evoluciona mediante el ciclo Operation-Initiation-Development-Implementation.**

---

## §1. CICLO SDA: SENSE-DECIDE-ACT

### Definición

El **ciclo SDA** es el patrón universal de acción inteligente que conecta percepción con decisión y ejecución.

```
   ┌──────────┐
   │  SENSE   │  Detectar estado del mundo
   └────┬─────┘
        │
   ┌────▼─────┐
   │  DECIDE  │  Elegir curso de acción
   └────┬─────┘
        │
   ┌────▼─────┐
   │   ACT    │  Ejecutar transformación
   └────┬─────┘
        │
        └──────► Nuevo estado → SENSE (loop)
```

### Universalidad

Este ciclo opera en:

- **Microsegundos:** Algoritmo control automático
- **Segundos:** Decisión humana táctica
- **Días:** Sprint planning
- **Meses:** Roadmap estratégico
- **Años:** Pivote organizacional

---

## §2. FASE 1: SENSE (Percepción)

### Definición

**Sense** es el proceso de capturar, comprender y proyectar el estado del mundo para informar decisiones.

### 3 Niveles de Percepción

#### S1. DETECTAR (Detection)

```yaml
Nivel: Detección
Función: Capturar señales raw del entorno
Actores_típicos: Sensores, instrumentación, observación directa
Output: Datos sin procesar

Ejemplos:
  - Sensor IoT: Temperatura = 78°C
  - Log aplicación: HTTP 500 error
  - Feedback cliente: NPS score = 3/10
  - Métrica: Cycle time = 8.3 días
```

**Capacidad IA:** Extremadamente alta - sensores algorítmicos operan 24/7 con volumen masivo.

---

#### S2. COMPRENDER (Comprehension)

```yaml
Nivel: Comprensión
Función: Extraer patrones, contexto y significado
Actores_típicos: Analistas (humanos/IA), dashboards, analytics
Output: Insights contextuales

Ejemplos:
  - Pattern: Temperatura >75°C correlaciona con fallas subsecuentes
  - Anomalía: 500 errors incrementaron 300% última hora
  - Sentimiento: NPS bajo concentrado en feature X
  - Bottleneck: 60% cycle time en etapa "Code Review"
```

**Capacidad IA:** Alta - pattern recognition, clustering, correlation excelentes. Causalidad profunda emergente.

---

#### S3. PROYECTAR (Projection)

```yaml
Nivel: Proyección
Función: Forecast evolución futura, escenarios, tendencias
Actores_típicos: Forecasting (ML), simulaciones, juicio experto
Output: Predicciones con incertidumbre

Ejemplos:
  - Forecast: Temperatura alcanzará 85°C en 12 horas (70% confianza)
  - Predicción: Si trend continúa, downtime en 2 días
  - Escenario: Si no mejoramos NPS, churn +15% Q4
  - Proyección: Con WIP actual, delivery retrasará 3 sprints
```

**Capacidad IA:** Emergente - forecasting cuantitativo excelente, escenarios cualitativos requieren contexto humano.

---

### Profundización en Dominios

Los 3 niveles de percepción (S1-S3) se detallan operacionalmente en **`DOMINIOS/D2_Percepcion.md` §5 (Niveles Awareness Cognitiva)** con:

- Conexión a delegación M1-M6
- Design principles por nivel
- Ejemplos KERNEL específicos (observables, crisis, triage)

---

### Observables KERNEL

**11 observables críticos** (ver `DOMINIOS/D2_Percepcion.md` para detalle):

**Externos (8):**

- O1: Demanda (clientes, mercado)
- O2: Valor entregado (outcomes)
- O3: Capacidad organizacional (recursos, skills)
- O4: Eventos disruptivos (crisis, oportunidades)
- O5: Restricciones (regulación, compliance)
- O6: Competencia (alternativas, benchmarks)
- O7: Dependencias (proveedores, partners)
- O8: Calidad información (data quality)

**Internos (3):**

- I1: Velocidad decisional (time-to-decision)
- I2: Salud talento (engagement, retention)
- I3: Eficiencia flujo (cycle time, throughput)

---

## §3. FASE 2: DECIDE (Decisión)

### Definición

**Decide** es el proceso de elegir curso de acción óptimo dado estado percibido y objetivos.

### 4 Modos de Decisión

#### D1. DIRECTA (Direct Control)

```yaml
Modo: Control Directo
Características: Feedback loop automático, sin deliberación
Latencia: Microsegundos-milisegundos
Actores_típicos: Algoritmos control, reflejos humanos
Incertidumbre: Muy baja

Ejemplos:
  - Termostato: Si T<20°C → encender calefacción
  - Auto-scaling: Si CPU>80% → +2 instancias
  - Circuit breaker: Si error_rate>10% → open circuit
  - Trading: Si precio<threshold → ejecutar compra
```

**Delegación IA:** Modo M6 (Ejecutar) - totalmente automatizable.

---

#### D2. BASADA EN REGLAS (Rule-based)

```yaml
Modo: If-Then explícito
Características: Condiciones conocidas, ramas predefinidas
Latencia: Segundos-minutos
Actores_típicos: Business rules engines, humanos con checklists
Incertidumbre: Baja

Ejemplos:
  - Aprobación factura: Si monto<$10K THEN aprobar_auto ELSE escalate
  - Triage bugs: Si severity=critical THEN P0 ELSE If severity=high THEN P1
  - Compliance: Si region=EU AND dato=personal THEN aplicar_GDPR
  - Code review: Si coverage<80% THEN rechazar PR
```

**Delegación IA:** Modo M4 (Controlar) - RPA + business rules engines.

---

#### D3. ASOCIATIVA (Associative/Heuristic)

```yaml
Modo: Pattern matching basado en experiencia
Características: Reconocimiento situaciones previas, heurísticas
Latencia: Minutos-horas
Actores_típicos: Expertos humanos, ML clasificadores
Incertidumbre: Media

Ejemplos:
  - Diagnóstico: "He visto esto antes, probablemente es X"
  - Estimación: "Similar stories tomaron ~5 días, este tomará ~6"
  - Hiring: "Perfil parece fit cultural basado en entrevistas previas"
  - Code review: "Este patrón generalmente causa bugs, rechazar"
```

**Delegación IA:** Modo M2-M3 (Informar/Habilitar) - ML provee recomendaciones, humano decide.

---

#### D4. ANALÍTICA (Knowledge-based/Analytic)

```yaml
Modo: Razonamiento explícito, trade-offs, simulación
Características: First-principles thinking, optimización multi-objetivo
Latencia: Horas-días
Actores_típicos: Equipos estratégicos, simulaciones, optimizadores
Incertidumbre: Alta (múltiples futuros posibles)

Ejemplos:
  - Portfolio priorización: Optimizar valor/riesgo/costo con constraints
  - Arquitectura: Elegir entre monolito/microservicios considerando 8 factors
  - M&A: Evaluar adquisición con DCF, sinergias, riesgos integración
  - Transformación: Diseñar roadmap 3 años con 15 OKRs interdependientes
```

**Delegación IA:** Modo M3 (Habilitar) - IA genera escenarios/optimizaciones, humano sintetiza y decide.

---

### Escalada entre Modos

```
D1 (Directa) → Si excepción → D2 (Reglas)
D2 (Reglas) → Si caso no cubierto → D3 (Asociativa)
D3 (Asociativa) → Si novedad alta → D4 (Analítica)
D4 (Analítica) → Si urgencia → D3 (Heurística temporal)
```

**Principio:** Usa el modo más simple suficiente (Parsimonia P7).

---

### Profundización en Dominios

Los 4 modos decisionales (D1-D4) se detallan operacionalmente en **`DOMINIOS/D3_Decision.md` §6 (Modos Decisionales por Complejidad)** con:

- Selection framework (cuándo usar cada modo)
- Evolution path (M4 → M3 → M2 → M1 codificación progresiva)
- Conexión awareness levels y execution levels
- Antipatrones decisionales

---

## §4. FASE 3: ACT (Ejecución)

### Definición

**Act** es el proceso de materializar la decisión en cambio observable del mundo.

### 3 Subfases de Ejecución

#### A1. PLANIFICAR (Action Planning)

```yaml
Subfase: Planificación
Función: Descomponer decisión en pasos ejecutables
Output: Plan de acción con recursos, secuencia, contingencias

Ejemplos:
  - Deploy aplicación: 12 pasos (backup DB, deploy canary, monitor, rollout)
  - Hiring: 8 pasos (post job, screen resumes, interviews, offer)
  - Feature development: Sprint backlog con 15 stories
  - Incident response: Runbook con 6 etapas
```

---

#### A2. ESPECIFICAR (Action Specification)

```yaml
Subfase: Especificación
Función: Definir parámetros precisos, timing, coordinación
Output: Instrucciones ejecutables, APIs calls, comandos

Ejemplos:
  - Deploy: kubectl apply -f deployment.yaml --namespace=prod
  - Email: To=[candidates], Subject="...", Body="...", Send_at=10:00
  - DB query: SELECT * FROM users WHERE created_at > '2024-01-01'
  - API call: POST /api/v1/orders {payload} with headers {auth}
```

---

#### A3. EJECUTAR (Execution)

```yaml
Subfase: Ejecución
Función: Materializar transformación física/digital
Output: Estado del mundo cambiado, eventos generados

Ejemplos:
  - Deploy: Pods corriendo en producción, traffic routeado
  - Email: Mensaje en inbox candidatos
  - DB: Registros retornados
  - API: Orden creada, confirmación retornada
```

**Capacidad IA:** Alta para acciones digitales (APIs, deploys), limitada para físicas (requiere robotics).

---

### Profundización en Dominios

Los 3 niveles de ejecución (A1-A3) se detallan operacionalmente en **`DOMINIOS/D4_Operacion.md` §12 (Niveles Execution Cognitiva)** con:

- Separación concerns (orchestration vs specification vs action)
- Bounded autonomy patterns
- Conexión con P52 Crisis Governance, CI/CD, Incident Response
- Antipatrón monolithic execution

**Nota:** D4 usa orden inverso (Level 1=A3, Level 2=A2, Level 3=A1) por perspectiva bottom-up.

---

### Monitoreo de Ejecución

```yaml
Durante A3 (Ejecutar):
  - Sense: Observar progreso real vs planificado
  - Decide: Si desviación → ajustar, retry, rollback, o escalate
  - Act: Aplicar corrección

→ Ciclo SDA opera dentro de cada fase del ciclo mayor
```

**Recursividad:** SDA opera a múltiples niveles anidados.

---

## §5. CICLO WSLC: WORK SYSTEM LIFE CYCLE

### Definición

El **ciclo WSLC** describe cómo unidades de trabajo evolucionan desde operación estable hasta cambios planificados/no-planificados.

```
   ┌─────────────────┐
   │   OPERATION &   │ ◄──┐
   │  MAINTENANCE    │    │
   └────────┬────────┘    │
            │             │
     ┌──────▼───────┐     │
     │  INITIATION  │     │
     └──────┬───────┘     │
            │             │
     ┌──────▼───────┐     │
     │ DEVELOPMENT  │     │
     └──────┬───────┘     │
            │             │
     ┌──────▼────────┐    │
     │IMPLEMENTATION │────┘
     └───────────────┘
```

---

### F1. OPERATION & MAINTENANCE (O&M)

```yaml
Fase: Operación y Mantenimiento
Estado: Sistema en producción, entrega valor continuo
Duración: Mayoría del tiempo de vida (60-80%)
Actividades:
  - Run: Ejecutar flujos diarios
  - Monitor: Sense continuo (11 observables)
  - Maintain: Patches, bugfixes, tuning
  - Support: Resolver incidentes usuarios
  - Evolve: Mejoras incrementales pequeñas

Transición a Initiation:
  - Trigger planificado: Nueva capability estratégica
  - Trigger no planificado: Incident grave, tech debt crítico, oportunidad mercado
```

**Principio P4:** Activos continuos - O&M nunca termina, sistema evoluciona perpetuamente.

---

### F2. INITIATION

```yaml
Fase: Iniciación
Estado: Decisión de cambio significativo tomada
Duración: 2-8 semanas típicamente
Actividades:
  - Sense: Diagnóstico problema/oportunidad (11 observables)
  - Decide: ¿Es worth it? ROI, urgencia, preparación (R1-R5)
  - Define: Objetivos, scope, constraints, éxito
  - Prepare: Recursos (R), Coalition building (R5), governance

Output:
  - Charter proyecto/iniciativa
  - OKRs definidos
  - Budget aprobado
  - Team asignado
  - Roadmap high-level

Transición a Development:
  - Go decision (ARB, sponsor)
  - No-go → volver a O&M
```

**Preparación (R1-R5):** Ver `DOMINIOS/D3_Decision.md` §3

- R1: Momentum
- R2: Capabilities
- R3: Forces
- R4: Drivers  
- R5: Catalysts

---

### F3. DEVELOPMENT

```yaml
Fase: Desarrollo
Estado: Construcción/configuración de cambio
Duración: 6-24 semanas (proyectos grandes hasta años)
Actividades:
  - Design: Arquitectura, procesos, datos, interfaces
  - Build: Código, configuración, integración
  - Test: Unitario, integración, UAT, performance
  - Document: Runbooks, training, arquitectura
  - Iterate: Sprints, demos, feedback loops

Prácticas:
  - Equipos estables (DOMINIOS/D4_Operacion §1)
  - Iteraciones 1-4 semanas
  - CI/CD pipeline
  - DoD (Definition of Done)
  - 70/30 planned/unplanned work

Transición a Implementation:
  - Todos tests passed
  - DoD satisfecho
  - Stakeholders sign-off
  - Deployment plan listo
```

---

### F4. IMPLEMENTATION

```yaml
Fase: Implementación
Estado: Despliegue a producción
Duración: 1-4 semanas
Actividades:
  - Deploy: Canary → Blue/Green → Full rollout
  - Monitor: Métricas críticas, error rates, performance
  - Train: Usuarios finales, soporte, operaciones
  - Handoff: Dev team → Ops team (si separados)
  - Stabilize: Hotfixes, tuning, optimization

Estrategias despliegue:
  - Big-bang: Todo a la vez (riesgoso, evitar)
  - Phased: Por región/segmento (controlled)
  - Canary: 5% → 25% → 100% (low risk)
  - Blue-Green: Entorno paralelo, switch instantáneo
  - Feature flags: Deploy code, activate features gradual

Transición a O&M:
  - Sistema estable en prod
  - SLAs cumplidos
  - Soporte operando
  - Retrospectiva completada
  - Knowledge transferido
```

---

### Cambio No-Planificado (Workarounds)

```yaml
Tipo: Cambio No-Planificado
Origen: Incident, bug crítico, workaround temporal
Proceso:
  1. O&M detecta problema
  2. Quick fix sin pasar por Init→Dev→Impl completo
  3. Workaround deployed
  4. → Deuda técnica registrada
  5. → Eventualmente entra a ciclo formal (Init) para solución permanente

Límite: Max 30% trabajo puede ser no-planificado (DOMINIOS/D4_Operacion §5)
Si >30% → síntoma de planning deficiente o entorno muy volátil
```

---

## §6. INTEGRACIÓN SDA × WSLC

### Mapeo Conceptual

| WSLC Phase | SDA Dominante | Foco |
|------------|---------------|------|
| **O&M** | **Sense + Act** | Monitoreo continuo + operación eficiente |
| **Initiation** | **Sense + Decide** | Diagnóstico profundo + decisión go/no-go |
| **Development** | **Decide + Act** | Diseño decisiones + construcción |
| **Implementation** | **Act + Sense** | Deploy + monitoreo estabilización |

### SDA opera DENTRO de cada fase WSLC

```
WSLC.Initiation:
  ├─ Sense: Diagnosticar estado actual (11 observables)
  ├─ Decide: ¿Proceder? ROI, urgencia, preparación
  └─ Act: Crear charter, asignar recursos

WSLC.Development:
  ├─ Sense: Feedback usuarios, tests, código review
  ├─ Decide: Priorización backlog, arquitectura, trade-offs
  └─ Act: Codificar, integrar, desplegar staging

WSLC.Implementation:
  ├─ Sense: Monitoreo métricas prod, error rates
  ├─ Decide: Rollout velocity, rollback?, hotfixes?
  └─ Act: Deploy incremental, aplicar fixes

WSLC.O&M:
  ├─ Sense: Dashboards 24/7, alertas, drift detection
  ├─ Decide: Patches prioritization, capacity planning
  └─ Act: Deploy patches, scale resources, incident response
```

---

## §7. VELOCIDAD DEL CICLO

### Métricas Críticas

```yaml
SDA_Cycle_Time:
  - Tactical: Segundos-minutos (decisions operacionales)
  - Operational: Horas-días (sprint planning, incident response)
  - Strategic: Semanas-meses (roadmap, portfolio)

WSLC_Cycle_Time:
  - O&M → Initiation: Días-semanas (detección problema → decisión actuar)
  - Initiation → Development: Semanas (aprobación → kick-off)
  - Development → Implementation: Semanas-meses (build time)
  - Implementation → O&M: Días-semanas (deploy → estabilización)

Total_WSLC: 3-12 meses típico para iniciativa mediana
```

### Aceleración mediante IA

| Fase | Sin IA | Con IA | Aceleración |
|------|--------|--------|-------------|
| **Sense (S1-S3)** | Días (análisis manual) | Minutos (sensores automáticos) | ~100x |
| **Decide (D1-D2)** | Horas (reuniones) | Segundos (rules engines) | ~1000x |
| **Decide (D3-D4)** | Días (análisis profundo) | Horas (simulaciones ML) | ~10x |
| **Act (A1-A3)** | Días (deploy manual) | Minutos (CI/CD + GitOps) | ~100x |

**Límite IA:** D4 (decisiones analíticas complejas) y A1 (planning novel) requieren juicio humano - aceleración menor.

---

## §8. PATRONES DE FALLA

### F1. Sense sin Decide

```yaml
Síntoma: "Analysis paralysis" - mucha data, ninguna decisión
Causa: Dashboards sin accountability decisional
Fix: Asignar owner decisión + thresholds acción automática
Ejemplo: Dashboard con 50 métricas, nadie actúa sobre ninguna
```

### F2. Decide sin Sense

```yaml
Síntoma: Decisiones "en el vacío" sin data
Causa: Culture opinion-driven, no data-driven
Fix: Mandato "no decision without observable state"
Ejemplo: Roadmap definido sin analizar competencia ni clientes
```

### F3. Act sin Decide

```yaml
Síntoma: "Firefighting" perpetuo - actuar sin estrategia
Causa: Reactivo puro, sin tiempo para decidir
Fix: Reservar 20% tiempo para trabajo planificado (D3-D4)
Ejemplo: Devs solo resuelven tickets, nunca mejoran arquitectura
```

### F4. WSLC sin O&M

```yaml
Síntoma: Proyectos "completados y olvidados", decay inmediato
Causa: Project thinking (viola P4: Flujo continuo)
Fix: Asset thinking - presupuesto OPEX para mantenimiento continuo
Ejemplo: App deployed, equipo disuelto, bugs acumulan sin fix
```

### F5. O&M sin Evolution

```yaml
Síntoma: Sistema estancado, tech debt creciente
Causa: Solo "keep lights on", no mejora continua
Fix: 20% tiempo O&M dedicado a mejoras (no solo bugfixes)
Ejemplo: Legacy system 10 años sin refactor, "nobody touches it"
```

---

## §9. VALIDACIÓN

### Completitud

```
¿Toda acción org cae en SDA? → SÍ
  - Sense: Observar estado
  - Decide: Elegir acción
  - Act: Ejecutar

¿Toda unidad trabajo evoluciona vía WSLC? → SÍ
  - Nace en Initiation
  - Se construye en Development
  - Se activa en Implementation
  - Vive en O&M (ciclos subsecuentes de cambio)
```

### Ortogonalidad

```
SDA vs WSLC:
  - SDA: Ciclo acción (micro-macro)
  - WSLC: Ciclo vida (macro únicamente)
  - No overlap: SDA opera DENTRO de WSLC
```

### Trazabilidad

```
Decisión D → rastreable a:
  - Sense: Qué estado motivó D
  - Act: Qué acciones resultaron de D
  - WSLC: En qué fase lifecycle ocurrió D
```

---

## §9. BOUNDED RECURSION SDA

### Concepto

**Observación**: §8 menciona "SDA opera a múltiples niveles anidados" pero no define límites formales.

**Problema potencial**: Recursión infinita teórica (SDA contiene SDA que contiene SDA...) genera paradojas lógicas y cognitive overload.

**Solución**: Formalizar bounded recursion con límite pragmático basado en organizational levels.

---

### Regla Bounded Recursion

```yaml
Límite_Anidación: Max 3 niveles SDA recursivos

Nivel_1_Macro (Estratégico):
  Horizonte: Meses-años
  Ciclo: Trimestral-anual
  Ejemplo:
    Sense: Market trends, competitive analysis (quarterly)
    Decide: Strategic OKRs, roadmap annual
    Act: Launch new product line (12+ meses execution)
  
  Delegación: Típicamente humano-led (M2-M3), C-level decisions
  Abstracción: Máxima (business outcomes, not implementation)

Nivel_2_Meso (Táctico):
  Horizonte: Días-semanas
  Ciclo: Weekly-monthly
  Ejemplo:
    Sense: Sprint retrospectiva, velocity tracking
    Decide: Sprint planning, backlog prioritization
    Act: Develop features (2 week sprint)
  
  Delegación: Mixto (M3-M5), team-level decisions
  Anidación: Dentro de Act(Nivel_1) - "launch product" contiene sprints
  Abstracción: Media (features, not code lines)

Nivel_3_Micro (Operacional):
  Horizonte: Segundos-horas
  Ciclo: Real-time-daily
  Ejemplo:
    Sense: CI/CD metrics, error rate monitoring
    Decide: Rollback si error >5%, continue si OK
    Act: Deploy canary, monitor, rollout
  
  Delegación: Automation (M5-M6), system-level decisions
  Anidación: Dentro de Act(Nivel_2) - "develop feature" contiene deploys
  Abstracción: Mínima (deployments, infrastructure actions)

Nivel_4_Prohibido:
  Razón: Diminishing returns cognitivos
  
  Si necesitas nivel 4 (ej: testing individual function):
    - Probablemente over-engineering organizational model
    - KERNEL modela organizational action, not code execution
    - Implementation details fuera de scope
  
  Regla: Si encuentras necesidad nivel 4, re-modelar como peer cycles
         o reconocer que es implementation detail (no org-level)
```

---

### Distinción SDA vs WSLC Anidación

```yaml
Confusión_Común:
  "¿WSLC anida dentro SDA?" o "¿SDA anida dentro WSLC?"
  
Respuesta: NEITHER - Son ciclos PEER-LEVEL

Clarificación:
  SDA: Ciclo action universal
    - Aplica a cualquier horizonte temporal
    - Recursivo (SDA contiene SDA hasta level 3)
    - Opera DENTRO de cada fase WSLC
  
  WSLC: Ciclo lifecycle de unidad de trabajo
    - O&M → Initiation → Development → Implementation
    - NO recursivo (WSLC NO contiene WSLC nested)
    - Cada fase EJECUTA múltiples SDA
  
  Relación:
    SDA ∈ WSLC_Phase (SDA operates within WSLC phases)
    WSLC ∉ SDA (WSLC no anida dentro SDA)

Ejemplo_Integración:
  WSLC.Development (fase):
    Contiene múltiples SDA instances:
      - SDA daily: Code review cycle
      - SDA weekly: Sprint planning cycle
      - SDA monthly: Architecture decision cycle
    
    PERO: Development NO contiene otro WSLC completo
          (eso sería meta-lifecycle, complexity unjustified)
```

---

### Validación Límite 3 Niveles

```yaml
Justificación_Empírica:
  
  Research_Cognitivo:
    - Working memory: 7±2 items (Miller's Law)
    - Nested comprehension: 3-4 levels máximo
    - KERNEL usa 3 (conservative within cognitive bounds)
  
  Casos_Validados:
    - 10 casos R1_Casos.md modelados
    - Todos representables con ≤3 levels SDA
    - Ningún caso real requirió nivel 4
    - Conclusión empírica: 3 levels suficiente

Counterexample_Fallacy:
  "Pero code execution tiene más levels (function → statement → instruction → bit)"
  
  Refutación:
    - Code execution NO es organizational action
    - KERNEL scope: Organizational systems (human + algorithmic actors)
    - Beyond team-level actions: Out of scope
    - Límite pragmático: Organization-level modeling stops at deployments/actions

Coverage_Test:
  ¿Organizational action fuera de 3 levels?
  
  Candidatos:
    - Individual keystrokes coding? → Implementation detail (out of scope)
    - CPU instructions? → Infrastructure detail (out of scope)
    - Neuron firing decisions? → Biological detail (definitely out of scope)
  
  Conclusión: 3 levels cubre todo org-level action
```

---

### Anti-Pattern: Over-Modeling Recursion

```yaml
Síntoma: Intentar modelar 4+ levels SDA
Causa: Confusión abstraction levels, over-engineering
Consecuencia: Modelo incomprensible, analysis paralysis

Ejemplo_Incorrecto:
  Level 1: Annual strategy
    Level 2: Quarterly OKRs
      Level 3: Sprint planning
        Level 4: Daily standup
          Level 5: Individual task commits
            Level 6: Code review approvals
              ...donde parar?

Fix: Collapse a 3 levels meaningful:
  - Level 1: Strategic (annual OKRs) ✓
  - Level 2: Tactical (sprint planning) ✓
  - Level 3: Operational (daily deploys, standups) ✓
  - Level 4-6: Collapse to level 3 o recognize fuera scope

Heurística: Si level afecta <10 personas → Probablemente too granular para KERNEL
```

---

## Referencias Cruzadas

- **11 Observables detallados:** `DOMINIOS/D2_Percepcion.md`
- **Preparación R1-R5:** `DOMINIOS/D3_Decision.md` §3
- **Operación equipos:** `DOMINIOS/D4_Operacion.md`
- **Delegación IA (M1-M6):** `CORE/04_Delegacion.md`
- **Bounded Recursion aplicado:** Este documento §9
- **Casos aplicados:** `REFERENCIA/R1_Casos.md`
