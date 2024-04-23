# BASE-DE-DATOS

8. [Triggers] ()


-Cliente:

Trigger antes de la inserción para validar la edad del cliente:

CREATE TRIGGER validar_edad_cliente
BEFORE INSERT ON clientes
FOR EACH ROW
BEGIN
    IF NEW.edad < 18 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'El cliente debe ser mayor de edad';
    END IF;
END;

-Trigger después de la eliminación para registrar la eliminación en un registro de auditoría:

CREATE TRIGGER registro_eliminacion_cliente
AFTER DELETE ON clientes
FOR EACH ROW
BEGIN
    INSERT INTO registro_auditoria (accion, tabla_afectada, id_afectado, fecha)
    VALUES ('Eliminación', 'clientes', OLD.id_cliente, NOW());
END;

-Ofertas:

-Trigger antes de la inserción para validar la fecha de vencimiento de la oferta:

CREATE TRIGGER validar_fecha_vencimiento_oferta
BEFORE INSERT ON ofertas
FOR EACH ROW
BEGIN
    IF NEW.fecha_vencimiento < CURDATE() THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'La fecha de vencimiento de la oferta debe ser en el futuro';
    END IF;
END;

-Trigger después de la eliminación para actualizar el recuento de ofertas para el cliente asociado:

CREATE TRIGGER actualizar_recuento_ofertas_cliente
AFTER DELETE ON ofertas
FOR EACH ROW
BEGIN
    UPDATE clientes
    SET cantidad_ofertas = cantidad_ofertas - 1
    WHERE id_cliente = OLD.cliente;
END;

-Operaciones del taller:

-Trigger antes de la inserción para verificar la disponibilidad del empleado:

CREATE TRIGGER verificar_disponibilidad_empleado
BEFORE INSERT ON operacionesTaller
FOR EACH ROW
BEGIN
    DECLARE empleado_disponible INT;
    SELECT COUNT(*) INTO empleado_disponible
    FROM operacionesTaller
    WHERE empleado = NEW.empleado AND fecha = NEW.fecha;
    
    IF empleado_disponible >= 2 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'El empleado ya tiene asignadas 2 operaciones para este día';
    END IF;
END;

-Trigger después de la eliminación para actualizar el estado del vehículo asociado:

CREATE TRIGGER actualizar_estado_vehiculo
AFTER DELETE ON operacionesTaller
FOR EACH ROW
BEGIN
    UPDATE vehiculo
    SET estado = 'Disponible'
    WHERE id_vehiculo = OLD.vehiculo;
END;

-Vehículo:

-Trigger antes de la inserción para validar la matrícula del vehículo:

CREATE TRIGGER validar_matricula_vehiculo
BEFORE INSERT ON vehiculo
FOR EACH ROW
BEGIN
    IF LENGTH(NEW.matricula) != 7 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'La matrícula del vehículo debe tener 7 caracteres';
    END IF;
END;

-Trigger después de la eliminación para eliminar registros relacionados en la tabla "clientes":

CREATE TRIGGER eliminar_registros_relacionados_clientes
AFTER DELETE ON vehiculo
FOR EACH ROW
BEGIN
    DELETE FROM clientes WHERE vehiculo = OLD.id_vehiculo;
END;

-Empleado:

-Trigger antes de la inserción para asignar un código de empleado único:

CREATE TRIGGER asignar_codigo_empleado
BEFORE INSERT ON empleado
FOR EACH ROW
BEGIN
    SET NEW.codigo_empleado = CONCAT('EMP-', LPAD((SELECT COUNT(*) + 1 FROM empleado), 4, '0'));
END;

-Trigger después de la eliminación para eliminar registros relacionados en la tabla "operacionesTaller":

CREATE TRIGGER eliminar_registros_relacionados_operaciones
AFTER DELETE ON empleado
FOR EACH ROW
BEGIN
    DELETE FROM operacionesTaller WHERE empleado = OLD.id_empleado;
END;
