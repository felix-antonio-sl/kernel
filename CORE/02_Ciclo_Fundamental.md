# 02_Ciclo_Fundamental v2.0.0

## §0. INVARIANTE

**Toda acción organizacional atraviesa Sense-Decide-Act, y toda unidad de trabajo evoluciona mediante Operation-Initiation-Development-Implementation.**

**Propiedad:** SDA opera recursivamente (max 3 niveles). WSLC no es recursivo (ciclo único por unidad).

## §1. CICLO SDA: SENSE-DECIDE-ACT

### Definición

Patrón universal de acción inteligente que conecta percepción → decisión → ejecución.

```
┌─────────┐
│  SENSE  │  Detectar, comprender, proyectar
└────┬────┘
     │
┌────▼────┐
│ DECIDE  │  Elegir curso de acción
└────┬────┘
     │
┌────▼────┐
│   ACT   │  Ejecutar transformación
└────┬────┘
     │
     └─────► Nuevo estado → SENSE (loop)
```

### Universalidad Temporal

| Horizonte | Ejemplo | Actor Típico |
|-----------|---------|--------------|
| **Microsegundos** | Control automático (termostato, circuit breaker) | Algoritmo |
| **Segundos** | Decisión táctica humana | Humano individual |
| **Días** | Sprint planning | Team |
| **Meses** | Roadmap estratégico | Org unit |
| **Años** | Pivote organizacional | C-level |

## §2. SENSE — Percepción (3 Niveles)

### S1. DETECTAR

```yaml
Función: Capturar señales raw del entorno
Output: Datos sin procesar
Latencia: Real-time
Capacidad IA: Extremadamente alta (sensores 24/7, volumen masivo)

Ejemplos:
  - Sensor: Temperatura = 78°C
  - Log: HTTP 500 error
  - Feedback: NPS = 3/10
  - Métrica: Cycle time = 8.3 días
```

### S2. COMPRENDER

```yaml
Función: Extraer patrones, contexto, significado
Output: Insights contextuales
Latencia: Minutos-horas
Capacidad IA: Alta (pattern recognition, clustering, correlation)

Ejemplos:
  - Pattern: T>75°C correlaciona con fallas
  - Anomalía: 500 errors +300% última hora
  - Sentimiento: NPS bajo concentrado en feature X
  - Bottleneck: 60% cycle time en Code Review
```

### S3. PROYECTAR

```yaml
Función: Forecast evolución futura, escenarios
Output: Predicciones con incertidumbre
Latencia: Horas-días
Capacidad IA: Emergente (forecasting cuantitativo excelente; escenarios cualitativos requieren humano)

Ejemplos:
  - Forecast: T alcanzará 85°C en 12h (70% confianza)
  - Predicción: Si trend continúa, downtime en 2 días
  - Escenario: Si no mejoramos NPS, churn +15% Q4
  - Proyección: Con WIP actual, delivery retrasará 3 sprints
```

**Profundización:** Ver `DOMINIOS/D2_Percepcion.md` §5 (Awareness Cognitiva) para conexión con M1-M6 y design principles.

### Observables KERNEL: 11 Base (+5 Security = 16 Extended)

**Base (11 observables):**

| Externos (8) | Internos (3) |
|--------------|--------------|
| O1: Demanda | IN1: Velocidad decisional |
| O2: Valor entregado | IN2: Salud talento |
| O3: Capacidad organizacional | IN3: Eficiencia flujo |
| O4: Eventos disruptivos | |
| O5: Restricciones | |
| O6: Competencia | |
| O7: Dependencias | |
| O8: Calidad información | |

**Nota:** Ver `CORE/03_Arquitectura.md` §6 Security para **H_Score Extended** (16 observables = 11 base + SO1-SO5, peso +10%).

## §3. DECIDE — Decisión (4 Modos)

### D1. DIRECTA

```yaml
Características: Feedback automático, sin deliberación
Latencia: μs-ms
Incertidumbre: Muy baja
Delegación IA: M6 (Ejecutar) - totalmente automatizable

Ejemplos:
  - Termostato: T<20°C → encender
  - Auto-scaling: CPU>80% → +2 instancias
  - Circuit breaker: error_rate>10% → open
  - Trading: precio<threshold → compra
```

### D2. BASADA EN REGLAS

```yaml
Características: If-Then explícito, condiciones predefinidas
Latencia: segundos-minutos
Incertidumbre: Baja
Delegación IA: M4 (Controlar) - RPA + business rules

Ejemplos:
  - Aprobación: monto<$10K → auto | >$10K → escalate
  - Triage: severity=critical → P0 | high → P1
  - Compliance: region=EU AND personal_data → GDPR
  - CI/CD: coverage<80% → rechazar PR
```

### D3. ASOCIATIVA

```yaml
Características: Pattern matching basado en experiencia
Latencia: minutos-horas
Incertidumbre: Media
Delegación IA: M2-M3 (Informar/Habilitar) - ML recomienda, humano decide

Ejemplos:
  - Diagnóstico: "He visto esto, probablemente X"
  - Estimación: "Stories similares ~5 días, este ~6"
  - Hiring: "Perfil fit cultural basado en previos"
  - Code review: "Patrón causa bugs, rechazar"
```

### D4. ANALÍTICA

```yaml
Características: First-principles, trade-offs, simulación
Latencia: horas-días
Incertidumbre: Alta (múltiples futuros posibles)
Delegación IA: M3 (Habilitar) - IA genera escenarios, humano sintetiza

Ejemplos:
  - Portfolio: Optimizar valor/riesgo/costo con constraints
  - Arquitectura: Monolito vs microservicios (8 factores)
  - M&A: DCF, sinergias, riesgos integración
  - Transformación: Roadmap 3 años, 15 OKRs interdependientes
```

### Escalación Entre Modos

```
D1 (Directa) → excepción → D2 (Reglas)
D2 (Reglas) → caso no cubierto → D3 (Asociativa)
D3 (Asociativa) → novedad alta → D4 (Analítica)
D4 (Analítica) → urgencia → D3 (Heurística temporal)
```

**Principio P7 (Parsimonia):** Usa el modo más simple suficiente.

**Profundización:** Ver `DOMINIOS/D3_Decision.md` §6 (Modos Decisionales) para selection framework y antipatrones.

## §4. ACT — Ejecución (3 Subfases)

### A1. PLANIFICAR

```yaml
Función: Descomponer decisión en pasos ejecutables
Output: Plan con recursos, secuencia, contingencias

Ejemplos:
  - Deploy: 12 pasos (backup, canary, monitor, rollout)
  - Hiring: 8 pasos (post, screen, interview, offer)
  - Feature: Sprint backlog 15 stories
  - Incident: Runbook 6 etapas
```

### A2. ESPECIFICAR

```yaml
Función: Definir parámetros precisos, timing, coordinación
Output: Instrucciones ejecutables (APIs, comandos)

Ejemplos:
  - Deploy: kubectl apply -f deployment.yaml --namespace=prod
  - Email: To=[candidates], Subject="...", Send_at=10:00
  - DB: SELECT * FROM users WHERE created_at > '2024-01-01'
  - API: POST /api/v1/orders {payload} + headers {auth}
```

### A3. EJECUTAR

```yaml
Función: Materializar transformación física/digital
Output: Estado del mundo cambiado, eventos generados
Capacidad IA: Alta (acciones digitales), limitada (físicas requieren robotics)

Ejemplos:
  - Deploy: Pods en prod, traffic routeado
  - Email: Mensaje en inbox
  - DB: Registros retornados
  - API: Orden creada, confirmación enviada
```

**Profundización:** Ver `DOMINIOS/D4_Operacion.md` §12 (Execution Cognitiva) para orchestration patterns y antipatrones.

### Monitoreo Recursivo

```yaml
Durante A3 (Ejecutar):
  Sense: Observar progreso real vs planificado
  Decide: Si desviación → ajustar | retry | rollback | escalate
  Act: Aplicar corrección

→ SDA opera DENTRO de cada fase del ciclo mayor (recursividad)
```

## §5. CICLO WSLC: WORK SYSTEM LIFE CYCLE

### Definición

Ciclo evolutivo de unidades de trabajo desde operación estable hasta cambios planificados/no-planificados.

```
┌──────────────┐
│ OPERATION &  │ ◄──┐
│ MAINTENANCE  │    │
└──────┬───────┘    │
       │            │
┌──────▼────────┐   │
│  INITIATION   │   │
└──────┬────────┘   │
       │            │
┌──────▼────────┐   │
│ DEVELOPMENT   │   │
└──────┬────────┘   │
       │            │
┌──────▼─────────┐  │
│ IMPLEMENTATION │──┘
└────────────────┘
```

### F1. OPERATION & MAINTENANCE

```yaml
Estado: Sistema en producción, entrega valor continuo
Duración: 60-80% vida útil
Actividades:
  - Run: Flujos diarios
  - Monitor: 16 observables continuo
  - Maintain: Patches, bugfixes, tuning
  - Support: Resolver incidentes
  - Evolve: Mejoras incrementales

Triggers → Initiation:
  - Planificado: Nueva capability estratégica
  - No-planificado: Incident grave, tech debt crítico, oportunidad mercado
```

**Principio P4 (Flujo Continuo):** O&M nunca termina; activos evolucionan perpetuamente.

### F2. INITIATION

```yaml
Estado: Decisión cambio significativo tomada
Duración: 2-8 semanas
Actividades:
  - Sense: Diagnóstico (16 observables)
  - Decide: ROI, urgencia, preparación (R1-R5)
  - Define: Objetivos, scope, constraints, éxito
  - Prepare: Recursos, coalition building, governance

Output:
  - Charter proyecto
  - OKRs definidos
  - Budget aprobado
  - Team asignado
  - Roadmap high-level

Transición:
  - Go → Development
  - No-go → O&M
```

**Preparación R1-R5:** Momentum, Capabilities, Forces, Drivers, Catalysts. Ver `DOMINIOS/D3_Decision.md` §3.

### F3. DEVELOPMENT

```yaml
Estado: Construcción/configuración de cambio
Duración: 6-24 semanas (grandes: años)
Actividades:
  - Design: Arquitectura, procesos, interfaces
  - Build: Código, configuración, integración
  - Test: Unit, integration, UAT, performance
  - Document: Runbooks, training
  - Iterate: Sprints, demos, feedback loops

Prácticas:
  - Teams estables (D4_Operacion §1)
  - Iteraciones 1-4 semanas
  - CI/CD pipeline
  - DoD (Definition of Done)
  - 70/30 planned/unplanned work

Transición → Implementation:
  - Tests passed
  - DoD satisfecho
  - Stakeholders sign-off
  - Deployment plan listo
```

### F4. IMPLEMENTATION

```yaml
Estado: Despliegue a producción
Duración: 1-4 semanas
Actividades:
  - Deploy: Canary → Blue/Green → Full rollout
  - Monitor: Métricas críticas, error rates
  - Train: Usuarios, soporte, operaciones
  - Handoff: Dev → Ops (si separados)
  - Stabilize: Hotfixes, tuning

Estrategias:
  - Big-bang: Todo a la vez (riesgoso, evitar)
  - Phased: Por región/segmento (controlled)
  - Canary: 5% → 25% → 100% (low risk)
  - Blue-Green: Entorno paralelo, switch instantáneo
  - Feature flags: Deploy code, activate gradual

Transición → O&M:
  - Sistema estable prod
  - SLAs cumplidos
  - Soporte operando
  - Retrospectiva completada
```

### Cambio No-Planificado

```yaml
Origen: Incident, bug crítico, workaround temporal
Proceso:
  1. O&M detecta problema
  2. Quick fix (sin Init→Dev→Impl completo)
  3. Workaround deployed
  4. Deuda técnica registrada
  5. Eventualmente ciclo formal (Init) para solución permanente

Límite: Max 30% trabajo no-planificado (D4_Operacion §5)
Síntoma: >30% → planning deficiente o entorno volátil
```

## §6. INTEGRACIÓN SDA × WSLC

### Relación Conceptual

**SDA y WSLC son ciclos PEER-LEVEL:**

- **SDA:** Ciclo acción universal (aplica a cualquier horizonte)
  - Recursivo (max 3 niveles)
  - Opera DENTRO de cada fase WSLC
  
- **WSLC:** Ciclo lifecycle de unidad trabajo
  - O&M → Init → Dev → Impl
  - NO recursivo (un ciclo por unidad)
  - Cada fase ejecuta múltiples SDA

**Regla:** SDA ∈ WSLC_Phase | WSLC ∉ SDA

### Mapeo por Fase

| WSLC Phase | SDA Dominante | Foco |
|------------|---------------|------|
| **O&M** | Sense + Act | Monitoreo + operación eficiente |
| **Initiation** | Sense + Decide | Diagnóstico + decisión go/no-go |
| **Development** | Decide + Act | Diseño + construcción |
| **Implementation** | Act + Sense | Deploy + monitoreo estabilización |

### Ejemplo Anidación

```yaml
WSLC.Development:
  Contiene múltiples SDA instances:
    - SDA daily: Code review cycle
    - SDA weekly: Sprint planning cycle
    - SDA monthly: Architecture decision cycle
  
  PERO: Development NO contiene otro WSLC completo
        (meta-lifecycle innecesario, complexity unjustified)
```

## §7. RECURSIÓN ACOTADA SDA

### Límite: Max 3 Niveles

```yaml
Nivel_1_Estratégico:
  Horizonte: Meses-años
  Ciclo: Trimestral-anual
  Delegación: Humano-led (M2-M3), C-level
  Abstracción: Máxima (business outcomes)
  Ejemplo: Annual OKRs → Product line launch (12 meses)

Nivel_2_Táctico:
  Horizonte: Días-semanas
  Ciclo: Weekly-monthly
  Delegación: Mixto (M3-M5), team-level
  Abstracción: Media (features)
  Anidación: Dentro de Act(Nivel_1)
  Ejemplo: Sprint planning → Feature development (2 semanas)

Nivel_3_Operacional:
  Horizonte: Segundos-horas
  Ciclo: Real-time-daily
  Delegación: Automation (M5-M6), system-level
  Abstracción: Mínima (deployments)
  Anidación: Dentro de Act(Nivel_2)
  Ejemplo: CI/CD metrics → Canary deploy → Rollout

Nivel_4_Prohibido:
  Razón: Diminishing returns cognitivos
  KERNEL modela org-level action, no code execution
  Si necesitas nivel 4 → Re-modelar como peer cycles o
                         reconocer implementation detail (fuera scope)
```

### Justificación Límite 3

**Investigación Cognitiva:**
- Working memory: 7±2 items (Miller's Law)
- Nested comprehension: 3-4 levels máximo
- KERNEL usa 3 (conservador dentro límites cognitivos)

**Validación Empírica:**
- 10 casos `R1_Casos.md` modelados
- Todos representables con ≤3 levels
- Ninguno requirió nivel 4
- Conclusión: 3 levels suficiente

**Anti-Pattern:** Intentar 4+ levels → Over-engineering, incomprensible.

**Heurística:** Si level afecta <10 personas → Muy granular para KERNEL.

## §8. VELOCIDAD Y ACELERACIÓN

### Métricas Temporales

```yaml
SDA_Cycle_Time:
  - Tactical: Segundos-minutos (operacional)
  - Operational: Horas-días (sprint, incident)
  - Strategic: Semanas-meses (roadmap, portfolio)

WSLC_Cycle_Time:
  - O&M → Init: Días-semanas
  - Init → Dev: Semanas
  - Dev → Impl: Semanas-meses
  - Impl → O&M: Días-semanas
  - Total: 3-12 meses (iniciativa mediana)
```

### Aceleración via IA

| Fase | Sin IA | Con IA | Factor |
|------|--------|--------|--------|
| **Sense (S1-S3)** | Días | Minutos | ~100x |
| **Decide (D1-D2)** | Horas | Segundos | ~1000x |
| **Decide (D3-D4)** | Días | Horas | ~10x |
| **Act (A1-A3)** | Días | Minutos | ~100x |

**Límite:** D4 (analítica compleja) y A1 (planning novel) requieren juicio humano — aceleración menor.

## §9. PATRONES DE FALLA

| Pattern | Síntoma | Causa | Fix |
|---------|---------|-------|-----|
| **F1: Sense sin Decide** | Analysis paralysis | Dashboards sin accountability | Owner + thresholds automáticos |
| **F2: Decide sin Sense** | Decisiones en vacío | Culture opinion-driven | Mandato "no decision without data" |
| **F3: Act sin Decide** | Firefighting perpetuo | Reactivo puro | 20% tiempo trabajo planificado |
| **F4: WSLC sin O&M** | Proyectos olvidados | Project thinking (viola P4) | Asset thinking + OPEX continuo |
| **F5: O&M sin Evolution** | Tech debt creciente | Solo "keep lights on" | 20% O&M para mejoras |

## §10. VALIDACIÓN

### Completitud

```
¿Toda acción org cae en SDA? → SÍ (Sense → Decide → Act)
¿Toda unidad trabajo evoluciona vía WSLC? → SÍ (O&M → Init → Dev → Impl)
```

### Ortogonalidad

```
SDA: Ciclo acción (micro-macro, recursivo)
WSLC: Ciclo vida (macro único, no recursivo)
Sin overlap: SDA opera DENTRO de WSLC
```

### Trazabilidad

```
Decisión D rastreable a:
  - Sense: Qué estado motivó D
  - Act: Qué acciones resultaron de D
  - WSLC: En qué fase lifecycle ocurrió D
```

## Referencias Cruzadas

- **Manifiesto (I1-I3, A1-A5, P1-P9):** `CORE/00_Manifiesto.md`
- **Primitivos (7):** `CORE/01_Primitivos.md`
- **Dominios (4):** `CORE/03_Arquitectura.md`
- **Delegación (M1-M6):** `CORE/04_Delegacion.md`
- **Observables (16) + H_Score Extended:** `CORE/03_Arquitectura.md` §6 + `DOMINIOS/D2_Percepcion.md`
- **Preparación R1-R5:** `DOMINIOS/D3_Decision.md` §3
- **Awareness Levels (S1-S3):** `DOMINIOS/D2_Percepcion.md` §5
- **Decision Modes (D1-D4):** `DOMINIOS/D3_Decision.md` §6
- **Execution Levels (A1-A3):** `DOMINIOS/D4_Operacion.md` §12
- **Casos aplicados:** `REFERENCIA/R1_Casos.md`

**Fin 02_Ciclo_Fundamental v2.0.0**
