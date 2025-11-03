# T14: User Story Template

**Propósito:** Escribir historias de usuario efectivas, consistentes y accionables.
**Audiencia:** Product Owners, Ingenieros, Diseñadores, QA.

---

## PRINCIPIOS FUNDAMENTALES

### Historia como Señal, no como Dato

```yaml
Concepto_Clave:
  - User Story = SEÑAL (placeholder para conversación futura)
  - Specification = DATO (registro formal y completo)
  
  La historia inicia la conversación, NO la reemplaza

Implicación:
  - No llenar historia con cada detalle posible
  - Capturar esencia, dejar matices para conversación
  - Conversación ocurre cuando story seleccionada (sprint planning, kick-off)

Participants_Conversación:
  - Product Owner (qué y por qué)
  - Engineer (cómo técnicamente)
  - Tester (casos edge, criterios verificación)
  - Designer (UI/UX, si aplica)

Timing:
  - Historia escrita: Semanas antes (high-level)
  - Conversación: Días antes/durante sprint planning
  - Especificación detallada: Durante desarrollo (tests, docs)
```

---

### Las Dos Reglas de Oro

```yaml
Regla_1_BENEFICIAL:
  - Toda historia debe tener valor de negocio claro
  - Beneficio debe ser explícito en "so that" clause
  - Si no hay beneficio articulable → No es story válida

Regla_2_SMALL:
  - Historia debe ser completable en <2 semanas (idealmente <2 días)
  - Grandes historias DEBEN dividirse
  - División preserva beneficio en cada parte

Balance:
  - "Beneficial" tiende a hacer stories grandes
  - "Small" tiende a hacer stories pequeñas
  - Tensión saludable: Buscar mínimo viable que entrega valor
  
  Autoridad_Final: Product Owner decide si split tiene valor
```

---

### Anti-Patrones a Evitar

```yaml
AP1_Generic_User:
  ❌ Malo: "Como un usuario..."
  ✅ Bueno: "Como un comprador frecuente..."
  Razón: "Usuario" no dice nada, necesitas persona específica

AP2_Developer_as_User:
  ❌ Malo: "Como un developer, quiero API endpoint..."
  ✅ Bueno: "Como un comprador, quiero checkout rápido..."
  Razón: Developer NO es cliente final (excepción: tools internos)

AP3_System_as_User:
  ❌ Malo: "Como el sistema de pagos, quiero validar tarjetas..."
  ✅ Bueno: "Como un comprador, quiero pagar con tarjeta segura..."
  Razón: Sistema no es beneficiario, encuentra humano detrás

AP4_Organization_as_User:
  ❌ Malo: "Como la empresa, queremos aumentar revenue..."
  ✅ Bueno: "Como un vendedor, quiero sugerir upsells para aumentar ticket..."
  Razón: "Empresa" es abstracta, identifica rol específico

AP5_Output_Disguised:
  ❌ Malo: "Como PM, quiero implementar feature X..."
  ✅ Bueno: "Como cliente, quiero filtrar productos para encontrar más rápido..."
  Razón: Focus en outcome (encontrar rápido), no output (feature X)

AP6_Too_Technical:
  ❌ Malo: "Como user, quiero GraphQL resolver para subscriptions..."
  ✅ Bueno: "Como user, quiero notificaciones real-time cuando item disponible..."
  Razón: Story es business need, no implementación técnica

AP7_Lost_Benefit_in_Splitting:
  ❌ Malo: Story "Save & Load data" split en "Save data" + "Load data"
           (cada mitad sin valor independiente)
  ✅ Bueno: Mantener como 1 story, split tasks técnicos internamente
  Razón: Si split pierde beneficio, no es válido para stories
```

---

## USER STORY TEMPLATE

```markdown
**ID:** [TICKET-XXXX]

**Título:** [Verbo de acción] + [Feature]

**User Story:**
Como un **[Tipo de Usuario]**, 
quiero **[Realizar una acción]**, 
para poder **[Obtener un beneficio/valor]**.

**Ejemplo:**
> Como un **comprador frecuente**,
> quiero **guardar mi dirección de envío**,
> para poder **hacer checkout más rápido en futuras compras**.

---

### Acceptance Criteria (AC)

*Define las condiciones que deben cumplirse para que la historia se considere completa. Usar formato Gherkin (Given/When/Then).*

**AC 1: Guardar una nueva dirección**
- **Given** que estoy en la página de mi perfil y no tengo direcciones guardadas,
- **When** hago clic en "Añadir Nueva Dirección" y lleno el formulario con datos válidos,
- **Then** la nueva dirección debe aparecer en mi lista de direcciones guardadas.

**AC 2: Usar dirección guardada en checkout**
- **Given** que tengo al menos una dirección guardada y estoy en la página de checkout,
- **When** selecciono una de mis direcciones guardadas,
- **Then** el formulario de envío se debe autocompletar con los datos de esa dirección.

**AC 3: Error con datos inválidos**
- **Given** que estoy en el formulario para añadir una nueva dirección,
- **When** intento guardar con un código postal inválido,
- **Then** debo ver un mensaje de error específico ("El código postal no es válido") y el formulario no se debe enviar.

**NOTA CRÍTICA: AC ≠ Tests**

```yaml
Acceptance_Criteria:
  - Naturaleza: Puntos principales, condiciones high-level
  - Audiencia: Producto + Tech + QA (todos entienden)
  - Timing: Escritos just-in-time (días antes desarrollo, no semanas)
  - Detalle: Deliberadamente incompleto (placeholder conversación)
  - Cantidad: 2-5 criterios por story

Acceptance_Tests:
  - Naturaleza: Especificación detallada, casos edge, validaciones
  - Audiencia: Principalmente QA + Engineers
  - Timing: Escritos durante desarrollo (no antes)
  - Detalle: Exhaustivo (100+ test cases posibles)
  - Cantidad: Tantos como necesario para coverage

Relación:
  AC → Tests
  "Debe validar postal code" (AC) 
    → 15 tests (code válido, inválido, vacío, formato wrong, 
                 internacional, caracteres especiales, etc.)

Peligro:
  Si PO intenta escribir todos los tests en AC → Analysis paralysis
  Si AC escritos meses antes → Obsoletos cuando llega momento desarrollo
  
Solución_KERNEL:
  1. AC escritos last moment (1-3 días antes sprint planning)
  2. Conversación "Three Amigos" (PO + Dev + QA) elabora detalles
  3. Tests escritos durante desarrollo (TDD, BDD)
```

---

### Technical Notes (Opcional)

*Detalles de implementación para el equipo de ingeniería. No debe contener lógica de negocio.*

- **Endpoint API:** `POST /api/v1/users/{userId}/addresses`
- **Esquema de Datos:** Se debe añadir una tabla `user_addresses` con `user_id`, `address_line_1`, `city`, `postal_code`, etc.
- **Contrato de Servicio:** Interactúa con el servicio de validación de direcciones de Google Maps.
- **Feature Flag:** Desplegar esta feature bajo el flag `enable-saved-addresses`.

---

### UX/UI Design

*Link a los diseños finales en Figma o Sketch.*

- **Link a Figma:** [URL al diseño del formulario y la lista de direcciones]
- **Prototipo Interactivo:** [URL al prototipo de InVision/Figma]
- **Notas de Diseño:**
  - La animación al guardar debe ser un fade-in sutil.
  - El botón primario debe ser color `#007bff`.

---

### Métricas de Éxito

*¿Cómo sabremos si esta historia aportó valor?*

- **Métrica Primaria:** Reducción del tiempo promedio de checkout en un 15% para usuarios registrados.
- **Métrica Secundaria:** Aumento del 20% en la tasa de usuarios que completan su perfil añadiendo una dirección.
- **Métrica de Calidad:** 0 bugs críticos relacionados con esta feature en los primeros 30 días post-lanzamiento.

---

### CHECKLIST (INVEST)

*Una buena User Story debe ser **I**ndependiente, **N**egociable, **V**aliosa, **E**stimable, **S**mall (Pequeña), y **T**estable.*

☐ **Independiente:** ¿Se puede desarrollar y desplegar esta historia por sí sola?
☐ **Negociable:** ¿Hay espacio para discutir los detalles de la implementación?
☐ **Valiosa:** ¿Aporta valor claro al usuario final?
☐ **Estimable:** ¿El equipo tiene suficiente información para estimar el esfuerzo (en Story Points)?
☐ **Pequeña (Small):** ¿Se puede completar en un solo sprint (idealmente en <3 días de trabajo)?
☐ **Testable:** ¿Los Criterios de Aceptación son claros y se pueden probar?

---

## DEFINITION OF DONE (DoD)

*Checklist final para marcar la historia como completada.*

☐ **Código Completo:** La implementación cumple con todos los AC.
☐ **Tests Pasados:** Todos los tests unitarios, de integración y E2E están en verde.
☐ **Code Review Aprobado:** Al menos 2 ingenieros han aprobado el Pull Request.
☐ **QA Verificado:** El equipo de QA ha validado la funcionalidad en el entorno de staging.
☐ **Diseño Aprobado:** El diseñador ha confirmado que la implementación coincide con los diseños.
☐ **Documentación Actualizada:** La documentación relevante (si aplica) ha sido actualizada.
☐ **Desplegado en Producción:** El cambio está disponible para los usuarios finales.

---

**Referencias:**

- D4_Operacion.md
- A1_Patrones.md (P29: Test-Driven Development)
