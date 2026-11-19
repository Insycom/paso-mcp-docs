# Usuarios, permisos y disponibilidad de flota

| Tarea | Web y API de la aplicación | MCP |
|---|---|---|
| Invitar al tenant activo | Gestión → Usuarios → Invitar por correo. La web llama a `POST /api/v1/usuarios/invitar` con sesión administrativa y CSRF. | La invitación por correo se emite desde la web. |
| Aceptar | El destinatario abre el enlace y define su contraseña. La web llama a `POST /api/v1/invitaciones/aceptar`. | El destinatario completa este paso en PASO. |
| Crear, consultar y editar perfiles | Gestión → Usuarios → Roles y permisos. `GET` y `POST /api/v1/perfiles-operativos`, `PUT /api/v1/perfiles-operativos/{clave}`. | La definición de perfiles se gestiona en la web. |
| Asignar rol | Usuarios → Permisos. `PATCH /api/v1/usuarios/{ident}/rol` recibe `rol` y `version`. | `administrar_rol_usuario` requiere autorización global. |
| Consultar estados y documentos | Disponibilidad de flota. `GET /api/v1/flota-disponibilidad`. | El catálogo actual carece de una herramienta de disponibilidad y vencimientos. |
| Cambiar estado | Desde la fila del equipo. `PUT /api/v1/flota-disponibilidad/{ident}`. | El cambio de estado se realiza por web o REST. |
| Consultar la unidad y sus trabajos | Ficha de unidad, mapa de cubiertas y órdenes. | `ficha_equipo_mantenimiento`, `consultar_cubiertas` y `consultar_orden_taller`. |

## Invitar y asignar acceso

Elegí el tenant y completá usuario, correo y rol. Para invitar a un responsable del taller elegí **Jefe de taller**. PASO envía un enlace de un solo uso con vigencia de 24 horas. El usuario se crea al aceptar y después ingresa con su contraseña. Un reenvío válido reemplaza el enlace anterior. La administración global también puede invitar desde Accesos globales. Conservá el token de aceptación dentro del correo del destinatario.

Los perfiles operativos se asignan por tenant. Los predefinidos incluyen Jefe de taller, Compras, Mecánico, Gomero y Mecánico / gomero. Chofer, Operador logístico y Administrador tienen circuitos propios. El chofer requiere una cuenta vinculada al chofer operativo. Gomero puede escribir en gomería y leer los maestros de referencia. Operador logístico puede consultar disponibilidad y operar logística. La superadministración corresponde a la cuenta de plataforma.

Para crear un perfil, elegí una plantilla o empezá con los permisos vacíos. Por ejemplo, el cuerpo de creación para un rol de gomería con consulta de equipos es:

```json
{"nombre":"Gomería turno noche","permisos":{"gomeria":"escritura","datos.equipos":"lectura"}}
```

Las claves omitidas quedan sin acceso. El catálogo de perfiles devuelve áreas y claves vigentes. Para editar, conservá la clave devuelta y enviá la versión leída. Para cambiar la asignación de una persona usá su `version_rol` como `version`. El cambio de asignación revoca sus sesiones y credenciales. La licencia, la habilitación de Mantenimiento y el alcance de la credencial se verifican además del rol.

## Disponibilidad y vencimientos

La consulta devuelve `estados` y una lista `items` con ID, patente, tipo, estado, versión, nota y vencimientos de RTO, póliza y permiso. Todos los perfiles del tenant con licencia vigente pueden consultarla. Para modificar el equipo se requiere Taller habilitado y autorización de escritura en disponibilidad o administración. Leé la versión actual antes de guardar. Ejemplo sintético de cuerpo para una unidad cuya versión leída es 3:

```json
{"estado":"externo","nota":"Reparación en taller externo","version":3}
```

| Valor | Significado |
|---|---|
| `activo` | Activo |
| `baja` | Baja |
| `mantenimiento` | En mantenimiento |
| `externo` | En mantenimiento externo |
| `prolongado` | Fuera de servicio prolongado |

Un viaje asignado bloquea pasar el equipo fuera de servicio. La asignación del viaje comprueba la disponibilidad del tractor y del semirremolque acoplado. Ante un conflicto `409`, consultá de nuevo la unidad y el viaje antes de decidir. El estado documental se calcula por fecha local argentina y se muestra por separado del estado operativo.

| Días hasta la fecha | Indicador |
|---|---|
| Menos de 0 | `vencido` |
| 0 a 29, incluido hoy | `por_vencer` |
| 30 o más | `vigente` |
| Fecha ausente o inválida | `sin_dato` |

## Recorrido de consulta con un asistente

1. Consultá `mi_cuenta` y `listar_tenants`. Usá el ID autorizado en cada llamada que lo requiera.
2. Buscá la patente con `listar_registros` sobre `equipos`. Verificá la coincidencia y conservá el ID.
3. Consultá `ficha_equipo_mantenimiento` con ese ID y una fecha de corte explícita. Revisá las posiciones de cubiertas y las órdenes asociadas.
4. Abrí una orden con `consultar_orden_taller` usando su propio ID. Para conocer el estado operativo y los tres vencimientos, consultá Disponibilidad de flota.

## Importación y telemetría

Para importar desde MCP se requiere Mantenimiento habilitado y una credencial administrativa autorizada para el tenant. Prepará la carga con el tamaño y SHA-256 del archivo SQLite. Enviá los fragmentos en orden, finalizá la carga y simulá antes de aplicar. Listá los conflictos por página y registrá las decisiones. Aplicá la revisión elegida por lotes de hasta 100 decisiones. Consultá el checkpoint para continuar después de una pausa. Los nombres y los argumentos exactos de cada herramienta figuran en el catálogo MCP.

Para telemetría, verificá las capacidades del proveedor y el vehículo, la conciliación por VIN y el período de cobertura. La sincronización depende de una conexión habilitada y de recursos contratados. Una lectura de nivel de combustible o AdBlue expresa nivel; el consumo por distancia requiere contadores compatibles y distancia medida. Conservá los valores ausentes como desconocidos.

[Catálogo MCP](https://github.com/Insycom/paso-mcp-docs/blob/main/tools.json) · [API para integradores](https://github.com/Insycom/paso-api-docs/blob/main/openapi.json)
