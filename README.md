# BASE-DE-DATOS
## Consultas monotablas (Si sois cuatro 8 consultas, 2 cada  uno de vosotros)
### Consultar todos los clientes y sus vehículos asociados:
SELECT clientes.nombre, clientes.apellido1, clientes.apellido2, vehiculo.marca, vehiculo.modelo
FROM clientes
JOIN vehiculo ON clientes.vehiculo = vehiculo.id_vehiculo;
### Consultar todas las operaciones realizadas en el taller:
SELECT empleado.nombre AS nombre_empleado, empleado.apellido1 AS apellido_empleado, 
       vehiculo.marca AS marca_vehiculo, vehiculo.modelo AS modelo_vehiculo, 
       operacionesTaller.descripcion AS descripcion_operacion
FROM operacionesTaller
JOIN empleado ON operacionesTaller.empleado = empleado.id_empleado
JOIN vehiculo ON operacionesTaller.vehiculo = vehiculo.id_vehiculo;
