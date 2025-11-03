# R4: Preguntas Frecuentes (FAQ)

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Todos

---

## §1. PREGUNTAS GENERALES

**P1: ¿Qué es KERNEL en una frase?**
> R: Es un sistema operativo para construir organizaciones adaptativas que aprenden y evolucionan, con un enfoque nativo en la colaboración entre humanos y agentes de IA.

**P2: ¿Es KERNEL otro framework de agilidad o de arquitectura empresarial?**
> R: No exactamente. Es un meta-framework que integra conceptos de arquitectura, agilidad, SRE y IA en un modelo coherente. No reemplaza a Scrum o TOGAF, sino que los organiza y les da un propósito sistémico. (Ver `R3_Comparacion_Frameworks.md`).

**P3: ¿Para qué tipo de organización es KERNEL?**
> R: Es ideal para organizaciones que operan en entornos de alta incertidumbre y que necesitan adaptarse rápidamente. Es particularmente potente para empresas de tecnología, transformaciones digitales y cualquier organización que busque integrar la IA de manera fundamental, no superficial.

**P4: ¿Cuánto tiempo se tarda en implementar KERNEL?**
> R: Depende del H_Score inicial. Una transformación completa puede tomar de 12 a 36 meses. Sin embargo, se pueden obtener beneficios incrementales desde los primeros 3 meses, por ejemplo, mejorando la observabilidad (`D2`) o la estructura de equipos (`D1`). (Ver `T10_Roadmap.md`).

---

## §2. PREGUNTAS SOBRE CONCEPTOS CORE

**P5: ¿Por qué 7 primitivos? ¿No son demasiados/pocos?**
> R: Los 7 primitivos (Actor, Flujo, Dato, Señal, Límite, Estado, Recurso) son el conjunto mínimo e irreducible necesario para describir cualquier sistema socio-técnico. Menos primitivos perderían poder expresivo; más primitivos introducirían redundancia.
>
> **Señal** (agregado v1.1) distingue disparadores/placeholders (user stories, eventos, alerts) de registros formales completos (Dato). Esta distinción es crítica para modelar la progresión natural: Señal → Conversación → Dato.
>
> (Ver `CORE/07_Validacion.md` y `CORE/01_Primitivos.md` §3A).

**P6: ¿Qué es el ciclo Sense-Decide-Act (SDA)?**
> R: Es el "latido" de una organización KERNEL. Es un ciclo de feedback continuo donde el sistema:
>
> 1. **Percibe (Sense):** Observa su estado y el del entorno.
> 2. **Decide (Decide):** Planifica qué hacer a continuación.
> 3. **Actúa (Act):** Ejecuta la acción y modifica su estado o el del entorno, generando nueva información para el siguiente ciclo.

**P7: ¿Qué es el H_Score?**
> R: Es el "Health Score" o Puntuación de Salud Organizacional. Es una métrica de 0 a 100 que evalúa la madurez de una organización en los 4 dominios de KERNEL. Un H_Score por debajo de 45 indica un riesgo crítico y la necesidad de estabilización antes de intentar una transformación a gran escala. (Ver `A3_Diagnostico.md`).

**P8: ¿Qué significa que la IA sea "nativa" en KERNEL?**
> R: Significa que la IA no se ve como una herramienta externa o un proyecto aislado. Los agentes de IA son considerados "Actores" de primera clase, al mismo nivel que los humanos. El framework está diseñado desde la base para la colaboración Humano-IA, a través de conceptos como la Matriz de Delegación (`T07`) y el modelo de Smartness (`CORE/05`).

---

## §3. PREGUNTAS SOBRE IMPLEMENTACIÓN

**P9: ¿Necesito una herramienta de software específica para implementar KERNEL?**
> R: No es estrictamente necesario para empezar, pero es altamente recomendable para escalar. Se puede empezar con herramientas existentes (Jira, Confluence, etc.), pero para lograr un "gemelo digital" dinámico, se necesita una plataforma que implemente las 20 capacidades definidas en `R2_Capacidades_Plataforma.md`.

**P10: ¿Por dónde empiezo?**
> R: El primer paso es siempre un diagnóstico. Usa la guía de entrevistas (`T05_Assessment.md`) para calcular el H_Score inicial de tu organización. Esto te dirá dónde están tus mayores debilidades y te permitirá crear un roadmap de transformación enfocado. (Ver `T10_Roadmap.md`).

**P11: ¿Qué rol cumple un Arquitecto Empresarial en una organización KERNEL?**
> R: El rol evoluciona de ser un "planificador de ciudades" que crea mapas estáticos, a ser un "ingeniero de sistemas" que diseña y ajusta el sistema operativo de la organización. Se enfocan menos en documentar el estado actual y más en mejorar la capacidad de adaptación del sistema.

**P12: ¿Cómo se relaciona KERNEL con los OKRs?**
> R: Los OKRs son la implementación principal del dominio `D3_Decision`. Los Objetivos de la organización definen la dirección estratégica, y los Key Results se convierten en las métricas que el dominio `D2_Percepcion` debe monitorear. KERNEL le da un contexto sistémico al framework de OKRs. (Ver `T01_OKR.md`).

---

## §4. PREGUNTAS SOBRE ERRORES COMUNES

**P13: ¿Cuál es el error más común al adoptar KERNEL?**
> R: Intentar implementar todo a la vez. KERNEL es un framework grande y debe ser adoptado de forma incremental. El error es tratarlo como un proyecto con una fecha de fin, en lugar de un cambio continuo en la forma de operar.

**P14: ¿Se puede aplicar KERNEL solo al departamento de TI?**
> R: Es un mal comienzo. KERNEL es un framework para toda la organización. Aplicarlo solo a TI crea una "isla de agilidad" que inevitablemente chocará con la burocracia del resto de la empresa. La transformación debe ser liderada desde el negocio y abarcar todas las áreas.

**P15: ¿Qué pasa si mi H_Score es muy bajo (ej. < 30)?**
> R: No intentes una transformación a gran escala. Tu prioridad número uno es la estabilización. Enfócate en quick wins que reduzcan el caos y aumenten la visibilidad (ej. implementar observabilidad básica, clarificar roles críticos). Intenta subir el H_Score por encima de 45 antes de embarcarte en cambios estructurales profundos.

---

*Esta lista se actualizará a medida que surjan nuevas preguntas de la comunidad.*
