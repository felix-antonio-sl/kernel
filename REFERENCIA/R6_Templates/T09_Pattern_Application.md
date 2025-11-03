# T09: Plantilla de Aplicación de Patrón

**Versión:** 2.2.1  
**Última Actualización:** 2025-11-03  
**Compatibilidad:** KERNEL v2.2.x

**Propósito:** Documentar la aplicación de un patrón específico de KERNEL a un problema concreto.
**Audiencia:** Arquitectos, Ingenieros, Product Owners.

---

## 1. METADATOS DE LA APLICACIÓN

```yaml
ID_Aplicación: [YYYYMMDD-PatternID]
Patrón_Aplicado: [ID y Nombre del Patrón, ej. "P21: Strangler Fig"]
Problema_Objetivo: [Descripción corta del problema que se resuelve]
Equipo_Owner: [Nombre del equipo que implementa el patrón]
Fecha: [YYYY-MM-DD]
Status: [Planificado | En Progreso | Completado | Fallido]
```

---

## 2. CONTEXTO Y PROBLEMA

*Describe la situación antes de aplicar el patrón. ¿Cuál era el dolor o la oportunidad?*

**Ejemplo (para P15: Strangler Fig):**
> El monolito de facturación es una caja negra de 10 años de antigüedad escrita en Perl. Cualquier cambio, por pequeño que sea, requiere 6 semanas de testing de regresión y un despliegue de alto riesgo. No podemos lanzar nuevos planes de precios ni integrarnos con métodos de pago modernos, lo que nos hace perder clientes frente a competidores más ágiles. El H_Score del dominio de Facturación es 28 (Crítico).

---

## 3. DECISIÓN: ¿POR QUÉ ESTE PATRÓN?

*Justifica por qué se eligió este patrón específico sobre otras alternativas.*

**Ejemplo (para P15: Strangler Fig):**
- **Alternativa 1: Reescritura Big Bang.** Descartada por su alto riesgo. Un proyecto de 2 años para reescribir todo habría congelado el desarrollo de features y probablemente habría fallado.
- **Alternativa 2: Refactorización interna.** Descartada porque la arquitectura subyacente del monolito es irreparable. Sería como remodelar los muebles de una casa con cimientos rotos.
- **Elección: P15 Strangler Fig.** Se eligió porque permite una migración gradual y de bajo riesgo. Podemos construir el nuevo servicio de facturación en paralelo y redirigir el tráfico poco a poco (ej. primero los nuevos clientes, luego los clientes pequeños), obteniendo valor de forma incremental y manteniendo el sistema antiguo funcionando hasta que sea completamente reemplazado.

---

## 4. PLAN DE IMPLEMENTACIÓN

*Detalla los pasos concretos para aplicar el patrón.*

**Ejemplo (para P15: Strangler Fig):**

1.  **Fase 1: Crear el Façade (Proxy) - (Mes 1-2)**
    -   Desplegar un proxy (ej. Nginx con Lua, o un servicio ligero en Go) que se siente en frente del monolito de facturación.
    -   Inicialmente, el proxy simplemente redirige el 100% del tráfico al monolito sin ninguna lógica.
    -   **Gate:** El proxy está en producción y maneja todo el tráfico sin añadir más de 10ms de latencia.

2.  **Fase 2: Implementar el Primer Microservicio (Mes 3-6)**
    -   Desarrollar el nuevo microservicio de "Gestión de Suscripciones" con su propia base de datos.
    -   Modificar el proxy para que las llamadas a `GET /api/subscriptions` sean redirigidas al nuevo servicio, mientras que todo lo demás sigue yendo al monolito.
    -   **Gate:** El 100% de las lecturas de suscripciones son servidas por el nuevo servicio. El monolito ya no maneja estas lecturas.

3.  **Fase 3: Migrar Escrituras y Lógica Compleja (Mes 7-12)**
    -   Implementar la lógica para crear y cancelar suscripciones en el nuevo servicio.
    -   Usar un patrón de "sincronización de datos de doble escritura" para mantener consistentes las bases de datos del monolito y del nuevo servicio durante la transición.
    -   Modificar el proxy para redirigir las escrituras (`POST`, `PUT`, `DELETE`) al nuevo servicio.
    -   **Gate:** El 100% de la lógica de suscripciones es manejada por el nuevo servicio.

4.  **Fase 4: "Estrangular" el Monolito (Mes 13-15)**
    -   Repetir las fases 2 y 3 para otras partes de la facturación (ej. "Generación de Facturas", "Procesamiento de Pagos").
    -   A medida que más y más funcionalidad se migra, el código correspondiente en el monolito se marca como obsoleto y eventualmente se elimina.

5.  **Fase 5: Retirar el Monolito (Mes 16)**
    -   Una vez que el proxy ya no redirige ninguna llamada al monolito, este puede ser apagado y decomisado.
    -   **Gate:** El monolito ha sido apagado. ¡Celebración del equipo!

---

## 5. MÉTRICAS Y RESULTADOS ESPERADOS

*¿Cómo mediremos el éxito de esta aplicación?*

- **KR1: Tiempo de Ciclo para Features de Facturación:** Reducir de 8 semanas a 1 semana para el Mes 12.
- **KR2: Tasa de Errores en Facturación:** Reducir de 1.5% a <0.1% para el Mes 15.
- **KR3: H_Score del Dominio de Facturación:** Aumentar de 28 a >70 para el Mes 16.
- **Métrica de Negocio:** Habilitar el lanzamiento de 3 nuevos planes de precios en el Mes 9, lo que actualmente es imposible.

---

## 6. RIESGOS Y MITIGACIONES

- **Riesgo 1: Inconsistencia de Datos durante la Migración.**
  - **Mitigación:** Usar un sistema de reconciliación diario que compare las bases de datos y alerte sobre cualquier discrepancia.

- **Riesgo 2: Impacto en el Rendimiento por el Proxy.**
  - **Mitigación:** Realizar pruebas de carga para asegurar que el proxy no añade más de 10-15ms de latencia. Usar un proxy de alto rendimiento.

- **Riesgo 3: El equipo se distrae y deja la migración a medias.**
  - **Mitigación:** Asignar un equipo dedicado (el "Strangler Team") cuyo único OKR es completar la migración. Proteger su capacidad.

---

## 7. LECCIONES APRENDIDAS (Post-Implementación)

*Esta sección se llena después de que el patrón ha sido implementado.*

- **Lección 1:** La sincronización de datos fue mucho más compleja de lo esperado. Deberíamos haber usado una herramienta de CDC (Change Data Capture) como Debezium desde el principio.
- **Lección 2:** El equipo se sintió mucho más empoderado al poder desplegar su propio servicio. La moral del equipo aumentó de 5/10 a 9/10.
- **Lección 3:** El patrón funcionó tan bien que ahora es el método estándar de la compañía para modernizar sistemas legacy.

---

**Referencias:**
- A1_Patrones.md
- R1_Casos.md (Ver Caso 4 para un ejemplo completo de aplicación de este patrón)
