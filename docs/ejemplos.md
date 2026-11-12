# Ejemplos de instrucciones

Estas consultas utilizan herramientas existentes, siempre dentro de los permisos concedidos:

- “Listá mis tenants y pedime que elija uno antes de continuar.”
- “Mostrame los viajes activos del tenant seleccionado.”
- “Consultá las rendiciones pendientes de revisión.”
- “Buscá los CRT de esta semana y organizalos por cliente.”
- “Resumí los gastos registrados para este viaje.”
- “Mostrame los vehículos con viajes asignados.”

Antes de una escritura, el asistente debe mostrar la acción prevista y utilizar datos e identificadores confirmados. Para operaciones financieras debe conservar la misma `clave_idempotencia` al reintentar y generar una nueva para otra intención.
