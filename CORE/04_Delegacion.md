# 04_Delegacion

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Arquitectos, Product Managers, Tech Leads

---

## Invariante

**Todo agente algorítmico opera mediante delegación explícita de un actor humano meta-nivel. Existen exactamente 6 modos de delegación ortogonales (M1-M6), desde monitoreo pasivo hasta ejecución autónoma supervisada.**

---

## §1. FUNDAMENTOS DE DELEGACIÓN

### Axioma de Delegación

```
∀ agente_algorítmico A:
  ∃ actor_humano H tal que:
    H delega responsabilidad R a A ∧
    H mantiene accountability de R ∧
    H puede override decisiones de A
```

**Implicación:** No existen agentes algorítmicos "autónomos absolutos". Siempre hay humano responsable meta-nivel (Principio P1: Autoridad=Responsabilidad).

---

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

---

## §2. MODO M1: MONITOREAR

### Definición

**Agente observa estado sin intervenir.** Solo captura datos, humano lee e interpreta.

### Características

```yaml
Modo: M1 - Monitorear (Monitor)
Iniciativa: Sistema → Agente lee pasivamente
Decisión: 100% humano
Acción: 0% agente (solo observación)
Loop: Human-in-the-loop (continuo)
Latencia_decision: Variable (humano decide cuándo actuar)
```

### Ejemplos

```yaml
Ejemplo_1_Dashboard:
  Agente: Sistema analytics
  Función: Muestra métricas en dashboard
  Humano: Lee dashboard, interpreta, decide acciones
  No hace: Agente no sugiere ni alerta automáticamente

Ejemplo_2_Logs:
  Agente: Log aggregator (Splunk, Datadog)
  Función: Captura y almacena eventos
  Humano: Busca patterns, diagnostica problemas
  No hace: Agente no identifica anomalías (eso sería M2)

Ejemplo_3_Telemetria:
  Agente: Sensores IoT
  Función: Reporta temperatura, presión, vibración
  Humano: Analiza trends, decide mantenimiento
  No hace: Agente no predice fallas (eso sería M2)
```

### Cuándo Usar M1

```yaml
Situaciones:
  - Primeras etapas adoption IA (exploración)
  - Datos históricos insuficientes para ML
  - Dominio novel sin patterns conocidos
  - Compliance requiere human oversight completo

Ventajas:
  - Mínimo riesgo automatización
  - Humano mantiene full context
  - Fácil explicación decisiones

Desventajas:
  - No escala (humano bottleneck)
  - Latencia alta
  - Depende completamente expertise humano
```

---

## §3. MODO M2: INFORMAR

### Definición

**Agente procesa datos y provee insights/recomendaciones.** Humano decide si actúa sobre ellos.

### Características

```yaml
Modo: M2 - Informar (Provide Information)
Iniciativa: Agente genera insights → Humano consume
Decisión: 100% humano (agente sugiere)
Acción: 0% agente (humano ejecuta)
Loop: Human-in-the-loop
Latencia_decision: Minutos-horas (humano evalúa recomendaciones)
```

### Ejemplos

```yaml
Ejemplo_1_Recomendador_Portfolio:
  Agente: Optimizador ML
  Función: "Sugiero priorizar Feature X (ROI 23%, riesgo medio)"
  Humano: Evalúa, considera contexto, decide si prioriza X
  No hace: Agente no cambia prioridades directamente

Ejemplo_2_Anomaly_Detector:
  Agente: ML classifier
  Función: "Alerta: Tráfico API incrementó 300% en 10 min"
  Humano: Investiga si es ataque, spike legítimo, o bug
  No hace: Agente no bloquea tráfico automáticamente (eso sería M4)

Ejemplo_3_Forecaster_Demanda:
  Agente: Time-series ML
  Función: "Forecast: Demanda +40% próximas 2 semanas"
  Humano: Decide si aumenta capacity, rechaza pedidos, etc.
  No hace: Agente no escala infra automáticamente (eso sería M6)
```

### Cuándo Usar M2

```yaml
Situaciones:
  - Decisiones de alto impacto (estrategia, hiring, M&A)
  - Contexto cambiante rápidamente
  - Humano tiene expertise que agente no captura
  - Regulación requiere human-in-loop (ej: medicina, finanzas)

Ventajas:
  - Humano valida antes de actuar (seguridad)
  - Agente reduce carga cognitiva (procesa datos masivos)
  - Explicabilidad: Humano entiende "por qué"

Desventajas:
  - No acelera ejecución (humano aún bottleneck)
  - Requiere humano disponible para revisar
  - Riesgo "alert fatigue" si demasiadas recomendaciones
```

---

## §4. MODO M3: HABILITAR

### Definición

**Agente provee capacidades bajo demanda.** Humano solicita explícitamente, agente ejecuta herramienta.

### Características

```yaml
Modo: M3 - Habilitar (Provide Capabilities)
Iniciativa: Humano solicita → Agente provee
Decisión: Humano elige cuándo/cómo usar
Acción: Agente ejecuta cuando invocado
Loop: Human-in-the-loop (on-demand)
Latencia_decision: Segundos (agente responde a request)
```

### Ejemplos

```yaml
Ejemplo_1_Copilot_Code:
  Agente: GitHub Copilot
  Función: Genera código cuando humano pide autocomplete
  Humano: Invoca, revisa, acepta/rechaza/modifica sugerencia
  No hace: Agente no escribe código sin ser solicitado

Ejemplo_2_SQL_Generator:
  Agente: Text-to-SQL LLM
  Función: Genera query desde pregunta natural language
  Humano: "¿Cuántos usuarios activos Q3?" → Agente genera SQL → Humano revisa y ejecuta
  No hace: Agente no ejecuta queries directamente en DB prod

Ejemplo_3_Chatbot_Support:
  Agente: LLM customer support
  Función: Responde FAQ cuando cliente pregunta
  Humano (cliente): Hace pregunta → Agente responde
  Humano (agente soporte): Puede override si respuesta incorrecta

Ejemplo_4_Simulator:
  Agente: Simulador escenarios
  Función: "Si aumentamos precio 10%, ¿impacto churn?"
  Humano: Solicita simulación, interpreta resultados, decide
  No hace: Agente no cambia precio automáticamente
```

### Cuándo Usar M3

```yaml
Situaciones:
  - Trabajo creativo asistido (coding, writing, diseño)
  - Análisis ad-hoc (exploración datos, what-if)
  - Herramientas especializadas (generación, optimización)
  - Humano quiere control completo timing

Ventajas:
  - Humano mantiene control total
  - Agente acelera tareas específicas masivamente
  - Bajo riesgo (humano valida cada output)

Desventajas:
  - No automático (requiere invocación manual)
  - Interrumpe flujo humano
  - No escala si demasiadas invocaciones necesarias
```

---

## §5. MODO M4: CONTROLAR

### Definición

**Agente ejecuta reglas y políticas automáticamente.** Humano define reglas, agente enforcement. Excepciones escalate.

### Características

```yaml
Modo: M4 - Controlar (Control Activities)
Iniciativa: Agente evalúa y actúa según reglas
Decisión: Agente (dentro de reglas), Humano (excepciones)
Acción: Agente ejecuta automáticamente
Loop: Human-on-the-loop (humano supervisa, no participa en cada caso)
Latencia_decision: Millisegundos-segundos
```

### Ejemplos

```yaml
Ejemplo_1_Approval_Workflow:
  Agente: Business rules engine
  Regla: "IF monto<$10K THEN aprobar_auto ELSE escalate_manager"
  Agente: Aprueba 85% facturas automáticamente
  Humano: Revisa solo facturas >$10K (15%)

Ejemplo_2_Code_Quality_Gates:
  Agente: CI/CD pipeline
  Regla: "IF coverage<80% OR vulnerabilities_high THEN block_merge"
  Agente: Rechaza PRs que no cumplen
  Humano: Puede override con justificación (excepcional)

Ejemplo_3_Fraud_Detection:
  Agente: ML fraud classifier
  Regla: "IF fraud_score>0.9 THEN block_transaction"
  Agente: Bloquea 0.1% transacciones sospechosas
  Humano: Revisa casos bloqueados, puede desbloquear

Ejemplo_4_Auto_Scaling:
  Agente: Cloud autoscaler
  Regla: "IF CPU>80% durante 5min THEN +2 instances"
  Agente: Escala automáticamente
  Humano: Monitorea dashboards, ajusta reglas si necesario
```

### Cuándo Usar M4

```yaml
Situaciones:
  - Reglas claras, bien definidas
  - Volumen alto (imposible revisar cada caso)
  - Latencia crítica (ms-seg response)
  - Compliance enforcement (SOX, GDPR, SOC2)

Ventajas:
  - Escala horizontal infinita
  - Consistencia perfecta (no fatiga, no sesgos)
  - Latencia mínima

Desventajas:
  - Rigidez (edge cases problemáticos)
  - Requiere reglas bien diseñadas
  - Riesgo "false positives/negatives"
```

---

## §6. MODO M5: COPRODUCIR

### Definición

**Colaboración mixta con iniciativa compartida.** Humano y agente co-crean, negocian, iteran.

### Características

```yaml
Modo: M5 - Coproducir (Coproduce Activities)
Iniciativa: Bidireccional (humano ↔ agente)
Decisión: Compartida (negociación continua)
Acción: Mixta (ambos ejecutan partes)
Loop: Mixed (in-loop para decisiones críticas, on-loop para ejecución)
Latencia_decision: Minutos-horas (iteración humano-IA)
```

### Ejemplos

```yaml
Ejemplo_1_Design_Colaborativo:
  Agente: Generative design AI
  Proceso:
    1. Humano: Define constraints ("oficina 500m², 50 personas")
    2. Agente: Genera 10 layouts
    3. Humano: Selecciona 2 favoritos, pide variaciones
    4. Agente: Refina
    5. → Iteración hasta convergencia

Ejemplo_2_Planning_Roadmap:
  Agente: Portfolio optimizer
  Proceso:
    1. Agente: Sugiere priorización basada en valor/riesgo/costo
    2. Humano: Ajusta ponderaciones ("valor más importante que riesgo")
    3. Agente: Re-optimiza
    4. Humano: Fuerza constraints ("Feature X debe estar en Q2")
    5. Agente: Ajusta plan respetando constraint
    6. → Convergencia colaborativa

Ejemplo_3_Research_Paper:
  Agente: LLM research assistant
  Proceso:
    1. Humano: Escribe outline
    2. Agente: Genera draft sección 1
    3. Humano: Edita, agrega insights
    4. Agente: Sugiere referencias relevantes
    5. Humano: Acepta algunas, rechaza otras
    6. → Paper co-creado
```

### Cuándo Usar M5

```yaml
Situaciones:
  - Trabajo creativo complejo
  - Optimización multi-objetivo con trade-offs subjetivos
  - Exploración espacio soluciones amplio
  - Expertise compartido (humano + IA complementarios)

Ventajas:
  - Combina fortalezas humano (juicio, ética) + IA (velocidad, escala)
  - Mejora outcome vs solo-humano o solo-IA
  - Humano aprende de IA, IA se affina con humano

Desventajas:
  - Latencia alta (iteraciones requieren tiempo)
  - Requiere interfaces colaborativas sofisticadas
  - Difícil asignar accountability (ambos contribuyen)
```

---

## §7. MODO M6: EJECUTAR

### Definición

**Agente ejecuta actividades end-to-end autónomamente.** Humano supervisa resultados, puede intervenir en excepciones.

### Características

```yaml
Modo: M6 - Ejecutar (Execute Activities)
Iniciativa: Agente detecta trigger y actúa
Decisión: 100% agente
Acción: 100% agente
Loop: Human-out-of-the-loop (supervisión periódica)
Latencia_decision: Millisegundos (fully automated)
```

### Ejemplos

```yaml
Ejemplo_1_RPA_Invoice_Processing:
  Agente: RPA bot
  Función:
    1. Detecta factura en email
    2. Extrae datos (OCR)
    3. Valida contra PO
    4. Registra en ERP
    5. Paga automáticamente (si<$10K)
  Humano: Revisa log daily, investiga solo errores

Ejemplo_2_Trading_Algorithm:
  Agente: High-frequency trading bot
  Función:
    1. Monitorea mercado en real-time
    2. Identifica arbitraje
    3. Ejecuta compra-venta en millisegundos
    4. Registra trade
  Humano: Define strategy y risk limits, monitorea P&L

Ejemplo_3_Predictive_Maintenance:
  Agente: ML maintenance system
  Función:
    1. Sensores detectan vibración anormal
    2. ML predice falla en 48 hrs (90% confianza)
    3. Crea work order automáticamente
    4. Schedules maintenance
    5. Notifica equipo
  Humano: Ejecuta mantenimiento, confirma trabajo completado

Ejemplo_4_Deploy_Automático:
  Agente: CI/CD + GitOps
  Función:
    1. Tests passed en PR merge
    2. Build image
    3. Deploy a staging
    4. Run smoke tests
    5. Deploy a prod (canary 5% → 100%)
    6. Rollback si error_rate>threshold
  Humano: Monitorea dashboards, puede pausar deploy manualmente
```

### Cuándo Usar M6

```yaml
Situaciones:
  - Tareas repetitivas alto volumen
  - Latencia crítica (<1 seg)
  - Reglas estables, bien validadas
  - Costo error bajo O mecanismos rollback automáticos

Ventajas:
  - Máxima velocidad y escala
  - 24/7 sin intervención
  - Libera humanos para trabajo alto valor

Desventajas:
  - Riesgo alto si mal configurado
  - Requiere monitoring robusto
  - "Automation bias" (confiar ciegamente en agente)
```

---

## §8. MATRIZ 6 MODOS × 4 DOMINIOS

### Delegación por Dominio

| Dominio ↓ / Modo → | M1 | M2 | M3 | M4 | M5 | M6 |
|--------------------|----|----|----|----|----|----|
| **ARQUITECTURA** | Dashboard org health | Detecta violaciones RACI | Simulador estructuras | Enforce governance rules | Co-diseño org con IA | ⚠️ No recomendado |
| **PERCEPCIÓN** | Métricas raw en dashboard | Insights narrativos | Drill-down analytics | Alertas automáticas | Investigación guiada | Data pipelines ETL |
| **DECISIÓN** | Track decision velocity | Recomendaciones portfolio | Optimizadores multi-objetivo | Auto-aprobaciones (reglas) | Planning colaborativo | Auto-priorización backlog |
| **OPERACIÓN** | Flow metrics real-time | Blockers predichos | Copilot code/docs | Quality gates CI/CD | Pair programming IA | Deploy automático |

**Leyenda:**  
- ✅ Alta viabilidad  
- ◐ Viabilidad contextual  
- ⚠️ No recomendado (riesgo alto)

---

## §9. HUMAN-IN/ON/OUT-THE-LOOP

### Definición Loops

```yaml
Human-IN-the-loop:
  - Humano participa en CADA decisión/acción
  - Modos: M1, M2, M3
  - Latencia: Alta (humano bottleneck)
  - Seguridad: Máxima

Human-ON-the-loop:
  - Humano supervisa, interviene solo en excepciones
  - Modos: M4
  - Latencia: Baja (mayoría casos automáticos)
  - Seguridad: Alta (humano puede override)

Human-OUT-of-the-loop:
  - Humano monitorea resultados agregados, no interviene en operación
  - Modos: M6
  - Latencia: Mínima (fully automated)
  - Seguridad: Requiere monitoring robusto + rollback automático
```

### Escalation entre Loops

```
OUT-of-loop (M6)
   │
   ├─ Si anomalía detectada → Escala a ON-loop (M4)
   │
ON-loop (M4)
   │
   ├─ Si excepción no cubierta → Escala a IN-loop (M2/M3)
   │
IN-loop (M1-M3)
   │
   └─ Humano resuelve, puede definir nueva regla → Vuelve a M4/M6
```

---

## §10. EVOLUCIÓN DE MODOS

### Progresión Típica

```
Fase 1: EXPLORACIÓN
  Modo: M1, M2
  Duración: 3-6 meses
  Objetivo: Entender problema, validar IA es útil

Fase 2: ASISTENCIA
  Modo: M3
  Duración: 6-12 meses
  Objetivo: Herramientas bajo demanda, humano aprende confiar IA

Fase 3: AUTOMATIZACIÓN PARCIAL
  Modo: M4
  Duración: 12-24 meses
  Objetivo: Reglas claras automatizadas, excepciones humanas

Fase 4: COLABORACIÓN
  Modo: M5
  Duración: 12+ meses (puede ser estado final)
  Objetivo: Co-creación para problemas complejos

Fase 5: AUTOMATIZACIÓN COMPLETA
  Modo: M6
  Duración: Variable (algunos procesos nunca llegan aquí)
  Objetivo: End-to-end autonomy con supervisión mínima
```

**Principio P8 (Herramienta no Oráculo):** No saltar directo a M6 sin pasar por M1-M4. Aprendizaje progresivo esencial.

---

## §11. ANTI-PATRONES DELEGACIÓN

### AP1. "M6 Prematuro"

```yaml
Síntoma: Implementar M6 sin haber validado M1-M4
Causa: "Move fast" sin considerar riesgos
Consecuencia: Fallos catastróficos, pérdida confianza IA
Ejemplo: Trading bot sin validar M2-M4 → Pérdida $M en horas
Fix: Siempre progresar M1 → M2 → M3 → M4 → M6
```

### AP2. "M1 Perpetuo"

```yaml
Síntoma: Nunca evolucionar de M1 después de años
Causa: Risk-aversion extrema, falta skills IA
Consecuencia: No capturar valor IA, competitors avanzan
Ejemplo: Dashboard manual análisis 10 años, competitors automatizan
Fix: Establecer roadmap progresión modos (Ver §10)
```

### AP3. "No Escalation Path"

```yaml
Síntoma: M6 sin mecanismo rollback a M4/M2
Causa: Diseño asume "IA nunca falla"
Consecuencia: Cuando IA falla, no hay escape hatch
Ejemplo: Deploy M6 sin circuit breaker → Outage 4 hrs
Fix: Siempre implementar escalation (§9)
```

### AP4. "Automation Bias"

```yaml
Síntoma: Humanos confían ciegamente en M6, no validan
Causa: "Computer said so" syndrome
Consecuencia: Errores sistemáticos no detectados
Ejemplo: Fraud detection M6 bloquea clientes legítimos, nadie revisa logs
Fix: Monitoring activo + auditoría periódica resultados M6
```

### AP5. "Mode Mismatch"

```yaml
Síntoma: Usar M3 (bajo demanda) cuando necesitas M4 (automático)
Causa: No entender diferencia modos
Consecuencia: Humano saturado con requests manuales
Ejemplo: Aprobar 1000 facturas/día con M3 → Humano bottleneck
Fix: Mapear volumen/latencia a modo adecuado (Ver §12)
```

---

## §12. DECISION TREE: ¿QUÉ MODO USAR?

```
┌─ ¿Volumen alto (>100 casos/día)? ──NO──► M1, M2, M3
│                                            (Análisis manual viable)
└─ SÍ
   │
   ┌─ ¿Latencia crítica (<1 min)? ──NO──► M2, M3, M4
   │                                       (Humano puede revisar)
   └─ SÍ
      │
      ┌─ ¿Reglas claras y estables? ──NO──► M2, M3, M5
      │                                       (Requiere juicio)
      └─ SÍ
         │
         ┌─ ¿Costo error alto? ──SÍ──► M4 (con escalation)
         │                                (Humano-on-loop)
         └─ NO
            │
            └─► M6 (con monitoring robusto)
                (Humano-out-loop)
```

---

## §13. VALIDACIÓN

### Completitud

```
¿Todo tipo interacción humano-IA cae en M1-M6? → SÍ
  Evidencia: Mapeo 30 patrones IA (APLICACION/A1_Patrones PA01-PA20)
```

### Ortogonalidad

```
¿Overlaps entre modos? → NO
  M1 observa, M2 informa, M3 habilita, M4 controla, M5 coprodujo, M6 ejecuta
  Cada modo tiene iniciativa y decisión únicas
```

### Suficiencia

```
¿Se necesitan más de 6 modos? → NO
  6 modos cubren espectro completo autonomía: 0% (M1) → 100% (M6)
```

---

## §8. DIMENSIÓN PURPOSE: ROL DEL AGENTE

### Concepto Ortogonalidad

```yaml
Observación:
  M1-M6 describe AUTONOMÍA (cuánto control humano)
  Pero no describe ROL (qué tipo de support provee agente)

Dimensiones_Ortogonales:
  - Autonomy (M1-M6): Spectrum control humano-agente
  - Purpose (4 roles): Tipo de support/función del agente
  
  Estas dimensiones son INDEPENDIENTES:
    - Agente puede ser Assistant con M6 autonomy (chatbot ejecuta acciones)
    - Agente puede ser Automation con M3 autonomy (requiere approval)
    - Misma autonomía, diferentes purposes → diferentes expectations

Implicación_Diseño:
  Al diseñar agente, especificar AMBAS dimensiones:
    1. Autonomy: ¿Qué modo M1-M6?
    2. Purpose: ¿Qué rol? (Assistant/Augment/Orchestrate/Automate)
```

### Purpose 1: Assistant

```yaml
Definición: Soporte directo a usuario mediante interacción natural conversacional

Características:
  - Interface: Natural language, chat, voice
  - Iniciativa: User-driven (user asks, agent responds)
  - Scope: Task-specific en respuesta a request
  - Interaction: Conversational, iterative

Ejemplos:
  Copilot:
    - Sugiere código, completa funciones
    - Explica code snippets, debugging help
    - Genera tests, documentation
    Purpose: Assistant
    Autonomy: M2-M3 (inform, enable)
  
  ChatGPT:
    - Responde preguntas, genera content
    - Summarizes documents, translations
    - Brainstorming, ideation support
    Purpose: Assistant
    Autonomy: M2-M4 (varies by task)
  
  Virtual_Assistant:
    - "Schedule meeting with John tomorrow 2pm"
    - "Send email to team about roadmap update"
    - "Find customer account with ID 12345"
    Purpose: Assistant
    Autonomy: M4-M6 (varies: suggest vs execute)

User_Expectations:
  - Transparency: Explain reasoning, sources
  - Explainability: "Why did you suggest X?"
  - Control: User can reject, modify, iterate
  - Conversational: Natural dialogue, context awareness

Failure_Mode: Incorrect suggestion
  → User can reject, no harm done
  → Learning: Improve from feedback
```

### Purpose 2: Augmentation Tool

```yaml
Definición: Funcionalidad empaquetada AI-enabled que augmenta user abilities

Características:
  - Interface: Direct manipulation, interactive GUI
  - Iniciativa: User-driven (tool usado intencionalmente)
  - Scope: Dominio específico de funcionalidad
  - Interaction: Direct, immediate feedback

Ejemplos:
  AI_Image_Editor:
    - Remove background (1-click)
    - Enhance quality, upscale resolution
    - Style transfer, filters
    Purpose: Augmentation Tool
    Autonomy: M3-M4 (enable, control)
  
  Code_Completion:
    - Auto-suggest next lines mientras escribes
    - Type hints, parameter info
    - Refactoring suggestions
    Purpose: Augmentation Tool
    Autonomy: M3 (enable)
  
  Grammar_Checker:
    - Highlight errors in real-time
    - Suggest corrections, style improvements
    - Plagiarism detection
    Purpose: Augmentation Tool
    Autonomy: M2-M3 (inform, enable)

User_Expectations:
  - Predictability: Same input → Same output
  - Immediacy: Real-time feedback
  - Undo-ability: Easy to reverse changes
  - Integration: Seamless in workflow

Failure_Mode: Unexpected behavior
  → User can undo immediately
  → Non-destructive (preserves original)
```

### Purpose 3: Orchestration Agent

```yaml
Definición: Meta-agent que coordina otros agents y manages delegation

Características:
  - Interface: Configuration, policies, dashboards
  - Iniciativa: Hybrid (supervises autonomous agents)
  - Scope: Cross-agent coordination
  - Interaction: Monitoring, intervention points

Ejemplos:
  Self_Driving_Car_Supervisor:
    - Coordina: Perception, Planning, Control agents
    - User interface: Set destination, driving mode
    - Intervention: Take steering wheel (override)
    Purpose: Orchestration Agent
    Autonomy: M4-M5 (control, co-produce)
  
  Workflow_Orchestrator:
    - Coordina: Order, Inventory, Shipping agents
    - User interface: Configure policies, monitor status
    - Intervention: Manual override for exceptions
    Purpose: Orchestration Agent
    Autonomy: M4-M5
  
  Crisis_Governance (P52):
    - Coordina: Financial, Customer, Talent agents
    - User interface: Daily meetings, decision protocols
    - Intervention: Crisis team makes decisions
    Purpose: Orchestration Agent (human-led)
    Autonomy: M3-M4

User_Expectations:
  - Agent_Network_Transparency: Who does what
  - Intervention_Capability: Override any agent
  - Coordination_Visibility: See handoffs, dependencies
  - Bounded_Autonomy: Clear limits per agent

Failure_Mode: Coordination breakdown
  → Human takes over orchestration
  → Agents continue working, orchestrator replaced
```

### Purpose 4: Automation Agent

```yaml
Definición: Agent ejecuta end-to-end sin user interaction directa (decoupled)

Características:
  - Interface: Configuration upfront, monitoring/alerts
  - Iniciativa: System-driven (detached from user)
  - Scope: Complete Sense-Decide-Act loop
  - Interaction: Minimal (exception-based)

Ejemplos:
  Fraud_Detection:
    - Sense: Detect transaction patterns (L2 Comprehend)
    - Decide: Apply rules, flag risk (Mode 2 Rule-Based)
    - Act: Block transaction (L1 Action)
    Purpose: Automation Agent
    Autonomy: M5-M6 (co-produce con oversight OR execute)
  
  Autoscaling:
    - Sense: Monitor CPU, memory (L1 Detect)
    - Decide: Threshold crossed (Mode 1 Direct Feedback)
    - Act: Add/remove instances (L1 Action)
    Purpose: Automation Agent
    Autonomy: M6 (execute, bounded)
  
  Surveillance_System:
    - Sense: Detect stranger on property (L2 Comprehend)
    - Decide: Unknown person (Mode 2 Rule-Based)
    - Act: Alert homeowner → Call police if not identified
    Purpose: Automation Agent
    Autonomy: M5 (co-produce, human validates escalation)

User_Expectations:
  - Bounded_Autonomy: Clear scope, limits
  - Auditability: Log all decisions, actions
  - Override_Capability: Human can intervene
  - Configuration: Policies, thresholds, escalations

Failure_Mode: Incorrect autonomous action
  → Requires rollback + intervention
  → Post-incident review, adjust policies
```

### Purpose × Autonomy Matrix

```yaml
Cross-Reference_Common_Patterns:

               M1      M2      M3      M4      M5      M6
               Monitor Inform  Enable  Control CoProd  Execute
  Assistant    -       ✓✓      ✓✓      ✓       ○       ○
  Augment      -       ○       ✓✓      ✓✓      ○       -
  Orchestrate  -       -       ○       ✓✓      ✓✓      ○
  Automate     -       -       -       ○       ✓✓      ✓✓

  ✓✓ = Very common, natural fit
  ✓  = Common
  ○  = Possible but less common
  -  = Rare/incompatible

Explicación_Patterns:

Assistant + M2-M3 (muy común):
  - Copilot: Informs suggestions, enables completion
  - ChatGPT: Informs answers, enables ideation
  - Natural fit: Conversational, user retains control

Augment + M3-M4 (muy común):
  - Image editor: Enables transformations, user controls
  - Grammar checker: Enables corrections, user accepts/rejects
  - Natural fit: Interactive tools, immediate feedback

Orchestrate + M4-M5 (muy común):
  - Workflow engine: Controls process, co-produces with humans
  - Self-driving supervisor: Controls agents, human intervenes
  - Natural fit: Coordination requires control, not full autonomy

Automate + M5-M6 (muy común):
  - Fraud detection: Co-produces with oversight OR executes bounded
  - Autoscaling: Executes within bounds
  - Natural fit: End-to-end autonomy, minimal human involvement

Anti-Patterns:

Assistant + M6 (posible pero raro):
  - "ChatGPT ejecuta acciones sin confirmation"
  - Risky: User expects conversational confirmation
  - Excepciones: Trivial actions (set timer, play music)

Automate + M2 (incompatible):
  - "Automation agent solo informa, no actúa"
  - Contradicción: No es automation si no ejecuta
```

---

### Design Implications

```yaml
Especificar_Ambas_Dimensiones:

Ejemplo_Completo_Design:
  "Diseñar fraud detection system"
  
  Step_1_Purpose:
    ¿Qué rol? → Automation Agent
    Rationale: Debe operar 24/7 sin humano, end-to-end loop
  
  Step_2_Autonomy:
    ¿Qué modo? → M5 Co-produce
    Rationale: Block transaction (action significant), daily review false positives
  
  Step_3_Expectations:
    Dado Purpose=Automate + Autonomy=M5:
      - Auditability: Log todas las decisiones
      - Override: Admin puede unblock transaction
      - Configuration: Rules, thresholds via dashboard
      - Monitoring: Daily review dashboard (false positives)
  
  Step_4_Failure_Handling:
    Si false positive (block legit transaction):
      → User reports, admin investigates
      → Unblock transaction manually
      → Tune rules to reduce future false positives

Evolution_Pattern:
  Purpose puede cambiar over time:
    - Start: Assistant (human validates todo)
    - Trust builds: Augmentation Tool (human uses proactively)
    - Maturity: Automation (human oversight only)
  
  Ejemplo_Churn_Prediction:
    t0: Assistant (M2) - "AI suggests: Customer X at risk"
    t1: Augmentation (M3) - "Tool highlights at-risk customers, PM reviews"
    t2: Automation (M5) - "System sends retention offer, PM reviews outcomes"
```

---

### Conexión con Awareness & Decision Modes

```yaml
Full_Stack_Design:

Awareness_Level → Decision_Mode → Execution_Level → Purpose → Autonomy:

Ejemplo_1_Simple_Automation:
  Awareness: L1 Detect (temperature sensor)
  Decision: Mode 1 Direct Feedback (threshold)
  Execution: L1 Action (turn on cooling)
  Purpose: Automation Agent
  Autonomy: M6 Execute
  → Thermostat fully autonomous

Ejemplo_2_Intelligent_Assistant:
  Awareness: L2 Comprehend (churn risk analysis)
  Decision: Mode 3 Associative (ML pattern matching)
  Execution: L1 Action (send retention offer)
  Purpose: Assistant (suggests) OR Automation (executes)
  Autonomy: M4 Control (suggest) OR M5 Co-produce (execute with review)
  → Depends on trust level

Ejemplo_3_Orchestration:
  Awareness: L3 Project (crisis forecast)
  Decision: Mode 4 Knowledge-Based (P52 activation)
  Execution: L3 Planning (orchestrate stabilization)
  Purpose: Orchestration Agent
  Autonomy: M3 Enable (human-led, AI supports)
  → Crisis governance hybrid
```

---

## Referencias Cruzadas

- **Primitivo Actor:** `CORE/01_Primitivos.md` §1
- **Purpose dimension:** Este documento §8
- **Awareness levels:** `DOMINIOS/D2_Percepcion.md` §5
- **Decision modes:** `DOMINIOS/D3_Decision.md` §6
- **Execution levels:** `DOMINIOS/D4_Operacion.md` §12
- **Ciclo SDA completo:** `CORE/02_Ciclo_Fundamental.md`
- **Axioma A8 (No Oráculo):** `CORE/00_Manifiesto.md` §3
- **Patrones delegación IA:** `APLICACION/A1_Patrones.md` §5 (IA)
- **Orchestration pattern:** `APLICACION/A1_Patrones.md` §13 (P53)
- **Casos delegación:** `REFERENCIA/R1_Casos.md` (Hiring, Ecommerce, Auction, Vehículo)
- **Madurez IA (6 niveles):** `APLICACION/A3_Diagnostico.md` §9
