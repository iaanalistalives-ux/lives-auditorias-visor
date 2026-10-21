# CLAUDE.md — Visor de Auditorías de Taller (lives-auditorias-visor)

Las reglas generales de trabajo están en el repo privado `lives-instrucciones` (CLAUDE.md). Este archivo solo describe esta herramienta.

## Qué hace
`index.html` es una **consulta de solo lectura**: "Hojas escaneadas y prendas observadas". Junta las capturas de `lives-auditorias-taller` y las fotos de `lives-auditoria-final`.
- Filtros:
  - Búsqueda libre.
  - Cliente, tipo, taller, proceso y auditora.
  - Rango de fechas. Si no se elige fecha, la base trae lo más reciente.
- Indicadores: registros, fotos, registros con fotos de prendas y talleres.
- Tarjetas con la regla 500 y lo más reciente arriba.
- Al abrir una tarjeta se ven sus datos y sus fotos, en un visor que permite girar, ampliar y descargar.
- Excel LIVES con lo filtrado.
- No guarda, edita ni borra nada.

## Base de datos (Supabase lives-datos)
- `fotos_listar`: capturas de taller, de las tablas `fotos_registros` y `fotos_archivos`.
- `fotos_listar_final`: fotos de Auditoría Final, de las tablas `auditorias` y `fotos_auditoria`.
- Las dos se llaman a la vez. Si falla solo la de Auditoría Final, igual se muestra lo de taller, con un aviso.
- Fotos: enlaces firmados que vencen en 6 h. Taller usa el bucket `fotos-taller` y Auditoría Final el bucket `auditorias-fotos`; cada foto trae el nombre de su bucket.

## Quién la usa
Según las entradas por el portal de los últimos 30 días al 21/10/2026: 10 personas. Son supervisoras de calidad (3), auditoras de calidad (3), la digitadora de Calidad Manufactura y personal de Desarrollo.

## Quién puede ver
- Lo decide la función de permiso `fotos_puede_ver()`, con la sesión del portal y la tabla `permisos` (`lives-auditorias-visor` o `lives-auditorias-taller`).
- A Sistemas: `fotos_puede_ver` es la pieza que reemplazan con su seguridad.

## Pendientes vistos al escribir esto (21/10/2026)
- En el detalle, el título usa `GRUPO · ESTILO` sin descartar los vacíos, así que puede salir "undefined". La tarjeta sí los descarta.
