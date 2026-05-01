# Baseline de Gobernanza de Datos (Fase 1)

## 1. Roles mínimos DAMA
- **Data Owner**: responsable de decisiones sobre calidad, acceso y uso del dato por dominio.
- **Data Steward**: custodio operativo de definiciones, reglas y trazabilidad.
- **Tech Owner**: responsable técnico de integración, seguridad, disponibilidad y continuidad.
- **Comité de Datos**: órgano de priorización, control de riesgos y aprobación de políticas.

## 2. Artefactos obligatorios
1. Catálogo de Datos Institucional.
2. Arquitectura de Datos Maestros.
3. Diccionario de datos por entidad crítica.
4. Matriz RACI de gobernanza.
5. Matriz de acceso y segregación de funciones.
6. Contratos de datos (JSON Schema) versionados.

## 3. Políticas mínimas
1. Clasificación de datos por sensibilidad (público, interno, sensible, restringido).
2. Mínimo privilegio para accesos y trazabilidad de cambios.
3. Versionado de encuestas, estructuras y contratos API.
4. Reglas de calidad automáticas en cargues y sincronización.
5. Gestión de respaldo, retención y portabilidad de datos.
6. Cumplimiento de tratamiento de datos personales (Ley 1581/2012, Decreto 1377/2013).

## 4. Reglas iniciales de calidad
- Completitud de campos obligatorios ≥ 98%.
- Unicidad de identificadores clave = 100%.
- Integridad referencial entre entidades maestras ≥ 99.5%.
- Validez de formatos críticos (documento, fecha, código DANE) = 100%.

## 5. Checklist de release
- [ ] Comité de Datos revisó y aprobó cambios de estructura.
- [ ] Diccionario y catálogo de datos actualizados.
- [ ] Contratos JSON Schema versionados y validados.
- [ ] Reglas de calidad ejecutadas en ambiente QA (sin fallos críticos).
- [ ] Evidencias de auditoría y linaje generadas.
- [ ] Validación de privacidad y seguridad completada.
