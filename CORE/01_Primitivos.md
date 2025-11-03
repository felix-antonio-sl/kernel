# 01_Primitivos

**Versión:** 1.1.0 | **Estado:** Definitivo | **Audiencia:** Arquitectos, Diseñadores

---

## Invariante

**Toda organización ejecutable se descompone en exactamente 7 primitivos ortogonales e irreducibles: Actor, Flujo, Dato, Señal, Límite, Estado, Recurso.**

**Nota:** Señal agregado en v1.1 para distinguir disparadores (impulsos acción) de datos formales (registros estructurados).

---

## §1. ACTOR - Entidad con Capacidad Decisional

### Definición

Entidad autónoma que ejecuta acciones y toma decisiones.

### Tipos

**Actor Humano:**

- Juicio contextual alto, velocidad variable, escala limitada
- Fortalezas: Ambigüedad, ética, creatividad, empatía
- Límites: Escala, velocidad, consistencia

**Actor Algorítmico:**

- Juicio contextual limitado, velocidad ms, escala infinita
- Fortalezas: Volumen masivo, velocidad, consistencia 24/7
- Límites: Contextos nuevos, decisiones éticas sin precedente
- **Delegación explícita:** Todo agente algorítmico opera delegado por humano meta-nivel

---

## §2. FLUJO - Secuencia de Transformaciones

### Definición

Secuencia ordenada que convierte entradas en salidas mediante pasos ejecutados por actores.

### Estructura

```
Flujo = Secuencia(Pasos)
Paso = {accion, actor, input, output, condiciones, duracion}
```

### Tipos

- **Estructurado:** Pasos predefinidos, automatizable (workflows)
- **Semi-estructurado:** Pasos conocidos, orden variable (diagnósticos)
- **No-estructurado:** Pasos emergentes, creativos (investigación)

---

## §3. DATO - Información Estructurada con Semántica

### Definición

Información que representa estado del mundo con significado explícito.

### Propiedades Críticas

- **Semántica:** Significado explícito
- **Estructura:** Schema definido
- **Linaje:** Trazabilidad origen y transformaciones
- **Calidad:** Score 0-100 (completitud, precisión, consistencia, actualidad)

### Tipos

- **Estructurado:** SQL, JSON con schema (validable, queryable)
- **Semi-estructurado:** JSON sin schema, logs (flexible)
- **No-estructurado:** Texto, imágenes, video (requiere NLP/CV)

---

## §3A. SEÑAL - Impulso para Acción

### Definición

Disparador que inicia acción o flujo. Placeholder para conversación futura, no registro formal completo.

### Nota sobre Relación con Dato (Minimalidad I1)

**Aclaración fundamental**: Señal y Dato están **relacionados temporalmente** (Señal precede y evoluciona a Dato), lo que plantea la pregunta: ¿Son primitivos verdaderamente ortogonales o Señal es un estado temporal de Dato?

**Justificación de ambos como primitivos**:

```yaml
Por_Qué_Mantener_Señal_Separado:
  
  1. Semántica_Diferenciada:
     - Señal: "Impulso que INICIA acción" (trigger, activation)
     - Dato: "Información que INFORMA acción" (knowledge, state)
     - Diferencia_Fundamental: Intención (iniciar vs informar)
  
  2. Ciclo_Operacional_Distinto:
     - Señal: Captured instantáneamente, minimal validation
     - Dato: Refined iterativamente, extensive validation
     - Si fusionamos: Perdemos representar "evento en tránsito"
  
  3. Patron_Uso_Asimétrico:
     - Señal → Dato: Común (user story elaborated)
     - Dato → Señal: Raro (dato genera trigger ocasionalmente)
     - No es relación simétrica, sugiere distinción válida
  
  4. Modelado_Sistemas_Reactivos:
     - Event-driven architectures requieren Señal (webhook, pub/sub)
     - Sin Señal: No puedes modelar "evento aún no procesado"
  
  5. Composición_Unidad_Trabajo:
     - señales_input: Triggers externos que inician trabajo
     - datos_input: Información consumida durante trabajo
     - Fusionar: Pierde claridad boundary-spanning
  
Reconocimiento_Overlap:
  "Señal evoluciona a Dato" es correcto
  PERO: Durante evolución, ambos coexisten temporalmente
  
  Timeline:
    t0: Señal existe (user story creada)
    t1: Señal + Dato parcial coexisten (conversation ongoing)
    t2: Señal consumida, Dato completo persiste
  
  → En t1, necesitas AMBOS primitivos representar estado sistema

Alternativa_Evaluada_Y_Rechazada:
  "Dato(completitud: placeholder) reemplaza Señal"
  
  Problema:
    - Obscurece intención (dato "placeholder" es antinatural)
    - Pierde semántica trigger (Señal activa, Dato pasivo)
    - Complica composición Outside-In
  
  Decisión: Mantener separación por claridad semántica
            Aceptar overlap temporal como trade-off explícito
```

**Posición formal**: Señal y Dato son **cuasi-ortogonales** (relacionados temporalmente pero semánticamente distintos). Esta es una **violación consciente y justificada** de ortogonalidad estricta en favor de **claridad operacional**.

---

### Distinción Clave: Señal vs Dato

```yaml
Señal:
  Naturaleza: Impulso, trigger, evento
  Propósito: Iniciar acción o conversación
  Completitud: Deliberadamente incompleta
  Timing: Precede a Dato (primero señal, luego especificación)
  Ejemplos:
    - User Story: "Como cliente quiero X para Y" (placeholder)
    - Incident Alert: "Error rate >5%" (trigger respuesta)
    - Customer Request: "Necesito feature Z" (inicia discovery)
    - Event: "Order_Created" (dispara workflow)

Dato:
  Naturaleza: Registro formal, información estructurada
  Propósito: Representar estado del mundo con fidelidad
  Completitud: Schema completo, validado
  Timing: Sigue a Señal (especificación detallada después)
  Ejemplos:
    - Acceptance Criteria detallados de user story
    - Incident Postmortem completo con RCA
    - PRD (Product Requirements Document) formal
    - Order record con todos campos (customer_id, items, total, etc.)
```

### Progresión Señal → Dato

```yaml
Ciclo_Típico:
  1. Señal captura esencia problema/oportunidad (high-level, rápido)
  2. Conversación elabora detalles (3 amigos: PO + Dev + QA)
  3. Dato formaliza especificación completa (tests, docs, contracts)

Ejemplo_User_Story:
  t0_Señal: "Como usuario quiero guardar dirección para checkout rápido"
  t1_Conversación: Sprint planning - discutir validaciones, UX, API
  t2_Dato: Acceptance criteria formales + API contract + tests
```

### Tipos

- **Request:** Demanda externa que inicia trabajo (customer request, ticket)
- **Event:** Suceso que dispara reacción (webhook, sensor trigger)
- **Story:** Necesidad de usuario que requiere implementación (user story, job story)
- **Alert:** Condición anormal que requiere atención (monitoring alert, SLA breach)

### Propiedades

- **Origen:** Externo (customer, sistema) o Interno (equipo, proceso)
- **Urgencia:** Inmediata, Normal, Baja
- **Claridad:** Alta (bien definida) vs Baja (requiere refinamiento)

---

## §4. LÍMITE - Restricción sobre Posibilidades

### Definición

Constraint que reduce espacio de opciones válidas.

### Tipos

1. **Físico:** Leyes naturales (velocidad luz, tiempo)
2. **Regulatorio:** Leyes, normas (GDPR, SOX, HIPAA)
3. **Organizacional:** Políticas internas (tech stack, WIP limits)
4. **Económico:** Budget, ROI, TCO
5. **Técnico:** Capacidades actuales (escalabilidad DB, context window LLM)

### Gestión

- Aceptar | Mitigar | Eliminar | Excepción | Transformar

---

## §5. ESTADO - Snapshot Temporal

### Definición

Snapshot de (Actores, Flujos, Datos, Recursos) en timestamp t.

### Dimensiones

```yaml
Estado(t):
  actores_activos: [Actor]
  flujos_en_ejecucion: [Flujo_Instancia]
  datos_vigentes: [Dato]
  recursos_disponibles: [Recurso]
  health_score: 0-100
```

### Transiciones

```
Estado(t0) --[Evento]--> Estado(t1)
```

---

## §6. RECURSO - Capacidad Habilitadora

### Definición

Capacidad tangible/intangible que permite a actores ejecutar flujos.

### Tipos

1. **Tangible:** Infraestructura, hardware, instalaciones
2. **Intangible:** Software, datos, conocimiento, IP, cultura
3. **Humano:** Tiempo + skills disponibles
4. **Temporal:** Tiempo como recurso finito
5. **Financiero:** Capital, presupuesto

### KPIs

- Utilization: % uso / disponible
- Availability: % disponible cuando necesario
- TCO: Costo total vida útil

---

## §7. COMPOSICIÓN: UNIDAD DE TRABAJO

```yaml
Unidad_Trabajo:
  # Capacidades internas (recursos de ejecución)
  actores: Set(Actor)           # ≥1 - Quiénes ejecutan
  flujos: Set(Flujo)            # ≥1 - Qué procesos ejecutan
  recursos: Set(Recurso)        # ≥1 - Con qué ejecutan
  
  # Inputs (boundary in - qué entra del exterior)
  señales_input: Set(Señal)     # Disparadores externos (eventos, requests)
  datos_input: Set(Dato)        # Información consumida (requisitos, contexto)
  
  # Outputs (boundary out - qué sale al exterior) - OUTSIDE-IN
  productos_servicios: Set(Producto_Servicio)  # ≥1 - Valor entregado
  destinatarios: Set(Destinatario)             # ≥1 - Receptores del valor
  
  # Contexto operacional (fuerzas externas)
  limites: Set(Limite)          # Constraints (regulación, presupuesto, técnicos)
  entorno: Set(Factor_Ambiental) # Fuerzas externas (competencia, mercado)
  
  # Estado temporal
  estados: Secuencia(Estado)    # ≥2 (inicio, fin)
```

**Nota crítica:** Esta composición formaliza perspectiva **Outside-In** (P3 Manifiesto). Primero se definen outputs (productos/servicios) y destinatarios (clientes/stakeholders), luego se diseña estructura interna para entregarlos.

---

### Definiciones Elementos Boundary-Spanning

#### Producto_Servicio

```yaml
Definición: Output tangible o intangible entregado a destinatarios externos/internos

Tipos:
  - Tangible: Objeto físico (hardware, producto manufacturado)
  - Intangible: Asset digital (software, datos, IP)
  - Servicio: Actividad ejecutada para beneficiario (soporte, consultoría)
  - Paquete: Combinación productos + servicios (SaaS con support)

Atributos:
  nombre: String                           # Identificador producto
  tipo: {Tangible, Intangible, Servicio, Paquete}
  valor_entregado: String                  # Outcome para destinatario
  destinatarios: Set(Destinatario)         # Quiénes lo consumen
  metricas_valor: Set(KPI)                 # Cómo medimos valor entregado

Ejemplos:
  Producto_1:
    nombre: "API Payments Processing"
    tipo: Servicio
    valor_entregado: "Procesa pagos con latencia <200ms, uptime 99.95%"
    destinatarios: [E-commerce_Teams, Mobile_App_Teams]
    metricas_valor: [Latency_P95, Success_Rate, Uptime]
  
  Producto_2:
    nombre: "Customer Analytics Dashboard"
    tipo: Intangible + Servicio
    valor_entregado: "Insights comportamiento cliente tiempo real"
    destinatarios: [Product_Managers, Marketing_Teams, Executives]
    metricas_valor: [Daily_Active_Users, Time_to_Insight, NPS]
```

#### Destinatario

```yaml
Definición: Entidad que consume productos/servicios de la Unidad de Trabajo

Tipos:
  - Cliente_Externo: Consumidor final fuera organización (paga/no paga)
  - Cliente_Interno: Otro equipo/departamento dentro organización
  - Stakeholder: No consume directamente pero tiene interés (regulador, inversor)

Atributos:
  tipo: {Cliente_Externo, Cliente_Interno, Stakeholder}
  segmento: String                         # Market segment, departamento, rol
  necesidad_satisfecha: String             # Job-to-be-done
  criticidad: {Alta, Media, Baja}          # Importancia para organización

Ejemplos:
  Destinatario_1:
    tipo: Cliente_Interno
    segmento: "Sales Operations Teams (15 personas, 3 regiones)"
    necesidad_satisfecha: "Cerrar deals más rápido con quotes automatizados"
    criticidad: Alta
  
  Destinatario_2:
    tipo: Cliente_Externo
    segmento: "SMB SaaS companies (ARR $100K-$2M)"
    necesidad_satisfecha: "Payments procesados sin friction técnico"
    criticidad: Alta
  
  Destinatario_3:
    tipo: Stakeholder
    segmento: "GDPR Compliance Officer"
    necesidad_satisfecha: "Garantía procesamiento datos personal conforme"
    criticidad: Alta
```

#### Factor_Ambiental

```yaml
Definición: Fuerza externa que influencia (positiva/negativamente) operación Unidad de Trabajo

Categorías:
  - Competencia: Alternativas que destinatarios pueden elegir
  - Regulacion: Leyes, normas, estándares obligatorios
  - Mercado: Tendencias demanda, poder adquisitivo, preferencias
  - Tecnologia: Disrupciones tech, obsolescencia, nuevas capacidades
  - Demografia: Cambios población, geografía, cultura

Atributos:
  categoria: {Competencia, Regulacion, Mercado, Tecnologia, Demografia}
  descripcion: String
  impacto: {Positivo, Neutral, Negativo}
  urgencia: {Inmediata, Corto_Plazo, Largo_Plazo}

Ejemplos:
  Factor_1:
    categoria: Competencia
    descripcion: "Stripe lanzó Instant Payouts (competidor directo)"
    impacto: Negativo
    urgencia: Inmediata
  
  Factor_2:
    categoria: Regulacion
    descripcion: "PSD2 requiere Strong Customer Authentication"
    impacto: Neutral (compliance cost, pero barrier to entry competidores)
    urgencia: Corto_Plazo
  
  Factor_3:
    categoria: Tecnologia
    descripcion: "LLMs permiten customer support automatizado nivel humano"
    impacto: Positivo
    urgencia: Corto_Plazo
```

---

### Ejemplo Completo: Unidad de Trabajo Outside-In

```yaml
Unidad_Trabajo: "Customer Support Automation"

# OUTPUTS FIRST (Outside-In)
productos_servicios:
  - nombre: "FAQ Resolution Automatizada"
    tipo: Servicio
    valor_entregado: "Resuelve 60% consultas sin humano, <30s response"
    metricas_valor: [Resolution_Rate, Response_Time, CSAT]

destinatarios:
  - tipo: Cliente_Externo
    segmento: "Enterprise customers (>500 usuarios)"
    necesidad_satisfecha: "Soporte 24/7 sin esperar agente humano"
    criticidad: Alta
  
  - tipo: Cliente_Interno
    segmento: "Support Agents (20 personas)"
    necesidad_satisfecha: "Reducir carga FAQ repetitivas 60%"
    criticidad: Alta

# ENTORNO (Fuerzas externas)
entorno:
  - categoria: Competencia
    descripcion: "Zendesk Answer Bot resuelve 40% tickets"
    impacto: Negativo
  
  - categoria: Tecnologia
    descripcion: "GPT-4 permite responses contextuales high-quality"
    impacto: Positivo

# ESTRUCTURA INTERNA (Diseñada para entregar outputs)
actores:
  - LLM_Agent (M4 delegation - genera responses)
  - Support_Agent_Humano (override si necesario)

flujos:
  - Recibir customer question
  - Classify intent (LLM)
  - Retrieve relevant docs (vector DB)
  - Generate response (LLM)
  - Validate quality score >0.8
  - If <0.8 → Escalate humano
  - Send response

recursos:
  - OpenAI API (LLM)
  - Pinecone (vector DB knowledge base)
  - Slack integration (escalation)

señales_input:
  - Customer question via chat/email

datos_input:
  - Knowledge base articles (500 docs)
  - Historical ticket resolutions

limites:
  - Budget: $5K/mes API costs
  - Latency: Response <30s
  - Accuracy: CSAT >4.0/5.0

estados:
  - Estado(t0): Backlog 200 tickets, 8hrs avg response
  - Estado(t1): Backlog 80 tickets, 30min avg response (automation activa)
```

**Ejemplo completo adicional:** Ver `REFERENCIA/R1_Casos.md` caso "Hiring Algorítmico"

---

## §8. PRUEBAS DE IRREDUCIBILIDAD

### Test 1: Eliminación

```
∀ primitivo P ∈ {Actor, Flujo, Dato, Señal, Límite, Estado, Recurso}:
  eliminar(P) → ∃ organización O que no puede representarse
```

### Test 2: Reducción

```
¿P puede expresarse como f(otros_primitivos)?
  Actor = Flujo que decide? → NO (autonomía ≠ secuencia)
  Flujo = Actor secuenciado? → NO (transformación ≠ agente)
  Dato = Estado? → NO (información ≠ snapshot temporal)
  Señal = Dato sin estructura? → NO (impulso ≠ registro, distinción semántica crítica)
  Límite = Dato constraint? → NO (restricción ≠ representación)
  Estado = Dato temporal? → NO (snapshot completo ≠ información)
  Recurso = Actor pasivo? → NO (capacidad ≠ agencia)
```

**Conclusión:** 7 primitivos mínimos e irreducibles ✅

**Nota composición:** Producto_Servicio, Destinatario y Factor_Ambiental NO son primitivos. Son **estructuras compuestas** en §7 que formalizan perspectiva Outside-In sin violar I1 (Minimalidad).

---

## §9. VALIDACIÓN FORMAL

**Ver:** `CORE/07_Validacion.md` para pruebas completas de:

- Completitud (todo modelable)
- Minimalidad (nada eliminable)
- Ortogonalidad (sin overlaps)
- Consistencia (sin contradicciones)

---

## Referencias Cruzadas

- **Manifiesto:** `CORE/00_Manifiesto.md`
- **Arquitectura 4 dominios:** `CORE/03_Arquitectura.md`
- **Ciclo SDA:** `CORE/02_Ciclo_Fundamental.md`
- **Delegación IA:** `CORE/04_Delegacion.md`
- **Casos aplicados:** `REFERENCIA/R1_Casos.md`
