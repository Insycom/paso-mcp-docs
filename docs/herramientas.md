# Herramientas MCP

Las 89 herramientas se descubren mediante `tools/list`. La cuenta, el tenant, la licencia, los módulos y la credencial determinan qué operaciones se pueden ejecutar. El [catálogo JSON](../tools.json) contiene los esquemas de entrada y salida.

### `mi_cuenta`

Identidad autenticada, rol efectivo y tenants disponibles para esta credencial. No devuelve secretos.

### `listar_tenants`

Lista exclusivamente los tenants autorizados por la cuenta y la credencial, con sus licencias.

### `seleccionar_tenant`

Valida el tenant de trabajo y devuelve su contexto. Conservá tenant_id para las llamadas siguientes.

### `catalogo_recursos`

Describe campos, tipos, referencias, condiciones y recursos disponibles antes de crear o editar registros.

### `listar_registros`

Consulta registros de un tenant con búsqueda y paginación. No mezcla información de otros tenants.

### `obtener_registro`

Obtiene un registro y su versión actual dentro del tenant autorizado.

### `abrir_documento_web`

Devuelve el enlace autenticado a la vista imprimible oficial de un CRT o MIC/DTA en PASO. No compone otro documento.

### `crear_registro`

Crea un maestro o borrador. Consultá el catálogo; para comprobantes, pagos o stock usá las herramientas específicas.

### `actualizar_registro`

Actualiza campos usando la versión leída. Rechaza conflictos y modificaciones de documentos bloqueados.

### `archivar_registro`

Archiva un registro cuando sus referencias lo permiten. Requiere intención explícita del usuario.

### `consultar_informe`

Consulta resumen operativo, cuentas corrientes, informe mensual o historial de acciones del tenant.

### `crear_comprobante`

Registra FC/NC/ND interna. Contado cancela automáticamente. Reutilizá la clave solo al reintentar la misma operación.

### `registrar_pago`

Registra un cobro o pago con sus imputaciones. Valida saldos, tercero, moneda y duplicados.

### `compensar_comprobantes`

Aplica una nota de crédito a una factura/nota de débito compatible sin superar el saldo disponible.

### `registrar_stock`

Registra entrada o salida de repuestos con su motivo. No permite stock negativo cuando se controla.

### `registrar_reparacion`

Registra una reparación y su consumo de stock dentro de la misma transacción.

### `accion_documento`

Confirma, factura o reabre CRT/MIC, o cierra una rendición. Conserva versión, permisos e idempotencia.

### `agregar_crt_a_mic`

Agrega un CRT al MIC/DTA. Crea hoja principal o continuación consecutiva según la lógica de ARTRANS.

### `quitar_ultimo_crt_de_mic`

Quita únicamente la última hoja del MIC/DTA para conservar la numeración consecutiva de ARTRANS.

### `anular_operacion`

Anula y revierte una operación cuando sus relaciones lo permiten. Requiere intención explícita del usuario.

### `configurar_tenant`

Configura moneda base y datos de empresa. Exige permiso MCP de administración y rol administrador.

### `listar_usuarios_tenant`

Lista usuarios del tenant. Exige cuenta administradora y credencial de administración.

### `administrar_listar_tenants`

Lista global de tenants. Solo superadministrador con credencial de administración para todos sus tenants.

### `administrar_usuarios`

Lista usuarios globales, empresas y roles. Requiere administración global.

### `administrar_crear_usuario`

Crea un usuario con sus roles y empresas. Requiere administración global.

### `administrar_editar_usuario`

Modifica el acceso global y las empresas del usuario. Requiere administración global.

### `administrar_desactivar_usuario`

Desactiva el acceso del usuario conservando su historial. Requiere administración global.

### `administrar_consultar_correo`

Consulta la configuración pública de avisos SMTP. Requiere administración global.

### `administrar_configurar_correo`

Actualiza la configuración de correo de plataforma. Requiere administración global.

### `administrar_probar_correo`

Envía un mensaje de prueba al destinatario indicado. Requiere administración global.

### `administrar_avisos`

Consulta los últimos avisos enviados o pendientes. Requiere administración global.

### `administrar_catalogo_modulos`

Consulta el catálogo general de módulos. Requiere administración global.

### `administrar_rol_usuario`

Actualiza el rol del usuario en el tenant con control de versión. Requiere administración global.

### `administrar_modulos_tenant`

Consulta habilitación y versión de los módulos del tenant.

### `administrar_habilitacion_modulo`

Habilita o pausa un módulo para el tenant seleccionado. Requiere administración global.

### `administrar_crear_tenant`

Crea un tenant y su licencia inicial. Requiere superadministración global expresamente autorizada en la credencial.

### `administrar_editar_tenant`

Edita nombre, contacto y notas de un tenant con control de versión. Solo superadministración global.

### `administrar_licencia`

Asigna, renueva o reemplaza una licencia por meses. Solo superadministración global; exige versión actual.

### `administrar_suspension`

Suspende o reactiva el acceso de un tenant sin borrar datos. Solo superadministración global.

### `administrar_historial`

Consulta auditoría global. Solo superadministrador con credencial global de administración.

### `ingresar_cubierta`

Ingresa una cubierta individual al depósito.

### `mover_cubierta`

Registra un movimiento o medición con versión de la cubierta.

### `consultar_cubiertas`

Consulta la posición, el estado y la versión de cada cubierta desde el último ID.

### `consultar_conexiones_telematicas`

Consulta recursos configurados, estado, cursor y reintentos del tenant.

### `configurar_sincronizacion_rfms`

Habilita o pausa un recurso contractual rFMS. Requiere administración del tenant.

### `configurar_sincronizacion_fleetboard`

Habilita o pausa un recurso SOAP del perfil Fleetboard contratado para el tenant.

### `consultar_historial_conciliado`

Consulta evidencia, identidad, procedencia y decisión de las filas aplicadas.

### `consultar_costos_mantenimiento`

Agrupa costos por origen y moneda para el período solicitado.

### `conciliar_vin`

Vincula un VIN observado a un equipo del mismo tenant.

### `consumo_por_periodo`

Calcula consumo con distancia e intervalos válidos para un VIN y proveedor.

### `abrir_orden_taller`

Abre una OT y reserva los repuestos disponibles.

### `actualizar_orden_taller`

Registra atención, cierre o anulación de OT.

### `cotizar_compra_taller`

Registra una oferta comparable de proveedor.

### `aprobar_compra_taller`

Aprueba una oferta con al menos tres proveedores.

### `recibir_compra_taller`

Recibe un remito y reserva el material de la OT.

### `registrar_lectura_tablero`

Registra lectura manual visible, con confirmación explícita de vuelta del contador.

### `relevar_urea`

Registra clasificación observada y fecha del relevamiento.

### `registrar_servicio_preventivo`

Registra el servicio de un ítem de la unidad.

### `configurar_plan_preventivo`

Registra la política y los intervalos de una tarea preventiva.

### `actualizar_acople`

Abre o termina el acople entre equipos existentes.

### `publicar_plantilla_diaria`

Publica una nueva versión de plantilla diaria.

### `registrar_checklist_diario`

Registra el control detallado de una plantilla y abre sus fallas.

### `registrar_checklist_porteria`

Registra ingreso, egreso o taller, con autorización de egreso y OT por incumplimiento.

### `cerrar_falla_diaria`

Registra acción, responsable y fecha de cierre de una falla.

### `crear_elemento_inventario`

Crea un elemento fungible o una pieza con serie.

### `registrar_movimiento_inventario`

Registra transferencia, préstamo, devolución, recepción, pérdida o conteo.

### `justificar_diferencia_inventario`

Registra la causa y el acta de una diferencia de inventario.

### `rotar_cubiertas`

Permuta dos montajes vigentes en una transacción.

### `reemplazar_cubierta`

Retira al destino indicado y monta desde depósito en una transacción.

### `cargar_csv_mantenimiento`

Previsualiza CSV de stock, km o enganches y aplica el lote con su hash confirmado.

### `registrar_cobertura_semanal`

Define cobertura de fuente y nómina obligada de una semana de checklists.

### `preparar_importacion_mantenimiento`

Abre o recupera una carga SQLite por tenant y SHA-256.

### `cargar_fragmento_importacion_mantenimiento`

Carga un fragmento base64 en orden y devuelve el próximo índice.

### `finalizar_carga_importacion_mantenimiento`

Verifica integridad, hash y versión del archivo recibido.

### `consultar_importacion_mantenimiento`

Consulta el estado y los bytes recibidos para reanudar una carga.

### `simular_importacion_mantenimiento`

Genera el plan y enumera fuentes pendientes sin aplicar efectos.

### `listar_conflictos_importacion_mantenimiento`

Devuelve hasta 50 incidencias a partir del ordinal.

### `resolver_conflicto_importacion_mantenimiento`

Registra una decisión explícita y genera otra revisión.

### `aplicar_importacion_mantenimiento`

Aplica hasta 100 decisiones del plan indicado desde su checkpoint. Repetir con el nuevo checkpoint para continuar.

### `pausar_importacion_mantenimiento`

Pausa entre lotes.

### `reanudar_importacion_mantenimiento`

Habilita la continuación desde el checkpoint.

### `ficha_equipo_mantenimiento`

Consulta preventivos, urea, acople y odómetro de una unidad a la fecha indicada.

### `consultar_orden_taller`

Consulta la OT, reservas y solicitudes de compra relacionadas.

### `capacidades_telematicas`

Consulta recursos contratados, soporte y presencia de datos para un VIN.

### `mensajes_telematicos`

Página de mensajes permitidos con medidas normalizadas y campos adicionales del contrato.

### `revertir_importacion_mantenimiento`

Evalúa dependencias y revierte altas en depósito con confirmación y motivo.

### `kilometros_por_montaje_y_acople`

Asigna distancia medida a cubiertas y semirremolques según sus períodos comprobados.

### `informe_mantenimiento`

Consulta movimientos, stock, bajas, proveedores, costos y alertas filtrados por fecha, marca y equipo.

### `cumplimiento_checklists`

Consulta documentos y semanas cumplidas por chofer, con denominadores y semanas sin evidencia.
