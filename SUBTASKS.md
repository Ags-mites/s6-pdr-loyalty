# HU-01
## Subtareas DEV
### Backend
- TDEV 1: Configurar estrategia de autenticación basada en JWT.
- TDEV 2: Implementar endpoint POST /auth/login con validación de credenciales y hashing.
- TDEV 3: Crear Guard de seguridad para protección de rutas privadas.
- TDEV 4: Implementar lógica de invalidación de sesión en el servidor.
- TDEV 5: Desarrollar pruebas unitarias para el flujo de emisión de tokens.

### Frontend
- TDEV 6: Crear formulario de inicio de sesión con validaciones de campos obligatorios.
- TDEV 7: Implementar manejo de estado global para el token de sesión.
- TDEV 8: Configurar persistencia en sessionStorage y limpieza en el cierre de sesión.
- TDEV 9: Desarrollar lógica de rutas protegidas para el Dashboard.
- TDEV 10: Implementar componente de cierre de sesión con redirección automática.

## Subtareas QA
### Análisis y diseño
- TQA 1: Revisar criterios de aceptación para mensajes de error de credenciales.
- TQA 2: Diseñar casos de prueba para sesiones expiradas y acceso por URL directa sin login.

### Validación técnica y funcional
- TQA 3: Verificar el rechazo de acceso con contraseñas incorrectas o usuarios inexistentes.
- TQA 4: Validar que el token no sea visible ni manipulable de forma insegura.
- TQA 5: Comprobar que el cierre de sesión elimine efectivamente los permisos de acceso.
- TQA 6: Ejecutar pruebas de regresión sobre el flujo de entrada al sistema.

## Estimación: 3 puntos
### Justificación:
- DEV: Esfuerzo bajo-medio. Se centra en la implementación de un estándar de seguridad conocido, sin integraciones complejas de terceros.
- QA: Esfuerzo bajo. Los escenarios de prueba son directos y se enfocan en la validación de acceso y seguridad básica del formulario.

---

# HU-02
## Subtareas DEV
### Backend
- TDEV 1: Diseñar la relación en base de datos entre la entidad Ecommerce y Usuario.
- TDEV 2: Implementar Interceptor para la inyección automática de ecommerce_id en consultas.
- TDEV 3: Crear endpoint POST /admin/users restringido a rol Super Admin.
- TDEV 4: Implementar validaciones de integridad para asegurar que el usuario pertenezca a un solo ecommerce.
- TDEV 5: Realizar pruebas unitarias de aislamiento de datos.

### Frontend
- TDEV 6: Desarrollar vista de gestión de usuarios para el Super Admin.
- TDEV 7: Implementar formulario de registro con vinculación obligatoria a un ecommerce.
- TDEV 8: Aplicar filtros en el estado global para asegurar la visualización única de datos del usuario de loyalty logueado.
- TDEV 9: Crear validaciones de UI para evitar la creación de usuarios sin ecommerce asignado.

## Subtareas QA
### Análisis y diseño
- TQA 1: Analizar riesgos de seguridad sobre la fuga de datos entre diferentes comercios.
- TQA 2: Diseñar matriz de pruebas de permisos.


### Validación técnica y funcional
- TQA 3: Verificar que un Admin no pueda consultar ni modificar usuarios de otro ecommerce.
- TQA 4: Validar que el Super Admin pueda asignar usuarios a cualquier comercio registrado.
- TQA 5: Comprobar que el ecommerce_id se guarde correctamente en cada transacción del usuario.
- TQA 6: Ejecutar pruebas negativas intentando saltar el aislamiento mediante manipulación de IDs.


## Estimación: 5 puntos
### Justificación:
- DEV: Esfuerzo medio-alto. La implementación del aislamiento de datos es la base del sistema y requiere lógica rigurosa para evitar brechas de seguridad entre clientes.
- QA: Esfuerzo medio. Requiere pruebas de seguridad exhaustivas para garantizar que no exista cruce de información entre cuentas.

---

# HU-03
## Subtareas DEV
### Backend
- TDEV 1: Implementar servicio de generación de API Keys mediante cadenas criptográficas aleatorias.
- TDEV 2: Crear lógica de almacenamiento seguro mediante hashing.
- TDEV 3: Desarrollar Guard de validación de API Keys para peticiones de servidor a servidor.
- TDEV 4: Implementar endpoints para listar, revocar y rotar llaves por ecommerce.
- TDEV 5: Realizar pruebas de cobertura sobre el middleware de validación de llaves.

### Frontend
- TDEV 6: Implementar panel de gestión de credenciales en la configuración del comercio.
- TDEV 7: Desarrollar funcionalidad para mostrar la llave completa solo en el momento de creación.
- TDEV 8: Implementar lógica de enmascaramiento de llaves en tablas de administración.
- TDEV 9: Crear diálogos de confirmación para la revocación o rotación de credenciales.

## Subtareas QA
### Análisis y diseño
- TQA 1: Revisar que el proceso de rotación de llaves no interrumpa el servicio si no es deseado.
- TQA 2: Diseñar pruebas de integración para el motor de cálculo usando llaves válidas y nulas.

### Validación técnica y funcional
- TQA 3: Verificar que las peticiones al motor sean rechazadas si la API Key está revocada o es incorrecta.
- TQA 4: Validar que la llave real no se guarde en logs ni se exponga en respuestas de API comunes.
- TQA 5: Comprobar que el enmascaramiento en la UI funcione correctamente (solo ver últimos dígitos).
- TQA 6: Ejecutar pruebas de carga básica para asegurar que la validación de la llave no degrade el performance.

## Estimación: 3 puntos
### Justificación:
- DEV: Esfuerzo medio. Implica el manejo de una capa de seguridad distinta a la de usuarios, centrada en la integración técnica entre sistemas.
- QA: Esfuerzo bajo-medio. Se centra en validar la denegación de acceso y la protección del secreto en la interfaz de usuario.

---

# HU-04
## Subtareas DEV
### Backend
- TDEV 1: Definir el modelo de datos para Reglas de Temporada con rangos de fechas.
- TDEV 2: Implementar algoritmo de validación para evitar solapamiento de fechas entre reglas activas.
- TDEV 3: Desarrollar CRUD completo con validaciones de porcentaje de descuento.
- TDEV 4: Implementar lógica de activación/desactivación manual de reglas.
- TDEV 5: Realizar pruebas unitarias enfocadas en el cálculo de colisiones de intervalos de tiempo.

### Frontend
- TDEV 6: Desarrollar formulario con selectores de fecha y validación de periodos lógicos.
- TDEV 7: Implementar tabla de gestión de reglas con filtros por estado activa/inactiva.
- TDEV 8: Crear indicadores visuales para alertar sobre solapamientos detectados por el servidor.
- TDEV 9: Implementar servicios de consumo para la actualización de estados de las reglas.

## Subtareas QA
### Análisis y diseño
- TQA 1: Revisar la lógica de negocio para casos donde una regla termina y otra empieza el mismo día.
- TQA 2: Diseñar casos de prueba para límites de descuento (mínimos y máximos permitidos).

### Validación técnica y funcional
- TQA 3: Validar el rechazo de creación de reglas que se solapen con fechas de una promoción ya existente.
- TQA 4: Verificar que el motor de descuentos ignore reglas que han sido marcadas como inactivas.
- TQA 5: Comprobar que la edición de fechas también dispare la validación de colisiones.
- TQA 6: Ejecutar pruebas de flujo completo Creación, Activación, Aplicación, Eliminación.

## Estimación: 5 puntos
### Justificación:
- DEV: Esfuerzo medio-alto. La lógica de solapamiento de fechas y la consistencia de los periodos de vigencia añaden una capa de complejidad algorítmica al CRUD tradicional.
- QA: Esfuerzo medio. Requiere pruebas matemáticas y de lógica temporal para asegurar que no se apliquen descuentos dobles por errores de configuración.

---

# HU-05
## Subtareas DEV
### Backend
- TDEV 1: Crear entidad y tabla para reglas por tipo de producto.
- TDEV 2: Implementar validación de unicidad para evitar duplicidad de reglas por categoría/tipo.
- TDEV 3: Desarrollar endpoints CRUD para la gestión de estas reglas.
- TDEV 4: Implementar lógica de validación de campos obligatorios y tipos de beneficio permitidos.
- TDEV 5: Realizar pruebas unitarias sobre el controlador y el servicio de reglas.

### Frontend
- TDEV 6: Implementar interfaz para el listado y filtrado de reglas por producto.
- TDEV 7: Desarrollar formulario de creación y edición con validaciones en tiempo real.
- TDEV 8: Manejar estados de error específicos para casos de duplicidad informados por la API.
- TDEV 9: Implementar confirmaciones visuales para la eliminación de reglas.

## Subtareas QA
### Análisis y diseño
- TQA 1: Identificar casos de borde en la definición de tipos de producto (strings vacíos, caracteres especiales).
- TQA 2: Diseñar matriz de pruebas para creación exitosa, duplicidad y edición parcial.

### Validación técnica y funcional
- TQA 3: Verificar que no se puedan crear dos reglas para el mismo tipo de producto.
- TQA 4: Validar que al eliminar una regla, esta deje de ser considerada por el motor de cálculo de inmediato.
- TQA 5: Comprobar que el sistema mantenga la versión válida si una edición falla por datos incompletos.
- TQA 6: Ejecutar pruebas de regresión en el motor para asegurar que las nuevas reglas de producto se apliquen correctamente.

## Estimación:  3 puntos
### Justificación:
- DEV: Esfuerzo bajo-medio. Se trata de un CRUD estándar con una restricción de unicidad simple. La lógica es menos compleja que la de fechas de temporada.
- QA: Esfuerzo bajo. Las pruebas son directas y se centran en la integridad referencial y validación de campos.

---

# HU-06
## Subtareas DEV
### Backend
- TDEV 1: Crear modelo de persistencia para niveles de fidelidad y sus umbrales.
- TDEV 2: Implementar algoritmo de validación de continuidad para asegurar que no existan vacíos entre rangos.
- TDEV 3: Implementar lógica de exclusividad para evitar superposición de límites (Min/Max).
- TDEV 4: Desarrollar lógica de ordenamiento ascendente para garantizar la jerarquía de niveles.
- TDEV 5: Realizar pruebas unitarias sobre el servicio de validación de rangos.

### Frontend
- TDEV 6: Diseñar interfaz dinámica para la definición de niveles (Bronce, Plata, Oro, etc.).
- TDEV 7: Implementar validaciones de UI que impidan ingresar rangos incoherentes antes de enviar al servidor.
- TDEV 8: Desarrollar visualización clara de la jerarquía de beneficios por nivel.

## Subtareas QA
- TQA 1: Revisar la lógica de negocio para la cobertura total del dominio de clasificación.
- TQA 2: Diseñar escenarios de prueba para rangos solapados, huecos entre niveles y orden descendente inválido.

Validación técnica y funcional
- TQA 3: Verificar el rechazo de la configuración si existe una discontinuidad (ej. Nivel 1 termina en 100 y Nivel 2 empieza en 110).
- TQA 4: Validar que la segmentación de clientes en el motor utilice los nuevos umbrales tras guardar cambios.
- TQA 5: Comprobar que no se puedan guardar niveles con umbrales negativos o iguales a cero.

## Estimación:  5 puntos
### Justificación:
- DEV: Esfuerzo medio. La complejidad radica en la validación matemática de la continuidad y no superposición de los rangos para evitar comportamientos erráticos en el motor. 
- QA: Esfuerzo medio. Requiere pruebas exhaustivas de lógica de intervalos para asegurar que cada posible valor del cliente caiga en un único segmento.

# HU-07
## Subtareas DEV
### Backend
- TDEV 1: Modelo `ConfigDescuentos` (topeMax, prioridades[]) + validaciones (tope>0, prioridades únicas).
- TDEV 2: Endpoint para registrar/actualizar configuración + mantener última válida en rechazos.
- TDEV 3: Ajustar motor: aplicar prioridad y recortar descuento total al tope.
- TDEV 4: Pruebas unitarias (cálculo tope/prioridad) + integración (API).

### Frontend
- TDEV 5: Pantalla de configuración (tope + ordenamiento de descuentos) y validaciones básicas.
- TDEV 6: Manejo de errores (tope inválido, prioridad ambigua).
- TDEV 7: Pruebas unitarias.

## Subtareas QA
- TQA 1: Casos: configuración OK, tope inválido, prioridad duplicada, aplicación de tope en acumulación.
- TQA 2: Validación API + pruebas funcionales del motor con múltiples descuentos.

## Estimación: 5 puntos
### Justificación
- DEV: Media (impacto directo en motor de descuentos).
- QA: Media (escenarios de concurrencia y verificación de cálculo).

# HU-08

## Subtareas DEV
### Backend / Motor
- TDEV 1: Definir contrato `PayloadCliente` + DTOs/respuestas de clasificación (nivel asignado, motivos de rechazo).
- TDEV 2: Validaciones: atributos obligatorios, dominios/formatos, determinismo (mismo input → mismo output).
- TDEV 3: Endpoint/función del motor para evaluar payload (o módulo interno) consumiendo matriz vigente (HU-06).
- TDEV 4: Pruebas unitarias (validación + clasificación) y de consistencia (repetición mismo payload).
- TDEV 5: Pruebas integración (API) con payloads válidos/ inválidos.

### Frontend (si aplica)
- TDEV 6: (Opcional) herramienta interna de prueba: pegar payload y ver resultado/mensajes.

## Subtareas QA
- TQA 1: Diseño de payloads: completo válido, faltantes, fuera de dominio, borde de rangos.
- TQA 2: Validación API/motor: rechazos con mensajes claros; determinismo con re-ejecución del mismo payload.

## Estimación: 8 puntos
### Justificación
- DEV: Alta (lógica núcleo del motor + contratos + validaciones + determinismo).
- QA: Media-alta (data-driven testing + bordes + consistencia).

# HU-09

## Subtareas DEV
### Backend
- TDEV 1: Ajustar DTOs y validar carrito.
- TDEV 2: Integrar autenticación S2S y control de ecommerce autorizado.
- TDEV 3: Aplicar reglas vigentes con prioridad y tope máximo.
- TDEV 4: Exponer `POST /carritos/calcular` con manejo de errores.
- TDEV 5: Agregar pruebas unitarias y de integración.
### Frontend
- TDEV 6: Consumir endpoint en checkout y mapear payload del carrito.
- TDEV 7: Mostrar subtotal, descuentos y precio final.
- TDEV 8: Manejar estados de carga, de error y sin descuentos y agregar pruebas unitarias.

## Subtareas QA
- TQA 1: Diseñar matriz de prueba para prioridad, tope y carrito inválido.
- TQA 2: Validar control de acceso del endpoint y cumplimiento del contrato de respuesta.
- TQA 3: Verificar orden de descuentos, límite por tope y flujo E2E.

## Estimación: 8 puntos
### Justificación:
- DEV: Alto por lógica de cálculo con reglas, prioridad, tope y validaciones.
- QA: Medio-alto por combinaciones funcionales y validación técnica del API.

# HU-10
## Subtareas DEV
### Backend
- TDEV 1: Implementar consulta por ecommerce para últimos 7 días y DTO de historial.
- TDEV 2: Marcar transacciones recortadas por tope máximo.
- TDEV 3: Exponer `GET /descuentos/historial?days=7` con paginación y control de acceso.
- TDEV 4: Asegurar que la respuesta no muestre datos personales del cliente.
- TDEV 5: Agregar pruebas unitarias y de integración de filtro temporal, tope y privacidad.
### Frontend
- TDEV 6: Crear módulo "Historial de Descuentos" con filtro de 7 días.
- TDEV 7: Mostrar tabla cronológica y resaltar transacciones con tope.
- TDEV 8: Mostrar un detalle técnico sin datos personales y contemplar estados de carga, sin resultados y error.

## Subtareas QA
- TQA 1: Diseñar casos para consulta exitosa, vacía y filtros por fecha.
- TQA 2: Verificar que se destaquen las transacciones ajustadas por tope y que no se muestren datos personales del cliente.
- TQA 3: Probar que todo siga funcionando y registrar hallazgos.

## Estimación: 5 puntos
### Justificación:
- DEV: Medio por consulta histórica, formateo y privacidad.
- QA: Medio por cobertura de filtros y validaciones de protección de datos.

# HU-11
## Subtareas DEV
### Backend
- TDEV 1: Implementar registro de auditoría.
- TDEV 2: Exponer `GET /auditoria/reglas` con filtros por ecommerce y tipo.
- TDEV 3: Garantizar orden cronológico, paginación y acceso exclusivo de Super Admin.
- TDEV 4: Agregar pruebas unitarias y de integración para trazabilidad y permisos.
### Frontend
- TDEV 5: Crear vista de auditoría global con tabla cronológica.
- TDEV 6: Implementar filtros por ecommerce y por tipo de regla, con paginación en la tabla.
- TDEV 7: Implementar y validar los estados de carga, sin resultados y error, junto con pruebas unitarias.

## Subtareas QA
- TQA 1: Diseñar casos de trazabilidad y exactitud de cambios.
- TQA 2: Validar filtros combinados y orden cronológico.
- TQA 3: Confirmar que solo el Super Admin pueda acceder al módulo y ejecutar pruebas de funcionamiento general del flujo.

## Estimación: 5 puntos
### Justificación:
- DEV: Medio por auditoría transversal y consulta segura filtrable.
- QA: Medio por consistencia histórica y pruebas de autorización.

# HU-12
## Subtareas DEV
### Backend
- TDEV 1: Actualizar el modelo de reglas para incluir estado y fecha de última modificación.
- TDEV 2: Exponer `PATCH /reglas/{id}/estado` con validaciones de existencia, permisos y transición.
- TDEV 3: Garantizar efecto inmediato en motor S2S y registrar auditoría del cambio.
- TDEV 4: Agregar pruebas unitarias y de integración del impacto en cálculo.
### Frontend
- TDEV 5: Implementar toggle de estado en listado de reglas.
- TDEV 6: Actualizar UI en tiempo real con rollback en error.
- TDEV 7: Mostrar feedback de resultado y agregar pruebas unitarias.

## Subtareas QA
- TQA 1: Diseñar casos de activación, desactivación, regla inexistente y permisos inválidos.
- TQA 2: Validar endpoint y consistencia entre UI y estado persistido.
- TQA 3: Verificar que una regla inactiva no se aplique en la siguiente petición S2S.

## Estimación: 3 puntos
### Justificación:
- DEV: Medio-bajo por alcance acotado con requisito de efecto inmediato.
- QA: Bajo-medio por validación de no regresión y permisos.
