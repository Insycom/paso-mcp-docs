# PASO MCP

Documentación pública del servidor MCP de **PASO — Plataforma de Administración y Seguimiento de Operaciones**.

- Producción: `https://mcp.paso.sys.ar/mcp`
- Sandbox: `https://mcp.demo.paso.sys.ar/mcp`
- Transporte: Streamable HTTP
- Catálogo: [`tools.json`](tools.json)

El catálogo contiene 89 herramientas. PASO admite tokens personales y autorización OAuth con PKCE. El cliente descubre el recurso protegido en `https://mcp.paso.sys.ar/.well-known/oauth-protected-resource`. La autorización ofrece los alcances solicitados por el cliente y permitidos a la cuenta: `paso.read`, `paso.write` y `paso.admin`. Para administrar desde un asistente, el cliente debe solicitar el alcance administrativo y la persona debe autorizarlo para los tenants correspondientes. Verificá el alcance efectivo con `mi_cuenta`.

## Configuración de referencia

```json
{
  "mcpServers": {
    "paso": {
      "type": "http",
      "url": "https://mcp.demo.paso.sys.ar/mcp",
      "headers": {
        "Authorization": "Bearer TU_TOKEN_MCP"
      }
    }
  }
}
```

El formato exacto depende del cliente. Nunca coloques el token en la URL ni lo publiques en archivos versionados.

## Guías

- [Usuarios, permisos y disponibilidad de flota](docs/roles-invitaciones-flota.md)

- [Conexión](docs/conexion.md)
- [Tenants y permisos](docs/permisos.md)
- [Herramientas](docs/herramientas.md)
- [Seguridad](docs/seguridad.md)
- [Ejemplos de instrucciones](docs/ejemplos.md)

Copyright © INSYCOM. Ver [licencia de la documentación](LICENSE.md).
