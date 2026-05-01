# Revisión técnica crítica y plan de implementación (alineado a propuesta Fundación Luker)

## Contexto actualizado
Con la información compartida, el proyecto objetivo ya está claramente definido: construir una plataforma institucional de datos educativos sobre **Odoo Community v18**, con enfoque **offline-first**, integración multi-fuente (incluyendo SIMAT) y gobernanza basada en **DAMA-DMBOK**.

## 1) Conclusiones de desarrollo (críticas y accionables)
1. La propuesta funcional está bien orientada (captura, validación, analítica y gobernanza), pero requiere una **traducción inmediata a artefactos técnicos versionados** (modelo de datos, APIs, reglas de calidad, backlog ejecutable).
2. La arquitectura de 5 capas es adecuada para fase 1, pero se debe formalizar con contratos de integración, SLAs y mecanismos de observabilidad.
3. El mayor riesgo no es tecnológico: es la **madurez operativa de gobernanza** (Comité, roles, decisiones y disciplina de calidad).
4. El enfoque SaaS + Odoo Community v18 permite escalar, pero exige políticas explícitas de portabilidad, respaldo, seguridad, cifrado y continuidad.
5. Se requiere alinear el cronograma macro (28 semanas) con entregables verificables por sprint para evitar desalineación entre “avance percibido” y “avance demostrado”.

## 2) Metodología recomendada
### Modelo de ejecución
- **Híbrido Ágil + DAMA-DMBOK** (confirmado):
  - Ágil para construcción incremental de valor.
  - DAMA-DMBOK para gobierno, calidad, metadatos y responsabilidad del dato.

### Cadencia sugerida
- Sprints de 2 semanas.
- Demo funcional obligatoria por sprint.
- Comité de Datos quincenal con acta de decisiones.
- Puerta de calidad (Quality Gate) antes de cada despliegue.

### Entregables base por sprint
- Historias terminadas con criterio de aceptación.
- Evidencia de pruebas.
- Reglas de calidad de datos ejecutadas.
- Trazabilidad entre requisito → modelo → API → tablero.

## 3) Tiempos de desarrollo (alineados al plan recibido)
### Plan maestro (28 semanas)
1. **Semanas 1–4**: Kick-Off, Comité de Datos, Catálogo de Datos, Arquitectura de Datos Maestros.
2. **Semanas 5–8**: Diseño técnico y configuración Odoo (CRM, Contactos, Encuestas, DMS), seguridad y permisos.
3. **Semanas 9–16**: Desarrollo Gestor Operativo + App PWA offline-first + API REST versionada.
4. **Semanas 17–22**: Pruebas, validación institucional, tableros y métricas.
5. **Semanas 23–28**: Capacitación, adopción, despliegue productivo y cierre fase 1.

### Hitos de control recomendados
- H1 (Semana 1): Acta de inicio y definición formal de roles.
- H2 (Semana 4): Catálogo y arquitectura maestra publicados y aprobados.
- H3 (Semana 12): Integración Odoo + Gestor Operativo + PWA en entorno de pruebas.
- H4 (Semana 20): Validación institucional + manual de implementación.
- H5 (Semana 28): Go-live y acta de cierre fase 1.

## 4) Productividad
### KPIs ejecutivos
- Lead time por historia y por incidencia.
- Velocidad por sprint (historias comprometidas vs completadas).
- % despliegues exitosos.
- Defectos críticos por release.
- % reglas de calidad de datos aprobadas.
- Tiempo de resolución de fallos de sincronización offline.

### Indicadores de gobernanza
- % datasets críticos con Data Owner asignado.
- % elementos del catálogo con definición semántica y linaje.
- % APIs con contrato JSON Schema y versionado.
- Cumplimiento de comité (sesiones realizadas / planificadas).

## 5) Comparativo: lo que se debe llevar vs lo que tenemos en el repositorio
| Dimensión | Objetivo del proyecto | Estado repositorio actual | Brecha |
|---|---|---|---|
| Odoo v18 parametrizado | CRM, Contactos, Encuestas, DMS operativos | No implementado | Alta |
| Gestor Operativo | Cargue/validación multi-fuente | No implementado | Alta |
| PWA offline-first | Captura en campo y sincronización | No implementado | Alta |
| API REST + contratos | Endpoints versionados + JSON Schema | No implementado | Alta |
| Catálogo de Datos | Definición, origen, trazabilidad | Sólo lineamientos iniciales | Media-Alta |
| Arquitectura de Datos Maestros | Entidades, relaciones y metadata | No implementado | Alta |
| Gobierno DAMA | Roles, comité, políticas, métricas | Baseline documental básico | Media |
| Seguridad y cumplimiento | Accesos, auditoría, cifrado, respaldo | No implementado | Alta |

## 6) Inicio de mejoras (arranque inmediato)
1. Crear backlog fase 1 con épicas: Odoo, Gestor Operativo, PWA, Integraciones, Gobernanza.
2. Definir diccionario de datos mínimo viable (estudiante, docente, institución, encuesta, evidencia).
3. Diseñar contratos JSON Schema v1 para las primeras integraciones.
4. Establecer reglas de calidad iniciales (completitud, unicidad, consistencia referencial).
5. Documentar RACI de gobernanza y protocolo del Comité de Datos.
6. Configurar ambientes Dev/QA/Prod con criterios de promoción.

## 7) Reestructuración para cumplimiento de gobernanza de datos
Se recomienda evolucionar la estructura del repositorio a:

```text
/docs
  /architecture
  /adr
  /data-governance
  /legal
/data-contracts
  /simat
  /surveys
/odoo
  /modules
  /config
/pwa
/integration
  /connectors
  /api
/tests
/.github/workflows
```

### Controles de gobernanza obligatorios de fase 1
- Catálogo de datos institucional versionado.
- Arquitectura de datos maestros con dueños de dato.
- Matriz de acceso por rol y segregación de funciones.
- Auditoría de cambios en encuestas, cargues y datos críticos.
- Versionado de contratos API y trazabilidad de transformaciones.
- Política de respaldo/retención/portabilidad de datos.
- Cumplimiento legal de tratamiento de datos personales (Ley 1581 de 2012 y Decreto 1377 de 2013).

## Riesgos críticos y mitigación priorizada
- **Datos (Alta):** inconsistencias de origen → validación automática + muestreo manual + bitácora de calidad.
- **Gobernanza (Media):** retrasos en comité/roles → formalización semana 1 + actas vinculantes.
- **Técnico (Media):** incompatibilidades Odoo/módulos → matriz de compatibilidad + pruebas tempranas.
- **Adopción (Media):** resistencia al cambio → capacitación práctica por perfiles + soporte de adopción.
- **Infraestructura (Baja):** indisponibilidad SaaS → respaldo automático + monitoreo + recuperación probada.

## Próximo paso de ejecución
En la siguiente iteración se debe construir el **paquete de arranque técnico**: plantillas de catálogo de datos, RACI, contratos JSON Schema iniciales y checklist de release con quality gates.

## Avance aplicado con insumos de encuesta
Con base en los instrumentos compartidos, se incorporaron dos activos iniciales al repositorio:
1. Blueprint funcional/técnico de EGMA/EGRA para parametrización en Odoo + PWA.
2. Contrato de datos JSON Schema para respuestas de encuesta con validaciones de calidad.

## Alineación estratégica SISPAR
Se incorpora la definición oficial: **SISPAR no es un sistema de encuestas**, es un sistema integral de operación de medición. Esto obliga a priorizar en el backlog el módulo `operational_management` (planeación, agenda, asignación, monitoreo y novedades) al mismo nivel del motor de instrumentos y sincronización.
