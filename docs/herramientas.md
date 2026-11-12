# Herramientas

PASO publica 27 herramientas:

- **Contexto:** `mi_cuenta`, `listar_tenants`, `seleccionar_tenant`, `catalogo_recursos`.
- **Datos:** `listar_registros`, `obtener_registro`, `crear_registro`, `actualizar_registro`, `archivar_registro`.
- **Gestión:** `consultar_informe`, `configurar_tenant`, `listar_usuarios_tenant`.
- **Documentos y finanzas:** `accion_documento`, `agregar_crt_a_mic`, `quitar_ultimo_crt_de_mic`, `crear_comprobante`, `registrar_pago`, `compensar_comprobantes`, `anular_operacion`.
- **Flota:** `registrar_stock`, `registrar_reparacion`.
- **Plataforma:** `administrar_listar_tenants`, `administrar_crear_tenant`, `administrar_editar_tenant`, `administrar_licencia`, `administrar_suspension`, `administrar_historial`.

Los esquemas completos están en [`tools.json`](../tools.json). Las herramientas administrativas requieren rol y credencial administrativa; las globales exigen además autorización de superadministración.

No existen herramientas de shell, SQL libre, lectura arbitraria de archivos, contraseñas ni acceso al servidor FoxPro.
