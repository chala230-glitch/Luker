# Blueprint de encuestas EGMA/EGRA para Odoo v18 + PWA

## Objetivo
Traducir los instrumentos compartidos (matemáticas y lenguaje) en un diseño implementable y gobernable para Odoo Community v18, App PWA offline-first y API versionada.

## 1) Estructura del instrumento

### 1.1 Sección de consentimiento y contexto
- Script de presentación del aplicador.
- Confirmación de comprensión del estudiante.
- Registro de inicio (timestamp, aplicador, dispositivo).

### 1.2 Ficha de estudiante
Campos mínimos:
- Tipo de documento (TI, CE, NES, PEP, PPT, RC, VISA).
- Número de identificación.
- Nombre completo.
- Género.
- Institución / sede.
- Grado / grupo / jornada / ubicación.
- Fecha de nacimiento / edad.
- Estado del estudiante (precargado / nuevo).

### 1.3 Secciones EGMA (matemáticas)
- Lectura de números.
- Escritura de números.
- Comparación de números.
- Número faltante.
- Completar suma o resta.
- Sumas cronometradas.
- Restas cronometradas.

### 1.4 Secciones EGRA (lenguaje)
- Conocimiento del sonido de letras.
- Lectura de pasaje.
- (Siguiente iteración) comprensión lectora y fluidez por minuto.

## 2) Tipos de ítems recomendados
- `single_choice`: correcto/incorrecto/no responde.
- `numeric_input`: para respuesta numérica abierta.
- `reading_prompt`: estímulo de lectura con evaluación del aplicador.
- `timed_grid`: batería de operaciones con cronómetro.
- `metadata_only`: datos operativos del levantamiento.

## 3) Reglas de puntuación
- Cada ítem debe definir `answer_key` y `score_weight`.
- Estado "no responde" puntúa 0 y marca bandera para analítica de abandono.
- Guardar `raw_response`, `scored_value` y `scoring_version` para trazabilidad.
- Soportar recalificación histórica al cambiar reglas de scoring.

## 4) Reglas de calidad de datos (fase 1)
1. No permitir envío sin identificación del estudiante y del aplicador.
2. Validar consistencia edad vs fecha de nacimiento.
3. Restringir catálogo de tipo de documento y jornada.
4. Bloquear duplicado exacto (mismo estudiante + mismo instrumento + misma fecha + mismo aplicador), salvo override con motivo.
5. Timestamps obligatorios: inicio, primera respuesta, fin, sincronización.

## 5) Modelo operativo offline-first
- La PWA captura todo localmente con `sync_status = pending`.
- Reintentos automáticos exponenciales para sincronización.
- Resolución de conflicto por versión + prioridad de evento más reciente (con log de conflicto).
- No borrar datos locales hasta recibir `server_ack`.

## 6) Diseño de auditoría y gobernanza
- Versionar cada instrumento (`instrument_version`).
- Registrar cambios de preguntas, claves de respuesta y pesos.
- Guardar evidencia de quién aplicó, quién corrigió y quién aprobó publicación.
- Comité de Datos aprueba versiones antes de entrar a producción.

## 7) Backlog técnico inmediato
1. Crear modelo de datos de instrumento/ítem/respuesta.
2. Parametrizar catálogos maestros de estudiante y contexto escolar.
3. Implementar endpoint de sincronización batch con validaciones.
4. Implementar motor de scoring para EGMA/EGRA v1.
5. Construir tablero de calidad y completitud por sede/jornada/grado.
