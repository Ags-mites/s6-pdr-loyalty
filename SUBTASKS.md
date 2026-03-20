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