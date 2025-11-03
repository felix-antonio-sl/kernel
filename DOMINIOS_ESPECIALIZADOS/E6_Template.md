# E6: Plantilla para Nuevo Dominio Especializado

**Versión:** 1.0.0 | **Estado:** Template | **Audiencia:** Arquitectos de Dominio, Expertos en la Materia

---

## §1. APLICACIÓN DE KERNEL AL DOMINIO DE [NOMBRE DEL DOMINIO]

*Instrucción: Comienza describiendo el dominio en 1-2 frases. ¿Cuáles son sus características únicas? (ej. alta regulación, velocidad extrema, sistemas físicos, etc.).*

> **Ejemplo:** Este documento adapta KERNEL al dominio de [la logística de última milla, caracterizado por su complejidad geoespacial, la optimización en tiempo real y la gestión de una fuerza laboral distribuida].

### Mapeo de Primitivos a Conceptos de [NOMBRE DEL DOMINIO]

*Instrucción: Completa la siguiente tabla. Es el paso más importante para traducir KERNEL a tu contexto. Sé lo más específico posible.*

| Primitivo KERNEL | Concepto en [NOMBRE DEL DOMINIO] |
| :--- | :--- |
| **Actor** | [Ej: Un conductor, un vehículo de reparto, un dron, un agente de IA que optimiza rutas, un cliente final] |
| **Flujo** | [Ej: El ciclo de vida de una entrega (desde el almacén hasta la puerta del cliente), un flujo de devolución] |
| **Dato** | [Ej: La ubicación GPS de un vehículo, el estado de una entrega, un modelo de predicción de tráfico, la prueba de entrega (foto)] |
| **Señal** | [Ej: Un pedido del cliente, un alert de retraso en ruta, un evento externo que inicia flujo (tráfico), una story de usuario, un cambio de prioridad] |
| **Límite** | [Ej: La API del sistema de gestión de flotas, la app del conductor, la interfaz de seguimiento para el cliente] |
| **Estado** | [Ej: El estado de un paquete (en almacén, en tránsito, entregado), la disponibilidad de un conductor] |
| **Recurso** | [Ej: Un vehículo, la capacidad de carga del vehículo, el tiempo del conductor, el combustible] |

---

## §2. PATRONES CLAVE PARA [NOMBRE DEL DOMINIO]

*Instrucción: Identifica 3-4 patrones de `A1_Patrones.md` que sean particularmente relevantes para tu dominio y describe su implementación específica.*

### [ID_Patrón]: [Nombre del Patrón]

- **Implementación:** [Describe cómo se aplica este patrón en tu dominio. Usa los términos que mapeaste en la sección anterior.]
- **Valor:** [¿Qué beneficio específico aporta en tu contexto?]

> **Ejemplo para Logística:**
>
> ### PA28: Optimización de Rutas con IA
>
> - **Implementación:** Un agente de IA (`Actor`) consume todas las órdenes de entrega (`Dato`) y el estado en tiempo real de la flota de vehículos (`Estado`). Cada 5 minutos, recalcula el `Flujo` de reparto óptimo para cada `Actor` (conductor), teniendo en cuenta el tráfico, las ventanas de entrega y la prioridad de los paquetes.
> - **Valor:** Reduce los costos de combustible en un 15-25%, aumenta el número de entregas por conductor por día y mejora la precisión de los ETAs (Tiempos Estimados de Llegada) comunicados al cliente.

---

## §3. MÉTRICAS (KPIs) PARA [NOMBRE DEL DOMINIO]

*Instrucción: Lista 4-5 KPIs que sean cruciales para medir el rendimiento en tu dominio. Conéctalos a los primitivos de KERNEL.*

- **[Nombre de la Métrica]:** [Descripción]. Mide la salud de [Primitivo/Dominio relevante].

> **Ejemplo para Logística:**
>
> - **Costo por Entrega:** Costo total (`Recurso`) dividido por el número de entregas exitosas. Mide la eficiencia del `Flujo` principal.
> - **Tasa de Entrega a Tiempo (On-Time Delivery Rate):** Porcentaje de entregas completadas dentro de la ventana de tiempo prometida al cliente. Mide la calidad del `Flujo`.
> - **Utilización de Vehículos:** Porcentaje del tiempo que los vehículos (`Actor`/`Recurso`) están activamente en ruta de entrega vs. parados.

---

## §4. EJEMPLO DE APLICACIÓN: [CASO DE USO TÍPICO DEL DOMINIO]

*Instrucción: Describe un problema común en tu dominio y cómo lo resolverías usando KERNEL. Sigue la estructura Diagnóstico -> Roadmap -> Resultados.*

1. **Diagnóstico (A3):** [Describe el H_Score y los problemas principales. Usa los términos del dominio.]
2. **Roadmap (T10):** [Define un plan fásico simple usando los patrones que identificaste.]
3. **Resultados Esperados:** [Cuantifica el impacto esperado en los KPIs que definiste.]

> **Ejemplo para Logística:**
>
> 1. **Diagnóstico:** H_Score de 51. Problema en `D3_Decision` (rutas planificadas manualmente cada mañana, sin capacidad de reaccionar a imprevistos).
> 2. **Roadmap:**
>     - **Fase 1:** Implementar seguimiento GPS en tiempo real para todos los vehículos (`D2_Percepcion`).
>     - **Fase 2:** Desplegar el agente de optimización de rutas (PA28) en modo **M1** (sugiriendo rutas a los despachadores).
>     - **Fase 3:** Promover el agente a modo **M4** (asignando rutas automáticamente e informando).
> 3. **Resultados Esperados:** Reducir el costo por entrega en un 10% y aumentar la tasa de entrega a tiempo del 85% al 95% en 9 meses.
