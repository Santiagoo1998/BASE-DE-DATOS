# BASE-DE-DATOS

## Consultas multitabla

- Consultar todas las ofertas disponibles junto con la información de los clientes que las han recibido:

SELECT ofertas.id_oferta, ofertas.descripcion AS descripcion_oferta, 
       clientes.nombre AS nombre_cliente, clientes.apellido1 AS apellido_cliente, 
       vehiculo.marca AS marca_vehiculo, vehiculo.modelo AS modelo_vehiculo
FROM ofertas
JOIN clientes ON ofertas.cliente = clientes.id_cliente
JOIN vehiculo ON clientes.vehiculo = vehiculo.id_vehiculo;

- Consultar todas las operaciones realizadas en el taller, incluyendo la información del empleado y del vehículo relacionado:

SELECT operacionesTaller.id_operacion, empleado.nombre AS nombre_empleado, 
       empleado.apellido1 AS apellido_empleado, vehiculo.marca AS marca_vehiculo, 
       vehiculo.modelo AS modelo_vehiculo, operacionesTaller.descripcion AS descripcion_operacion
FROM operacionesTaller
JOIN empleado ON operacionesTaller.empleado = empleado.id_empleado
JOIN vehiculo ON operacionesTaller.vehiculo = vehiculo.id_vehiculo;
