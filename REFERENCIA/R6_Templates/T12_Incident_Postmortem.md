# T12: Incident Postmortem Template

**Propósito:** Análisis estructurado y sin culpa de incidentes para prevenir recurrencia.
**Audiencia:** Equipos de ingeniería, SRE, Product Owners.

---

## INCIDENT SUMMARY

```yaml
ID: [YYYYMMDD-ShortName]
Fecha: [YYYY-MM-DD]
Inicio: [HH:MM UTC]
Fin: [HH:MM UTC]
Duración: [Horas, Minutos]
Severidad: [SEV-1 (Crítico) a SEV-4 (Bajo)]
Impacto: [Resumen 1-2 frases: ej. "Checkout caído para 30% usuarios por 45 min"]
Owner: [Persona que lidera el postmortem]
```

---

## TIMELINE (5-Minute Granularity)

| Hora (UTC) | Evento |
|------------|--------|
| 14:30 |  alerta `HighLatencyAPI` en Datadog |
| 14:32 | SRE on-call (Jane) notificado por PagerDuty |
| 14:35 | Jane inicia war room en Slack #incidents |
| 14:40 | Se confirma impacto cliente: fallos en checkout |
| 14:45 | Hipótesis 1: Deploy reciente (feature flag X) |
| 14:52 | Rollback de feature flag X → sin efecto |
| 15:05 | Hipótesis 2: Sobrecarga DB por query ineficiente |
| 15:15 | Se identifica query en logs de PostgreSQL |
| 15:22 | Rollback de deploy que introdujo la query |
| 15:28 | Métricas de latencia y error rate vuelven a la normalidad |
| 15:30 | Incidente declarado resuelto |
| 16:00 | Postmortem agendado para el día siguiente |

---

## ROOT CAUSE ANALYSIS (The 5 Whys)

**Principio:** No culpar a personas, culpar a fallos del sistema.

1.  **¿Por qué falló el checkout?**
    - Porque la base de datos estaba sobrecargada y no respondía a tiempo.

2.  **¿Por qué se sobrecargó la base de datos?**
    - Porque una nueva query ineficiente estaba consumiendo todos los recursos.

3.  **¿Por qué se desplegó una query ineficiente a producción?**
    - Porque no fue detectada durante el code review ni en los tests automatizados.

4.  **¿Por qué no fue detectada en los tests?**
    - Porque nuestro entorno de staging no tiene una carga de datos representativa de producción, por lo que la query parecía rápida.

5.  **¿Por qué nuestro staging no es representativo?**
    - Porque no tenemos un proceso automatizado para sanear y replicar datos de producción a staging. **(Causa Raíz Sistémica)**

---

## ACTION ITEMS (SMART)

| ID | Acción | Tipo | Owner | ETA |
|----|--------|------|-------|-----|
| AI-1 | Crear script para sanear y replicar datos de prod a staging | Prevención | DevOps Team | 2 semanas |
| AI-2 | Añadir alerta para queries de larga duración en Datadog | Detección | SRE Team | 1 semana |
| AI-3 | Implementar `EXPLAIN ANALYZE` en el pipeline de CI para PRs de DB | Prevención | Platform Team | 3 semanas |
| AI-4 | Documentar este incidente en el runbook de "DB Overload" | Mitigación | SRE Team | 3 días |
| AI-5 | Revisar otros servicios que podrían tener queries similares | Prevención | Backend Guild | 1 mes |

**Tipos de Acción:**
- **Prevención:** Evita que el problema vuelva a ocurrir.
- **Detección:** Ayuda a encontrar el problema más rápido la próxima vez.
- **Mitigación:** Reduce el impacto si el problema vuelve a ocurrir.

---

## LECCIONES APRENDIDAS

1.  **Lo que salió bien:**
    - La alerta de latencia funcionó como se esperaba.
    - El on-call respondió en menos de 2 minutos.
    - El rollback del deploy fue rápido y efectivo.

2.  **Lo que podría haber salido mejor:**
    - El tiempo para identificar la causa raíz fue de 40 minutos. Podríamos mejorarlo con mejores logs.
    - La comunicación con stakeholders (soporte, negocio) fue reactiva.

3.  **Dónde tuvimos suerte:**
    - El incidente ocurrió fuera de las horas pico de compra.
    - El ingeniero que escribió la query estaba disponible para ayudar a diagnosticar.

---

## IMPACTO CUANTIFICADO

- **Usuarios afectados:** ~15,000 (30% de usuarios activos durante 45 min)
- **Transacciones fallidas:** ~1,200
- **Pérdida de ingresos estimada:** ~$60,000
- **Tiempo de ingeniería invertido:** ~20 horas-persona (diagnóstico + postmortem)

---

## CHECKLIST POSTMORTEM

☐ **Blameless:** El análisis se centra en el sistema, no en las personas.
☐ **Timeline detallado:** Eventos clave con timestamps precisos.
☐ **Causa raíz sistémica:** Se llegó más allá del error humano o técnico superficial.
☐ **Action Items SMART:** Específicos, Medibles, Alcanzables, Relevantes, con Plazo.
☐ **Owners asignados:** Cada Action Item tiene un dueño claro.
☐ **Tickets creados:** Se han creado tickets en Jira/Asana para cada Action Item.
☐ **Compartido:** El postmortem ha sido compartido con toda la organización de ingeniería.

---

**Referencias:**
- P42_SRE_Practices (A1_Patrones.md)
- D2_Percepcion.md
