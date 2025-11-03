# 06_Trazabilidad v2.0.0

## §0. INVARIANTE

**Todo artefacto organizacional debe trazarse bidireccionalmente desde propósito estratégico hasta valor entregado, atravesando exactamente 10 capas conectadas sin islas de información.**

**Propiedad I3:** ∀ artefacto A: ∃ camino_traza completo tal que Propósito_Estratégico ⟿ A ⟿ Valor_Entregado ∧ linaje(A) es computable ∧ impacto(A) es predecible.

**Principio P3 (Outside-In):** Trazabilidad completa requiere visión Inside-Out (10 capas internas) Y Outside-In (productos, destinatarios, entorno).

## §1. LAS 10 CAPAS DE TRAZABILIDAD

### Grafo Completo E2E

```
1. OBJETIVOS       → Propósito estratégico, North Star
         ↓
2. CAPACIDADES     → What org puede hacer
         ↓
3. PROCESOS        → How se ejecutan capacidades
         ↓
4. APLICACIONES    → Software que habilita procesos
         ↓
5. DATOS           → Información que fluye
         ↓
6. TECNOLOGÍA      → Infra que soporta apps+datos
         ↓
7. CONTROLES       → Seguridad, compliance, policies
         ↓
8. RIESGOS         → Amenazas, vulnerabilidades
         ↓
9. INICIATIVAS     → Proyectos que mitigan riesgos/mejoran capabilities
         ↓
10. VALOR          → Outcomes medibles
         ↓
         → Loop back to OBJETIVOS (ajuste estrategia)
```

### Tabla Comparativa Capas

| Capa | Relación | Cardinalidad | Métrica Cobertura Target |
|------|----------|--------------|--------------------------|
| **1→2: Objetivos→Capacidades** | REQUIEREN | 1→N | >95% objetivos con ≥1 capacidad mapeada |
| **2→3: Capacidades→Procesos** | SE_REALIZAN_MEDIANTE | 1→N | >90% capacidades con ≥1 proceso implementado |
| **3→4: Procesos→Aplicaciones** | SON_SOPORTADOS_POR | 1→N | >95% procesos con ≥1 app soporte |
| **4→5: Aplicaciones→Datos** | CONSUMEN/PRODUCEN | N↔M | 100% datos con source app conocido |
| **5→6: Datos→Tecnología** | RESIDEN_EN | 1→N | <5% datos en tech deprecated |
| **6→7: Tecnología→Controles** | REQUIERE | 1→N | 100% tech con controles mandatorios |
| **7→8: Controles→Riesgos** | MITIGAN | N↔M | 100% riesgos con controles asignados |
| **8→9: Riesgos→Iniciativas** | MOTIVAN | 1→N | >80% riesgos high con iniciativas |
| **9→10: Iniciativas→Valor** | ENTREGAN | 1→N | 100% iniciativas con métricas valor definidas |
| **10→1: Valor→Objetivos** | ALIMENTA | N→Ajuste | 100% objetivos con métricas valor rastreadas |

## §2. CAPA 1→2: OBJETIVOS → CAPACIDADES

```yaml
Relación: Objetivos REQUIEREN Capacidades
Dirección: Top-down (estrategia define capabilities)

Ejemplo:
  Objetivo: "Ser líder regional ecommerce B2C"
    → Capacidad: "Gestión pedidos online"
    → Capacidad: "Logística última milla"
    → Capacidad: "Payments processing multi-método"
    → Capacidad: "Customer support omnichannel"

Métricas:
  - % Objetivos con ≥1 Capacidad: Target >95%
  - % Capacidades sin Objetivo parent: Target <5% (retirement candidates)

Violación:
  Capacidad "Gestión fax" sin Objetivo → Legacy, eliminar
```

## §3. CAPA 2→3: CAPACIDADES → PROCESOS

```yaml
Relación: Capacidades SE_REALIZAN_MEDIANTE Procesos
Dirección: Bidireccional (capabilities definen qué, processes cómo)

Ejemplo:
  Capacidad: "Gestión pedidos online"
    → Proceso: "Recibir pedido"
    → Proceso: "Validar pago"
    → Proceso: "Asignar inventario"
    → Proceso: "Confirmar pedido cliente"
    → Proceso: "Notificar warehouse"

Métricas:
  - % Capacidades con ≥1 Proceso: Target >90%
  - % Procesos sin Capacidad parent: Target <10%

Gap_Analysis:
  Capacidad SIN procesos → Aspiracional (no operativa)
  Proceso SIN capacidad → Candidato eliminación (no valor estratégico)
```

## §4. CAPA 3→4: PROCESOS → APLICACIONES

```yaml
Relación: Procesos SON_SOPORTADOS_POR Aplicaciones
Dirección: Processes demandan apps, apps habilitan processes

Ejemplo:
  Proceso: "Validar pago"
    → Aplicación: "PaymentGateway_Stripe"
    → Aplicación: "FraudDetection_ML"
    → Aplicación: "ERP_SAP" (registro transacción)

Métricas:
  - % Procesos con ≥1 App: Target >95%
  - % Procesos manuales (0 apps): Target <10% (automation opportunity)

App_Rationalization:
  - Duplicidad: N apps mismo proceso → Consolidate
  - TCO/ROI: Costo app / # procesos soportados
  
  Ejemplo:
    App A ($500K/año) soporta 1 proceso
    App B ($200K/año) soporta 5 procesos
    → App B más eficiente, evaluar migrar
```

## §5. CAPA 4→5: APLICACIONES → DATOS

```yaml
Relación: Aplicaciones CONSUMEN/PRODUCEN Datos
Dirección: Bidireccional (many-to-many)

Ejemplo:
  Aplicación: "PaymentGateway_Stripe"
    → Consume: Customer_Profile, Payment_Method, Order_Amount
    → Produce: Transaction_ID, Payment_Status, Receipt_URL

Métricas:
  - % Datos con source app: Target 100%
  - % Datos con consumer apps: Target >90%
  - % Dark data (no usado): Target <5%

Quality_Gates:
  - App crítica consume datos quality_score >85
  - Datos PII/sensitive requieren encryption en apps consumers

Data_Flow_Ejemplo:
  Order_Service (produce Order_Created)
    → Kafka "orders"
      → Payment_Service (consume, procesa)
        → Produce Payment_Completed
          → Kafka "payments"
            → Warehouse_Service (consume, asigna inventario)
```

## §6. CAPA 5→6: DATOS → TECNOLOGÍA

```yaml
Relación: Datos RESIDEN_EN Tecnología (storage, infra)
Dirección: Datos requieren tech stack específico

Ejemplo:
  Dato: "Customer_Profile"
    → Tech_Primary: PostgreSQL_RDS (transaccional)
    → Tech_Replica: Elasticsearch (búsqueda)
    → Tech_Analytics: Snowflake (warehouse)
    → Tech_Backup: S3_Glacier

Métricas:
  - # Tech platforms: Target <20 para org <500 personas
  - % Datos en tech deprecated: Target <5%
  - Costo tech / TB almacenado: Benchmark market

Compliance:
  - % Datos EU en servers EU (GDPR): Target 100%
  - % Datos health en HIPAA-compliant infra: Target 100%
```

## §7. CAPA 6→7: TECNOLOGÍA → CONTROLES

```yaml
Relación: Tecnología REQUIERE Controles (seguridad, compliance)
Dirección: Compliance mandates controls on tech

Ejemplo:
  Tecnología: "PostgreSQL_RDS_Production"
    → Control: "Encryption at rest (AES-256)"
    → Control: "Encryption in transit (TLS 1.3)"
    → Control: "Access via IAM roles only"
    → Control: "Backups daily retention 30 días"
    → Control: "Audit logs enabled (CloudWatch)"
    → Control: "Network isolation (VPC privada)"

Métricas:
  - % Tech con todos controles mandatorios: Target 100%
  - % Controles tested (automatizados): Target >80%
  - Tiempo remediation findings: Target <7 días

Frameworks:
  - SOC2 Type II: 64 controles
  - ISO 27001: 114 controles
  - NIST CSF: 108 controles
  - GDPR: 73 artículos (subset tech controls)
```

## §8. CAPA 7→8: CONTROLES → RIESGOS

```yaml
Relación: Controles MITIGAN Riesgos
Dirección: Riesgos demandan controles, controles reducen riesgos

Ejemplo:
  Riesgo: "Data breach DB customer profiles"
    Prob_Sin_Controles: 40%/año
    Impacto: $5M (multas GDPR + reputación)
    
    → Control: "Encryption at rest" (-15% prob)
    → Control: "IAM roles only" (-10% prob)
    → Control: "Network isolation" (-10% prob)
    → Control: "Audit logs" (-5% impacto, detección rápida)
    
    Prob_Con_Controles: 15%/año
    Riesgo_Residual: 15% × $5M = $750K/año

Métricas:
  - % Riesgos con controles: Target 100%
  - % Riesgos high (>$1M) con residual <20%: Target 100%
  - % Controles que mitigan 0 riesgos: Target 0% (eliminar)

Violación:
  Control "Firewall legacy" no mitiga ningún riesgo → Eliminar (costo sin beneficio)
```

## §9. CAPA 8→9: RIESGOS → INICIATIVAS

```yaml
Relación: Riesgos MOTIVAN Iniciativas (proyectos, mejoras)
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
       ROI: ($1.2M - $120K residual) / $800K = 135% año 1

Priorización:
  Score = (Risk_Reduction × Prob × Impacto - Costo) / Duración
  
  Ordenar descendente por Score
  Budget_Allocation hasta agotar presupuesto
  
  Constraints:
    - Iniciativas compliance mandatorias (no ROI-based)
    - Max 3 iniciativas mayores simultáneas (capacity limitada)
```

## §10. CAPA 9→10: INICIATIVAS → VALOR

```yaml
Relación: Iniciativas ENTREGAN Valor (outcomes medibles)
Dirección: Iniciativas justificadas con valor esperado/realizado

Ejemplo:
  Iniciativa: "Implementar agente IA customer support (M4)"
    Inversión: $300K (desarrollo) + $50K/año (OPEX)
    Duración: 6 meses
    
    Valor_Esperado:
      - Tiempo respuesta: 4 hrs → 5 min (98.9% mejora)
      - Costo support: $800K/año → $500K/año (38% reducción)
      - CSAT: 72 → 85 (+13 puntos)
      - Liberar 5 agentes → casos complejos (valor: $400K/año)
    
    Valor_Total_Anual: $700K/año
    Payback: $300K / $700K = 5.1 meses
    NPV (3 años, 10% discount): $1.4M

Métricas:
  - % Iniciativas con métricas valor ex-ante: Target 100%
  - % Iniciativas con valor realizado ≥70% esperado: Target >80%
  - % Iniciativas valor 0: Target <10% (learning permitido)

Violación:
  Iniciativa sin métricas valor → Rechazar en ARB
  Iniciativa valor 0 post-mortem → RCA, lecciones aprendidas
```

## §11. CAPA 10→1: VALOR → OBJETIVOS (Loop Cierre)

```yaml
Relación: Valor ALIMENTA revisión Objetivos
Dirección: Feedback loop continuo (Outside-in P3)

Ejemplo:
  Valor_Realizado_Q4:
    - NPS: 85 (target 80) ✅ Superó
    - Churn: 8% (target 5%) ❌ No cumplió
    - Revenue growth: 15% (target 20%) ❌ No cumplió
    
  Ajuste_Objetivos_2025:
    - Nuevo: "Reducir churn a 5%" (alta prioridad)
    - Ajuste: "Revenue growth 15% realista" (bajar expectativa)
    - Mantener: "NPS >80" (ya logrado)
    
    → Requiere nuevas Capacidades:
       - "Customer success proactive"
       - "Churn prediction ML"
    
    → Inicia nuevo ciclo: Objetivos → Capacidades → ...

Métricas:
  - % Objetivos con métricas valor rastreadas: Target 100%
  - Frecuencia review: Anual (mínimo), Trimestral (recomendado)
  - % Valor entregado alineado a objetivos activos: Target >85%

Violación:
  30% valor no alinea a objetivo actual → Estrategia desalineada de ejecución
```

## §12. TRAZABILIDAD OUTSIDE-IN

### Extensión Boundary-Spanning

**Referencia:** `CORE/01_Primitivos.md` §7 (Composición Unidad_Trabajo)

```yaml
Trazabilidad_Clásica (Inside):
  Objetivos → Capacidades → ... → Valor (10 capas internas)

Trazabilidad_Outside-In (Boundary-Spanning):
  
  Productos_Servicios:
    - Qué valor entregamos
    - A quién (destinatarios)
    - Cómo medimos éxito (métricas_valor)
  
  Destinatarios:
    - Cliente_Externo (fuera org)
    - Cliente_Interno (otros equipos)
    - Stakeholder (reguladores, inversores)
    - Necesidades satisfechas (job-to-be-done)
  
  Entorno:
    - Competencia (alternativas disponibles)
    - Regulación (compliance, estándares)
    - Mercado (demanda, tendencias)
    - Tecnología (disrupciones, obsolescencia)
    - Demografía (población, geografía)
```

### Cadena Causal Completa

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
  Objetivo: "Ser payment gateway más confiable SMBs"
  
  # Fuerzas externas
  Entorno:
    - Competencia: "Stripe, Adyen features similares"
    - Regulación: "PSD2 requiere Strong Customer Authentication"
    - Tecnología: "Blockchain podría disrupcionar pagos"
```

### Conexión con Observables

```yaml
Outside-In conecta con D2_Percepcion observables:
  
  Productos_Servicios → O2 (Valor entregado)
  Destinatarios → O1 (Demanda)
  Entorno.Competencia → O6 (Competencia)
  Entorno.Regulación → O5 (Restricciones)
  Entorno.Mercado → O1 (Demanda) + O2 (Valor)
  Entorno.Tecnología → O4 (Eventos disruptivos)

Cobertura_Targets:
  - 100% Unidades_Trabajo tienen ≥1 producto/servicio definido
  - 100% Productos_Servicios tienen ≥1 destinatario identificado
  - >80% Unidades críticas tienen factores ambientales mapeados
```

## §13. TRAZABILIDAD DE AGENTES IA

```yaml
Agente_IA_Trazabilidad_Completa:
  - ¿Qué proceso soporta? (Capa 3)
  - ¿Qué datos consume/produce? (Capa 5)
  - ¿Qué tecnología usa? (Capa 6: GPU, LLM API, ML framework)
  - ¿Qué controles aplican? (Capa 7: Bias detection, XAI, oversight)
  - ¿Qué riesgos mitiga/introduce? (Capa 8)
  - ¿Qué valor entrega? (Capa 10)

Ejemplo_Completo:
  Agente: "AlgoRank_Hiring"
    Objetivo: "Contratar top talent eficientemente" (Capa 1)
    Capacidad: "Gestión recruiting" (Capa 2)
    Proceso: "Evaluar candidatos" → "Ranking inicial" (Capa 3)
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
      - "Bias algorítmico si training data sesgado" (10% prob) (Capa 8)
    Iniciativa: "Proyecto AI-Hiring-Q3-2024" (Capa 9)
    Valor:
      - Time-to-hire: 45 días → 28 días (-38%) (Capa 10)
      - Costo hiring: $5K → $3K (-40%) (Capa 10)
      - Quality-of-hire (1yr retention): 85% → 92% (+7pp) (Capa 10)
```

## §14. QUERIES CRÍTICOS

### Q1: Impact Analysis

```
PREGUNTA: "Si elimino Aplicación X, ¿qué se rompe?"

TRAZA:
  App_X → Soporta Procesos [P1, P2, P3]
         → P1-P3 realizan Capacidades [C1, C2]
                → C1-C2 contribuyen a Objetivos [O1]
                       → O1 entrega Valor [$2M/año revenue]

RESPUESTA:
  Impacto eliminar App_X:
    - 3 procesos (necesitan app alternativa)
    - 2 capacidades (quedan sin soporte)
    - 1 objetivo estratégico (en riesgo)
    - $2M/año valor (pérdida potencial)
  
  RECOMENDACIÓN: NO eliminar sin migración a App_Y
```

### Q2: Orphan Detection

```
PREGUNTA: "¿Qué aplicaciones no soportan ningún proceso?"

TRAZA:
  ∀ App_i:
    IF NOT EXISTS Proceso_j tal que App_i soporta Proceso_j
    THEN App_i es "orphan" (candidata retirement)

RESPUESTA:
  Apps_Orphan: [LegacyFax_System, OldCRM_v1, ReportGenerator_Deprecated]
  TCO_Total: $450K/año
  
  RECOMENDACIÓN: Decommission, recuperar $450K/año
```

### Q3: Value Tracing

```
PREGUNTA: "¿Qué iniciativas contribuyeron a 'Churn -3%' en Q4?"

TRAZA:
  Valor: Churn_Q4 = 5% (vs 8% Q3, delta -3%)
    ← Iniciativas: [I1_CustomerSuccess, I2_Churn_Prediction_ML]
      ← I1 mejoró Proceso: "Proactive outreach at-risk"
      ← I2 mejoró Proceso: "Identify churn risk 30d anticipado"
        ← Ambos contribuyen a Capacidad: "Customer retention"
          ← Capacidad soporta Objetivo: "Reduce churn a 5%"

RESPUESTA:
  I1 contribuyó -1.5% churn ($600K valor)
  I2 contribuyó -1.5% churn ($600K valor)
  Total: $1.2M/año
  
  ROI: I1 ($200K) → 300% | I2 ($300K) → 200%
```

### Q4: Compliance Gap

```
PREGUNTA: "¿Qué tecnologías GDPR-scope no tienen 'Encryption at rest'?"

TRAZA:
  ∀ Tech_i donde procesa_datos_EU(Tech_i) = True:
    IF NOT EXISTS Control_j tal que:
      Control_j = "Encryption at rest" AND
      Control_j aplica_a Tech_i
    THEN Tech_i es "gap GDPR"

RESPUESTA:
  Tech_Gaps: [Analytics_DB_Legacy, LogServer_Old]
  Risk: GDPR multa hasta €20M o 4% revenue global
  
  RECOMENDACIÓN: Iniciativa urgente "Encrypt Analytics_DB" (2 semanas)
```

## §15. HERRAMIENTAS DE TRAZABILIDAD

| Tipo | Ejemplos | Fortaleza | Limitación | Uso Recomendado |
|------|----------|-----------|------------|----------------|
| **Repository EA** | Ardoq, LeanIX, BiZZdesign | Modelado visual, dependencies, impact analysis | Requiere input manual, no auto-discovery | Capas 1-3, 8-10 (estrategia) |
| **Service Catalog** | ServiceNow CMDB, Backstage, OpsLevel | Auto-discovery apps/services, ownership tracking | Foco tech, débil en estrategia | Capas 4-6 (tech stack) |
| **Data Lineage** | Collibra, Alation, Apache Atlas | Data lineage granular (campo-level) | Solo datos, no end-to-end | Capa 5 (datos) |
| **Custom Graph DB** | Neo4j + modelo KERNEL custom | Flexibilidad total, queries complejas | Requiere desarrollo custom, mantenimiento | Full 10 capas (avanzado) |

### Implementación MVP (3 meses)

```yaml
Fase_1 (1 mes):
  - Modelar Capas 1-3 (Objetivos → Capacidades → Procesos) en Excel/Miro
  - 1 Objetivo piloto end-to-end

Fase_2 (1 mes):
  - Agregar Capas 4-5 (Apps → Datos)
  - Auto-discovery apps con Backstage

Fase_3 (1 mes):
  - Agregar Capas 6-10 (Tech → Controles → Riesgos → Iniciativas → Valor)
  - Primer impact analysis: "Si elimino App X, ¿qué falla?"

Escalamiento (12 meses):
  - Migrar a EA platform (Ardoq/LeanIX)
  - Integrar CMDB, Jira, financials (APIs, webhooks)
  - Automatizar actualizaciones
```

## §16. ANTI-PATRONES TRAZABILIDAD

| Anti-Pattern | Síntoma | Causa | Consecuencia | Fix |
|--------------|---------|-------|--------------|-----|
| **AP_T1: Documentación sin Uso** | Traza modelada, nadie consulta | No integrado workflows decisionales | Modelo desactualizado, no trusted | Integrar queries en ARB, portfolio review, incident postmortem |
| **AP_T2: Granularidad Extrema** | Modelar hasta función código | Confundir EA con code-level architecture | Mantenimiento imposible, modelo colapsa | Límite: Aplicación → Servicios (no funciones) |
| **AP_T3: Islas de Información** | Apps en CMDB, procesos en Wiki, riesgos en Excel | No sistema integrado | Impact analysis imposible | EA platform única o integración APIs |
| **AP_T4: Trazabilidad Post-Facto** | Modelar traza solo cuando auditor pide | No cultura data-driven | Modelo incompleto, gaps críticos | Mandato: Toda iniciativa actualiza modelo (DoD) |

## §17. VALIDACIÓN

### Completitud

```
¿Toda organización modelable con 10 capas? → SÍ
  Evidencia: 10 casos diversos (R1_Casos.md)
```

### Conectividad

```
¿Todas capas conectadas sin gaps? → SÍ
  Prueba: Existe path Objetivos → Valor para toda capa intermedia
```

### Utilidad

```
¿Queries críticos respondibles? → SÍ
  - Impact analysis: ✅
  - Orphan detection: ✅
  - Value tracing: ✅
  - Compliance gap: ✅
```

### Ortogonalidad

```
¿Overlaps entre capas? → NO
  Cada capa responsabilidad única y clara
```

## Referencias Cruzadas

- **Manifiesto (I3: Trazabilidad):** `CORE/00_Manifiesto.md` §2
- **Manifiesto (P3: Outside-In):** `CORE/00_Manifiesto.md` §3
- **Primitivos (Unidad_Trabajo):** `CORE/01_Primitivos.md` §7
- **4 Dominios:** `CORE/03_Arquitectura.md`
- **Observables (O1-O8):** `DOMINIOS/D2_Percepcion.md`
- **Delegación (M1-M6):** `CORE/04_Delegacion.md`
- **Validación formal:** `CORE/07_Validacion.md`
- **Casos aplicados:** `REFERENCIA/R1_Casos.md`

**Fin 06_Trazabilidad v2.0.0**
