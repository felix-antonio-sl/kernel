# 04_Delegacion v2.0.0

## §0. INVARIANTE

**Todo agente algorítmico opera mediante delegación explícita de un actor humano meta-nivel.**

**Existen exactamente 6 modos de delegación ortogonales (M1-M6), desde monitoreo pasivo hasta ejecución autónoma supervisada.**

**Propiedad:** ∀ agente A, ∃ humano H: H delega responsabilidad R a A ∧ H mantiene accountability de R ∧ H puede override decisiones de A.

## §1. LOS 6 MODOS DE DELEGACIÓN

### Espectro de Autonomía

```
M1 ────────────────────────────────────────────────► M6
(Humano decide todo)              (Agente ejecuta autónomo)

├─────────┬─────────┬─────────┬─────────┬─────────┬─────────┤
│   M1    │   M2    │   M3    │   M4    │   M5    │   M6    │
│Monitor  │Informar │Habilitar│Controlar│Coproducir│Ejecutar│
└─────────┴─────────┴─────────┴─────────┴─────────┴─────────┘

Human-in-loop ←────────────────────────→ Human-out-loop
```

### Tabla Comparativa Modos

| Modo | Iniciativa | Decisión | Acción | Loop | Latencia | Uso Típico |
|------|-----------|----------|--------|------|----------|------------|
| **M1 Monitorear** | Sistema → Agente lee pasivo | 100% humano | 0% agente (solo observa) | In-loop | Variable | Exploración inicial, compliance total |
| **M2 Informar** | Agente genera insights → Humano consume | 100% humano (agente sugiere) | 0% agente (humano ejecuta) | In-loop | Min-horas | Decisiones alto impacto, estrategia |
| **M3 Habilitar** | Humano solicita → Agente provee | Humano elige cuándo/cómo | Agente ejecuta cuando invocado | In-loop | Segundos | Herramientas on-demand, copilots |
| **M4 Controlar** | Agente evalúa según reglas | Agente (dentro reglas), Humano (excepciones) | Agente automático | On-loop | ms-seg | Reglas claras, volumen alto |
| **M5 Coproducir** | Bidireccional (humano ↔ agente) | Compartida (negociación) | Mixta (ambos ejecutan) | Mixed | Min-horas | Trabajo creativo complejo, optimización |
| **M6 Ejecutar** | Agente detecta trigger y actúa | 100% agente | 100% agente | Out-loop | ms | Tareas repetitivas, latencia crítica |

## §2. M1: MONITOREAR

```yaml
Definición: Agente observa estado sin intervenir

Características:
  - Solo captura datos, humano lee e interpreta
  - No sugiere ni alerta automáticamente
  - Humano decide cuándo/cómo actuar

Ejemplos:
  Dashboard_Analytics:
    - Agente: Muestra métricas
    - Humano: Lee, interpreta, decide acciones
  
  Log_Aggregator:
    - Agente: Captura y almacena eventos
    - Humano: Busca patterns, diagnostica
  
  Sensores_IoT:
    - Agente: Reporta temperatura, presión
    - Humano: Analiza trends, decide mantenimiento

Cuándo_Usar:
  ✓ Primeras etapas adoption IA
  ✓ Datos históricos insuficientes
  ✓ Dominio novel sin patterns
  ✓ Compliance requiere oversight completo

Ventajas: Mínimo riesgo, full context humano, fácil explicación
Desventajas: No escala, latencia alta, depende expertise humano
```

## §3. M2: INFORMAR

```yaml
Definición: Agente procesa datos y provee insights/recomendaciones

Características:
  - Agente genera insights → Humano decide si actúa
  - Sugerencias explícitas pero no ejecuta

Ejemplos:
  Recomendador_Portfolio:
    - Agente: "Sugiero priorizar Feature X (ROI 23%, riesgo medio)"
    - Humano: Evalúa contexto, decide si prioriza
  
  Anomaly_Detector:
    - Agente: "Alerta: Tráfico API +300% en 10 min"
    - Humano: Investiga si ataque, spike legítimo, o bug
  
  Forecaster_Demanda:
    - Agente: "Forecast: Demanda +40% próximas 2 semanas"
    - Humano: Decide si aumenta capacity

Cuándo_Usar:
  ✓ Decisiones alto impacto (estrategia, hiring, M&A)
  ✓ Contexto cambiante rápidamente
  ✓ Humano tiene expertise que agente no captura
  ✓ Regulación requiere human-in-loop

Ventajas: Humano valida antes actuar, agente reduce carga cognitiva
Desventajas: No acelera ejecución, requiere humano disponible, riesgo alert fatigue
```

## §4. M3: HABILITAR

```yaml
Definición: Agente provee capacidades bajo demanda

Características:
  - Humano solicita explícitamente
  - Agente ejecuta herramienta cuando invocado
  - Humano revisa output antes usar

Ejemplos:
  Copilot_Code:
    - Agente: Genera código cuando humano pide autocomplete
    - Humano: Invoca, revisa, acepta/rechaza/modifica
  
  SQL_Generator:
    - Agente: Genera query desde pregunta natural
    - Humano: "¿Usuarios activos Q3?" → SQL generado → Humano revisa y ejecuta
  
  Chatbot_Support:
    - Agente: Responde FAQ cuando cliente pregunta
    - Humano: Puede override si respuesta incorrecta
  
  Simulator:
    - Agente: "Si precio +10%, ¿impacto churn?"
    - Humano: Solicita simulación, interpreta, decide

Cuándo_Usar:
  ✓ Trabajo creativo asistido (coding, writing, diseño)
  ✓ Análisis ad-hoc (exploración datos, what-if)
  ✓ Herramientas especializadas
  ✓ Humano quiere control completo timing

Ventajas: Control total humano, agente acelera tareas específicas, bajo riesgo
Desventajas: No automático, interrumpe flujo, no escala si muchas invocaciones
```

## §5. M4: CONTROLAR

```yaml
Definición: Agente ejecuta reglas y políticas automáticamente

Características:
  - Humano define reglas, agente enforcement
  - Excepciones escalate a humano
  - Human-on-the-loop (supervisa, no participa cada caso)

Ejemplos:
  Approval_Workflow:
    - Regla: "IF monto<$10K THEN aprobar_auto ELSE escalate_manager"
    - Agente: Aprueba 85% facturas automáticamente
    - Humano: Revisa solo >$10K (15%)
  
  Code_Quality_Gates:
    - Regla: "IF coverage<80% OR vulnerabilities_high THEN block_merge"
    - Agente: Rechaza PRs que no cumplen
    - Humano: Puede override con justificación
  
  Fraud_Detection:
    - Regla: "IF fraud_score>0.9 THEN block_transaction"
    - Agente: Bloquea 0.1% transacciones sospechosas
    - Humano: Revisa casos bloqueados, puede desbloquear
  
  Auto_Scaling:
    - Regla: "IF CPU>80% durante 5min THEN +2 instances"
    - Agente: Escala automáticamente
    - Humano: Monitorea dashboards, ajusta reglas

Cuándo_Usar:
  ✓ Reglas claras, bien definidas
  ✓ Volumen alto (imposible revisar cada caso)
  ✓ Latencia crítica (ms-seg response)
  ✓ Compliance enforcement (SOX, GDPR)

Ventajas: Escala horizontal infinita, consistencia perfecta, latencia mínima
Desventajas: Rigidez (edge cases problemáticos), requiere reglas bien diseñadas
```

## §6. M5: COPRODUCIR

```yaml
Definición: Colaboración mixta con iniciativa compartida

Características:
  - Humano y agente co-crean, negocian, iteran
  - Iniciativa bidireccional
  - Mixed loop (in-loop para crítico, on-loop para ejecución)

Ejemplos:
  Design_Colaborativo:
    1. Humano: Define constraints ("oficina 500m², 50 personas")
    2. Agente: Genera 10 layouts
    3. Humano: Selecciona 2 favoritos, pide variaciones
    4. Agente: Refina
    5. → Iteración hasta convergencia
  
  Planning_Roadmap:
    1. Agente: Sugiere priorización (valor/riesgo/costo)
    2. Humano: Ajusta ponderaciones ("valor > riesgo")
    3. Agente: Re-optimiza
    4. Humano: Fuerza constraints ("Feature X en Q2")
    5. Agente: Ajusta plan respetando constraint
    6. → Convergencia colaborativa
  
  Research_Paper:
    1. Humano: Escribe outline
    2. Agente: Genera draft sección 1
    3. Humano: Edita, agrega insights
    4. Agente: Sugiere referencias relevantes
    5. → Paper co-creado

Cuándo_Usar:
  ✓ Trabajo creativo complejo
  ✓ Optimización multi-objetivo con trade-offs subjetivos
  ✓ Exploración espacio soluciones amplio
  ✓ Expertise compartido (humano + IA complementarios)

Ventajas: Combina fortalezas humano (juicio) + IA (velocidad), mejora outcome vs solo
Desventajas: Latencia alta, requiere interfaces sofisticadas, difícil asignar accountability
```

## §7. M6: EJECUTAR

```yaml
Definición: Agente ejecuta actividades end-to-end autónomamente

Características:
  - Agente detecta trigger y actúa
  - Humano supervisa resultados, puede intervenir en excepciones
  - Human-out-of-the-loop (supervisión periódica)

Ejemplos:
  RPA_Invoice_Processing:
    1. Detecta factura en email
    2. Extrae datos (OCR)
    3. Valida contra PO
    4. Registra en ERP
    5. Paga automáticamente (si<$10K)
    Humano: Revisa log daily, investiga solo errores
  
  Trading_Algorithm:
    1. Monitorea mercado real-time
    2. Identifica arbitraje
    3. Ejecuta compra-venta en ms
    4. Registra trade
    Humano: Define strategy y risk limits, monitorea P&L
  
  Predictive_Maintenance:
    1. Sensores detectan vibración anormal
    2. ML predice falla en 48h (90% confianza)
    3. Crea work order automáticamente
    4. Schedules maintenance
    5. Notifica equipo
    Humano: Ejecuta mantenimiento, confirma completado
  
  Deploy_Automático:
    1. Tests passed en PR merge
    2. Build image
    3. Deploy staging
    4. Run smoke tests
    5. Deploy prod (canary 5%→100%)
    6. Rollback si error_rate>threshold
    Humano: Monitorea dashboards, puede pausar

Cuándo_Usar:
  ✓ Tareas repetitivas alto volumen
  ✓ Latencia crítica (<1 seg)
  ✓ Reglas estables, bien validadas
  ✓ Costo error bajo O rollback automático

Ventajas: Máxima velocidad y escala, 24/7 sin intervención, libera humanos
Desventajas: Riesgo alto si mal configurado, requiere monitoring robusto, automation bias
```

## §8. HUMAN-IN/ON/OUT-THE-LOOP

| Loop Type | Participación Humano | Modos | Latencia | Seguridad | Uso |
|-----------|---------------------|-------|----------|-----------|-----|
| **IN-the-loop** | En CADA decisión/acción | M1, M2, M3 | Alta (humano bottleneck) | Máxima | Alto impacto, exploración |
| **ON-the-loop** | Supervisa, interviene solo excepciones | M4 | Baja (mayoría automática) | Alta (puede override) | Reglas claras, volumen alto |
| **OUT-of-the-loop** | Monitorea resultados agregados | M6 | Mínima (fully automated) | Requiere monitoring + rollback | Tareas repetitivas, latencia crítica |

### Escalation entre Loops

```
M6 (OUT-of-loop)
   │
   ├─ Anomalía detectada → Escala a M4 (ON-loop)
   │
M4 (ON-loop)
   │
   ├─ Excepción no cubierta → Escala a M2/M3 (IN-loop)
   │
M1-M3 (IN-loop)
   │
   └─ Humano resuelve → Define nueva regla → Vuelve a M4/M6
```

## §9. DIMENSIÓN PURPOSE: ROL DEL AGENTE

**Concepto:** M1-M6 describe AUTONOMÍA (cuánto control). Purpose describe ROL (qué tipo support).

**Dimensiones ortogonales:** Autonomy (M1-M6) × Purpose (4 roles) = 24 combinaciones posibles.

### Los 4 Roles

| Role | Definición | Interface | Iniciativa | Interaction | Ejemplos |
|------|-----------|-----------|-----------|-------------|----------|
| **Assistant** | Soporte directo mediante conversación natural | Chat, voice | User-driven | Conversational, iterative | Copilot, ChatGPT, Virtual Assistant |
| **Augmentation Tool** | Funcionalidad AI-enabled que augmenta abilities | GUI, direct manipulation | User-driven | Direct, immediate feedback | Image editor, Grammar checker, Code completion |
| **Orchestration Agent** | Meta-agent que coordina otros agents | Configuration, dashboards | Hybrid | Monitoring, intervention | Self-driving supervisor, Workflow orchestrator |
| **Automation Agent** | Ejecuta end-to-end sin user interaction directa | Config upfront, alerts | System-driven | Minimal (exception-based) | Fraud detection, Autoscaling, RPA |

### Purpose × Autonomy Matrix

|               | M1 | M2 | M3 | M4 | M5 | M6 |
|---------------|----|----|----|----|----|----|
| **Assistant** | - | ✓✓ | ✓✓ | ✓ | ○ | ○ |
| **Augment** | - | ○ | ✓✓ | ✓✓ | ○ | - |
| **Orchestrate** | - | - | ○ | ✓✓ | ✓✓ | ○ |
| **Automate** | - | - | - | ○ | ✓✓ | ✓✓ |

**Leyenda:** ✓✓ = Muy común | ✓ = Común | ○ = Posible pero menos común | - = Raro/incompatible

### Expectativas por Purpose

```yaml
Assistant:
  - Transparency: Explain reasoning, sources
  - Explainability: "¿Por qué sugeriste X?"
  - Control: User puede reject, modify, iterate
  - Conversational: Natural dialogue, context awareness
  Failure: Sugerencia incorrecta → User rechaza, no harm

Augmentation:
  - Predictability: Same input → Same output
  - Immediacy: Real-time feedback
  - Undo-ability: Easy to reverse
  - Integration: Seamless in workflow
  Failure: Behavior inesperado → User undo inmediato

Orchestration:
  - Agent Network Transparency: Who does what
  - Intervention Capability: Override any agent
  - Coordination Visibility: Handoffs, dependencies
  - Bounded Autonomy: Clear limits per agent
  Failure: Breakdown coordinación → Human toma orchestration

Automation:
  - Bounded Autonomy: Clear scope, limits
  - Auditability: Log decisiones, actions
  - Override Capability: Human puede intervenir
  - Configuration: Policies, thresholds, escalations
  Failure: Acción incorrecta → Rollback + intervention
```

## §10. EVOLUCIÓN DE MODOS

### Progresión Típica

```yaml
Fase_1_Exploración (3-6 meses):
  Modos: M1, M2
  Objetivo: Entender problema, validar IA útil

Fase_2_Asistencia (6-12 meses):
  Modo: M3
  Objetivo: Herramientas on-demand, humano aprende confiar

Fase_3_Automatización_Parcial (12-24 meses):
  Modo: M4
  Objetivo: Reglas claras automatizadas, excepciones humanas

Fase_4_Colaboración (12+ meses):
  Modo: M5
  Objetivo: Co-creación problemas complejos (puede ser estado final)

Fase_5_Automatización_Completa (Variable):
  Modo: M6
  Objetivo: End-to-end autonomy (algunos procesos nunca llegan)
```

**Principio P8 (Herramienta no Oráculo):** No saltar directo a M6 sin pasar por M1-M4. Aprendizaje progresivo esencial.

## §11. ANTI-PATRONES DELEGACIÓN

| Anti-Pattern | Síntoma | Causa | Consecuencia | Fix |
|--------------|---------|-------|--------------|-----|
| **AP_D1: M6 Prematuro** | Implementar M6 sin validar M1-M4 | "Move fast" sin considerar riesgos | Fallos catastróficos, pérdida confianza | Siempre progresar M1→M2→M3→M4→M6 |
| **AP_D2: M1 Perpetuo** | Nunca evolucionar después de años | Risk-aversion extrema, falta skills | No capturar valor IA, competitors avanzan | Roadmap progresión modos |
| **AP_D3: No Escalation Path** | M6 sin mecanismo rollback a M4/M2 | Diseño asume "IA nunca falla" | Sin escape hatch cuando falla | Siempre implementar escalation |
| **AP_D4: Automation Bias** | Humanos confían ciegamente en M6 | "Computer said so" syndrome | Errores sistemáticos no detectados | Monitoring activo + auditoría periódica |
| **AP_D5: Mode Mismatch** | Usar M3 cuando necesitas M4 | No entender diferencia modos | Humano saturado con requests | Mapear volumen/latencia a modo adecuado |

## §12. MATRIZ 6 MODOS × 4 DOMINIOS

| Dominio ↓ / Modo → | M1 | M2 | M3 | M4 | M5 | M6 |
|--------------------|----|----|----|----|----|----|
| **D1 Arquitectura** | Dashboard org health | Detecta violaciones RACI | Simulador estructuras | Enforce governance rules | Co-diseño org con IA | ⚠️ No recomendado |
| **D2 Percepción** | Métricas raw dashboard | Insights narrativos | Drill-down analytics | Alertas automáticas | Investigación guiada | Data pipelines ETL |
| **D3 Decisión** | Track decision velocity | Recomendaciones portfolio | Optimizadores multi-objetivo | Auto-aprobaciones (reglas) | Planning colaborativo | Auto-priorización backlog |
| **D4 Operación** | Flow metrics real-time | Blockers predichos | Copilot code/docs | Quality gates CI/CD | Pair programming IA | Deploy automático |

## §13. DECISION TREE: ¿QUÉ MODO USAR?

```
¿Volumen alto (>100 casos/día)?
├─ NO → M1, M2, M3 (Análisis manual viable)
└─ SÍ
   │
   ¿Latencia crítica (<1 min)?
   ├─ NO → M2, M3, M4 (Humano puede revisar)
   └─ SÍ
      │
      ¿Reglas claras y estables?
      ├─ NO → M2, M3, M5 (Requiere juicio)
      └─ SÍ
         │
         ¿Costo error alto?
         ├─ SÍ → M4 con escalation (Human-on-loop)
         └─ NO → M6 con monitoring (Human-out-loop)
```

## §14. CONEXIÓN CON AWARENESS & DECISION MODES

### Full Stack Design

```yaml
Awareness_Level → Decision_Mode → Execution_Level → Purpose → Autonomy

Ejemplo_1_Simple_Automation:
  Awareness: S1 Detectar (temperature sensor)
  Decision: D1 Directa (threshold)
  Execution: A3 Ejecutar (turn on cooling)
  Purpose: Automation Agent
  Autonomy: M6 Ejecutar
  → Thermostat fully autonomous

Ejemplo_2_Intelligent_Assistant:
  Awareness: S2 Comprender (churn risk analysis)
  Decision: D3 Asociativa (ML pattern matching)
  Execution: A3 Ejecutar (send retention offer)
  Purpose: Assistant (suggests) OR Automation (executes)
  Autonomy: M2 Informar OR M5 Coproducir
  → Depends on trust level

Ejemplo_3_Orchestration:
  Awareness: S3 Proyectar (crisis forecast)
  Decision: D4 Analítica (P52 activation)
  Execution: A1 Planificar (orchestrate stabilization)
  Purpose: Orchestration Agent
  Autonomy: M3 Habilitar (human-led, IA supports)
  → Crisis governance hybrid
```

## §15. VALIDACIÓN

### Completitud

```
¿Todo tipo interacción humano-IA cae en M1-M6? → SÍ
  Evidencia: Mapeo 30+ patrones IA (A1_Patrones PA01-PA20)
```

### Ortogonalidad

```
¿Overlaps entre modos? → NO
  M1 observa | M2 informa | M3 habilita | M4 controla | M5 coprodujo | M6 ejecuta
  Cada modo tiene iniciativa y decisión únicas
```

### Suficiencia

```
¿Se necesitan más de 6 modos? → NO
  6 modos cubren espectro completo autonomía: 0% (M1) → 100% (M6)

¿Se necesitan más de 4 purposes? → NO
  4 roles cubren tipos fundamentales: Assistant, Augment, Orchestrate, Automate
```

## Referencias Cruzadas

- **Manifiesto (A8: No Oráculo):** `CORE/00_Manifiesto.md` §3
- **Primitivo Actor:** `CORE/01_Primitivos.md` §1
- **Ciclo SDA completo:** `CORE/02_Ciclo_Fundamental.md`
- **4 Dominios (D1-D4):** `CORE/03_Arquitectura.md`
- **Awareness levels (S1-S3):** `DOMINIOS/D2_Percepcion.md` §5
- **Decision modes (D1-D4):** `DOMINIOS/D3_Decision.md` §6
- **Execution levels (A1-A3):** `DOMINIOS/D4_Operacion.md` §12
- **Patrones delegación IA:** `APLICACION/A1_Patrones.md` §5 (IA)
- **Orchestration pattern:** `APLICACION/A1_Patrones.md` P53
- **Casos delegación:** `REFERENCIA/R1_Casos.md` (Hiring, Ecommerce, Auction, Vehículo)
- **Madurez IA (6 niveles):** `APLICACION/A3_Diagnostico.md` §9

**Fin 04_Delegacion v2.0.0**
