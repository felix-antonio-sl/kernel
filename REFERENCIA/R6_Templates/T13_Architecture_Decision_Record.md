# T13: Architecture Decision Record (ADR) Template

**Versión:** 2.2.1  
**Última Actualización:** 2025-11-03  
**Compatibilidad:** KERNEL v2.2.x

**Propósito:** Documentar decisiones de arquitectura importantes de forma asíncrona.
**Audiencia:** Arquitectos, Tech Leads, Ingenieros Senior.

---

## ADR-XXXX: [Título de la Decisión]

- **Status:** [Propuesto | Aceptado | Rechazado | Obsoleto]
- **Fecha:** [YYYY-MM-DD]
- **Owners:** [Nombres de los principales proponentes]

---

### 1. Contexto

*¿Cuál es el problema que estamos tratando de resolver? ¿Cuáles son las restricciones y los requisitos?*

**Ejemplo:**
> El servicio de autenticación actual es un monolito que se ha vuelto un cuello de botella. No escala independientemente y cualquier cambio requiere un deploy completo de la aplicación principal. Necesitamos una solución que permita al equipo de identidad iterar más rápido y que pueda servir a múltiples aplicaciones cliente con alta disponibilidad.

---

### 2. Decisión

*¿Qué hemos decidido hacer?* Ser claro y conciso.

**Ejemplo:**
> Hemos decidido extraer el servicio de autenticación del monolito principal y reconstruirlo como un microservicio independiente, escrito en Go. Se comunicará con el resto del sistema a través de gRPC y tendrá su propia base de datos PostgreSQL.

---

### 3. Opciones Consideradas

*¿Qué otras opciones se evaluaron?* Es importante mostrar que se hizo una evaluación rigurosa.

#### Opción A: Mantener el Módulo en el Monolito (Status Quo)

- **Pros:**
  - No requiere esfuerzo de migración.
  - Menos complejidad operacional a corto plazo.
- **Contras:**
  - No resuelve el problema de escalabilidad.
  - Mantiene el acoplamiento y la baja velocidad de desarrollo.

#### Opción B: Reconstruir como Microservicio en Go (La opción elegida)

- **Pros:**
  - Escalabilidad independiente.
  - Despliegue autónomo, permitiendo iteración rápida.
  - Go es ideal para servicios de red de alta concurrencia.
  - Fomenta el ownership del equipo de identidad.
- **Contras:**
  - Mayor complejidad operacional (nueva base de datos, nuevo servicio que monitorear).
  - Esfuerzo de migración inicial (estimado: 3 meses, 4 ingenieros).

#### Opción C: Usar un Proveedor de Identidad de Terceros (ej. Auth0, Okta)

- **Pros:**
  - Solución gestionada, reduce la carga operacional.
  - Features de seguridad avanzadas out-of-the-box.
- **Contras:**
  - Costo significativo y dependencia de un tercero (vendor lock-in).
  - Menos flexibilidad para lógicas de negocio de autenticación personalizadas que necesitamos.
  - Riesgos de seguridad si el proveedor es comprometido.

---

### 4. Consecuencias

*¿Cuáles son los resultados, tanto positivos como negativos, de tomar esta decisión?*

- **Positivas:**
  - El equipo de identidad podrá desplegar cambios diariamente en lugar de cada 3 semanas.
  - El servicio de autenticación podrá escalar para soportar el lanzamiento de nuestra nueva aplicación móvil.
  - Se establece un patrón (Strangler Fig) para extraer otros servicios del monolito en el futuro.
- **Negativas:**
  - Se introduce un nuevo lenguaje (Go) en nuestro stack tecnológico, lo que requiere capacitación.
  - El presupuesto de infraestructura aumentará en ~$5K/mes por la nueva base de datos y los nuevos pods de servicio.
  - Se requerirá un nuevo runbook y rotación on-call para este servicio.

---

### 5. Proceso de Decisión

*¿Quiénes participaron en la decisión y cómo se llegó a un consenso?*

- **Participantes:** Arquitectos, Tech Leads de los equipos de plataforma e identidad, VP de Ingeniería.
- **Proceso:**
  1. Se presentó el problema en el foro de arquitectura (2025-09-15).
  2. Se escribieron y compartieron documentos de diseño para las opciones B y C (2025-09-22).
  3. Se realizó una sesión de debate y votación. La opción B fue elegida con 8 de 10 votos (2025-09-29).
  4. El VP de Ingeniería dio la aprobación final (2025-09-30).

---

### CHECKLIST ADR

☐ **Problema claro:** El contexto explica bien el *porqué*.
☐ **Decisión concisa:** La decisión es fácil de entender.
☐ **Opciones evaluadas:** Se consideraron al menos 2-3 alternativas realistas.
☐ **Consecuencias honestas:** Se listan tanto los pros como los contras.
☐ **Proceso transparente:** Se documenta quién y cómo se decidió.
☐ **Formato Markdown:** Fácil de leer y versionar en Git.

---

**Referencias:**
- D1_Arquitectura.md
- P15_Strangler_Fig (A1_Patrones.md)
