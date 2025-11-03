# T02: Capability Map Template

**Propósito:** Modelar, analizar y planificar las capacidades de negocio de la organización.
**Audiencia:** Arquitectos Empresariales, Estrategas, Product Managers.

---

## 1. ESTRUCTURA DEL MAPA DE CAPACIDADES

*El mapa se organiza jerárquicamente en 3 niveles.*

- **Nivel 1 (L1):** Áreas de valor principales (ej. "Gestionar Clientes", "Desarrollar Productos").
- **Nivel 2 (L2):** Capacidades core dentro de cada área (ej. "Soporte al Cliente", "Marketing Digital").
- **Nivel 3 (L3):** Capacidades específicas y detalladas (ej. "Gestión de Tickets", "Análisis de Sentimiento en Redes Sociales").

**Ejemplo de Estructura:**
```yaml
L1: Gestionar Clientes
  L2: Adquisición de Clientes
    L3: Generación de Leads
    L3: Campañas de Marketing
  L2: Relacionamiento con Clientes
    L3: Gestión de Cuentas
    L3: Soporte al Cliente
      L4: Gestión de Tickets
      L4: Base de Conocimiento
```

---

## 2. PLANTILLA DE CAPACIDAD INDIVIDUAL

*Cada capacidad en el mapa (especialmente L3) se detalla usando esta plantilla.*

```markdown
### Capacidad: [Nombre de la Capacidad]

- **ID:** [CXXX]
- **Descripción:** [Qué hace la capacidad y qué valor de negocio entrega.]
- **Owner:** [Rol o equipo responsable de la madurez de esta capacidad.]

#### Evaluación (Análisis PACE)

- **Performance (P):** ¿Qué tan bien la ejecutamos hoy? (1-5)
- **Agility (A):** ¿Qué tan fácil es de cambiar o escalar? (1-5)
- **Centrality (C):** ¿Qué tan crítica es para nuestra estrategia? (1-5)
- **Excellence (E):** ¿Necesitamos ser los mejores del mundo en esto? (Diferenciadora, Paridad, Utility)

#### Realización (Recursos)

- **Personas:** [Roles o equipos que la ejecutan (ej. "Equipo de Soporte N1")]
- **Procesos:** [Link al proceso de negocio documentado (ej. "Proceso de Resolución de Tickets")]
- **Tecnología:** [Aplicaciones o sistemas que la soportan (ej. "Zendesk, Jira")]
- **Datos:** [Entidades de datos clave que consume o produce (ej. "Ticket", "Cliente")]

#### Métricas

- **KPI Primario:** [Métrica principal que mide el éxito (ej. "Tiempo de Primera Respuesta")]
- **KPIs Secundarios:** [Otras métricas relevantes (ej. "CSAT", "Tasa de Resolución en Primer Contacto")]
```

---

## 3. VISUALIZACIÓN (HEATMAPS)

*El verdadero poder del mapa de capacidades viene de superponer datos para visualizar insights.*

### Heatmap de Performance

- **Propósito:** Identificar dónde la ejecución es pobre.
- **Visualización:** Colorear cada capacidad en el mapa según su score de **Performance** (Rojo = 1-2, Amarillo = 3, Verde = 4-5).
- **Insight:** "Estamos fallando consistentemente en las capacidades de 'Soporte al Cliente'".

### Heatmap de Agilidad

- **Propósito:** Encontrar dónde la rigidez impide el cambio.
- **Visualización:** Colorear cada capacidad según su score de **Agility**.
- **Insight:** "Nuestras capacidades de 'Facturación' son extremadamente difíciles de cambiar, lo que bloquea nuevos modelos de negocio".

### Heatmap de Inversión Estratégica

- **Propósito:** Alinear el presupuesto con la estrategia.
- **Visualización:** Colorear según la combinación de **Centrality** y **Excellence**.
  - **Verde (Invertir para Ganar):** Alta Centralidad, Excelencia Diferenciadora.
  - **Amarillo (Optimizar):** Alta Centralidad, Excelencia de Paridad.
  - **Rojo (Desinvertir/Automatizar):** Baja Centralidad, Excelencia Utility.
- **Insight:** "Estamos sobreinvirtiendo en capacidades no estratégicas y desatendiendo las que nos diferencian".

### Heatmap de Costo vs. Performance

- **Propósito:** Identificar ineficiencias.
- **Visualización:** Colorear según el ratio `Costo Total de Propiedad (TCO) / Score de Performance`.
- **Insight:** "La capacidad 'Gestión de Inventario' es extremadamente cara y tiene un bajo rendimiento. Es un candidato ideal para re-ingeniería o reemplazo de software".

---

## 4. PROCESO DE GOBERNANZA

1.  **Creación (Una vez):** Un equipo multifuncional (arquitectura, negocio, producto) define la versión 1.0 del mapa.
2.  **Evaluación (Anual):** Se realiza una evaluación completa (PACE, costos, etc.) de todas las capacidades.
3.  **Revisión Estratégica (Anual):** Durante el ciclo de planificación estratégica, se usan los heatmaps para decidir dónde invertir, desinvertir u optimizar.
4.  **Actualización (Continua):** El mapa es un artefacto vivo. Se actualiza cuando:
    -   Se crea una nueva capacidad (ej. nuevo producto).
    -   Se retira una capacidad (ej. se deprecia un sistema).
    -   Cambia la estrategia de la empresa (puede cambiar la Centralidad de las capacidades).

---

**Referencias:**
- D1_Arquitectura.md
- R1_Casos.md (para ver ejemplos de cómo se usó el mapa de capacidades en transformaciones reales)
