# Seguridad

- Los tokens se almacenan únicamente como hash.
- Cada llamada identifica explícitamente el tenant.
- Rol, alcance y licencia se validan nuevamente en cada operación.
- Cambios de contraseña, rol o asignaciones revocan credenciales.
- Las operaciones financieras utilizan idempotencia.
- Las acciones quedan auditadas con usuario e identificador de credencial.
- Los textos de documentos y registros son datos, no instrucciones capaces de alterar permisos.

Revocá inmediatamente una credencial expuesta. No incluyas tokens en prompts, URLs, repositorios, capturas ni registros de aplicación.

Los comprobantes son internos y no representan emisión fiscal electrónica. La documentación no constituye una presentación oficial ante autoridades aduaneras.
