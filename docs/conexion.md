# Conexión

1. Ingresá a PASO con tu cuenta.
2. Abrí **Asistentes IA · MCP → Autorizar asistente**.
3. Elegí nombre, permiso, vigencia y tenants.
4. Guardá el token mostrado una única vez.
5. Configurá la URL `/mcp` y el encabezado `Authorization: Bearer ...` en el cliente.

La credencial es personal, revocable y diferente de una clave API REST. Las cuentas de chofer no pueden emitir credenciales MCP.

Para sandbox solicitá una credencial de prueba. Los tokens de sandbox no funcionan en producción.


## OAuth en clientes compatibles

PASO admite tokens personales y autorización OAuth con PKCE. El cliente descubre el recurso protegido en `https://mcp.paso.sys.ar/.well-known/oauth-protected-resource`. La autorización ofrece los alcances solicitados por el cliente y permitidos a la cuenta: `paso.read`, `paso.write` y `paso.admin`. Para administrar desde un asistente, el cliente debe solicitar el alcance administrativo y la persona debe autorizarlo para los tenants correspondientes. Verificá el alcance efectivo con `mi_cuenta`.
