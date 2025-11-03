# 01_Primitivos v2.0.0

## §0. INVARIANTE

**Toda organización ejecutable se descompone en exactamente 7 primitivos irreducibles con responsabilidades no solapadas:**

**Actor • Flujo • Señal • Dato • Límite • Estado • Recurso**

**Propiedad I1 (Minimalidad):** Eliminar cualquier primitivo → Sistema incompleto.

**Propiedad I2 (Ortogonalidad):** Responsabilidades únicas, sin overlaps.

**Nota histórica:** Señal agregado en v1.1 para distinguir impulsos-disparadores de registros-persistentes.

## §1. ACTOR — Entidad con Capacidad Decisional

### Definición

Entidad autónoma que ejecuta acciones y toma decisiones.

### Tipos

**A1. Actor Humano**

```yaml
Características:
  Juicio: Alto (ambigüedad, ética, creatividad, empatía)
  Velocidad: Variable (segundos a días)
  Escala: Limitada (cognitive load bound)
  
Fortalezas:
  - Contextos nuevos sin precedente
  - Decisiones éticas complejas
  - Resolución ambigüedad irreducible
  
Límites:
  - Volumen (no escala >100 casos/día)
  - Consistencia (fatiga, sesgos)
  - Velocidad (vs ms response algorítmica)
```

**A2. Actor Algorítmico**

```yaml
Características:
  Juicio: Limitado (contextos conocidos, patrones entrenados)
  Velocidad: ms (microsegundos en casos)
  Escala: Infinita (paralelizable)
  
Fortalezas:
  - Volumen masivo (millones transacciones/seg)
  - Consistencia 24/7 (sin fatiga)
  - Velocidad extrema
  
Límites:
  - Contextos nuevos (out-of-distribution)
  - Decisiones éticas sin precedente
  - Explicabilidad causal (black box risk)
  
Restricción_Fundamental:
  Todo agente algorítmico opera bajo delegación explícita
  humano meta-nivel (A3, P1, P8). Ver CORE/04_Delegacion.md
```

### Composición Híbrida

Actor Humano + Actor Algorítmico → **Sistema de Delegación** (M1-M6), no "actor híbrido indivisible" (viola A2).

## §2. FLUJO — Secuencia de Transformaciones

### Definición

Secuencia ordenada que convierte entradas en salidas mediante pasos ejecutados por actores.

### Estructura

```yaml
Flujo = Secuencia(Pasos)

Paso:
  accion: String                    # Qué se hace
  actor: Actor                      # Quién ejecuta
  input: Set(Dato | Señal)          # Qué consume
  output: Set(Dato | Señal)         # Qué produce
  condiciones: Set(Predicado)       # Cuándo ejecuta
  duracion: Tiempo                  # Cuánto tarda
```

### Tipología

| Tipo | Predictibilidad | Automatización | Ejemplos |
|------|----------------|----------------|----------|
| **Estructurado** | Alta (pasos predefinidos) | Alta | Workflows, pipelines CI/CD |
| **Semi-estructurado** | Media (orden variable) | Media | Diagnósticos médicos, debugging |
| **No-estructurado** | Baja (pasos emergentes) | Baja | Investigación, diseño creativo |

## §3. SEÑAL — Impulso Disparador

### Definición

**Impulso atómico y transitorio que notifica evento significativo, diseñado para disparar acción inmediata.**

### Propósito vs Dato

| Dimensión | Señal | Dato |
|-----------|-------|------|
| **Intención** | Iniciar acción (trigger) | Informar acción (knowledge) |
| **Ciclo de vida** | Efímera (consumida) | Persistente (almacenada) |
| **Contenido** | Mínimo (notificación) | Rico (registro completo) |
| **Timing** | Precede (t0) | Sigue (t1+) |
| **Completitud** | Deliberadamente incompleta | Schema completo validado |

**Relación temporal:** Señal → conversación/refinamiento → Dato formal.

**Ortogonalidad:** Responsabilidades distintas con acoplamiento temporal permitido (Señal inicia; Dato informa y persiste). No viola I2.

### Analogía

- **Señal:** Sonido del trueno (te hace buscar refugio inmediatamente)
- **Dato:** Informe meteorológico completo (temperatura, humedad, presión)

El trueno notifica evento (tormenta), no es el informe completo.

### Tipos

- **Request:** Demanda externa (customer ticket, support request)
- **Event:** Suceso disparador (webhook, sensor trigger, system event)
- **Story:** Necesidad usuario (user story, job story)
- **Alert:** Condición anormal (monitoring alert, SLA breach)

### Propiedades

```yaml
origen: {Externo, Interno}
urgencia: {Inmediata, Normal, Baja}
claridad: {Alta, Baja}        # Baja → requiere refinamiento
```

### Ejemplos

```yaml
Señal_1:
  tipo: Story
  contenido: "Como cliente quiero guardar dirección para checkout rápido"
  timing: t0 (captura esencia problema)
  
Señal_2:
  tipo: Alert
  contenido: "Error rate >5% en payments API"
  urgencia: Inmediata
  
Señal_3:
  tipo: Event
  contenido: "Order_Created (order_id: 12345)"
  origen: Externo (webhook)
```

## §4. DATO — Información Estructurada con Semántica

### Definición

Información que representa estado del mundo con significado explícito, estructura definida y trazabilidad.

### Propiedades Críticas

```yaml
Semántica: Significado explícito (no raw bytes)
Estructura: Schema definido (validable)
Linaje: Trazabilidad origen y transformaciones (I3)
Calidad: Score 0-100 (completitud, precisión, consistencia, actualidad)
```

### Tipos

| Tipo | Estructura | Queryable | Ejemplos |
|------|-----------|-----------|----------|
| **Estructurado** | Schema rígido | Alta | SQL, JSON+schema, Parquet |
| **Semi-estructurado** | Schema flexible | Media | JSON sin schema, XML, logs |
| **No-estructurado** | Sin schema | Baja (requiere NLP/CV) | Texto, imágenes, video, audio |

### Diferencia vs Señal

Señal evoluciona a Dato mediante refinamiento:

```
t0: Señal "Como usuario quiero X"
t1: Conversación (PO + Dev + QA elaboran detalles)
t2: Dato formal (Acceptance Criteria + API contract + tests)
```

## §5. LÍMITE — Restricción sobre Posibilidades

### Definición

Constraint que reduce espacio de opciones válidas.

### Tipología

| Tipo | Fuente | Modificabilidad | Ejemplos |
|------|--------|-----------------|----------|
| **Físico** | Naturaleza | Inmutable | Velocidad luz, tiempo, entropía |
| **Regulatorio** | Leyes/normas | Baja (requiere cambio legal) | GDPR, SOX, HIPAA, PSD2 |
| **Organizacional** | Políticas internas | Alta | Tech stack, WIP limits, RACI |
| **Económico** | Budget/ROI | Media | Presupuesto, TCO, payback |
| **Técnico** | Capacidades actuales | Media | Escalabilidad DB, context window LLM |

### Estrategias Gestión

```
Aceptar:     Límite inevitable → diseñar alrededor
Mitigar:     Reducir impacto (ej: cache para latencia)
Eliminar:    Cambiar contexto (ej: cambiar regulación via lobby)
Excepción:   Override puntual con aprobación
Transformar: Convertir límite en ventaja (ej: constraint breeds creativity)
```

## §6. ESTADO — Snapshot Temporal

### Definición

Snapshot completo del sistema en timestamp t.

### Estructura

```yaml
Estado(t):
  actores_activos: Set(Actor)              # Quiénes operan
  flujos_en_ejecucion: Set(Flujo_Instancia) # Qué está corriendo
  datos_vigentes: Set(Dato)                # Información actual
  recursos_disponibles: Set(Recurso)       # Capacidades disponibles
  health_score: Float[0,100]               # Salud organizacional
  timestamp: DateTime                      # Cuándo se capturó
```

### Transiciones y Eventos

**Evento NO es primitivo.** Es el mecanismo de cambio entre estados:

```
Estado(t0) --[Evento: "Compra Realizada"]--> Estado(t1)
```

Propiedades:

- **Evento:** Instantáneo (punto en tiempo)
- **Estado:** Duración (intervalo temporal)
- **Señal:** Notifica que Evento ocurrió para que Actor reaccione

## §7. RECURSO — Capacidad Habilitadora

### Definición

Capacidad tangible/intangible que permite a actores ejecutar flujos.

### Tipología

| Tipo | Naturaleza | Agotabilidad | Ejemplos |
|------|-----------|--------------|----------|
| **Tangible** | Físico | Finito | Infraestructura, hardware, instalaciones |
| **Intangible** | Digital/IP | Replicable | Software, datos, conocimiento, marcas |
| **Humano** | Tiempo + skills | Finito | Desarrolladores, diseñadores, managers |
| **Temporal** | Tiempo | Finito no-recuperable | Deadlines, ventanas oportunidad |
| **Financiero** | Capital | Finito renovable | Presupuesto, inversión, cash flow |

### KPIs

```yaml
Utilization: % uso / disponible         # Target 70-85% (no 100% - buffer)
Availability: % disponible cuando needed # Target >99% para críticos
TCO: Costo total vida útil              # CAPEX + OPEX + End-of-Life
```

## §8. COMPOSICIÓN — UNIDAD DE TRABAJO

### Estructura Completa

```yaml
Unidad_Trabajo:
  
  # BOUNDARY IN (qué entra)
  señales_input: Set(Señal)              # Disparadores (events, requests)
  datos_input: Set(Dato)                 # Información consumida (requirements)
  
  # CAPACIDADES INTERNAS (cómo opera)
  actores: Set(Actor)                    # ≥1 - Quiénes ejecutan
  flujos: Set(Flujo)                     # ≥1 - Qué procesos
  recursos: Set(Recurso)                 # ≥1 - Con qué capacidades
  
  # BOUNDARY OUT (qué sale) — OUTSIDE-IN (P3)
  outputs: Set(Producto_Servicio)        # ≥1 - Valor entregado
  destinatarios: Set(Destinatario)       # ≥1 - Para quiénes
  
  # CONTEXTO OPERACIONAL (fuerzas externas)
  limites: Set(Limite)                   # Constraints
  entorno: Set(Factor_Ambiental)         # Fuerzas mercado/competencia
  
  # EVOLUCIÓN TEMPORAL
  estados: Secuencia(Estado)             # ≥2 (inicio, fin mínimo)
```

**Perspectiva Outside-In (P3):** Primero definir outputs + destinatarios; luego diseñar estructura interna.

### Elementos Boundary-Spanning

**Producto_Servicio** (output tangible/intangible):

```yaml
Atributos:
  nombre: String
  tipo: {Tangible, Intangible, Servicio, Paquete}
  valor_entregado: String                # Outcome para destinatario
  metricas_valor: Set(KPI)               # Cómo se mide valor
```

**Destinatario** (quién consume):

```yaml
Tipos:
  - Cliente_Externo: Fuera organización
  - Cliente_Interno: Otro equipo/departamento
  - Stakeholder: No consume directamente (regulador, inversor)
  
Atributos:
  segmento: String
  necesidad_satisfecha: String           # Job-to-be-done
  criticidad: {Alta, Media, Baja}
```

**Factor_Ambiental** (fuerza externa):

```yaml
Categorías:
  - Competencia: Alternativas disponibles
  - Regulacion: Leyes, normas obligatorias
  - Mercado: Tendencias demanda, preferencias
  - Tecnologia: Disrupciones tech emergentes
  - Demografia: Cambios población, geografía
  
Atributos:
  impacto: {Positivo, Neutral, Negativo}
  urgencia: {Inmediata, Corto_Plazo, Largo_Plazo}
```

**Nota:** Estos NO son primitivos (no violan I1). Son estructuras compuestas que formalizan perspectiva Outside-In.

## §9. EJEMPLO COMPLETO

```yaml
Unidad_Trabajo: "Customer Support Automation"

# OUTSIDE-IN: Outputs primero
outputs:
  - nombre: "FAQ Resolution Automatizada"
    valor_entregado: "60% consultas sin humano, <30s response"
    metricas_valor: [Resolution_Rate, Response_Time, CSAT]

destinatarios:
  - tipo: Cliente_Externo
    segmento: "Enterprise customers (>500 usuarios)"
    criticidad: Alta
  - tipo: Cliente_Interno
    segmento: "Support Agents (20 personas)"
    criticidad: Alta

# Contexto externo
entorno:
  - categoria: Competencia
    descripcion: "Zendesk Answer Bot (40% resolution)"
    impacto: Negativo
  - categoria: Tecnologia
    descripcion: "GPT-4 (responses contextuales high-quality)"
    impacto: Positivo

# Estructura interna diseñada para entregar outputs
actores:
  - LLM_Agent (M4 delegation)
  - Support_Agent_Humano (escalation)

flujos:
  - Receive customer question → Classify intent (LLM) →
    Retrieve docs (vector DB) → Generate response (LLM) →
    Validate quality >0.8 → Send | Escalate if <0.8

recursos:
  - OpenAI API (LLM)
  - Pinecone (vector DB)
  - Slack (escalation)

señales_input:
  - Customer question (chat/email)

datos_input:
  - Knowledge base (500 docs)
  - Historical resolutions

limites:
  - Budget: $5K/mes
  - Latency: <30s
  - Accuracy: CSAT >4.0/5.0
```

Ver `REFERENCIA/R1_Casos.md` para más ejemplos completos.

## §10. PRUEBAS DE IRREDUCIBILIDAD

### Test Eliminación

```
∀ P ∈ {Actor, Flujo, Señal, Dato, Límite, Estado, Recurso}:
  eliminar(P) → ∃ organización O que no puede representarse
```

**Ejemplo:** Eliminar Señal → No puedes modelar sistemas event-driven donde evento existe pero aún no se procesó/persistió.

### Test Reducción

```
¿P puede expresarse como f(otros_primitivos)?

Actor = Flujo que decide?               → NO (autonomía ≠ secuencia)
Flujo = Actores secuenciados?           → NO (transformación ≠ agentes)
Señal = Dato sin estructura?            → NO (impulso ≠ registro)
Dato = Estado?                          → NO (información ≠ snapshot completo)
Límite = Dato constraint?               → NO (restricción ≠ representación)
Estado = Dato + timestamp?              → NO (snapshot sistema ≠ dato individual)
Recurso = Actor pasivo?                 → NO (capacidad ≠ agencia)
```

**Conclusión:** 7 primitivos mínimos e irreducibles ✅

## §11. VALIDACIÓN FORMAL

Ver `CORE/07_Validacion.md` para pruebas completas:

- **Completitud:** Todo modelable con 7 primitivos
- **Minimalidad:** Nada eliminable sin pérdida capacidad
- **Ortogonalidad:** Sin overlaps de responsabilidad
- **Consistencia:** Sin contradicciones internas

## Referencias Cruzadas

- **Manifiesto (I1-I3, A1-A5, P1-P9):** `CORE/00_Manifiesto.md`
- **Ciclo SDA (uso primitivos):** `CORE/02_Ciclo_Fundamental.md`
- **Dominios (agrupación primitivos):** `CORE/03_Arquitectura.md`
- **Delegación (Actor Algorítmico):** `CORE/04_Delegacion.md`
- **Casos aplicados:** `REFERENCIA/R1_Casos.md`
- **Glosario:** `REFERENCIA/R5_Glosario.md`

**Fin 01_Primitivos v2.0.0**
