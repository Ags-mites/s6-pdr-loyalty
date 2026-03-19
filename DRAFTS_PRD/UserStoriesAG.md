E01 - Seguridad e Identidad - IAM

- HU 1.1:
	Como Super Admin, quiero autenticar me con email y contraseña, para acceder de forma segura al panel de configuración de Loyalty.

- HU 1.2:
	Como Super Admin, quiero crear perfiles para marketing con permisos limitados, para restringir acciones criticas como manipulación de API KEYS o eliminación de configuraciones críticas.

- HU 1.3: 
	Como Super Admin, quiero generar, revocar y rotar API Keys desde mi panel, para asegurar que solo las plataformas de e-commerce autorizadas consuman el motor de descuentos .

E02 - Cálculo de descuentos

+ HU 2.1:
	Como personal de marketing, quiero definir el orden de prioridad de las reglas de descuentos, producto, fidelidad, temporada, para que el sistema aplique primero los descuentos mas críticos para mi negocio antes de llegar al tope máximo.

+  HU 2.2:
	Como motor de descuentos, quiero clasificar al cliente basándome en su gasto y numero de compras totales recibidas por el e-comercio, para determinar el nivel del consumidor y aplicar el descuento correspondiente.
	
+  HU 2.3:
	Como personal de marketing, quiero aplicar un tope máximo de descuento, para asegurar que ninguna combinación de reglas afecte el margen de ganancia configurado 

+  HU 2.4:
	Como e-commerce quiero recibir el cálculo final y las reglas del descuento aplicadas como respuesta del servicio de Loyalty, para mostrar al usuario final en el checkout

E03 - Dashboard

+ HU 3.1:
	Como personal de marketing, quiero crear, editar y eliminar reglas de descuentos para tipo de producto y temporada, para que sigan las reglas y estrategias de marketing creadas. 

+ HU 3.2:
	Como personal de marketing, quiero configurar los umbrales de compras para la clasificación de fidelidad, para definir que clientes se clasifican como bronce, plata u oro.

+ HU 3.3:
	Como personal de marketing, quiero establecer un tope máximo global y por campaña para asegurar que la suma de los beneficios nunca comprometan el margen operativo

E04 - Auditoria

+ HU 4.1:
	Como analista de negocio, quiero consultar un registro de los descuentos aplicados en cada transacción, para verificar que el motor de calculo este operando bajo los parámetros del tope máximo.

+ HU 4.2
	Como dueño, quiero ver el registro de los cambios de las reglas de descuento, para saber que administrador modifico un descuento o tope máximo.