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
