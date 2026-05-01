# SISPAR – Historias de usuario operativas (base de ejecución)

## EPIC 1: Campañas
### HU-OP-001 Crear campaña operativa
- Actor: Coordinador.
- Estado: `draft`.
- Reglas: instrumento obligatorio, fecha fin mayor a fecha inicio.
- Validación técnica: `instrument_version_id` obligatorio.

### HU-OP-002 Activar campaña
- Actor: Coordinador.
- Regla: no activar sin población asignada.
- Transición: `draft -> active`.

## EPIC 2: Segmentación y población
### HU-OP-010 Definir población objetivo
- Actor: Coordinador.
- Regla: no se permite población vacía.
- Persistencia: `operation_segment`.

## EPIC 3: Asignación
### HU-OP-020 Generar asignaciones
- Actor: Sistema.
- Regla: no duplicar participante por campaña.
- Persistencia: `operation_assignment`.

### HU-OP-021 Asignar aplicador
- Actor: Coordinador.
- Regla: aplicador activo obligatorio.

## EPIC 4: Ejecución offline
### HU-OP-030 Descargar tareas
- Actor: Aplicador.
- Resultado: persistencia local de tareas, participantes e instrumentos.

### HU-OP-031 Ejecutar instrumento
- Actor: Aplicador.
- Reglas: sin duplicados, contexto congelado.
- Validaciones: `uuid_local` obligatorio, `sync_status` obligatorio.
- Casos borde: cierre inesperado y desconexión.

## EPIC 5: Sincronización
### HU-OP-040 Sincronizar aplicaciones
- Actor: Sistema.
- Regla: idempotencia obligatoria.
- Estados: `queued -> syncing -> synced|error|conflict`.

### HU-OP-041 Manejo de conflictos
- Actor: Sistema.
- Resultado: registro de conflicto + log auditable.

## EPIC 6: Monitoreo
### HU-OP-050 Consultar avance
- Actor: Supervisor.
- Métricas: % ejecución, pendientes, completadas, cobertura.

### HU-OP-051 Detectar anomalías
- Actor: Supervisor.
- Reglas: tiempos fuera de rango, respuestas inconsistentes.

## EPIC 7: Cierre
### HU-OP-060 Cerrar campaña
- Actor: Coordinador.
- Regla: no cerrar con pendientes críticas.
- Efecto: bloquear nuevas aplicaciones.
