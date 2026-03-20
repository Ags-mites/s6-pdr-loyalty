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

Scenario: Validar que el usuario solo accede a su ecommerce
Given que existe un usuario asociado a un ecommerce,
When el usuario inicia sesión,
Then solo puede visualizar y gestionar información de su ecommerce
And no puede acceder a datos de otros ecommerce

HU 3:
Como Super Admin,
quiero gestionar y validar las API Keys de cada ecommerce,
para asegurar que solo sistemas autorizados puedan acceder a sus recursos en la plataforma.

Scenario: Crear una clave de acceso para un ecommerce válido
Given que soy un Super Admin con acceso al sistema,
And existe un ecommerce registrado,
When creo una nueva clave de acceso para ese ecommerce,
Then el sistema genera la clave de acceso correctamente.

Scenario: Ver las claves de acceso de un ecommerce
Given que soy un Super Administrador con acceso al sistema
And existen claves de acceso registradas para un ecommerce
When consulto las claves de acceso de ese ecommerce
Then el sistema muestra la lista de claves de acceso asociadas
And oculta parte de la información de cada clave para proteger su seguridad

HU 4. 
Como usuario de LOYALTY, 
Quiero crear, editar y eliminar reglas de temporada 
Para automatizar las promociones por demanda de temporada

Scenario: Creación exitosa de una regla de temporada
Given no hay una regla activa para esa temporada,
When se registra una regla de descuento con vigencia y beneficio válidos,
Then la regla queda almacenada en el sistema,
And la regla queda disponible para su aplicación durante la vigencia definida.

Scenario: Rechazo de creación por superposición de fechas
Given ya hay una regla activa para esa temporada
When se intenta registrar una nueva regla con las mismas fechas
Then el sistema rechaza el registro
And informa el conflicto de superposición de fechas entre reglas de temporada

Scenario: Edición exitosa de una regla de temporada
Given existe una regla de temporada registrada
When se actualizan sus condiciones con valores válidos
Then el sistema conserva la regla con la nueva configuración
And la versión actualizada es la considerada para nuevas evaluaciones

Scenario: Rechazo de edición por incumplir rangos
Given existen límites de descuento definidos 
When la actualización propuesta excede los límites permitidos
Then el sistema rechaza la modificación
And mantiene la última configuración válida

Scenario: Eliminación exitosa de una regla de temporada
Given existe una regla de temporada registrada
When se confirma su eliminación
Then la regla deja de participar en evaluaciones futuras

Scenario: Rechazo de eliminación de regla inexistente
Given no existe una regla asociada al identificador solicitado
When se solicita su eliminación
Then el sistema rechaza la operación
And informa que no existe una regla para el identificador solicitado

Scenario: Rechazo de edición de regla inexistente
Given no existe una regla asociada al identificador solicitado
When se solicita su edición 
Then el sistema rechaza la operación
And informa que no existe una regla para el identificador solicitado

HU 5:
Como usuario de LOYALTY, 
Quiero crear, editar y eliminar reglas por tipo de producto,
Para automatizar las promociones en base a inventario 

Scenario: Creación exitosa de una regla por tipo de producto
Given no hay una regla activa para ese tipo de producto
When se define una nueva regla de descuento con parámetros válidos.
Then la regla queda registrada
And la regla puede ser aplicada por el motor

Scenario: Rechazo de creación por duplicidad
Given existe una regla para el mismo tipo de producto
When se registra una regla
Then el sistema rechaza la creación
And reporta conflicto de reglas para ese tipo de producto

Scenario: Edición exitosa de una regla por tipo de producto
Given existe una regla por tipo de producto registrada
When se modifican sus parámetros dentro de los límites permitidos
Then el sistema guarda la nueva versión
And las nuevas evaluaciones consideran la configuración actualizada

Scenario: Rechazo de edición por datos incompletos
Given la regla requiere tipo de producto y beneficio para ser válida
When la actualización omite uno o más datos obligatorios
Then el sistema rechaza la modificación
And mantiene la versión previamente válida

Scenario: Eliminación exitosa de una regla por tipo de producto
Given existe una regla por tipo de producto
When se solicita su eliminación
Then la regla deja de estar disponible para nuevas transacciones

Scenario: Rechazo de eliminación por regla no encontrada
Given no existe una regla para el tipo de producto indicado
When se intenta eliminar la regla
Then el sistema rechaza la operación
And mantiene sin cambios la configuración 

Scenario: Rechazo de edición de regla inexistente
Given no existe una regla asociada al tipo de producto indicado
When se solicita su edición 
Then el sistema rechaza la operación
And informa que no existe una regla para el identificador solicitado

HU 6. 
Como usuario de LOYALTY,
Quiero definir los rangos de clasificación de fidelidad,
Para segmentar a los clientes y sus beneficios.

Scenario: Configuración exitosa de rangos de fidelidad
Given los rangos propuestos son completos y no se superponen
When se registran los nuevos umbrales de clasificación
Then el sistema guarda la configuración de rangos
And la segmentación de clientes utiliza los nuevos umbrales

Scenario: Rechazo por superposición de rangos
Given existen reglas de clasificación que requieren exclusividad entre niveles
When se define una configuración con rangos superpuestos
Then el sistema rechaza la configuración
And reporta inconsistencia en la definición de niveles

Scenario: Rechazo por discontinuidad o vacíos en rangos
Given la clasificación exige cobertura continua del dominio definido
When se registra una configuración con vacíos entre rangos
Then el sistema rechaza la configuración
And mantiene la última segmentación válida

Scenario: Rechazo por orden inválido de niveles
Given los niveles deben mantener progresión ascendente de exigencia
When se define un nivel superior con umbral menor o igual que uno inferior
Then el sistema rechaza la configuración
And notifica incumplimiento de jerarquía de fidelidad

Scenario: Aplicación efectiva de la nueva segmentación
Given la configuración de rangos fue aceptada
When el motor clasifica a un cliente con métricas vigentes
Then el cliente queda asignado al nivel correspondiente a su rango
And los beneficios aplicables se determinan según ese nivel


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
