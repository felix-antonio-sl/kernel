# 00_Manifiesto

**Versión:** 1.0.0  
**Estado:** Definitivo  
**Audiencia:** Todos

---

## §1. INVARIANTES NO NEGOCIABLES

Toda organización ejecutable debe satisfacer estas tres leyes fundamentales:

### I1. MINIMALIDAD

**Enunciado:** Todo elemento del sistema debe ser irreducible; eliminar cualquiera destruye capacidades.

**Prueba de violación:** Si puedes eliminar un componente sin perder funcionalidad, el sistema no es minimal.

**Consecuencia:** No agregar elementos "por si acaso". Cada primitivo, principio, dominio existe por necesidad lógica.

**Ejemplo:**

- ✅ Correcto: 7 primitivos (Actor, Flujo, Dato, Señal, Límite, Estado, Recurso) - cada uno irreducible
- ❌ Incorrecto: Agregar primitivo "Evento" cuando es composición de Estado + Flujo

---

### I2. ORTOGONALIDAD

**Enunciado:** Dominios funcionales sin overlap; cada responsabilidad tiene un único dueño.

**Prueba de violación:** Si dos componentes tienen responsabilidades que se intersectan, violas ortogonalidad.

**Consecuencia:** Claridad de responsabilidades, no duplicación de esfuerzos, trazabilidad unívoca.

**Ejemplo:**

- ✅ Correcto: Arquitectura define estructura, Percepción detecta estado, Decisión planifica, Operación ejecuta - sin overlaps
- ❌ Incorrecto: Arquitectura también "ejecuta cambios estructurales" - overlap con Operación

---

### I3. TRAZABILIDAD

**Enunciado:** Todo artefacto conecta propósito con valor entregado; no hay islas de información.

**Prueba de violación:** Si existe un elemento cuyo origen o impacto es desconocido, violas trazabilidad.

**Consecuencia:** Causalidad explícita, auditoría completa, decisiones basadas en evidencia.

**Ejemplo:**

- ✅ Correcto: Objetivo → Capacidad → Proceso → App → Dato → Tecnología → Control → Riesgo → Iniciativa → Valor
- ❌ Incorrecto: Aplicación sin traza a proceso que soporta, o proceso sin vínculo a objetivo estratégico

---

## §2. AXIOMAS OPERACIONALES

### A1. Unidad de Trabajo como Célula

**Axioma:** Toda organización se descompone en unidades de trabajo - sistemas mínimos que transforman entradas en salidas mediante coordinación de capacidades.

**Implicación:** No modelar "departamentos" o "áreas" como primitivos; modelar unidades de trabajo con entradas, salidas, actores, flujos.

---

### A2. Actor Dual

**Axioma:** Todo actor es humano O algorítmico; no existe actor "híbrido" indivisible.

**Implicación:** Colaboración humano-IA se modela como composición de actores, no como actor único con "inteligencia mixta".

---

### A3. Delegación Explícita

**Axioma:** Agentes algorítmicos solo operan mediante delegación de unidad de trabajo; no hay autonomía absoluta.

**Implicación:** Toda acción algorítmica tiene un responsable humano meta-nivel (principio P1).

---

### A4. Ciclo SDA Universal

**Axioma:** Toda acción organizacional atraviesa: Sense (detectar, comprender, proyectar) → Decide (directa, reglas, asociativa, analítica) → Act (planificar, especificar, ejecutar).

**Implicación:** No modelar "decisiones sin contexto" o "acciones sin decisión previa" - todo es ciclo completo o subciclo.

**Referencias:**

- Framework general: `CORE/02_Ciclo_Fundamental.md` (S1-S3, D1-D4, A1-A3)
- Operacionalización dominio-específica:
  - `DOMINIOS/D2_Percepcion.md` §5 (Niveles Awareness)
  - `DOMINIOS/D3_Decision.md` §6 (Modos Decisionales)
  - `DOMINIOS/D4_Operacion.md` §12 (Niveles Execution)

---

### A5. Evolución Continua

**Axioma:** Organizaciones evolucionan mediante combinación de cambio planificado (proyectos) y no planificado (adaptaciones/workarounds).

**Implicación:** No diseñar sistemas que asumen "implementación única perfecta" - diseñar para evolución incremental.

---

## §3. LOS 9 PRINCIPIOS

### P1. AUTORIDAD = RESPONSABILIDAD

**Definición:** Quien tiene autoridad para decidir debe asumir responsabilidad por las consecuencias.

**Corolario:** No delegar autoridad sin accountability. No asignar responsabilidad sin autoridad.

**Aplicación:**

- RACI tradicional viola esto: "Responsible" sin "Accountable" matching
- Solución KERNEL: Authority = Accountability siempre 1:1

**Test de violación:**

```
¿Quién decide X? → Persona A
¿Quién asume consecuencias de X? → Persona B (B ≠ A)
→ VIOLACIÓN P1
```

**Caso real:** Manager de sistemas-ingeniería reporta a 3 jefes diferentes (airline case). Autoridad fragmentada = responsabilidad diluida = 3 despidos.

---

### P2. ESPECIALIZACIÓN + COLABORACIÓN

**Definición:** World-class expertise en dominio específico + teamwork efectivo entre especialistas.

**Paradoja:** Necesitas silos (especialización profunda) y anti-silos (colaboración fluida) simultáneamente.

**Aplicación:**

- Building blocks especializados con interfaces claras
- Procesos cross-functional que conectan especialistas
- No generalistas mediocres, no silos incomunicados

**Test de violación:**

```
¿Hay especialistas sin procesos colaborativos? → Silos patológicos
¿Hay "equipos cross-funcionales" sin especialistas? → Mediocridad
→ VIOLACIÓN P2
```

**Solución:** Estructura matricial con dominios precisos + equipos temporales cross-functional.

---

### P3. OUTSIDE-IN

**Definición:** Entorno externo determina viabilidad; sensing antes que planning.

**Implicación:** Primero observar (clientes, competencia, mercado, restricciones), luego planificar.

**Aplicación:**

- 11 observables (8 externos + 3 internos)
- Sensores continuos, no análisis periódicos
- Estrategia emergente, no solo deliberada

**Test de violación:**

```
¿Roadmap definido sin analizar competencia/clientes? → Inside-out
¿Planificación anual sin feedback continuo mercado? → Inside-out
→ VIOLACIÓN P3
```

**Patrón:** EA Organism approach - outputs, inputs, environment primero; estructura después.

---

### P4. FLUJO CONTINUO

**Definición:** Activos que evolucionan continuamente, no proyectos con inicio/fin.

**Implicación:** Software-as-Asset, teams estables, reinversión continua, no "project closure".

---

#### Fundamento: Asset Decay

**Ley del decay:** Software decae si no evoluciona, porque el mundo alrededor cambia:

- **Regulación:** Nuevas leyes (GDPR, normativas sectoriales)
- **Expectativas usuario:** Lo que era "bueno" hace 2 años hoy es "inaceptable"
- **Tecnología:** Frameworks obsoletos, vulnerabilidades emergentes
- **Competencia:** Alternativas mejores aparecen continuamente

**Paradoja del éxito:** Software exitoso inicia su propio decay al cambiar comportamiento y expectativas de usuarios.

**Consecuencia:** Sistema "completado y congelado" pierde valor exponencialmente. En 2-3 años sin inversión, costo de cambio crece 10x vs mantenimiento continuo.

---

#### Daño del Project Thinking

**Project thinking** (anti-patrón) trata software como construcción temporal:

**Problema 1: Pérdida de conocimiento tácito**

- Equipos se disuelven al "completar" proyecto
- Conocimiento crítico no documentable se pierde
- Próxima iniciativa requiere ramp-up desde cero
- **Costo real:** 6-12 meses productividad perdida

**Problema 2: Scope cutting para cierre**

- Deadline proyecto fuerza recortar features para "terminar"
- Technical debt y defectos conocidos ignorados deliberadamente
- **Resultado:** Sistema deployed técnicamente frágil, incapaz de evolucionar

**Problema 3: Gaps entre proyectos**

- Tiempo sin funding entre "proyecto completado" y "siguiente proyecto aprobado"
- Durante gap: cero mantenimiento, decay acelerado, pérdida memoria institucional
- **Efecto acumulativo:** Cada gap amplifica el próximo

**Contraste:** Asset thinking provee funding OPEX continuo, equipos estables, evolución incremental sin fracturas.

---

#### Obliquity: Objetivos Complejos via Experimentación

**Principio:** Objetivos complejos raramente se logran mediante planes directos; emergen de experimentación iterativa.

**Razón:** Software convierte objetivos difusos en sistemas precisos. Esto requiere:

- Descubrir qué quiere realmente el usuario (no lo saben hasta ver working software)
- Explorar espacio de soluciones técnicas
- Adaptar a feedback y cambios de contexto

**Project thinking** asume objetivo claro desde inicio → plan detallado → ejecución rígida.  
**Asset thinking** permite objetivo evolutivo → experimentos → pivotes → convergencia gradual.

**Ejemplo:** Producto digital exitoso típicamente pivota 3-5 veces en primeros 2 años. Project model mata pivotes (scope bloqueado); asset model los habilita.

---

**Aplicación:**

- Equipos estables (ownership continuidad)
- Funding continuo (OPEX, no solo CAPEX)
- Despliegue frecuente (weekly/daily, no quarterly)
- Asset decay monitoreado (métricas health: tech debt score, deployment frequency, time-to-fix)
- No "completado y olvidado" (software vive en O&M perpetuo)

**Test de violación:**

```
¿Proyecto termina y equipo se disuelve? → Project thinking
¿Software "completado" sin plan mantenimiento? → Project thinking
¿Funding solo para "nuevos proyectos", no para evolución? → Project thinking
→ VIOLACIÓN P4
```

**Consecuencia:** Sin flujo continuo, debt técnica crece, velocity cae, costo de cambio explota, eventualmente sistema requiere rewrite total (10x más caro que mantenimiento continuo).

---

### P5. OUTCOMES SOBRE OUTPUTS

**Definición:** Medir resultados e impacto, no actividades o entregables.

**Diferencia:**

- Output: "Desarrollamos 10 features"
- Outcome: "Reducimos churn 15%, NPS +12 puntos"

**Aplicación:**

- OKRs outcome-focused (Key Results = métricas impacto)
- No medir "story points completados", medir "valor entregado"
- Vanity metrics vs actionable metrics

**Test de violación:**

```
KPI: "100% proyectos on-time on-budget" → Output
KPI: "Health Score >85, NPS >50, TTM <30 días" → Outcome
→ Primer KPI viola P5
```

**Patrón:** Time-value profiles - medir cuándo se captura valor, no cuándo se completa trabajo.

---

### P6. PROBABILÍSTICO

**Definición:** Planificar con incertidumbre explícita; forecasts con rangos, no commitments deterministas.

**Implicación:** No "prometemos entregar X en fecha Y"; sí "70% probabilidad entregar X entre Y1-Y2".

**Aplicación:**

- Velocity rolling average con desviación estándar
- Monte Carlo simulations para roadmaps
- No penalties por no cumplir estimaciones

**Test de violación:**

```
¿Compromisos rígidos sin buffer de incertidumbre? → Determinista
¿Penalizan por estimaciones incorrectas? → Determinista
→ VIOLACIÓN P6
```

**Consecuencia:** Commitments deterministas fuerzan shortcuts, deuda técnica, gaming del sistema.

---

### P7. PARSIMONIA

**Definición:** Mínimos elementos para máxima claridad; simplicidad como precondición, no aspiración.

**Navaja de Occam:** Entre dos modelos con igual capacidad explicativa, elegir el más simple.

**Aplicación:**

- 7 primitivos (no 10)
- 9 principios (no 15)
- 4 dominios (no 7)
- 35 documentos (no 150)

**Test de violación:**

```
¿Puedes eliminar elemento sin perder capacidad? → No parsimonioso
¿Dos elementos hacen lo mismo de formas distintas? → No parsimonioso
→ VIOLACIÓN P7
```

**Consecuencia:** Complejidad innecesaria aumenta fricción cognitiva, reduce adoption, genera errores.

---

### P8. HERRAMIENTA, NO ORÁCULO

**Definición:** Agentes algorítmicos son medios para fines humanos; humano siempre en control meta-nivel.

**Implicación:** No delegar decisiones críticas a IA sin supervisión; no tratar outputs IA como verdad absoluta.

**Aplicación:**

- 6 modos delegación (M1-M6) con escalation explícita
- Human-in/on/out-the-loop según criticidad
- Explicabilidad causal obligatoria (P9)

**Test de violación:**

```
¿IA decide autónomamente sin escape hatch humano? → Oráculo
¿Output IA no es cuestionable por humano? → Oráculo
→ VIOLACIÓN P8
```

**Patrón:** Copilot (M3) para tareas rutinarias, humano decide en ambigüedad/ética/novel contexts.

---

### P9. EXPLICABILIDAD CAUSAL

**Definición:** Todo agente algorítmico debe poder explicar "por qué" (causalidad), no solo "qué" (correlación).

**Diferencia:**

- Correlación: "Clientes con feature X tienen 20% más retention"
- Causalidad: "Feature X causa retention porque reduce friction en workflow crítico"

**Aplicación:**

- XAI (Explainable AI) obligatorio para decisiones críticas
- No cajas negras en compliance, contratación, medicina, finanzas
- Traces auditables de razonamiento algorítmico

**Test de violación:**

```
Humano: "¿Por qué recomendaste esto?"
IA: "Correlación 0.87 con objetivo" → Solo correlación
IA: "Feature X impacta Y porque análisis causal muestra Z" → Causalidad
→ Primera respuesta viola P9
```

**Tecnologías:** Causal AI, causal graphs, counterfactual explanations, SHAP/LIME con causalidad.

---

### P10. CULTURE AS EMERGENT PROPERTY

**Definición:** Cultura organizacional emerge de estructura y dynamics sostenidas; no puede diseñarse ni mandarse directamente.

**Mecánica de Emergencia:**

```
Estructura (roles, boundaries, authorities)
    ↓ crea
Incentivos (qué comportamientos se premian/castigan)
    ↓ guía
Comportamiento (acciones repetidas individuales)
    ↓ consolida
Cultura (normas colectivas, "cómo hacemos las cosas aquí")
```

**Feedback Loops:**

- **Positivo:** Buena estructura → dynamics efectivos → cultura sana → refuerza estructura
- **Negativo:** Mala estructura → dynamics disfuncionales → cultura tóxica → degrada estructura más

**Prohibición Fundamental:**

```
❌ "Vamos a cambiar la cultura a innovadora/colaborativa/customer-centric"
   → Mandato directo falla siempre

✅ "Vamos a cambiar estructura (P8 Entrepreneurship, P9 Avoid Conflicts)
    + dynamics (governance, feedback, incentivos)
    → Cultura emerge como resultado"
```

**Ejemplos Reales:**

```yaml
Caso_Blame_Culture:
  Síntoma: Staff no toma riesgos, no innova
  Causa_Root: Estructura penaliza errores (KPIs individuales, no team)
  Fix_Incorrecto: "Comunicar que errores son OK" (mandato cultural)
  Fix_Correcto: Cambiar metrics a team-level, implementar blameless postmortems
  Resultado: Cultura learning emerge orgánicamente

Caso_Silos_Culture:
  Síntoma: Departments no colaboran, "not my job" attitude
  Causa_Root: Estructura sin shared OKRs, handoff hell (viola P5 D1)
  Fix_Incorrecto: "Team building events" (superficie)
  Fix_Correcto: Rediseñar estructura cross-functional, shared OKRs
  Resultado: Cultura colaborativa emerge de necesidad estructural
```

**Test de violación:**

```
¿Intentas "culture change initiative" sin cambiar estructura/dynamics?
¿Esperas que "comunicación" o "training" cambien cultura?
¿CEO anuncia "nueva cultura" pero incentivos siguen igual?
→ VIOLACIÓN P10
```

**Implicación Temporal:** Culture emergence toma 6-18 meses post cambio estructural. Patience required.

**Conexión Invariantes:** P10 explica cómo I3 (Trazabilidad) funciona en práctica: cultura trazable a estructura y dynamics, no a discursos.

---

## §4. JERARQUÍA CONCEPTUAL

### Nivel 1: Invariantes (I1-I3)

**Inviolables.** Si violas un invariante, el sistema colapsa lógicamente.

### Nivel 2: Axiomas (A1-A5)

**Fundacionales.** Definen la realidad operacional; no son "opcionales".

### Nivel 3: Principios (P1-P10)

**Guías normativas.** Violarlos es posible pero contraproducente; generan deuda organizacional.

**Ejemplo de jerarquía:**

```
I3 (Trazabilidad) → Invariante
  ↓ requiere
A3 (Delegación Explícita) → Axioma
  ↓ requiere
P1 (Autoridad=Responsabilidad) → Principio
  ↓ requiere
P8 (Herramienta no Oráculo) → Principio
```

Si violas P8 (IA autónoma sin supervisión), eventualmente violas P1 (no hay humano accountable), luego A3 (delegación implícita), y finalmente I3 (no hay trazabilidad de decisiones).

---

## §5. TENSIONES ENTRE PRINCIPIOS

Los principios no siempre son armónicos; diseño organizacional es gestión de trade-offs.

### Tensión 1: P2 vs P4

**P2 (Especialización):** Requiere estabilidad para desarrollar expertise profundo.  
**P4 (Flujo continuo):** Requiere adaptabilidad y cambio constante.

**Resolución:** Stable teams (P2) con continuous evolution of practices (P4). Team membership estable, métodos/tech evolucionan.

---

### Tensión 2: P5 vs P6

**P5 (Outcomes):** Necesitas medir impacto real.  
**P6 (Probabilístico):** Outcomes tienen incertidumbre inherente.

**Resolución:** Medir outcomes con distribuciones, no puntos. "NPS entre 45-55 con 80% confianza", no "NPS = 50".

---

### Tensión 3: P7 vs P9

**P7 (Parsimonia):** Modelos simples.  
**P9 (Explicabilidad Causal):** Causalidad es compleja.

**Resolución:** Parsimonia en ontología (7 primitivos), complejidad en implementación (causal graphs complejos OK). Simplicidad conceptual ≠ simplicidad operacional.

---

### Tensión 4: P8 vs Eficiencia

**P8 (Humano en control):** Requiere supervisión, ralentiza.  
**Eficiencia operacional:** Automatización completa es más rápida.

**Resolución:** Escalation by exception. IA autónoma (M6) para rutina, humano-in-loop (M1-M3) para excepciones/criticidad. Definir triggers escalation explícitos.

---

## §6. REGLAS DE COMPOSICIÓN

### R1. Primitivos → Unidad de Trabajo

```
Unidad_Trabajo = f(Actores, Flujos, Datos, Límites, Estados, Recursos)

donde:
  Actores: {humanos, algorítmicos} ≠ ∅
  Flujos: secuencia(transformaciones) ≠ ∅
  Datos: información_estructurada con semántica
  Límites: restricciones sobre posibilidades
  Estados: snapshot(Actores, Flujos, Datos, Recursos, t)
  Recursos: capacidades_habilitadoras
```

**Propiedad:** Eliminar cualquier primitivo → Unidad de Trabajo indefinida.

---

### R2. Unidades de Trabajo → Dominio

```
Dominio ∈ {Arquitectura, Percepción, Decisión, Operación}

Arquitectura: Define(estructura, responsabilidades)
Percepción: Detecta(estado_interno, estado_externo)
Decisión: Planifica(cambio, priorización)
Operación: Ejecuta(flujos, valor)
```

**Propiedad:** Dominios ortogonales - `Responsabilidad(Di) ∩ Responsabilidad(Dj) = ∅` para i≠j.

---

### R3. Dominios → Organización

```
Organización = Sistema(
  estructura: Arquitectura,
  salud: Percepción,
  estrategia: Decisión,
  entrega: Operación,
  ciclo: SDA_loop(Sense, Decide, Act)
)
```

**Propiedad:** Organización ejecutable ↔ (I1 ∧ I2 ∧ I3) ∧ ∀i ∈ [1..9]: Pi satisfecho ≥ 70%.

---

## §7. CRITERIOS DE ÉXITO

### Completitud

Sistema es completo si puede representar cualquier configuración organizacional válida sin extensiones ad-hoc.

**Test:** ¿Puedes modelar tu organización actual usando solo KERNEL? Si necesitas "inventar" primitivos/principios, KERNEL no es completo.

---

### Consistencia

Sistema es consistente si no genera contradicciones internas.

**Test:** ¿Aplicar principios X e Y simultáneamente genera conflicto irresoluble? Si sí, sistema inconsistente.

---

### Operacionalidad

Sistema es operacional si permite pasar de modelo a implementación sin ambigüedades.

**Test:** ¿Puedes derivar acciones concretas desde conceptos KERNEL? Si modelo es "bonito pero inútil", no es operacional.

---

### Parsimonia

Sistema es parsimonioso si es minimal (I1) y ortogonal (I2).

**Test:** ¿Puedes eliminar elemento sin perder capacidad? Si sí, no es parsimonioso.

---

## §8. VALIDACIÓN DEL MANIFIESTO

### Prueba de Completitud

```
∀ organización O:
  KERNEL puede representar O ↔
    ∃ configuración C de (Primitivos, Principios, Dominios) tal que:
      modelo(C) ≅ O
```

**Verificado:** 10 casos en R1_Casos.md cubren sectores diversos (insurance, airline, university, ecommerce, gov, health, etc.).

---

### Prueba de Minimalidad

```
∀ elemento E ∈ KERNEL:
  eliminar(E) → ∃ organización O que no puede representarse
```

**Verificado:** Ver CORE/07_Validacion.md para pruebas formales.

---

### Prueba de Consistencia

```
¬∃ P_i, P_j ∈ Principios tal que:
  aplicar(P_i) ∧ aplicar(P_j) → contradicción_irresoluble
```

**Verificado:** Tensiones existen (§5) pero son resolubles mediante trade-offs.

---

## §9. ANTI-MANIFIESTO

Lo que KERNEL **NO** es:

### ❌ No es metodología prescriptiva

KERNEL no dice "debes usar Scrum", "debes usar SAFe", "debes usar TOGAF". Es agnóstico a metodologías.

### ❌ No es herramienta software

KERNEL no es Jira, Ardoq, ServiceNow. Es especificación que herramientas implementan.

### ❌ No es framework de certificación

No hay "KERNEL Certified Architect". Es conocimiento abierto.

### ❌ No es dogma

Violar principios no es "herejía", es decisión de diseño con consecuencias conocidas.

### ❌ No es completo por sí solo

KERNEL necesita complementarse con: prácticas específicas (Agile, DevOps), herramientas (EA platforms), contexto (sector, regulación).

---

## §10. EVOLUCIÓN DEL MANIFIESTO

**Versión 1.0.0** (2025-10-30): Versión inicial.

**Cambios permitidos:**

- ✅ Clarificaciones de lenguaje
- ✅ Ejemplos adicionales
- ✅ Correcciones de errores lógicos

**Cambios prohibidos sin incremento major version:**

- ❌ Cambiar invariantes (I1-I3)
- ❌ Agregar/eliminar primitivos
- ❌ Modificar principios fundamentales (P1-P10)

**Criterio de cambio major:** Si cambio rompe compatibilidad con modelos KERNEL existentes.

---

## Referencias Cruzadas

- **Primitivos detallados:** `CORE/01_Primitivos.md`
- **Arquitectura 4 dominios:** `CORE/03_Arquitectura.md`
- **Validación formal:** `CORE/07_Validacion.md`
- **Casos de aplicación:** `REFERENCIA/R1_Casos.md`
- **FAQ sobre principios:** `REFERENCIA/R4_FAQ.md` §2

---

**Fin del Manifiesto**
