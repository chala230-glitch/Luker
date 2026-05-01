# SISPAR – Plan Maestro Integral (aterrizado a implementación)

## 1. Definición oficial
SISPAR es una **plataforma integral de medición** para diseñar, planificar, operar, ejecutar, analizar y gobernar instrumentos sobre población objetivo, con operación **offline-first**, sincronización robusta e idempotente, trazabilidad completa y lineamientos DAMA-DMBOK.

> SISPAR no es un sistema de encuestas; es un sistema de operación de medición.

## 2. Meta principal
Construir la radiografía longitudinal del participante para responder:
- Qué instrumentos ha realizado.
- Cuándo y cuántas veces.
- Qué resultados obtuvo.
- Bajo qué contexto.
- Cómo evoluciona en el tiempo.

## 3. Principios no negociables
1. Participante como eje.
2. Offline-first obligatorio.
3. Gobernanza de datos obligatoria.
4. Versionamiento obligatorio.
5. Separación de capas (maestro, operativa, transaccional, analítica, metadatos, sincronización).
6. Trazabilidad completa.
7. Idempotencia obligatoria en sincronización.

## 4. Arquitectura general por capas
1. **Capa Maestra**: participantes, contexto, atributos dinámicos.
2. **Capa Operativa (crítica)**: planeación, asignación, ejecución, monitoreo.
3. **Capa Transaccional**: aplicaciones y respuestas.
4. **Capa Analítica**: resultados y agregaciones.
5. **Capa de Metadatos**: instrumentos y versiones.
6. **Capa de Sincronización**: API, colas y control de idempotencia.

## 5. Módulos del sistema
- `mdm_participant`
- `mdm_context`
- `mdm_dynamic_attributes`
- `instrument_engine`
- `application_engine`
- `result_engine`
- `mobile_api`
- `pwa_offline_app`
- `operational_management` (crítico)

## 6. Gestión operativa (diseño funcional)
### 6.1 Propósito
Orquestar el ciclo completo de medición desde planeación hasta cierre.

### 6.2 Submódulos
- Planeación de campañas.
- Cargue y administración de maestros operativos de población.
- Segmentación.
- Asignación operativa.
- Agenda y planeación logística.
- Gestión de aplicadores/equipo de campo.
- Ejecución offline.
- Monitoreo.
- Control de calidad.
- Gestión de novedades operativas (crítico).
- Cierre operativo.

## 7. Modelo de datos operativo (núcleo)
- `operation_campaign`
- `operation_population_master`
- `operation_population_load`
- `operation_population_load_detail`
- `operation_population_segment`
- `operation_segment`
- `operation_assignment`
- `operation_task`
- `operation_executor`
- `operation_logistic_team`
- `operation_work_plan`
- `operation_agenda`
- `operation_agenda_item`
- `operation_route`
- `operation_incident`
- `operation_incident_type`
- `operation_incident_log`
- `operation_progress`
- `operation_validation`

## 8. Flujo end-to-end
1. Crear participantes o cargar maestros poblacionales.
2. Caracterizar población objetivo.
3. Crear instrumento y versión.
4. Crear campaña.
5. Cargar/validar maestros operativos.
6. Segmentar población.
7. Construir agenda y plan logístico.
8. Asignar equipo, rutas, jornadas y tareas.
9. Descargar offline.
10. Ejecutar aplicaciones.
11. Registrar novedades de campo.
12. Reprogramar/escalar.
13. Sincronizar.
14. Calcular resultados.
15. Analizar.
16. Cerrar operación.

## 9. Historias de usuario priorizadas (fase inicial)
- HU-OP-001 Crear campaña operativa.
- HU-OP-002 Activar campaña.
- HU-OP-010 Definir población objetivo.
- HU-OP-020 Generar asignaciones.
- HU-OP-021 Asignar aplicador.
- HU-OP-030 Descargar tareas offline.
- HU-OP-031 Ejecutar instrumento.
- HU-OP-040 Sincronizar aplicaciones.
- HU-OP-041 Manejo de conflictos.
- HU-OP-050 Consultar avance.
- HU-OP-051 Detectar anomalías.
- HU-OP-060 Cerrar campaña.

## 10. Criterios técnicos obligatorios
- `uuid_local` obligatorio en aplicaciones offline.
- `sync_status` obligatorio con máquina de estados.
- Backend como fuente única de verdad.
- Idempotencia en endpoint de sincronización.
- Trazabilidad de cambios y auditoría por evento.

## 11. Fases
- F0: Arquitectura.
- F1: Maestro.
- F2: Instrumentos.
- F3: Operación (crítica).
- F4: Aplicación.
- F5: Sincronización.
- F6: Resultados.
- F7: Analítica.

## 12. Definición de terminado
- Funciona offline en condiciones reales.
- Sin duplicados en sincronización.
- Trazabilidad completa de punta a punta.
- QA aprobado (funcional, datos y seguridad).
