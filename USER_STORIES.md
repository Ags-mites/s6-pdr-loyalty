Users Stories

## HU 1:
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

### Definition of Ready (DoR)
* Historia claramente entendida por el equipo, flujo de login/logout y ciclo de vida del token definido.
* Criterios de aceptación completos.
* Reglas de negocio definidas:

> Política de sesiones concurrentes.
> Redirección estricta según el rol del usuario Super Admin vs. Admin de Ecommerce.
> Tiempo de Vida TTL de la sesión establecido.

* Diseño de base de datos de usuarios con campos para intentos fallidos y logs de acceso disponible.
* Definición del mecanismo de autenticación ej. JWT, cookies HttpOnly acordada.
* Mensajes de error unificados evitar revelar si el usuario existe o si la contraseña es la incorrecta; usar "Credenciales inválidas".

### Definition of Done (DoD)
* Código implementado y revisado - code review aprobado.
* Pruebas unitarias:

> Generación, firmado y validación de expiración del token JWT.
> Algoritmo de validación de contraseñas hasheadas.

* Pruebas de integración:

> Login exitoso y generación correcta del payload del token.
> Redirección en el frontend/backend basada en los claims del rol.
> Protección de rutas privadas retorno de HTTP 401/403.

* Pruebas de seguridad:

> Bloqueo de cuenta tras 5 intentos fallidos.
> Protección contra inyección SQL en los campos de email y contraseña.

* Manejo de sesiones:

> Expiración de sesión validada forzando el timeout en pruebas.
> Logout añade el token a una blacklist o invalida la cookie correctamente.

* Validaciones y Edge Cases Casos Borde:

> Intento de envío de payload con campos nulos o vacíos.
> Intento de login de un usuario que ha sido desactivado lógicamente.

* QA validado en ambiente de pruebas.
* Sin bugs críticos o bloqueantes.

---

## HU 2:
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

### Definition of Ready (DoR)
* Historia claramente entendida flujo de creación de usuarios y aislamiento de datos.
* Criterios de aceptación completos incluye el rechazo de operaciones si el id no coincide.
* Reglas de negocio definidas:

> Aislamiento estricto: Todo usuario excepto Super Admin, debe tener un id inmutable.
> Un Super Admin no puede crear un usuario sin vincularlo a un ID de ecommerce válido y existente.

* Diseño de base de datos actualizado: Entidad Ecommerce creada y relación obligatoria 1:N con la tabla Usuarios.
* Estrategia de filtrado global de consultas a base de datos definida por el equipo backend.

### Definition of Done (DoD)
* Código implementado y revisado code review aprobado.
* Pruebas unitarias:

> Validar que la asignación del ID del ecommerce en la entidad usuario sea inmutable post-creación.

* Pruebas de integración:

> Creación exitosa del perfil vinculando correctamente el UUID del ecommerce.
> Verificar que al consultar un recurso de otro ecommerce, el sistema responde con HTTP 403 Forbidden o 404 Not Found.

* Pruebas de seguridad:

> Prevención de vulnerabilidades IDOR Insecure Direct Object Reference manipulando IDs en la URL.

* Validaciones y Edge Cases Casos Borde:

> Super Admin intenta crear un usuario asociándolo a un ID de ecommerce que no existe.
> Intento de inyectar un tenant_id distinto mediante manipulación del LocalStorage o Headers en el navegador.

* QA validado en ambiente de pruebas.
* Sin bugs críticos o bloqueantes.

---

## HU 3:
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

### Definition of Ready (DoR)
* Historia claramente entendida flujo de generación, almacenamiento seguro y visualización parcial.
* Criterios de aceptación completos incluye soporte para rotación de claves sin caídas de servicio.
* Reglas de negocio definidas:

> Permitir un máximo de dos API Keys activas simultáneamente por ecommerce para permitir la rotación.
> La API Key solo se muestra completa una única vez al momento de la creación.

* Diseño de base de datos: Tabla de api_keys con campos de hash unidireccional, prefijo para visualización, y estado activa/revocada.
* Definición de mecanismo criptográfico SHA-256 para el hash, generación de cadenas criptográficamente seguras.

### Definition of Done (DoD)
* Código implementado y revisado code review aprobado.
* Pruebas unitarias:

> Generación de prefijos y aplicación del hashing unidireccional de la API Key.
> Función de enmascaramiento visual para la interfaz.

* Pruebas de integración:

> Creación, listado y revocación de API Keys en base de datos.
> Validación de middleware: Rechazo de peticiones S2S usando una clave revocada o inexistente.

* Pruebas de seguridad:

> Imposibilidad de recuperar la clave original desde la base de datos o cualquier endpoint post-creación.

* Validaciones y Edge Cases Casos Borde:

> Intento de generar una tercera API Key cuando el límite de negocio dos ya está alcanzado.
> Envío de una petición S2S en el milisegundo exacto en que la clave es marcada como revocada.

* QA validado en ambiente de pruebas.
* Sin bugs críticos o bloqueantes.

---

## HU 4:
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

### Definition of Ready (DoR)
* Historia claramente entendida por el equipo flujo de evaluación temporal estandarizado.
* Criterios de aceptación completos.
* Reglas de negocio definidas:

> Obligatoriedad de uso del estándar en formato UTC para todas las fechas.
> Definición de precedencia si una regla inicia exactamente en el milisegundo que otra termina.

* Diseño de base de datos actualizado para soportar índices de rangos de fechas sin superposición.
* Tipos de descuento y sus límites documentados en la historia.

### Definition of Done (DoD)
* Código implementado y revisado code review aprobado.
* Pruebas unitarias:

> Algoritmo de detección de solapamiento de fechas.
> Conversión y evaluación de timestamps UTC vs Locales.

* Pruebas de integración:

> CRUD completo de la regla en base de datos.
> Aplicación activa de la regla en el motor solo dentro del rango [inicio, fin).

* Manejo de Reglas de Negocio:

> Rechazo automático de fechas de fin menores o iguales a las de inicio.

* Validaciones y Edge Cases:

> Edición de una regla que actualmente está en ejecución vigente en este segundo.
> Solicitud de creación con fecha de inicio y fin idénticas.

* QA validado en ambiente de pruebas.
* Sin bugs lógicos de superposición o parseo de fechas.

---

## HU 5:
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

### Definition of Ready (DoR)
* Historia claramente entendida flujo de CRUD y estandarización de strings.
* Criterios de aceptación completos incluye manejo de rechazos por duplicidad exacta y normalizada.
* Reglas de negocio definidas:

> Algoritmo de normalización obligatorio antes de inserción/evaluación.
> Definición del beneficio.

* Diseño de base de datos actualizado: Índice único compuesto por id + tipo_producto normalizado para evitar duplicidad a nivel físico, no solo lógico.
* Límite de caracteres para el campo tipo_producto definido para evitar inyección de payloads gigantes.

### Definition of Done (DoD)
* Código implementado y revisado code review aprobado.
* Pruebas unitarias:

> Función de normalización de texto validada contra variaciones de mayúsculas y espacios.
> Rechazo de guardado ante violación del índice único.

* Pruebas de integración:

> CRUD completo verificando que la edición no permita sobreescribir otro tipo de producto existente.

* Manejo de Reglas de Negocio:

> Validación de campos obligatorios (producto, tipo de beneficio, valor).

* Validaciones y Edge Cases:

> Intento de creación con strings vacíos o compuestos solo por espacios ("   ").
> Envío de caracteres especiales o emojis en el tipo de producto.
> Actualización de una regla omitiendo el payload del valor de descuento.

* QA validado en ambiente de pruebas.
* Sin bugs lógicos de duplicidad.

---

## HU 6. 
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

### Definition of Ready (DoR)
* Historia claramente entendida flujo de validación de continuidad numérica.
* Criterios de aceptación completos incluye validación matemática de umbrales.
* Reglas de negocio definidas:

> Estándar de intervalo algebraico a usar: Límite Inferior Inclusivo y Límite Superior Exclusivo [min, max).
> Métrica exacta sobre la cual se clasifica.

* Diseño de base de datos preparado para manejar valores numéricos de alta precisión.
* Regla de progresión: El sistema debe forzar que el Límite Inferior del Nivel N+1 sea exactamente igual al Límite Superior del Nivel N.

### Definition of Done (DoD)
* Código implementado y revisado code review aprobado.
* Pruebas unitarias:

> Algoritmo de validación de continuidad y no-superposición.
> Ordenamiento jerárquico de niveles asegurando progresión ascendente.

* Pruebas de integración:

> Inserción/Actualización en lote de toda la matriz de rangos para asegurar atomicidad si falla un rango, falla toda la configuración.

* Manejo de Reglas de Negocio:

> Rechazo si el Límite Superior es menor o igual al Límite Inferior.

* Validaciones y Edge Cases:

> Clasificación exacta en el límite del rango.
> Configuración del nivel máximo con límite superior abierto.
> Eliminación de un nivel intermedio que genere un vacío.

* QA validado mediante pruebas de escritorio con tablas de valores.
* Sin bugs matemáticos de clasificación.

---

## HU 7. 
Como usuario de LOYALTY,
Quiero definir el tope maximo y la prioridad de descuentos,
Para proteger la rentabilidad del negocio.

Scenario: Configuración válida de tope y prioridad
Given existen tipos de descuento disponibles en el ecommerce
And el tope máximo propuesto es un valor positivo
And la prioridad define un orden único entre descuentos
When se registra la configuración de topes y prioridad
Then la configuración queda vigente para el ecommerce
And el motor utiliza ese orden para resolver descuentos concurrentes

Scenario: Rechazo por tope máximo inválido
Given existen límites de negocio para proteger la rentabilidad
When se intenta registrar un tope máximo menor o igual a cero
Then la configuración es rechazada
And se mantiene la última configuración válida

Scenario: Rechazo por prioridad ambigua
Given la prioridad de descuentos debe ser determinística
When se registra una prioridad con empates o niveles duplicados
Then la configuración es rechazada
And no se altera la prioridad vigente

Scenario: Aplicación del tope ante acumulación de descuentos
Given existe una configuración vigente de tope y prioridad
And una transacción califica para múltiples descuentos
When el descuento total calculado supera el tope máximo
Then el descuento final aplicado se limita al tope máximo configurado

### Definition of Ready (DoR)
* Historia claramente entendida flujo matemático de sumatoria y descarte por prioridad.
* Criterios de aceptación completos incluye el comportamiento matemático exacto al alcanzar el tope.
* Reglas de negocio definidas:

> Fórmula de acumulación explícita aditiva o multiplicativa.
> Algoritmo de recorte truncamiento parcial del descuento de menor prioridad vs eliminación total del mismo.

* Esquema de base de datos preparado para almacenar el campo priority y max_discount_cap.
* Restricciones matemáticas acordadas.

### Definition of Done (DoD)
* Código implementado y revisado code review aprobado.
* Pruebas unitarias:

> Ordenamiento estricto de arreglos de descuentos basados en el índice de prioridad.
> Función de limitación que trunca el cálculo al porcentaje exacto del tope.

* Pruebas de integración:

> Simulaciones de evaluación de 3+ reglas simultáneas respetando el orden.

* Validaciones y Edge Cases:

> Múltiples descuentos que, sumados, dan exactamente el valor del tope límite matemático.
> Configuración de 2 reglas intentando guardar la misma prioridad manejo del error de unicidad.
> Tope configurado deliberadamente al 100%.

* QA validado en ambiente de pruebas.
* Sin bugs financieros de sobredescuento.

---

## HU 8. 
Como motor de descuentos,
Quiero clasificar al cliente segun el payload recibido 
Para asignar su nivel de descuento.

Scenario: Clasificación exitosa con payload completo y válido
Given existe una matriz de clasificación vigente
And el payload contiene todos los atributos requeridos
When el motor evalúa el payload del cliente
Then el cliente queda asignado a un único nivel de fidelidad
And el nivel asignado corresponde a las reglas de clasificación vigentes

Scenario: Rechazo por payload incompleto
Given existen atributos obligatorios para clasificar al cliente
When se recibe un payload sin uno o más atributos obligatorios
Then la clasificación es rechazada
And se informa que no es posible determinar el nivel de descuento

Scenario: Rechazo por valores fuera de dominio
Given existen reglas de validación para los atributos del payload
When se recibe un payload con valores inválidos para el dominio definido
Then la clasificación es rechazada
And no se asigna nivel de descuento al cliente

Scenario: Consistencia de clasificación para mismo payload
Given existe una configuración de clasificación vigente
When el motor evalúa dos veces el mismo payload
Then el nivel de fidelidad asignado es el mismo en ambas evaluaciones

### Definition of Ready (DoR)
* Historia claramente entendida evaluación in-memory de atributos B2C.
* Criterios de aceptación completos incluye el esquema estricto de rechazo.
* Reglas de negocio definidas:

> Asignación de nivel "Default" si el cliente es nuevo o sus métricas son cero.
> Comportamiento ante métricas negativas.

* Documentación de API: JSON Schema del objeto customer dentro del S2S definido, con tipado fuerte.
* Política de evaluación idempotente: Mismo payload de entrada, mismo nivel asignado, independientemente del tiempo.

### Definition of Done (DoD)
* Código implementado y revisado code review enfocado en manejo de errores.
* Pruebas unitarias:

> Validación estricta contra el JSON Schema.
> Algoritmo de búsqueda de rango eficiente.

* Pruebas de integración:

> Petición con payload válido y respuesta con el nivel correcto mapeado desde la BD de reglas.

* Manejo de Reglas de Negocio:

> Retorno de HTTP 400 Bad Request estructurado si faltan atributos obligatorios para la clasificación.

* Validaciones y Edge Cases:

> Payload con tipos incorrectos.
> Payload con números negativos.
> Payload sin el nodo customer.

* QA validado inyectando JSONs malformados por S2S.
* Sin bugs de excepciones no controladas.

---

## HU 9. 
Como ecommerce, 
Quiero enviar el carrito y recibir el precio final con descuentos aplicados, 
Para mostrarle al usuario final en el checkout.

Scenario: Cálculo exitoso de precio final
Given el ecommerce está autorizado para consumir el servicio
And el carrito contiene ítems válidos con cantidades y precios válidos
And existen reglas de descuento vigentes aplicables
And existe una configuración vigente de topes y prioridad de descuentos
And el carrito califica para múltiples descuentos
When el ecommerce solicita el cálculo del carrito
Then el servicio responde el precio final del carrito
And el total incluye los descuentos aplicados según reglas vigentes y prioridades configuradas
And el orden de aplicación de descuentos respeta la prioridad configurada
And el descuento total no supera el tope máximo vigente
And el precio final refleja ambas restricciones de negocio

Scenario: Carrito sin descuentos aplicables
Given el ecommerce está autorizado para consumir el servicio
And el carrito es válido
And no existen descuentos aplicables para ese carrito
When el ecommerce solicita el cálculo del carrito
Then el precio final es igual al subtotal del carrito
And la respuesta indica que no hubo descuentos aplicados

Scenario: Rechazo por carrito inválido
Given el servicio requiere estructura mínima y datos válidos de carrito
When el ecommerce envía un carrito con datos incompletos o inconsistentes
Then la solicitud es rechazada
And no se retorna precio final hasta contar con un carrito válido

### Definition of Ready (DoR)
* Historia claramente entendida flujo de entrada del JSON, evaluación en memoria y salida del JSON.
* Criterios de aceptación completos.
* Reglas de negocio y técnicas definidas:

> Estándar de redondeo monetario exacto a utilizar.
> Acuerdo de Nivel de Servicio de latencia máxima de respuesta < 150ms.

* JSON Schema estricto documentado Payload de entrada y salida con tipos de datos y campos requeridos.
* Manejo de errores HTTP definidos 400 Bad Request para payloads inválidos, 401 para API Keys inválidas, 200 OK para cálculos exitosos.

### Definition of Done (DoD)
* Código implementado y revisado code review aprobado.
* Pruebas unitarias:

> Cálculos matemáticos precisos forzando decimales periódicos conflictivos.
> Validación estricta contra el JSON Schema rechazo de strings donde van floats.

* Pruebas de integración:

> Ciclo completo S2S: Entrada -> Auth -> Motor -> Topes -> Respuesta en JSON.

* Pruebas de Rendimiento:

> Pruebas de carga demostrando que el endpoint responde bajo el SLA establecido.

* Validaciones y Edge Cases:

> Payload con precios base de íte m en negativo o $0.00.
> Inyección de caracteres no válidos en IDs de producto.
> Cálculo dinámico verificando que nunca se retorne un total a pagar negativo.

* QA validado mediante Postman/cURL u otra herramienta de testing de APIs.
* Sin cuellos de botella bloqueantes ni discrepancias de redondeo.

---

## HU 10. 
Como usuario de LOYALTY, 
Quiero consultar los descuentos aplicados en las transacciones de los últimos siete días, 
Para verificar que el motor de cálculo esté operando bajo las reglas y topes máximos configurados.

Scenario: Verificación exitosa de transacciones recientes
Given soy un usuario de LOYALTY con acceso al dashboard de mi ecommerce
When accedo al módulo de "Historial de Descuentos" y filtro por los últimos 7 días
Then el sistema debe mostrar una lista con: id de transacción, fecha/hora, reglas aplicadas, descuento calculado y descuento final
And debe resaltar aquellas transacciones donde el descuento fue rechazado por alcanzar el tope máximo configurado.

Scenario: Cumplimiento de privacidad de datos
Given que el sistema registra el uso del motor de descuentos
When se visualiza el detalle de una transacción en el log
Then el sistema no debe mostrar nombres, correos, ni datos de identidad del comprador final.
And solo se debe mostrar el payload técnico que justifica el descuento

### Definition of Ready (DoR)
* Historia claramente entendida registro de auditoría operativa del motor.
* Criterios de aceptación completos incluye políticas de retención y privacidad.
* Reglas de negocio definidas:

> Lista explícita de campos PII que deben ser eliminados/enmascarados antes de escribir en la base de datos (nombres, correos, IPs, direcciones).
> Obligatoriedad de paginación Limit/Offset en la UI y API.

* Diseño de base de datos: Tabla de logs particionada por fecha o con un Job/Cron configurado para borrar físicamente registros created_at < NOW() - 7 days.
* Definición de carga máxima a mostrar por página en el Dashboard.

### Definition of Done (DoD)
* Código implementado y revisado code review aprobado.
* Pruebas unitarias:

> Función de sanitización de payload verificada.
> Formateo correcto de respuestas de log.

* Pruebas de integración:

> Endpoint de recuperación respetando el id.
> Funcionamiento correcto del filtro "últimos 7 días".

* Manejo de Reglas de Negocio:

> Resaltado en UI de logs marcados con status: rejected_by_cap.

* Validaciones y Edge Cases:

> Inyección de 100,000 logs simulados para verificar tiempos de respuesta y paginación.
> Intento de consultar datos del día 8.

* QA validado verificando la base de datos directamente.
* Sin bugs de rendimiento ni fugas de datos de clientes finales.

---

## HU 11. 
Como super admin,
Quiero ver el registro de los cambios de las reglas de descuento de todos los ecommerce,
Para identificar que usuarios realizaron modificaciones y en que momentos.

Scenario: Trazabilidad de modificaciones por el Super Admin
Given que soy un Super Admin y accedo al panel global de auditoría
When consulto el historial de cambios de un ecommerce específico
Then el sistema debe mostrar una tabla cronológica con: usuario que realizó el cambio, fecha/hora, regla afectada, valor anterior y valor nuevo.
And debe permitir filtrar por tipo de regla Temporada, Producto o Fidelidad.

### Definition of Ready (DoR)
* Historia claramente entendida registro de mutaciones del sistema.
* Criterios de aceptación completos incluye campos de estado previo y nuevo.
* Reglas de negocio definidas:

> Formato de almacenamiento del historial campos old_value y new_value en formato JSONB para soportar cualquier estructura de regla.
> Registro inmutable: Nadie, ni un Super Admin, puede borrar un registro de auditoría.

* Arquitectura definida: Implementación vía Interceptores/Middlewares o Triggers de Base de Datos para garantizar que ninguna mutación evada el log.
* Relación de usuario autoría: Registrar el UUID de quién hizo el cambio.

### Definition of Done (DoD)
* Código implementado y revisado code review aprobado.
* Pruebas unitarias:

> Generación correcta del Diff comparando dos objetos de estado.

* Pruebas de integración:

> Todo endpoint de mutación (POST/PUT/PATCH/DELETE) de reglas de negocio inserta automáticamente en la tabla de auditoría.
> Filtros del panel global por tipo de regla y por ecommerce operativos.

* Manejo de Reglas de Negocio:

> Manejo de borrados almacenar old_value completo y new_value: null.

* Validaciones y Edge Cases:

> Petición de actualización sin cambios reales el sistema no debe generar un log fantasma.
> Super Admin es eliminado del sistema; sus registros históricos deben mantener su nombre referenciado.

* QA validado cruzando acciones reales con la tabla de logs.
* Sin bugs de inconsistencia de datos históricos.

---

## HU 12. 
Como usuario de LOYALTY,
Quiero poder activar o desactivar reglas con un solo click
Para reaccionar rápidamente a cambios en el mercado sin tener que borrar la configuración.

Scenario: Desactivación inmediata de una regla activa
Given que existe una regla de descuento por Temporada en estado "activa"
When el usuario hace click en el botón para cambiarlo a "Inactivo"
Then el sistema debe actualizar el estado de la regla inmediatamente
And el motor de cálculo debe ignorar esta regla en todas las peticiones S2S recibidas a partir de ese momento.

Scenario: Reactivación de regla sin pérdida de datos
Given que una regla de fidelidad oro fue desactivada previamente
When el usuario activa nuevamente
Then la regla debe volver a participar en el cálculo del motor con sus parámetros originales sin necesidad de reconfigurarla

### Definition of Ready (DoR)
* Historia claramente entendida.
* Criterios de aceptación completos incluye latencia de propagación.
* Reglas de negocio definidas:

> Definición del SLA para "inmediatamente" el cambio debe propagarse al motor en menos de 100ms.
> Desactivar una regla no altera sus configuraciones internas; solo cambia un flag is_active.

* Arquitectura definida: Estrategia de invalidación de caché o modelo Event-Driven documentado por el equipo de backend para este caso de uso.
* Interfaz de usuario: El botón debe reflejar estado de carga y bloquearse durante la petición para evitar envíos múltiples.

### Definition of Done (DoD)
* Código implementado y revisado code review aprobado.
* Pruebas unitarias:

> Mutación correcta del estado is_active preservando el resto del objeto.

* Pruebas de integración:

> Flujo completo: Cambio de Toggle -> Purga de Caché -> Lectura del Motor S2S reflejando el nuevo estado.

* Manejo de Reglas de Negocio:

> Reactivación restaura el estado operativo sin pedir configuración extra.

* Validaciones y Edge Cases:

> Prueba de "Debounce" en UI: Usuario haciendo click al toggle 10 veces en 1 segundo.
> Concurrencia severa: Una petición S2S entrando en el exacto milisegundo en que la regla se está marcando como inactiva.

* QA validado usando Postman lanzar S2S repetitivo mientras se apaga la regla en otro monitor.
* Sin bugs de sincronización de estados ni reglas "zombies" cobrando descuentos.