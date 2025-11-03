# T08: AI Ethics Checklist

**Versión:** 2.2.1  
**Última Actualización:** 2025-11-03  
**Compatibilidad:** KERNEL v2.2.x

**Propósito:** Asegurar que los sistemas de IA se diseñen, construyan y operen de manera justa, transparente y responsable.
**Audiencia:** AI/ML Engineers, Product Owners, Equipos Legales y de Cumplimiento.

---

## INSTRUCCIONES

*Este checklist debe ser completado y revisado en tres momentos clave del ciclo de vida de un agente de IA:*

1.  **Fase de Diseño:** Antes de escribir la primera línea de código.
2.  **Fase de Pre-Lanzamiento:** Antes de que el sistema sea expuesto a usuarios reales.
3.  **Revisión Periódica:** Anualmente, o después de cualquier cambio significativo en el modelo o sus datos.

--- 

## CHECKLIST DE ÉTICA EN IA

**Agente de IA:** [Nombre del Agente]
**Fecha de Revisión:** [YYYY-MM-DD]
**Revisores:** [Nombres y Roles]

### 1. Equidad y Sesgo (Fairness & Bias)

☐ **Análisis de Datos de Entrenamiento:** ¿Se han auditado los datos de entrenamiento para detectar sesgos históricos (género, raza, edad, etc.)? ¿Qué técnicas se usaron (ej. análisis de distribución, métricas de paridad)?

☐ **Métricas de Equidad:** ¿Se están midiendo métricas de equidad (ej. `Demographic Parity`, `Equalized Odds`) para diferentes subgrupos de usuarios? ¿Cuáles son los umbrales aceptables?

☐ **Mitigación de Sesgo:** Si se detectó sesgo, ¿qué técnicas se están utilizando para mitigarlo (ej. re-sampling de datos, re-weighting, algoritmos adversarios)?

☐ **Impacto Diferencial:** ¿Podría el error del modelo afectar de manera desproporcionada a ciertos grupos de usuarios? (Ej. un error en un modelo de crédito tiene un impacto mayor en poblaciones vulnerables).

**Estado (Rojo/Amarillo/Verde):** [Color]
**Acciones Requeridas:** [Lista de acciones para abordar los puntos no cubiertos]

---

### 2. Transparencia y Explicabilidad (Transparency & Explainability)

☐ **Caja Negra vs. Caja Blanca:** ¿Es el modelo interpretable (ej. regresión logística, árbol de decisión) o una caja negra (ej. red neuronal profunda)?

☐ **Técnicas de Explicabilidad (XAI):** Si es una caja negra, ¿se están utilizando técnicas como LIME o SHAP para explicar las decisiones individuales del modelo?

☐ **Comunicación al Usuario:** ¿Se le informa al usuario de manera clara y sencilla que está interactuando con una IA? ¿Se le explica (en términos simples) cómo toma sus decisiones el sistema?

☐ **Trazabilidad de la Decisión:** ¿Podemos trazar una decisión específica del modelo hasta los datos que la influyeron y la versión del modelo que la tomó?

**Estado (Rojo/Amarillo/Verde):** [Color]
**Acciones Requeridas:** [Lista de acciones]

---

### 3. Privacidad y Gobernanza de Datos (Privacy & Data Governance)

☐ **Minimización de Datos:** ¿Estamos recolectando solo los datos estrictamente necesarios para el funcionamiento del modelo? ¿Podríamos lograr el mismo resultado con menos datos o datos menos sensibles?

☐ **Anonimización y PII:** ¿Se han anonimizado o pseudo-anonimizado los datos? ¿Se han eliminado todos los Datos de Identificación Personal (PII) innecesarios?

☐ **Consentimiento del Usuario:** ¿Los usuarios han dado su consentimiento explícito para el uso de sus datos de esta manera? ¿Es fácil para ellos retirar su consentimiento?

☐ **Seguridad de los Datos:** ¿Están los datos (tanto en reposo como en tránsito) debidamente encriptados y protegidos contra accesos no autorizados?

**Estado (Rojo/Amarillo/Verde):** [Color]
**Acciones Requeridas:** [Lista de acciones]

---

### 4. Confiabilidad y Seguridad (Reliability & Safety)

☐ **Robustez ante Ataques Adversarios:** ¿Se ha probado la resistencia del modelo a entradas maliciosas diseñadas para engañarlo (ej. `adversarial attacks`)?

☐ **Manejo de Incertidumbre:** ¿El modelo puede cuantificar su propia incertidumbre? ¿Qué hace el sistema cuando el modelo tiene baja confianza en su predicción?

☐ **Pruebas Rigurosas:** ¿El modelo ha sido probado en un amplio rango de escenarios, incluyendo casos de borde (edge cases) y escenarios de fallo del mundo real?

☐ **Monitoreo Continuo:** ¿Existen sistemas para monitorear el rendimiento del modelo en producción y detectar "model drift" (cuando el modelo se degrada con el tiempo)?

**Estado (Rojo/Amarillo/Verde):** [Color]
**Acciones Requeridas:** [Lista de acciones]

---

### 5. Responsabilidad y Recurso (Accountability & Recourse)

☐ **Propiedad Clara:** ¿Está claro qué equipo y qué persona son responsables del comportamiento del agente de IA en producción?

☐ **Camino de Escalado Humano:** Si un usuario se ve perjudicado por una decisión de la IA, ¿existe un proceso claro, rápido y accesible para que pueda apelar a un humano?

☐ **Impacto Social y Laboral:** ¿Se ha considerado el impacto del agente en los roles laborales existentes? ¿Existe un plan para la re-capacitación o re-asignación de los empleados afectados?

☐ **Cumplimiento Regulatorio:** ¿El sistema cumple con las regulaciones relevantes (ej. GDPR, AI Act de la UE)? ¿Ha sido revisado por el equipo legal?

**Estado (Rojo/Amarillo/Verde):** [Color]
**Acciones Requeridas:** [Lista de acciones]

---

## RESUMEN DE LA EVALUACIÓN

**Puntuación General de Riesgo Ético:** [Bajo / Medio / Alto / Crítico]

**Decisión:**
☐ **Aprobado para Producción:** Todos los checks están en verde.
☐ **Aprobado con Condiciones:** Algunos checks en amarillo. Las acciones requeridas deben completarse en [plazo].
☐ **Rechazado:** Uno o más checks en rojo. El sistema no puede pasar a la siguiente fase hasta que se resuelvan los problemas críticos.

**Justificación de la Decisión:** [Resumen de los principales riesgos y por qué se tomó esta decisión.]

**Firmas de Aprobación:**
- **Product Owner:** [Firma]
- **Tech Lead / AI Lead:** [Firma]
- **Legal / Compliance Officer:** [Firma]

---

**Referencias:**
- CORE/05_Smartness.md
- A1_Patrones.md (Patrones de IA Responsable)
