# T11: Technical Debt Register

**Propósito:** Visualizar, cuantificar y priorizar deuda técnica para pago sistemático
**Audiencia:** Engineering Managers, Tech Leads, Arquitectos

---

## DEBT REGISTER

| ID | Descripción | Dominio | Severidad (1-5) | Costo Delay ($/mes) | Esfuerzo (SP) | ROI (Costo/Esfuerzo) | Owner | Status |
|----|-------------|---------|-----------------|---------------------|---------------|----------------------|-------|--------|
| D01 | Monolito PHP sin tests | D1_Arquitectura | 5 (CRÍTICO) | $120K | 800 | 150 | Platform Team | 🟡 En Progreso |
| D02 | API Gateway sin rate limiting | D1_Arquitectura | 4 (ALTO) | $45K | 80 | 562 | SRE Team | 🔴 Pendiente |
| D03 | Librería UI obsoleta (React 16) | D4_Operacion | 3 (MEDIO) | $15K | 120 | 125 | Frontend Guild | 🔴 Pendiente |
| D04 | Proceso CI/CD manual | D4_Operacion | 4 (ALTO) | $60K | 200 | 300 | DevOps | 🟢 Completado |
| D05 | Falta de documentación onboarding | D4_Operacion | 2 (BAJO) | $5K | 40 | 125 | Tech Writing | 🔴 Pendiente |

---

## GUÍA DE CAMPOS

- **ID:** Identificador único (ej: D01, D02...)
- **Descripción:** Qué es la deuda y dónde está.
- **Dominio:** A qué dominio KERNEL afecta (D1-D4).
- **Severidad:**
  - 5: CRÍTICO - Causa outages, bloquea features core.
  - 4: ALTO - Ralentiza significativamente, alto riesgo.
  - 3: MEDIO - Causa fricción, pero hay workarounds.
  - 2: BAJO - Molestia menor, bajo impacto.
  - 1: TRIVIAL - Estético, nice-to-have.
- **Costo Delay ($/mes):** Impacto económico mensual de NO pagar la deuda (horas extra, pérdida clientes, costo oportunidad).
- **Esfuerzo (SP):** Story points estimados para resolverla.
- **ROI:** `Costo Delay / Esfuerzo`. Métrica para priorizar (más alto = mejor).
- **Owner:** Equipo/persona responsable de pagarla.
- **Status:**
  - 🔴 Pendiente: En backlog.
  - 🟡 En Progreso: Se está trabajando en ello.
  - 🟢 Completado: Resuelto y verificado.

---

## PROCESO DE GESTIÓN

### 1. Identificación (Continuo)
- **Quién:** Cualquier ingeniero puede proponer un item de deuda.
- **Cuándo:** Durante retrospectivas, postmortems, o en cualquier momento.
- **Cómo:** Llenar un "Debt Card" con la información del registro.

### 2. Priorización (Trimestral)
- **Quién:** Tech Leads, Arquitectos, Product Owners.
- **Cuándo:** Durante el planning del trimestre.
- **Cómo:**
  1. Revisar todos los items `Pendiente`.
  2. Calcular ROI para cada uno.
  3. Asignar 20-30% de la capacidad del trimestre para pagar deuda.
  4. Seleccionar los items con mayor ROI hasta llenar la capacidad asignada.

### 3. Pago (Continuo)
- **Quién:** El equipo Owner.
- **Cómo:** Los items de deuda seleccionados se tratan como cualquier otra feature en el backlog. Tienen tickets, se trabajan en sprints y se verifican.

### 4. Verificación (Al completar)
- **Quién:** QA, Tech Lead.
- **Cómo:**
  - Verificar que la solución funciona.
  - Actualizar métricas (ej: si se pagó deuda de tests, el coverage debe subir).
  - Marcar como `🟢 Completado`.

---

## MÉTRICAS DE SALUD (Λ)

### Tech Debt Ratio (Λ)
```python
# Λ = (Esfuerzo Total Deuda Pendiente) / (Esfuerzo Total Features Entregadas Últimos 12M)

Λ_total = sum(sp for debt in register if debt.status == 'Pendiente')
features_sp = get_features_sp_last_12m()

lambda_ratio = (Λ_total / features_sp) * 100
```

**Interpretación:**
- **< 15% (Saludable):** Deuda bajo control.
- **15-35% (Advertencia):** Requiere acción proactiva.
- **> 35% (Peligro):** La deuda está ahogando el desarrollo de nuevas features.

### Deuda Neta (ΔΛ)
```python
# ΔΛ = (Deuda Creada este Q) - (Deuda Pagada este Q)

# Objetivo: ΔΛ <= 0 (pagas más deuda de la que creas)
```

---

## VISUALIZACIÓN

**Burndown Chart de Deuda:**
- Eje Y: Total Story Points de deuda pendiente.
- Eje X: Tiempo (trimestres).
- Línea objetivo: Tendencia decreciente hacia Λ < 15%.

**Heatmap de Deuda:**
- Matriz de componentes del sistema vs. severidad de la deuda.
- Permite visualizar dónde se concentra la deuda más crítica.

---

**Referencias:**
- A2_Antipatrones.md
- D1_Arquitectura.md
