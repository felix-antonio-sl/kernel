# T06: AI Agent Design Template

**Versión:** 2.2.1  
**Última Actualización:** 2025-11-03  
**Compatibilidad:** KERNEL v2.2.x

**Propósito:** Diseñar y documentar agentes de IA que colaboran con equipos humanos.
**Audiencia:** AI/ML Engineers, Product Owners, Arquitectos.

---

## AGENT METADATA

```yaml
ID: [Agent-XXX]
Nombre: [Ej: "CodeReviewer", "IncidentCommander", "OnboardingBuddy"]
Versión: [1.0.0]
Owner: [Team/Persona responsable del agente]

# Purpose Dimension (CORE/04 §8)
Purpose: [Assistant | Augmentation Tool | Orchestration Agent | Automation Agent]
  # Assistant: Conversational support, user asks → agent responds
  # Augmentation Tool: Interactive capability user controls proactively
  # Orchestration Agent: Coordinates other agents/systems
  # Automation Agent: End-to-end autonomous (Sense-Decide-Act loop)

# Autonomy Level (CORE/04 §1-7)
Modo_Delegación: [M1 | M2 | M3 | M4 | M5 | M6]
  # M1 Monitor: Agent observes, human decides+acts
  # M2 Inform: Agent suggests, human validates+acts
  # M3 Enable: Agent acts, human can easily revert
  # M4 Control: Agent acts, human supervises
  # M5 Co-produce: Agent autonomous, human oversight for exceptions
  # M6 Execute: Agent fully autonomous in bounded domain

# Purpose × Autonomy Common Patterns:
  # Assistant typically M2-M3 (inform, enable)
  # Augment typically M3-M4 (enable, control)
  # Orchestrate typically M4-M5 (control, co-produce)
  # Automate typically M5-M6 (co-produce, execute)
```

---

### 1. Misión (Job to Be Done)

*¿Qué problema resuelve este agente para su equipo humano? ¿Cuál es su propósito principal en una frase?*

**Ejemplo (CodeReviewer):**
```yaml
Purpose: Augmentation Tool
Modo_Delegación: M3 (Enable)
Rationale: Tool augments reviewer capability by automating routine checks.
          Human reviews suggestions and can easily ignore/override.
```

> Acelerar el ciclo de code review automatizando la detección de errores comunes, violaciones de estilo y vulnerabilidades de seguridad, permitiendo a los revisores humanos centrarse en la lógica de negocio y el diseño arquitectónico.

---

### 2. Capacidades (Skills)

*¿Qué tareas específicas puede realizar el agente?*

**Ejemplo (CodeReviewer):**
- **C1: Análisis Estático:** Detectar anti-patrones de código, complejidad ciclomática alta, y violaciones de DRY.
- **C2: Revisión de Estilo:** Validar el cumplimiento de la guía de estilo del lenguaje (ej. PEP8 para Python).
- **C3: Detección de Secretos:** Escanear en busca de claves de API, contraseñas y otros secretos hardcodeados.
- **C4: Análisis de Dependencias:** Alertar sobre la adición de dependencias nuevas o vulnerables (usando `snyk`).
- **C5: Estimación de Impacto de Test:** Sugerir qué tests unitarios o de integración son más relevantes para los cambios en el PR.
- **C6: Generación de Resumen:** Escribir un resumen en lenguaje natural de los cambios propuestos en el PR para facilitar la revisión.

---

### 3. Interfaz y Disparadores (Triggers)

*¿Cómo y cuándo interactúa el agente con los humanos y otros sistemas?*

- **Disparador Principal:** Se activa automáticamente cuando se abre un nuevo Pull Request en GitHub.
- **Interacción Humana:**
  - Publica comentarios en el PR, etiquetando el código relevante.
  - Puede ser invocado manualmente en un comentario con `@CodeReviewer re-run`.
  - Envía un resumen al canal de Slack del equipo (`#team-checkout-prs`).
- **Interacción Sistema:**
  - Lee el contenido del PR desde la API de GitHub.
  - Ejecuta herramientas de linting y seguridad en un contenedor efímero.
  - Escribe resultados en la API de GitHub (comentarios, status checks).

---

### 4. Modelo y Datos (Cerebro)

*¿Qué modelos de IA y fuentes de datos utiliza el agente?*

- **Modelo Principal:** `GPT-4` para resumen de PRs y sugerencias de refactorización.
- **Modelos Secundarios:**
  - `CodeLlama-7b` para análisis de complejidad.
  - Modelos de clasificación de `scikit-learn` para estimación de impacto de tests.
- **Fuentes de Datos para Fine-Tuning:**
  - Historial de 10,000 PRs anteriores de la compañía.
  - Comentarios de revisión de ingenieros senior para aprender el estilo de feedback.
  - Base de datos de vulnerabilidades de `snyk` y `OWASP`.
- **Prompt Engineering:**
  - Prompts estructurados con ejemplos few-shot para garantizar consistencia.
  - Cadena de prompts: Resumir -> Analizar -> Sugerir.

---

### 5. Guardarraíles y Escalado (Safety & Reliability)

*¿Cómo nos aseguramos de que el agente no cause daño y cómo manejamos los errores?*

- **Guardarraíl 1 (Falsos Positivos):** El agente nunca bloquea un PR automáticamente. Todas sus sugerencias son no-vinculantes y requieren aprobación humana.
- **Guardarraíl 2 (Tono):** El prompt del modelo está diseñado para ser constructivo y colaborativo, nunca crítico. (Ej: "Una sugerencia a considerar..." en lugar de "Error: ...")
- **Escalado a Humano:** Si el agente no entiende una pieza de código o tiene baja confianza, etiqueta automáticamente a un Tech Lead senior para una revisión manual.
- **Monitoreo:**
  - **Precisión:** Se mide el ratio de aceptación de sus sugerencias por parte de los humanos.
  - **Latencia:** El tiempo de ejecución del agente no debe superar los 2 minutos.
  - **Costo:** Se monitorea el consumo de tokens de la API de OpenAI.

---

### 6. Métricas de Éxito (KPIs)

*¿Cómo sabremos si el agente está aportando valor?*

- **KR1: Reducción del Tiempo de Ciclo de PR:** De 48 horas a 24 horas en 3 meses.
- **KR2: Reducción de Comentarios Humanos sobre Estilo/Errores:** De 8 por PR a 2 por PR.
- **KR3: Aumento de la Tasa de Aceptación de Sugerencias del Agente:** De 40% a 75%.
- **KR4: Reducción de Bugs Post-Deploy:** Relacionados con cambios en PRs revisados, de 3/mes a <1/mes.

---

### CHECKLIST DE DISEÑO DE AGENTE

☐ **Misión Clara:** El "Job to Be Done" es específico y valioso.
☐ **Capacidades Definidas:** Las skills son concretas y medibles.
☐ **Interfaz Intuitiva:** La interacción humano-agente es fluida y predecible.
☐ **Guardarraíles Robustos:** Existen mecanismos para prevenir errores y daños.
☐ **Escalado a Humano:** Hay un camino claro cuando el agente falla o no está seguro.
☐ **KPIs Medibles:** El éxito del agente se puede cuantificar.
☐ **Modo de Delegación Correcto:** El nivel de autonomía (M1-M6) es apropiado para la tarea.

---

**Referencias:**
- CORE/04_Delegacion.md
- A1_Patrones.md (Patrones de IA)