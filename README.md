# BASE-DE-DATOS
## Procedimientos almacenados

- Procedimiento Almacenado para Actualizar el Estado del Vehículo:

DELIMITER //

CREATE PROCEDURE ActualizarEstadoVehiculo (
    IN p_id_vehiculo INT,
    IN p_nuevo_estado VARCHAR(50)
)
BEGIN
    UPDATE vehiculo
    SET estado = p_nuevo_estado
    WHERE id_vehiculo = p_id_vehiculo;
END //

DELIMITER ;

- Procedimiento Almacenado para Obtener Detalles de Cliente y Vehículo:

DELIMITER //

CREATE PROCEDURE ObtenerDetallesClienteVehiculo (
    IN p_id_cliente INT
)
BEGIN
    SELECT 
        c.id_cliente, c.nombre, c.apellido1, c.apellido2,
        v.id_vehiculo, v.marca, v.modelo, v.matricula
    FROM
        clientes c
    INNER JOIN
        vehiculo v ON c.vehiculo = v.id_vehiculo
    WHERE
        c.id_cliente = p_id_cliente;
END //

DELIMITER ;
