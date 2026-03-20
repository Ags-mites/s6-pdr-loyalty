# HU-01
## Subtareas DEV
### Backend
- Configurar estrategia de autenticación basada en JWT.
- Implementar endpoint POST /auth/login con validación de credenciales y hashing.
- Crear Guard de seguridad para protección de rutas privadas.
- Implementar lógica de invalidación de sesión en el servidor.
- Desarrollar pruebas unitarias para el flujo de emisión de tokens.

### Frontend
- Crear formulario de inicio de sesión con validaciones de campos obligatorios.
- Implementar manejo de estado global para el token de sesión.
- Configurar persistencia en sessionStorage y limpieza en el cierre de sesión.
- Desarrollar lógica de rutas protegidas para el Dashboard.
- Implementar componente de cierre de sesión con redirección automática.

## Subtareas QA
### Análisis y diseño
- Revisar criterios de aceptación para mensajes de error de credenciales.
- Diseñar casos de prueba para sesiones expiradas y acceso por URL directa sin login.

### Validación técnica y funcional
- Verificar el rechazo de acceso con contraseñas incorrectas o usuarios inexistentes.
- Validar que el token no sea visible ni manipulable de forma insegura.
- Comprobar que el cierre de sesión elimine efectivamente los permisos de acceso.
- Ejecutar pruebas de regresión sobre el flujo de entrada al sistema.

## Estimación: 3 puntos
### Justificación:
- DEV: Esfuerzo bajo-medio. Se centra en la implementación de un estándar de seguridad conocido, sin integraciones complejas de terceros.
- QA: Esfuerzo bajo. Los escenarios de prueba son directos y se enfocan en la validación de acceso y seguridad básica del formulario.

---

# HU-02
## Subtareas DEV
### Backend
- Diseñar la relación en base de datos entre la entidad Ecommerce y Usuario.
- Implementar Interceptor para la inyección automática de ecommerce_id en consultas.
- Crear endpoint POST /admin/users restringido a rol Super Admin.
- Implementar validaciones de integridad para asegurar que el usuario pertenezca a un solo ecommerce.
- Realizar pruebas unitarias de aislamiento de datos

### Frontend
- Desarrollar vista de gestión de usuarios para el Super Admin.
- Implementar formulario de registro con vinculación obligatoria a un ecommerce.
- Aplicar filtros en el estado global para asegurar la visualización única de datos del usuario de loyalty logueado.
- Crear validaciones de UI para evitar la creación de usuarios sin ecommerce asignado.

## Subtareas QA
### Análisis y diseño
- Analizar riesgos de seguridad sobre la fuga de datos entre diferentes comercios.
- Diseñar matriz de pruebas de permisos


### Validación técnica y funcional
- Verificar que un Admin no pueda consultar ni modificar usuarios de otro ecommerce.
- Validar que el Super Admin pueda asignar usuarios a cualquier comercio registrado.
- Comprobar que el ecommerce_id se guarde correctamente en cada transacción del usuario.
- Ejecutar pruebas negativas intentando saltar el aislamiento mediante manipulación de IDs.


## Estimación: 5 puntos
### Justificación:
- DEV: Esfuerzo medio-alto. La implementación del aislamiento de datos es la base del sistema y requiere lógica rigurosa para evitar brechas de seguridad entre clientes.
- QA: Esfuerzo medio. Requiere pruebas de seguridad exhaustivas para garantizar que no exista cruce de información entre cuentas.

---

# HU-03
## Subtareas DEV
### Backend
- Implementar servicio de generación de API Keys mediante cadenas criptográficas aleatorias.
- Crear lógica de almacenamiento seguro mediante hashing.
- Desarrollar Guard de validación de API Keys para peticiones de servidor a servidor.
- Implementar endpoints para listar, revocar y rotar llaves por ecommerce.
- Realizar pruebas de cobertura sobre el middleware de validación de llaves.

### Frontend
- Implementar panel de gestión de credenciales en la configuración del comercio.
- Desarrollar funcionalidad para mostrar la llave completa solo en el momento de creación.
- Implementar lógica de enmascaramiento de llaves en tablas de administración.
- Crear diálogos de confirmación para la revocación o rotación de credenciales.

## Subtareas QA
### Análisis y diseño
- Revisar que el proceso de rotación de llaves no interrumpa el servicio si no es deseado.
- Diseñar pruebas de integración para el motor de cálculo usando llaves válidas y nulas.

### Validación técnica y funcional
- Verificar que las peticiones al motor sean rechazadas si la API Key está revocada o es incorrecta.
- Validar que la llave real no se guarde en logs ni se exponga en respuestas de API comunes.
- Comprobar que el enmascaramiento en la UI funcione correctamente (solo ver últimos dígitos).
- Ejecutar pruebas de carga básica para asegurar que la validación de la llave no degrade el performance.

## Estimación: 3 puntos
### Justificación:
- DEV: Esfuerzo medio. Implica el manejo de una capa de seguridad distinta a la de usuarios, centrada en la integración técnica entre sistemas.
- QA: Esfuerzo bajo-medio. Se centra en validar la denegación de acceso y la protección del secreto en la interfaz de usuario.

---

# HU-04
## Subtareas DEV
### Backend
- Definir el modelo de datos para Reglas de Temporada con rangos de fechas.
- Implementar algoritmo de validación para evitar solapamiento de fechas entre reglas activas.
- Desarrollar CRUD completo con validaciones de porcentaje de descuento.
- Implementar lógica de activación/desactivación manual de reglas.
- Realizar pruebas unitarias enfocadas en el cálculo de colisiones de intervalos de tiempo.

### Frontend
- Desarrollar formulario con selectores de fecha y validación de periodos lógicos.
- Implementar tabla de gestión de reglas con filtros por estado activa/inactiva.
- Crear indicadores visuales para alertar sobre solapamientos detectados por el servidor.
- Implementar servicios de consumo para la actualización de estados de las reglas.

## Subtareas QA
### Análisis y diseño
- Revisar la lógica de negocio para casos donde una regla termina y otra empieza el mismo día.
- Diseñar casos de prueba para límites de descuento (mínimos y máximos permitidos).

### Validación técnica y funcional
- Validar el rechazo de creación de reglas que se solapen con fechas de una promoción ya existente.
- Verificar que el motor de descuentos ignore reglas que han sido marcadas como inactivas.
- Comprobar que la edición de fechas también dispare la validación de colisiones.
- Ejecutar pruebas de flujo completo Creación, Activación, Aplicación, Eliminación.

## Estimación: 5 puntos
### Justificación:
- DEV: Esfuerzo medio-alto. La lógica de solapamiento de fechas y la consistencia de los periodos de vigencia añaden una capa de complejidad algorítmica al CRUD tradicional.
- QA: Esfuerzo medio. Requiere pruebas matemáticas y de lógica temporal para asegurar que no se apliquen descuentos dobles por errores de configuración.

---

# HU-05
## Subtareas DEV
### Backend
- Crear entidad y tabla para reglas por tipo de producto.
- Implementar validación de unicidad para evitar duplicidad de reglas por categoría/tipo.
- Desarrollar endpoints CRUD para la gestión de estas reglas.
- Implementar lógica de validación de campos obligatorios y tipos de beneficio permitidos.
- Realizar pruebas unitarias sobre el controlador y el servicio de reglas.

### Frontend
- Implementar interfaz para el listado y filtrado de reglas por producto.
- Desarrollar formulario de creación y edición con validaciones en tiempo real.
- Manejar estados de error específicos para casos de duplicidad informados por la API.
- Implementar confirmaciones visuales para la eliminación de reglas.

## Subtareas QA
### Análisis y diseño
- Identificar casos de borde en la definición de tipos de producto (strings vacíos, caracteres especiales).
Diseñar matriz de pruebas para creación exitosa, duplicidad y edición parcial.

### Validación técnica y funcional
- Verificar que no se puedan crear dos reglas para el mismo tipo de producto.
- Validar que al eliminar una regla, esta deje de ser considerada por el motor de cálculo de inmediato.
- Comprobar que el sistema mantenga la versión válida si una edición falla por datos incompletos.
- Ejecutar pruebas de regresión en el motor para asegurar que las nuevas reglas de producto se apliquen correctamente.

## Estimación:  3 puntos
### Justificación:
- DEV: Esfuerzo bajo-medio. Se trata de un CRUD estándar con una restricción de unicidad simple. La lógica es menos compleja que la de fechas de temporada.
- QA: Esfuerzo bajo. Las pruebas son directas y se centran en la integridad referencial y validación de campos.

---

# HU-06
## Subtareas DEV
### Backend
- Crear modelo de persistencia para niveles de fidelidad y sus umbrales.
- Implementar algoritmo de validación de continuidad para asegurar que no existan vacíos entre rangos.
- Implementar lógica de exclusividad para evitar superposición de límites (Min/Max).
- Desarrollar lógica de ordenamiento ascendente para garantizar la jerarquía de niveles.
- Realizar pruebas unitarias sobre el servicio de validación de rangos.

### Frontend
- Diseñar interfaz dinámica para la definición de niveles (Bronce, Plata, Oro, etc.).
- Implementar validaciones de UI que impidan ingresar rangos incoherentes antes de enviar al servidor.
- Desarrollar visualización clara de la jerarquía de beneficios por nivel.

## Subtareas QA
- Revisar la lógica de negocio para la cobertura total del dominio de clasificación.
- Diseñar escenarios de prueba para rangos solapados, huecos entre niveles y orden descendente inválido.

Validación técnica y funcional
- Verificar el rechazo de la configuración si existe una discontinuidad (ej. Nivel 1 termina en 100 y Nivel 2 empieza en 110).
- Validar que la segmentación de clientes en el motor utilice los nuevos umbrales tras guardar cambios.
- Comprobar que no se puedan guardar niveles con umbrales negativos o iguales a cero.

## Estimación:  5 puntos
### Justificación:
- DEV: Esfuerzo medio. La complejidad radica en la validación matemática de la continuidad y no superposición de los rangos para evitar comportamientos erráticos en el motor. 
- QA: Esfuerzo medio. Requiere pruebas exhaustivas de lógica de intervalos para asegurar que cada posible valor del cliente caiga en un único segmento.

# HU-07
## Subtareas DEV
### Backend
- Modelo `ConfigDescuentos` (topeMax, prioridades[]) + validaciones (tope>0, prioridades únicas).
- Endpoint para registrar/actualizar configuración + mantener última válida en rechazos.
- Ajustar motor: aplicar prioridad y recortar descuento total al tope.
- Pruebas unitarias (cálculo tope/prioridad) + integración (API).

### Frontend
- Pantalla de configuración (tope + ordenamiento de descuentos) y validaciones básicas.
- Manejo de errores (tope inválido, prioridad ambigua).
- Pruebas unitarias.

## Subtareas QA
- Casos: configuración OK, tope inválido, prioridad duplicada, aplicación de tope en acumulación.
- Validación API + pruebas funcionales del motor con múltiples descuentos.

## Estimación: 5 puntos
### Justificación
- DEV: Media (impacto directo en motor de descuentos).
- QA: Media (escenarios de concurrencia y verificación de cálculo).

# HU-08

## Subtareas DEV
### Backend / Motor
- Definir contrato `PayloadCliente` + DTOs/respuestas de clasificación (nivel asignado, motivos de rechazo).
- Validaciones: atributos obligatorios, dominios/formatos, determinismo (mismo input → mismo output).
- Endpoint/función del motor para evaluar payload (o módulo interno) consumiendo matriz vigente (HU-06).
- Pruebas unitarias (validación + clasificación) y de consistencia (repetición mismo payload).
- Pruebas integración (API) con payloads válidos/ inválidos.

### Frontend (si aplica)
- (Opcional) herramienta interna de prueba: pegar payload y ver resultado/mensajes.

## Subtareas QA
- Diseño de payloads: completo válido, faltantes, fuera de dominio, borde de rangos.
- Validación API/motor: rechazos con mensajes claros; determinismo con re-ejecución del mismo payload.

## Estimación: 8 puntos
### Justificación
- DEV: Alta (lógica núcleo del motor + contratos + validaciones + determinismo).
- QA: Media-alta (data-driven testing + bordes + consistencia).

# HU-09

## Subtareas DEV
### Backend
- Ajustar DTOs y validar carrito.
- Integrar autenticación S2S y control de ecommerce autorizado.
- Aplicar reglas vigentes con prioridad y tope máximo.
- Exponer `POST /carritos/calcular` con manejo de errores.
- Agregar pruebas unitarias y de integración.
### Frontend
- Consumir endpoint en checkout y mapear payload del carrito.
- Mostrar subtotal, descuentos y precio final.
- Manejar estados de carga, de error y sin descuentos y agregar pruebas unitarias.

## Subtareas QA
- Diseñar matriz de prueba para prioridad, tope y carrito inválido.
- Validar control de acceso del endpoint  y cumplimiento del contrato de respuesta.
- Verificar orden de descuentos, límite por tope y flujo E2E.

## Estimación: 8 puntos
### Justificación:
- DEV: Alto por lógica de cálculo con reglas, prioridad, tope y validaciones.
- QA: Medio-alto por combinaciones funcionales y validación técnica del API.

# HU-10 | Consultar descuentos aplicados en los últimos 7 días
## Subtareas DEV
### Backend
- Implementar consulta por ecommerce para últimos 7 días y DTO de historial.
- Marcar transacciones recortadas por tope máximo.
- Exponer `GET /descuentos/historial?days=7` con paginación y control de acceso.
- Asegurar que la respuesta no muestre datos personales del cliente.
- Agregar pruebas unitarias y de integración de filtro temporal, tope y privacidad.
### Frontend
- Crear módulo "Historial de Descuentos" con filtro de 7 días.
- Mostrar tabla cronológica y resaltar transacciones con tope.
- Mostrar un detalle técnico sin datos personales y contemplar estados de carga, sin resultados y error.

## Subtareas QA
- Diseñar casos de trazabilidad y exactitud de cambios.
- Validar filtros combinados y orden cronológico.
- Confirmar que solo el Super Admin pueda acceder al módulo y ejecutar pruebas de funcionamiento general del flujo.

## Estimación: 5 puntos
### Justificación:
- DEV: Medio por consulta histórica, formateo y privacidad.
- QA: Medio por consistencia histórica y pruebas de autorización.

