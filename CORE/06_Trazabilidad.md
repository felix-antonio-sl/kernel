# 06_Trazabilidad

**Versión:** 1.0.0 | **Estado:** Definitivo | **Audiencia:** Arquitectos Empresariales, Auditores, Compliance

---

## Invariante

**Todo artefacto organizacional debe trazarse bidireccionalmente desde propósito estratégico hasta valor entregado, atravesando exactamente 10 capas conectadas sin islas de información.**

---

## §1. FUNDAMENTOS DE TRAZABILIDAD

### Axioma de Trazabilidad

```
∀ artefacto A ∈ {Objetivo, Capacidad, Proceso, Aplicación, Dato, ...}:
  ∃ camino_traza completo tal que:
    Propósito_Estratégico ⟿ A ⟿ Valor_Entregado ∧
    linaje(A) es computable ∧
    impacto(A) es predecible
```

**Implicación:** Ningún elemento organizacional existe "porque sí". Todo tiene origen causal y consecuencia medible (Principio I3: Trazabilidad).

---

## §2. LAS 10 CAPAS

### Grafo Completo E2E

```
1. OBJETIVOS          (Propósito estratégico, North Star)
        ↓
2. CAPACIDADES        (What org puede hacer)
        ↓
3. PROCESOS           (How se ejecutan capacidades)
        ↓
4. APLICACIONES       (Software que habilita procesos)
        ↓
5. DATOS              (Información que fluye)
        ↓
6. TECNOLOGÍA         (Infra que soporta apps+datos)
        ↓
7. CONTROLES          (Seguridad, compliance, policies)
        ↓
8. RIESGOS            (Amenazas, vulnerabilidades)
        ↓
9. INICIATIVAS        (Proyectos que mitigan riesgos/mejoran capabilities)
        ↓
10. VALOR             (Outcomes medibles)
        ↓
        → Loop back to OBJETIVOS (ajuste estrategia)
```

---

## §3. CAPA 1: OBJETIVOS → CAPACIDADES

### Relación

```yaml
Relación: Objetivos REQUIEREN Capacidades
Cardinalidad: 1 Objetivo → N Capacidades
Dirección: Top-down (estrategia define capabilities necesarias)

Ejemplo:
  Objetivo: "Ser líder regional ecommerce B2C"
    → Requiere Capacidad: "Gestión pedidos online"
    → Requiere Capacidad: "Logística última milla"
    → Requiere Capacidad: "Payments processing multi-método"
    → Requiere Capacidad: "Customer support omnichannel"
```

### Métrica de Cobertura

```yaml
Coverage_Objetivos:
  - % Objetivos con al menos 1 Capacidad mapeada: Target >95%
  - % Capacidades sin Objetivo parent: Target <5% (son candidatas a retirement)

Ejemplo violación:
  Capacidad "Gestión fax" sin Objetivo asociado → Probablemente legacy, eliminar
```

---

## §4. CAPA 2: CAPACIDADES → PROCESOS

### Relación

```yaml
Relación: Capacidades SE_REALIZAN_MEDIANTE Procesos
Cardinalidad: 1 Capacidad → N Procesos
Dirección: Bidireccional (capabilities definen qué, processes definen cómo)

Ejemplo:
  Capacidad: "Gestión pedidos online"
    → Proceso: "Recibir pedido"
    → Proceso: "Validar pago"
    → Proceso: "Asignar inventario"
    → Proceso: "Confirmar pedido cliente"
    → Proceso: "Notificar warehouse"
```

### Métrica de Cobertura

```yaml
Coverage_Capacidades:
  - % Capacidades con al menos 1 Proceso implementado: Target >90%
  - % Procesos sin Capacidad parent: Target <10%

Gap Analysis:
  Capacidad SIN procesos → "Aspiracional" (no operativa aún)
  Proceso SIN capacidad → Candidato a eliminación (no agrega valor estratégico)
```

---

## §5. CAPA 3: PROCESOS → APLICACIONES

### Relación

```yaml
Relación: Procesos SON_SOPORTADOS_POR Aplicaciones
Cardinalidad: 1 Proceso → N Aplicaciones (típicamente 1-3)
Dirección: Processes demandan apps, apps habilitan processes

Ejemplo:
  Proceso: "Validar pago"
    → Aplicación: "PaymentGateway_Stripe"
    → Aplicación: "FraudDetection_ML"
    → Aplicación: "ERP_SAP" (registro transacción)
```

### Métricas

```yaml
Coverage_Procesos:
  - % Procesos con al menos 1 App soporte: Target >95%
  - % Procesos manuales (0 apps): Target <10% (automation opportunity)

App Rationalization:
  - Duplicidad: N apps haciendo mismo proceso → Consolidate
  - TCO/ROI: Costo app / # procesos soportados
  
Ejemplo:
  Si App A ($500K/año) soporta 1 proceso
  Y App B ($200K/año) soporta 5 procesos
  → App B más eficiente, evaluar migrar proceso de A a B
```

---

## §6. CAPA 4: APLICACIONES → DATOS

### Relación

```yaml
Relación: Aplicaciones CONSUMEN/PRODUCEN Datos
Cardinalidad: N Aplicaciones ↔ M Datos (many-to-many)
Dirección: Bidireccional

Ejemplo:
  Aplicación: "PaymentGateway_Stripe"
    → Consume: Customer_Profile, Payment_Method, Order_Amount
    → Produce: Transaction_ID, Payment_Status, Receipt_URL
```

### Métricas

```yaml
Data Lineage:
  - % Datos con source app conocido: Target 100%
  - % Datos con consumer apps conocidos: Target >90%
  - % Datos "dark data" (no usado por ninguna app): Target <5%

Quality Gates:
  - Aplicación crítica debe consumir datos con quality_score >85
  - Datos PII/sensitive deben tener encryption en apps que los consumen
```

### Data Flow Mapping

```yaml
Ejemplo_Flujo_Completo:
  Order_Service (produce Order_Created event)
    → Kafka topic "orders"
      → Payment_Service (consume, procesa pago)
        → Produce Payment_Completed event
          → Kafka topic "payments"
            → Warehouse_Service (consume, asigna inventario)
              → Produce Shipment_Created event
```

---

## §7. CAPA 5: DATOS → TECNOLOGÍA

### Relación

```yaml
Relación: Datos RESIDEN_EN Tecnología (storage, infra)
Cardinalidad: 1 Dato → 1-N Tecnologías (original + replicas)
Dirección: Datos requieren tech stack específico

Ejemplo:
  Dato: "Customer_Profile"
    → Tecnología_Primary: PostgreSQL_RDS (transaccional)
    → Tecnología_Replica: Elasticsearch (búsqueda)
    → Tecnología_Analytics: Snowflake (warehouse)
    → Tecnología_Backup: S3_Glacier
```

### Métricas

```yaml
Tech_Stack_Rationalization:
  - # Tech platforms total: Target <20 para org <500 personas
  - % Datos en tech deprecated: Target <5%
  - Costo tech / TB almacenado: Benchmark contra market

Data Residency Compliance:
  - % Datos EU en servers EU (GDPR): Target 100%
  - % Datos health en HIPAA-compliant infra: Target 100%
```

---

## §8. CAPA 6: TECNOLOGÍA → CONTROLES

### Relación

```yaml
Relación: Tecnología REQUIERE Controles (seguridad, compliance)
Cardinalidad: 1 Tech → N Controles
Dirección: Compliance mandates controls on tech

Ejemplo:
  Tecnología: "PostgreSQL_RDS_Production"
    → Control: "Encryption at rest (AES-256)"
    → Control: "Encryption in transit (TLS 1.3)"
    → Control: "Access via IAM roles only (no passwords)"
    → Control: "Backups daily con retention 30 días"
    → Control: "Audit logs enabled (CloudWatch)"
    → Control: "Network isolation (VPC privada)"
```

### Métricas

```yaml
Control_Coverage:
  - % Tech con todos controles mandatorios: Target 100%
  - % Controles tested (automatizados): Target >80%
  - Tiempo remediation findings: Target <7 días

Frameworks:
  - SOC2 Type II: 64 controles
  - ISO 27001: 114 controles
  - NIST CSF: 108 controles
  - GDPR: 73 artículos (subset requiere controles tech)
```

---

## §9. CAPA 7: CONTROLES → RIESGOS

### Relación

```yaml
Relación: Controles MITIGAN Riesgos
Cardinalidad: 1 Control → N Riesgos, 1 Riesgo → N Controles (many-to-many)
Dirección: Riesgos demandan controles, controles reducen riesgos

Ejemplo:
  Riesgo: "Data breach DB customer profiles"
    Probabilidad_Sin_Controles: 40%/año
    Impacto: $5M (multas GDPR + reputación)
    
    → Mitigado por Control: "Encryption at rest" (-15% probabilidad)
    → Mitigado por Control: "IAM roles only" (-10% probabilidad)
    → Mitigado por Control: "Network isolation" (-10% probabilidad)
    → Mitigado por Control: "Audit logs" (-5% impacto, detección rápida)
    
    Probabilidad_Con_Controles: 15%/año
    Riesgo_Residual: 15% × $5M = $750K/año
```

### Métricas

```yaml
Risk_Management:
  - % Riesgos con controles asignados: Target 100%
  - % Riesgos high (>$1M) con riesgo residual <20%: Target 100%
  - % Controles que mitigan 0 riesgos: Target 0% (eliminar)

Ejemplo violación:
  Control "Firewall legacy" no mitiga ningún riesgo actual → Eliminar (costo sin beneficio)
```

---

## §10. CAPA 8: RIESGOS → INICIATIVAS

### Relación

```yaml
Relación: Riesgos MOTIVAN Iniciativas (proyectos, mejoras)
Cardinalidad: 1 Riesgo → 0-N Iniciativas
Dirección: Riesgos altos priorizan iniciativas remediation

Ejemplo:
  Riesgo: "Legacy app sin mantenimiento (tech debt crítico)"
    Probabilidad: 60%/año falla catastrófica
    Impacto: $2M (downtime + recovery)
    Riesgo_Residual: $1.2M/año
    
    → Iniciativa: "Modernizar App X a microservicios"
       Budget: $800K
       Duración: 12 meses
       Risk_Reduction: 60% → 10% (85% reducción)
       ROI: ($1.2M - $120K residual) / $800K = 135% en año 1
```

### Priorización

```yaml
Portfolio_Prioritization:
  Score_Iniciativa = (Risk_Reduction × Probabilidad × Impacto - Costo) / Duración
  
  Ordenar descendente por Score
  Budget_Allocation hasta agotar presupuesto disponible
  
Constraint:
  - Iniciativas compliance (regulatorio) son mandatorias (no ROI-based)
  - Max 3 iniciativas mayores simultáneas (capacidad org limitada)
```

---

## §11. CAPA 9: INICIATIVAS → VALOR

### Relación

```yaml
Relación: Iniciativas ENTREGAN Valor (outcomes medibles)
Cardinalidad: 1 Iniciativa → N Métricas Valor
Dirección: Iniciativas deben justificarse con valor esperado/realizado

Ejemplo:
  Iniciativa: "Implementar agente IA customer support (M4)"
    Inversión: $300K (desarrollo) + $50K/año (OPEX)
    Duración: 6 meses
    
    Valor_Esperado:
      - Reducir tiempo respuesta: 4 hrs → 5 min (98.9% mejora)
      - Reducir costo support: $800K/año → $500K/año (38% reducción)
      - Aumentar CSAT: 72 → 85 (+13 puntos)
      - Liberar 5 agentes humanos para casos complejos (valor: $400K/año)
    
    Valor_Total_Anual: $700K/año
    Payback: $300K / $700K = 5.1 meses
    NPV (3 años, 10% discount): $1.4M
```

### Métricas

```yaml
Value_Tracking:
  - % Iniciativas con métricas valor definidas ex-ante: Target 100%
  - % Iniciativas con valor realizado ≥ 70% valor esperado: Target >80%
  - % Iniciativas que entregan valor 0: Target <10% (learning permitido)

Ejemplo violación:
  Iniciativa sin métricas valor → Rechazar en ARB (no aprobable)
  Iniciativa entregó 0 valor post-mortem → Root cause analysis, lecciones aprendidas
```

---

## §12. CAPA 10: VALOR → OBJETIVOS (Loop Cierre)

### Relación

```yaml
Relación: Valor ALIMENTA revisión Objetivos
Cardinalidad: N Métricas Valor → Ajuste Objetivos estratégicos
Dirección: Feedback loop continuo (Outside-in P3)

Ejemplo:
  Valor_Realizado_Q4:
    - NPS: 85 (target 80) ✅ Superó
    - Churn: 8% (target 5%) ❌ No cumplió
    - Revenue growth: 15% (target 20%) ❌ No cumplió
    
  Ajuste_Objetivos_2025:
    - Nuevo Objetivo: "Reducir churn a 5%" (alta prioridad)
    - Ajuste: "Revenue growth 15% realista" (bajar expectativa)
    - Mantener: NPS >80 (ya logrado)
    
    → Requiere nuevas Capacidades:
       - "Customer success proactive"
       - "Churn prediction ML"
    
    → Inicia nuevo ciclo trazabilidad Objetivos → Capacidades → ...
```

### Métricas

```yaml
Strategic_Alignment:
  - % Objetivos con métricas valor rastreadas: Target 100%
  - Frecuencia review objetivos: Anual (mínimo), Trimestral (recomendado)
  - % Valor entregado alineado a objetivos activos: Target >85%

Ejemplo violación:
  30% valor entregado no alinea a objetivo actual → Estrategia desalineada de ejecución
```

---

## §13. TRAZABILIDAD DE AGENTES IA

### Extensión para Agentes Algorítmicos

```yaml
Agente_IA_Trazabilidad:
  - ¿Qué proceso soporta? (Capa 3)
  - ¿Qué datos consume/produce? (Capa 5)
  - ¿Qué tecnología usa? (Capa 6: GPU, LLM API, ML framework)
  - ¿Qué controles aplican? (Capa 7: Bias detection, XAI, human oversight)
  - ¿Qué riesgos mitiga/introduce? (Capa 8)
  - ¿Qué valor entrega? (Capa 10)

Ejemplo_Completo:
  Agente: "AlgoRank_Hiring"
    Objetivo: "Contratar top talent eficientemente" (Capa 1)
    Capacidad: "Gestión recruiting" (Capa 2)
    Proceso: "Evaluar candidatos" → Paso "Ranking inicial" (Capa 3)
    Aplicación: "HiringPlatform_v2" (Capa 4)
    Datos_Consume: [Resumes_PDF, JobDescription_Text] (Capa 5)
    Datos_Produce: [CandidateScore_0-100, Ranking_List] (Capa 5)
    Tecnología: [OpenAI_GPT4, Python_FastAPI, PostgreSQL] (Capa 6)
    Controles:
      - "Bias detection weekly audit" (Capa 7)
      - "Human review top 20% candidates" (Capa 7)
      - "XAI: SHAP values for each score" (Capa 7)
    Riesgos_Mitiga:
      - "Hiring bias inconsciente" (-40% incidentes) (Capa 8)
      - "Tiempo screening excesivo" (-75% time-to-shortlist) (Capa 8)
    Riesgos_Introduce:
      - "Bias algorítmico si training data sesgado" (10% probabilidad) (Capa 8)
    Iniciativa: "Proyecto AI-Hiring-Q3-2024" (Capa 9)
    Valor:
      - Time-to-hire: 45 días → 28 días (-38%) (Capa 10)
      - Costo hiring: $5K/hire → $3K/hire (-40%) (Capa 10)
      - Quality-of-hire (1-yr retention): 85% → 92% (+7 pp) (Capa 10)
```

---

## §14. HERRAMIENTAS DE TRAZABILIDAD

### Tipos de Plataformas

```yaml
Tipo_1_Repository_EA:
  Ejemplos: Ardoq, LeanIX, BiZZdesign Enterprise Studio
  Fortaleza: Modelado visual, dependencies, impact analysis
  Limitación: Requiere input manual, no auto-discovery

Tipo_2_Service_Catalog:
  Ejemplos: ServiceNow CMDB, Backstage, OpsLevel
  Fortaleza: Auto-discovery apps/services, ownership tracking
  Limitación: Foco tech, débil en estrategia/valor

Tipo_3_Data_Lineage:
  Ejemplos: Collibra, Alation, Apache Atlas
  Fortaleza: Data lineage granular (campo-level)
  Limitación: Solo cubre datos, no end-to-end org

Tipo_4_Custom_Graph_DB:
  Ejemplos: Neo4j con modelo KERNEL custom
  Fortaleza: Flexibilidad total, queries complejas
  Limitación: Requiere desarrollo custom, mantenimiento
```

### Implementación Mínima Viable

```yaml
MVP_Trazabilidad (3 meses):
  Fase_1 (1 mes):
    - Modelar Capas 1-3 (Objetivos → Capacidades → Procesos) en Excel/Miro
    - 1 Objetivo piloto end-to-end
  
  Fase_2 (1 mes):
    - Agregar Capas 4-5 (Apps → Datos)
    - Auto-discovery apps con Backstage o similar
  
  Fase_3 (1 mes):
    - Agregar Capas 6-10 (Tech → Controles → Riesgos → Iniciativas → Valor)
    - Primer impact analysis: "Si elimino App X, ¿qué procesos fallan?"

Escalamiento (12 meses):
  - Migrar a EA platform (Ardoq/LeanIX)
  - Integrar con CMDB, Jira, financials
  - Automatizar actualizaciones (APIs, webhooks)
```

---

## §15. QUERIES CRÍTICOS

### Q1. Impact Analysis

```
QUERY: "Si elimino Aplicación X, ¿qué se rompe?"

TRAZA:
  App_X
    → Soporta Procesos [P1, P2, P3]
      → P1-P3 realizan Capacidades [C1, C2]
        → C1-C2 contribuyen a Objetivos [O1]
          → O1 entrega Valor [V: $2M/año revenue]
          
RESPUESTA:
  Eliminar App_X impacta:
    - 3 procesos (necesitan app alternativa)
    - 2 capacidades (quedan sin soporte)
    - 1 objetivo estratégico (en riesgo)
    - $2M/año valor (pérdida potencial)
  
  RECOMENDACIÓN: NO eliminar sin migración a App_Y
```

---

### Q2. Orphan Detection

```
QUERY: "¿Qué aplicaciones no soportan ningún proceso?"

TRAZA:
  ∀ App_i:
    IF NOT EXISTS Proceso_j tal que App_i soporta Proceso_j
    THEN App_i es "orphan" (candidata a retirement)

RESPUESTA:
  Apps_Orphan: [LegacyFax_System, OldCRM_v1, ReportGenerator_Deprecated]
  Total_TCO_Apps_Orphan: $450K/año
  
  RECOMENDACIÓN: Decommission, recuperar $450K/año
```

---

### Q3. Value Tracing

```
QUERY: "¿Qué iniciativas contribuyeron a métrica 'Churn -3%' en Q4?"

TRAZA:
  Valor: Churn_Q4 = 5% (vs 8% Q3, delta -3%)
    ← Iniciativas: [I1_CustomerSuccess_Team, I2_Churn_Prediction_ML]
      ← I1 mejoró Proceso: "Proactive outreach at-risk customers"
      ← I2 mejoró Proceso: "Identify churn risk 30 días anticipado"
        ← Ambos contribuyen a Capacidad: "Customer retention"
          ← Capacidad soporta Objetivo: "Reduce churn a 5%"

RESPUESTA:
  I1 contribuyó -1.5% churn ($600K valor)
  I2 contribuyó -1.5% churn ($600K valor)
  Total: $1.2M/año valor generado
  
  ROI: I1 costó $200K → ROI 300%
       I2 costó $300K → ROI 200%
```

---

### Q4. Compliance Gap

```
QUERY: "¿Qué tecnologías GDPR-scope no tienen control 'Encryption at rest'?"

TRAZA:
  ∀ Tech_i donde procesa_datos_EU(Tech_i) = True:
    IF NOT EXISTS Control_j tal que:
      Control_j = "Encryption at rest" AND
      Control_j aplica_a Tech_i
    THEN Tech_i es "gap GDPR"

RESPUESTA:
  Tech_Gaps: [Analytics_DB_Legacy, LogServer_Old]
  Risk_Exposure: GDPR multa hasta €20M o 4% revenue global
  
  RECOMENDACIÓN: Iniciativa urgente "Encrypt Analytics_DB" (2 semanas)
```

---

## §16. ANTI-PATRONES TRAZABILIDAD

### AP1. "Documentación sin Uso"

```yaml
Síntoma: Traza modelada en EA tool, nadie consulta
Causa: No integrado en workflows decisionales
Consecuencia: Modelo desactualizado, no trusted
Fix: Integrar queries en ARB, portfolio review, incident postmortem
```

### AP2. "Granularidad Extrema"

```yaml
Síntoma: Modelar hasta nivel función de código
Causa: Confundir EA con code-level architecture
Consecuencia: Mantenimiento imposible, modelo colapsa
Fix: Límite granularidad: Aplicación → Servicios (no funciones)
```

### AP3. "Islas de Información"

```yaml
Síntoma: Apps en CMDB, procesos en Wiki, riesgos en Excel separados
Causa: No tener sistema integrado trazabilidad
Consecuencia: Impact analysis imposible
Fix: EA platform única o integración vía APIs
```

### AP4. "Trazabilidad Post-Facto"

```yaml
Síntoma: Modelar traza solo cuando auditor pide
Causa: No cultura data-driven
Consecuencia: Modelo incompleto, gaps críticos
Fix: Mandato: Toda iniciativa debe actualizar modelo (DoD)
```

---

## §17. VALIDACIÓN

### Completitud

```
¿Toda organización puede modelarse con 10 capas? → SÍ
  Evidencia: 10 casos diversos mapeados (REFERENCIA/R1_Casos.md)
```

### Conectividad

```
¿Todas las capas están conectadas sin gaps? → SÍ
  Prueba: Existe path desde Objetivos → Valor para toda capa intermedia
```

### Utilidad

```
¿Queries críticos son respondibles? → SÍ
  - Impact analysis: ✅
  - Orphan detection: ✅
  - Value tracing: ✅
```

---

## §11. TRAZABILIDAD OUTSIDE-IN

### Extensión: Productos/Servicios → Destinatarios

La composición **Unidad_Trabajo** (ver `CORE/01_Primitivos.md` §7) formaliza elementos boundary-spanning que extienden trazabilidad más allá de fronteras organizacionales:

```yaml
Trazabilidad_Clásica (Inside):
  Objetivos → Capacidades → Procesos → Apps → Datos → Tech → Controles → Riesgos → Iniciativas → Valor

Trazabilidad_Outside-In (Boundary-Spanning):
  
  # Outputs al exterior
  Productos_Servicios:
    - Qué valor entregamos
    - A quién lo entregamos (destinatarios)
    - Cómo medimos éxito (métricas_valor)
    
  # Receptores externos
  Destinatarios:
    - Cliente_Externo (fuera organización)
    - Cliente_Interno (otros equipos)
    - Stakeholder (reguladores, inversores)
    - Necesidades satisfechas (job-to-be-done)
    
  # Fuerzas ambientales
  Entorno:
    - Competencia (alternativas disponibles)
    - Regulación (compliance, estándares)
    - Mercado (demanda, tendencias)
    - Tecnología (disrupciones, obsolescencia)
    - Demografía (cambios población, geografía)
```

### Cadena Causal Outside-In

```yaml
Ejemplo_E-commerce:
  
  # Desde exterior hacia interior
  Destinatario: "SMB retailers (10-50 empleados)"
    ↓ necesita
  Producto_Servicio: "Payments processing <200ms, 99.95% uptime"
    ↓ requiere
  Capacidad: "Real-time payment processing"
    ↓ ejecutada por
  Proceso: "Validate → Authorize → Settle → Notify"
    ↓ soportada por
  Aplicación: "Stripe API integration"
    ↓ produce
  Dato: "Transaction_Record (id, amount, status, timestamp)"
    ↓ almacenado en
  Tecnología: "PostgreSQL + Redis cache"
    ↓ medido por
  Valor: "Success_Rate 99.97%, Latency_P95 180ms"
    ↓ retroalimenta
  Objetivo: "Ser payment gateway más confiable para SMBs"
  
  # Fuerzas externas
  Entorno:
    - Competencia: "Stripe, Adyen tienen features similares"
    - Regulación: "PSD2 requiere Strong Customer Authentication"
    - Tecnología: "Blockchain podría disrupcionar pagos centralizados"
```

### Métricas Trazabilidad Outside-In

```yaml
Coverage_Productos_Servicios:
  Target: 100% Unidades_Trabajo tienen ≥1 producto/servicio definido
  Validación: ¿Toda unidad sabe qué valor entrega?

Coverage_Destinatarios:
  Target: 100% Productos_Servicios tienen ≥1 destinatario identificado
  Validación: ¿Todo output tiene consumidor conocido?

Coverage_Entorno:
  Target: >80% Unidades_Trabajo críticas tienen factores ambientales mapeados
  Validación: ¿Conocemos competencia/regulación/tendencias que nos afectan?

Traceability_Bidireccional:
  Forward: Destinatario → Producto → Capacidad → Proceso → App
  Backward: App → Proceso → Capacidad → Producto → Destinatario → Valor medible
```

### Conexión con Observables

```yaml
Trazabilidad_Outside-In conecta con D2_Percepcion observables:
  
  Productos_Servicios → O2 (Valor entregado)
  Destinatarios → O1 (Demanda)
  Entorno.Competencia → O6 (Competencia)
  Entorno.Regulación → O5 (Restricciones)
  Entorno.Mercado → O1 (Demanda) + O2 (Valor)
  Entorno.Tecnología → O4 (Eventos disruptivos)
```

**Principio:** Trazabilidad completa requiere visión **Inside-Out** (10 capas internas) **Y Outside-In** (productos, destinatarios, entorno). Ambas perspectivas son complementarias.

---

## Referencias Cruzadas

- **Trazabilidad completa 10 capas:** Este documento
- **Composición Outside-In:** `CORE/01_Primitivos.md` §7
- **Primitivos base:** `CORE/01_Primitivos.md`
- **Validación formal:** `CORE/07_Validacion.md`
- **Manifiesto I3:** `CORE/00_Manifiesto.md` (Invariante Trazabilidad)
- **Manifiesto P3:** `CORE/00_Manifiesto.md` (Principio Outside-In)
- **Casos aplicados:** `REFERENCIA/R1_Casos.md`
