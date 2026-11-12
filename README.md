# PASO MCP

Documentación pública del servidor MCP de **PASO — Plataforma de Administración y Seguimiento de Operaciones**.

- Producción: `https://mcp.paso.sys.ar/mcp`
- Sandbox: `https://mcp.demo.paso.sys.ar/mcp`
- Transporte: Streamable HTTP
- Catálogo: [`tools.json`](tools.json)

PASO ofrece 27 herramientas para agentes externos. No incluye actualmente un agente propio. La conexión usa un token Bearer personal en clientes compatibles con encabezados; OAuth guiado para ChatGPT y Claude continúa en desarrollo.

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

- [Conexión](docs/conexion.md)
- [Tenants y permisos](docs/permisos.md)
- [Herramientas](docs/herramientas.md)
- [Seguridad](docs/seguridad.md)
- [Ejemplos de instrucciones](docs/ejemplos.md)

Copyright © INSYCOM. Ver [licencia de la documentación](LICENSE.md).
