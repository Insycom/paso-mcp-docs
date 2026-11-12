# Tenants y permisos

| Permiso | Alcance |
|---|---|
| Lectura | Contexto, catálogos, registros e informes. |
| Escritura | Lectura y operaciones autorizadas por el rol. |
| Administración | Configuración y administración permitidas por el rol. |

Cada herramienta vuelve a validar usuario, credencial, tenant, rol y licencia. El asistente debe llamar primero a `mi_cuenta` y `listar_tenants`, validar el elegido con `seleccionar_tenant` e incluir `tenant_id` en cada operación.

No existe un tenant global compartido entre conversaciones, clientes ni la interfaz web. Una credencial nunca permite acceder a un tenant ajeno.
