# BASE-DE-DATOS

5. Vistas

-Persona 1: Analista de Datos y Métricas

Vista de Análisis de Participación de Clientes:

Esta vista proporciona un análisis detallado de la participación de los clientes en las ofertas ofrecidas por la aplicación. Incluiría métricas como la frecuencia de participación de los clientes en ofertas específicas, la tasa de conversión de las ofertas en ventas, el valor promedio de compra por cliente después de recibir una oferta, y otros datos relevantes para evaluar la efectividad de las estrategias de marketing y retención de clientes.

CREATE VIEW AnalisisParticipacionClientes AS
SELECT
    clientes.id_cliente,
    clientes.nombre,
    clientes.apellido1,
    clientes.apellido2,
    ofertas.id_oferta,
    ofertas.descripcion AS descripcion_oferta,
    COUNT(*) AS cantidad_ofertas_recibidas,
    AVG(ofertas.valor_compra) AS promedio_valor_compra
FROM
    clientes
JOIN
    ofertas ON clientes.id_cliente = ofertas.cliente
GROUP BY
    clientes.id_cliente, ofertas.id_oferta;


Vista de Análisis de Interfaz de Usuario (UI):

Esta vista proporcionaría un análisis exhaustivo de la interfaz de usuario actual de la aplicación. Incluiría métricas como la tasa de interacción con elementos de la interfaz, el tiempo promedio de completación de tareas, los puntos de fricción identificados durante las pruebas de usabilidad, y cualquier retroalimentación de los usuarios sobre la usabilidad y el diseño de la interfaz. La vista también podría incluir recomendaciones para mejorar la usabilidad y la experiencia del usuario en la aplicación, basadas en los datos recopilados y el análisis realizado.

CREATE VIEW AnalisisInterfazUsuario AS
SELECT
    usuario_id,
    nombre_pantalla,
    COUNT(*) AS cantidad_interacciones,
    AVG(duracion_interaccion) AS duracion_promedio_interaccion
FROM
    registros_interacciones_usuario
GROUP BY
    usuario_id, nombre_pantalla;
