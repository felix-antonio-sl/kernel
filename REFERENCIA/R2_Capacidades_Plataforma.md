# R2: Capacidades de la Plataforma KERNEL

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Arquitectos Empresariales, CIOs, CTOs

---

## §1. PROPÓSITO

Este documento define las 20 capacidades funcionales que una plataforma de software de Arquitectura Empresarial (EA) debe tener para ser considerada "KERNEL-compliant". Sirve como una guía para evaluar herramientas existentes o para construir una plataforma interna.

El objetivo no es la herramienta en sí, sino usar la herramienta para implementar el **sistema operativo** KERNEL en la organización.

---

## §2. LAS 20 CAPACIDADES DE LA PLATAFORMA

*Las capacidades se agrupan por los 4 dominios de KERNEL.*

### Dominio D1: Arquitectura (5 Capacidades)

1. **C1: Repositorio de Primitivos:**
    - **Descripción:** Un inventario centralizado para todos los primitivos de KERNEL (Actores, Recursos, Flujos, etc.). Debe permitir crear, modificar y relacionar estos elementos.
    - **Mapeo KERNEL:** `CORE/01_Primitivos.md`

2. **C2: Modelador de Capacidades de Negocio:**
    - **Descripción:** Herramienta visual para crear y gestionar el mapa de capacidades de la organización (ver `T02_Capability_Map.md`).
    - **Mapeo KERNEL:** `D1_Arquitectura.md`

3. **C3: Visualizador de Trazabilidad:**
    - **Descripción:** Capacidad de generar grafos dinámicos que muestren la trazabilidad completa desde los objetivos hasta los recursos tecnológicos (ver `CORE/06_Trazabilidad.md`).
    - **Mapeo KERNEL:** `I3: Trazabilidad`

4. **C4: Catálogo de Patrones y Antipatrones:**
    - **Descripción:** Una base de conocimiento para documentar y reutilizar patrones de arquitectura y antipatrones comunes.
    - **Mapeo KERNEL:** `A1_Patrones.md`, `A2_Antipatrones.md`

5. **C5: Gestor de Estándares Tecnológicos:**
    - **Descripción:** Un registro de las tecnologías aprobadas, en evaluación o prohibidas en la organización (Tech Radar).
    - **Mapeo KERNEL:** `Recurso` (tipo: Tecnología)

### Dominio D2: Percepción (4 Capacidades)

6. **C6: Conectores de Datos (Integración):**
    - **Descripción:** APIs y conectores para ingestar datos automáticamente desde sistemas externos (Jira, GitHub, Datadog, Workday, etc.) y mantener el repositorio actualizado.
    - **Mapeo KERNEL:** `D2_Percepcion.md`

7. **C7: Motor de Métricas y KPIs:**
    - **Descripción:** Capacidad de definir, calcular y almacenar métricas clave (ej. H_Score, métricas DORA, Tech Debt Ratio).
    - **Mapeo KERNEL:** `A5_Medicion.md`

8. **C8: Creador de Dashboards:**
    - **Descripción:** Herramienta para construir y visualizar dashboards personalizados para diferentes audiencias (ejecutivos, managers, equipos).
    - **Mapeo KERNEL:** `T03_Health_Dashboard.md`

9. **C9: Motor de Alertas y Notificaciones:**
    - **Descripción:** Sistema para configurar alertas proactivas cuando las métricas cruzan umbrales predefinidos (ej. "Alertar si el H_Score de un dominio cae por debajo de 50").
    - **Mapeo KERNEL:** `D2_Percepcion.md` (Agentes Sensoriales)

### Dominio D3: Decisión (5 Capacidades)

10. **C10: Módulo de OKRs:**
    - **Descripción:** Herramienta para definir, alinear y dar seguimiento a los OKRs a nivel de organización, equipo e individuo.
    - **Mapeo KERNEL:** `D3_Decision.md`, `T01_OKR.md`

11. **C11: Gestor de Roadmaps y Programas:**
    - **Descripción:** Capacidad para crear roadmaps de transformación, agrupar iniciativas en programas y visualizar cronogramas.
    - **Mapeo KERNEL:** `T10_Roadmap.md`

12. **C12: Motor de Priorización:**
    - **Descripción:** Herramientas para priorizar iniciativas usando frameworks como RICE (Reach, Impact, Confidence, Effort) o WSJF (Weighted Shortest Job First).
    - **Mapeo KERNEL:** `D3_Decision.md`

13. **C13: Análisis de Escenarios (What-If):**
    - **Descripción:** Capacidad de simular el impacto de diferentes decisiones de inversión en el mapa de capacidades y los OKRs.
    - **Mapeo KERNEL:** `CORE/05_Smartness.md` (Decisión Simulada)

14. **C14: Gestor de Decisiones (ADRs):**
    - **Descripción:** Un repositorio para crear y gestionar Architecture Decision Records (ADRs).
    - **Mapeo KERNEL:** `T13_Architecture_Decision_Record.md`

### Dominio D4: Operación (6 Capacidades)

15. **C15: Gestor de Equipos y Topologías:**
    - **Descripción:** Herramienta para definir equipos, sus miembros, su misión y su tipo de topología (Stream-Aligned, Platform, etc.).
    - **Mapeo KERNEL:** `D4_Operacion.md`, `T04_Team_Charter.md`

16. **C16: Módulo de Diagnóstico y Assessments:**
    - **Descripción:** Capacidad para conducir assessments (ej. entrevistas, encuestas) y calcular automáticamente el H_Score.
    - **Mapeo KERNEL:** `A3_Diagnostico.md`, `T05_Assessment.md`

17. **C17: Workflow de Gobernanza:**
    - **Descripción:** Un motor de flujos de trabajo para automatizar procesos de gobernanza (ej. aprobación de nuevos estándares tecnológicos, revisión de ADRs).
    - **Mapeo KERNEL:** `D1_Arquitectura.md`

18. **C18: Plataforma de Colaboración:**
    - **Descripción:** Funcionalidades sociales como comentarios, notificaciones y wikis para facilitar la colaboración asíncrona.
    - **Mapeo KERNEL:** (Capacidad transversal)

19. **C19: API Extensible:**
    - **Descripción:** Una API completa que permite a los equipos extender la plataforma y construir sus propias automatizaciones sobre ella.
    - **Mapeo KERNEL:** (Capacidad transversal)

20. **C20: Gestor de Permisos y Roles (RBAC):**
    - **Descripción:** Control de acceso basado en roles para asegurar que los usuarios solo vean y modifiquen la información que les corresponde.
    - **Mapeo KERNEL:** (Capacidad transversal)

---

## §3. EVALUACIÓN DE HERRAMIENTAS (EJEMPLO)

*Esta tabla puede ser usada para evaluar proveedores de EA en el mercado.*

| Capacidad | Herramienta A (ej. LeanIX) | Herramienta B (ej. Ardoq) | Plataforma Interna |
| :--- | :--- | :--- | :--- |
| **C1: Repositorio** | ✅ Nativo | ✅ Nativo | ❌ Por construir |
| **C2: Mapa Capacidades** | ✅ Nativo | ✅ Nativo | ❌ Por construir |
| **C6: Conectores** | ✅ Extenso | 🟡 Limitado | ✅ Customizables |
| **C13: Simulación** | ❌ No Soportado | 🟡 Básico | ✅ Potencialmente |
| **C17: Workflow** | 🟡 Básico | ❌ No Soportado | ✅ Customizables |
| **...** | ... | ... | ... |

---

**Conclusión:** Una plataforma "KERNEL-compliant" no es solo un repositorio pasivo de diagramas. Es un **sistema operativo activo** que integra los 4 dominios para permitir una gestión adaptativa y basada en datos de la organización.
