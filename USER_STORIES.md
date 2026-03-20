Users Stories

HU 1:
Como usuario de LOYALTY,
Quiero iniciar sesión y cerrar sesión, 
Para acceder de forma segura al dashboard.

Scenario: Inicio de sesión exitoso
Given: que existe un usuario registrado en el LOYALTY
When: Intenta ingresar con credenciales válidas 
Then: El sistema le otorga el acceso
And: debe redirigir el usuario al Dashboard correspondiente según el rol con todas las funciones pertinentes

Scenario: Intento de inicio de sesión con credenciales erróneas 
Given: que existe un usuario registrado en el LOYALTY
When: Intenta ingresar con credenciales inválidas
Then: El sistema debe rechazar el ingreso de sesión 
And: Muestra un mensaje de credenciales inválidas

Scenario: Validación de campos obligatorios 
Given: que existe un usuario registrado en el LOYALTY
When: Intenta ingresar olvidando llenar los campos obligatorios
Then: El sistema debe negar la solicitud 
And: Muestra un mensaje de faltan campos obligatorios

HU 2:
Como Super Admin,
Quiero crear usuarios vinculados a un ecommerce,
Para garantizar que cada uno gestione únicamente sus propias reglas de descuento sin afectar a otros ecommerce.

Scenario: Creación de perfil asociado a un ecommerce específico
Given que existe un usuario con rol super admin
And un e-commerce contrató los servicios de LOYALTY
When el Super Admin crea un perfil de usuario asociado a ese ecommerce
Then el perfil queda vinculado exclusivamente a dicho ecommerce

HU 3:
Como Super Admin,
quiero gestionar y validar las API Keys de cada ecommerce,
para asegurar que solo sistemas autorizados puedan acceder a sus recursos en la plataforma.

HU 4. 
Como usuario de LOYALTY, 
Quiero crear, editar y eliminar reglas de temporada 
Para automatizar las promociones por demanda de temporada

HU 5:
Como usuario de LOYALTY, 
Quiero crear, editar y eliminar reglas por tipo de producto,
Para automatizar las promociones en base a inventario 


HU 6. Como usuario de LOYALTY,
Quiero definir los rangos de clasificación de fidelidad,
Para segmentar a los clientes y sus beneficios.

HU 9. Como usuario de LOYALTY ,
Quiero eliminar reglas de descuentos para cada temporada, 
Para poder tomar una decisión estratégica y eliminar aquellas reglas que no hayan resultado acorde a la temporada

HU 10. Como usuario de LOYALTY,
Quiero crear reglas de descuentos,
Para tipo de producto, para automatizar las promociones en base a inventario

HU 11. Como usuario de LOYALTY,
Quiero editar reglas de descuento,
Para tipo de producto para ajustar las promociones según las necesidades de rotación de inventario

HU 12. Como usuario de LOYALTY,
Quiero eliminar reglas de descuento para tipo de producto 
Para no seguir contando con promociones en determinado producto cuando no hay suficiente mercadería

HU 13. Como usuario de LOYALTY,
Quiero configurar los umbrales de compras para la clasificación de fidelidad,
Para definir qué clientes se clasifican como bronce, plata u oro.

HU 14. Como usuario de LOYALTY,
Quiero establecer un tope máximo global de descuentos permitidos, 
Para asegurar que la suma de los beneficios nunca comprometan el margen operativo.

HU 15. Como usuario de LOYALTY, 
Quiero definir el orden de prioridad de las reglas de descuentos, producto, fidelidad, temporada, 
Para que el sistema aplique primero los descuentos más críticos para mi negocio antes de llegar al tope máximo.

HU 16. Como motor de descuentos,
Quiero clasificar al cliente basándome en su gasto histórico y número de compras,
Para garantizar que reciba los beneficios correspondientes

HU 17. Como motor de descuentos, 
Quiero aplicar un tope máximo de descuento, 
Para asegurar que ninguna combinación de promociones afecte el margen de ganancia configurado

HU 18. Como e-commerce, quiero poder enviar un payload con el carrito y las métricas a un endpoint de LOYALTY y recibir el precio final y las reglas descuento calculado, para mostrarle al usuario final en el checkout el precio final y los beneficios aplicados.

HU 19. Como usuario de LOYALTY, 
Quiero consultar un registro de los descuentos aplicados en las transacciones de los últimos siete días, 
Para verificar que el motor de cálculo esté operando bajo los parámetros del tope máximo

HU 20. Como super admin,
Quiero ver el registro de los cambios de las reglas de descuento de todos los usuarios,
Para saber a qué hora y qué usuario modificó un descuento o tope máximo.