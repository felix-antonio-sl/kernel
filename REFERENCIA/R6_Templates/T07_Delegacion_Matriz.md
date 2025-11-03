# T07: Matriz de Delegación Humano-IA

**Propósito:** Definir y gobernar los niveles de autonomía de los agentes de IA en diferentes tareas.
**Audiencia:** AI Product Owners, Arquitectos, Líderes de Equipo, Equipos de Ética y Riesgo.

---

## 1. DIMENSIONES CLASIFICACIÓN AGENTES

*Basado en `CORE/04_Delegacion.md`, clasificamos agentes en dos dimensiones ortogonales:*

### Dimensión 1: PURPOSE (Rol del Agente)

- **Assistant:** Soporte conversacional, user asks → agent responds
  - *Ejemplo: ChatGPT responde preguntas, explica código*
- **Augmentation Tool:** Capacidad empaquetada que user controls interactively
  - *Ejemplo: AI image editor, grammar checker, code completion*
- **Orchestration Agent:** Coordina otros agents/systems, meta-level
  - *Ejemplo: CI/CD pipeline orchestrator, workflow engine*
- **Automation Agent:** End-to-end autónomo (Sense-Decide-Act loop)
  - *Ejemplo: Fraud detection, autoscaling, spam filter*

### Dimensión 2: AUTONOMY (Niveles M1-M6)

- **M1: IA Sugiere (Humano Decide y Ejecuta)**
  - La IA analiza y presenta opciones. El humano tiene control total.
  - *Ejemplo: Un agente que sugiere 3 posibles refactorizaciones para un bloque de código.*

- **M2: IA Sugiere, Humano Aprueba (IA Ejecuta)**
  - La IA propone una acción específica. El humano la aprueba con un clic, y la IA la ejecuta.
  - *Ejemplo: Un agente de Code Review que sugiere un fix y lo aplica automáticamente si el revisor humano comenta "@bot apply".*

- **M3: IA Actúa, Humano Revisa (Puede Revertir)**
  - La IA ejecuta la acción de forma autónoma, pero notifica al humano, quien puede revertirla fácilmente.
  - *Ejemplo: Un agente que refactoriza automáticamente código no crítico y abre un PR, que puede ser revertido si no es correcto.*

- **M4: IA Actúa, Humano Supervisa (Informa)**
  - La IA actúa de forma autónoma y solo informa al humano. La reversión es posible pero no trivial.
  - *Ejemplo: Un agente de CI/CD que escala automáticamente los runners de un pipeline y notifica al equipo de DevOps en Slack.*

- **M5: IA Actúa de Forma Autónoma (Humano en el Loop para Excepciones)**
  - La IA opera de forma totalmente autónoma. Solo involucra a un humano si encuentra una situación novedosa o de baja confianza.
  - *Ejemplo: Un agente de self-healing que resuelve el 95% de los incidentes de red y solo alerta a un SRE si el problema persiste después de 3 intentos.*

- **M6: IA Actúa de Forma Soberana (Sin Intervención Humana)**
  - La IA tiene autonomía total en un dominio bien definido y de bajo riesgo. Las decisiones no son reversibles por un humano.
  - *Ejemplo: Un agente que optimiza la asignación de precios en una subasta de anuncios en tiempo real.*

---

## 2. PLANTILLA DE LA MATRIZ DE DELEGACIÓN

*Esta matriz se debe completar para cada equipo o dominio de negocio.*

**Dominio:** [Ej: "Gestión de Infraestructura Cloud"]
**Equipo Owner:** [Ej: "Equipo SRE"]

| Tarea / Capacidad | Agente de IA | Purpose | Modo Actual | Modo Objetivo (Q+1) | Riesgo (1-5) | Guardarraíles Necesarios |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Provisionamiento de Recursos** | `TerraformBot` | Augment | **M2** (Sugiere plan, humano aplica) | **M3** (Aplica plan, humano revisa) | 3 (Medio) | - Plan debe ser validado por `checkov`.<br>- Reversión con `terraform destroy` documentada. |
| **Detección de Anomalías** | `MetricsWatcher` | Assistant | **M1** (Sugiere posibles anomalías) | **M1** (Sin cambios) | 2 (Bajo) | - Dashboard conversational con drill-down. |
| **Resolución de Incidentes** | `HealerBot` | Automate | **M3** (Resuelve incidentes conocidos) | **M5** (Resuelve todo, escala en excepciones) | 5 (Crítico) | - Solo opera en servicios no críticos (Tier 3).<br>- Escalado a humano si el MTTR supera los 15 min. |
| **Optimización de Costos** | `CostOptimizer` | Augment | **M1** (Sugiere instancias para redimensionar) | **M2** (Sugiere y aplica con aprobación) | 4 (Alto) | - Requiere aprobación del Tech Lead y FinOps.<br>- No aplica a bases de datos productivas. |
| **Code Review de Seguridad** | `SecurityScanner` | Assistant | **M4** (Comenta en PRs, informa) | **M4** (Sin cambios) | 2 (Bajo) | - Nunca bloquea el PR, solo informa. |

---

## 3. PROCESO DE GOBERNANZA

### Definición Inicial

1.  **Identificar Tareas:** Listar las tareas repetitivas, basadas en datos o que consumen mucho tiempo dentro de un dominio.
2.  **Evaluar Viabilidad de IA:** Determinar qué tareas son aptas para la automatización con IA.
3.  **Asignar Modo Actual:** Definir el nivel de autonomía inicial para cada agente, comenzando siempre por M1 o M2.
4.  **Evaluar Riesgo:** Analizar el impacto de un fallo del agente en cada tarea (financiero, reputacional, de seguridad).
5.  **Definir Guardarraíles:** Diseñar los mecanismos de seguridad necesarios para mitigar los riesgos identificados.

### Evolución del Modo de Delegación (Promoción de un Agente)

*Un agente no puede ser "promovido" a un nivel de autonomía superior sin un proceso formal.*

1.  **Propuesta de Promoción:** El equipo owner del agente propone moverlo de un modo a otro (ej. de M3 a M4).
2.  **Requisitos de Performance:** El agente debe cumplir con umbrales de éxito predefinidos durante al menos un trimestre.
    - *Ejemplo para `HealerBot`*: Debe haber resuelto con éxito >99% de los incidentes conocidos durante 3 meses, sin intervenciones humanas.
3.  **Revisión de Riesgo:** Se re-evalúa el riesgo para el nuevo modo de delegación.
4.  **Desarrollo de Nuevos Guardarraíles:** Se implementan los guardarraíles adicionales necesarios para el nuevo nivel de autonomía.
5.  **Aprobación Formal:** La promoción debe ser aprobada por un comité de IA y Riesgo (o el CTO en organizaciones más pequeñas).
6.  **Implementación Gradual:** El nuevo modo se despliega de forma controlada (ej. solo para un servicio, o durante horas de bajo tráfico) antes del rollout completo.

---

## CHECKLIST DE DELEGACIÓN SEGURA

☐ **Tarea bien definida:** El alcance de la tarea del agente es claro y limitado.
☐ **Métricas de éxito claras:** Se sabe cómo medir si el agente está haciendo un buen trabajo.
☐ **Riesgo evaluado:** Se ha cuantificado el impacto de un posible fallo.
☐ **Guardarraíles implementados:** Existen mecanismos de seguridad para contener los fallos.
☐ **Camino de escalado a humano:** Hay un proceso claro para cuando el agente falla o no está seguro.
☐ **Transparencia:** Los humanos entienden cuándo y por qué el agente está actuando.
☐ **Reversibilidad:** Las acciones del agente pueden ser deshechas (especialmente en modos M1-M3).

---

**Referencias:**
- CORE/04_Delegacion.md
- T09_AI_Agent_Design.md
