# BASE-DE-DATOS
## Inserciones, modificaciones y eliminación de datos
## Inserciones:

- Inserción de un nuevo cliente junto con su vehículo asociado:

INSERT INTO vehiculo (marca, modelo, matricula) VALUES ('Mazda', 'CX-5', 'PQR678');
INSERT INTO clientes (nombre, apellido1, apellido2, vehiculo) VALUES ('Laura', 'González', 'Martínez', LAST_INSERT_ID());

- Inserción de una nueva oferta para un cliente existente:

INSERT INTO ofertas (descripcion, cliente) VALUES ('Oferta de mantenimiento gratuito por un año', 2);

## Modificaciones:

- Modificación del trabajo de un empleado:

UPDATE empleado SET trabajo = 'Mecánico especializado en motores' WHERE id_empleado = 1;

- Modificación de la descripción de una operación en el taller:

UPDATE operacionesTaller SET descripcion = 'Revisión de frenos y cambio de discos' WHERE id_operacion = 3;

## Eliminaciones:

- Eliminación de un cliente y su vehículo asociado:

DELETE FROM clientes WHERE id_cliente = 4;

- Eliminación de una oferta específica:

DELETE FROM ofertas WHERE id_oferta = 3;
