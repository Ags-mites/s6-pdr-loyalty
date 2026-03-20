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
And un ecommerce contrató los servicios de LOYALTY
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

HU 6. 
Como usuario de LOYALTY,
Quiero definir los rangos de clasificación de fidelidad,
Para segmentar a los clientes y sus beneficios.

HU 7. 
Como usuario de LOYALTY,
Quiero definir el tope maximo y la prioridad de descuentos,
Para proteger la rentabilidad del negocio.

HU 8. 
Como motor de descuentos,
Quiero clasificar al cliente segun el payload recibido 
Para asignar su nivel de descuento.

HU 9. 
Como ecommerce, 
Quiero enviar el carrito y recibir el precio final con descuentos aplicados, 
Para mostrarle al usuario final en el checkout.

HU 10. 
Como usuario de LOYALTY, 
Quiero consultar los descuentos aplicados en las transacciones de los últimos siete días, 
Para verificar que el motor de cálculo esté operando bajo las reglas y topes máximos configurados.

HU 11. 
Como super admin,
Quiero ver el registro de los cambios de las reglas de descuento de todos los ecommerce,
Para identificar que usuarios realizaron modificaciones y en que momentos.

HU 12. 
Como usuario de LOYALTY,
Quiero poder activar o desactivar reglas con un solo click
Para reaccionar rápidamente a cambios en el mercado sin tener que borrar la configuración.
