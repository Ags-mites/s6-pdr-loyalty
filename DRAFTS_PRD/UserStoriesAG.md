E01 - Seguridad e Identidad - IAM

- HU 1.1:
	Como Super Admin, quiero autenticar me con email y contraseña, para acceder de forma segura al panel de configuración de Loyalty.

- HU 1.2:
	Como Super Admin, quiero crear perfiles de administrador de e-commerce con permisos limitados, para restringir acciones criticas como la eliminación de llaves o creación de perfiles

- HU 1.3: 
	Como Super Admin, quiero generar, revocar y rotar API Keys desde mi panel, para permitir que una plataforma e-commerce se conecte de forma segura al motor de descuentos .

E02 - Cálculo de descuentos

+ HU 2.1:
	Como personal de marketing, quiero definir el orden de prioridad de las reglas de descuentos, producto, fidelidad, temporada, para que el sistema aplique primero los descuentos mas críticos para mi negocio

+  HU 2.2:
	Como motor de descuentos, quiero clasificar al cliente basándome en su gasto y numero de compras totales recibidas por el e-comercio, para determinar el nivel del consumidor y aplicar el descuento correspondiente.
	
+  HU 2.3:
	Como personal de marketing, quiero aplicar un tope máximo de descuento, para asegurar que ninguna combinación de reglas afecte el margen de ganancia configurado 
	
+  HU 2.4:
	Como personal de marketing, quiero configurar los diferentes tipos de descuento, para asegurar que sigan las reglas y estrategias de marketing creadas. 

+  HU 2.5:
	Como e-commerce quiero recibir el cálculo final y las reglas del descuento aplicadas como respuesta del servicio de Loyalty, para mostrar al usuario final en el checkout