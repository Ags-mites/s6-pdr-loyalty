# PRD

## Visión
En LOYALTY buscamos crear la mejor calculadora de descuentos dinámicos para e-commerce, ayudando a comercios de cualquier tamaño a tomar decisiones promocionales inteligentes basadas en temporada, fidelidad del cliente y tipo de producto, para construir relaciones más justas, sostenibles y duraderas con sus clientes.

## Objetivos
1. Durante las primeras 6 semanas del MVP, lograr que al menos 93% de los comercios clientes configure una promoción completa (temporada, fidelidad y tipo de producto) en menos de 3 minutos.
2. Durante los primeros 60 días del MVP, lograr que al menos 99% de las simulaciones con entradas válidas devuelvan un precio final válido y mayor o igual a 0, aplicando correctamente las reglas configuradas de temporada, fidelidad y tipo de producto.
3. Durante las primeras 10 semanas del MVP, lograr que al menos 92% de los comercios activos semanalmente guarde y reutilice al menos una configuración de reglas de descuento por semana.
4. Desde el lanzamiento del MVP, lograr que al menos 98% de las simulaciones completadas muestren, antes de confirmar el precio final, el desglose trazable del descuento por temporada, fidelidad y tipo de producto (porcentaje y monto por cada variable), junto con el precio final.

## Alcance del MVP
- IN 
   1. Lógica de descuentos que combine:
       - Temporada
       - Nivel de fidelidad del cliente
       - Tipo de producto
    2. Pantalla única de simulación con los campos:
       - Precio base del producto
       - Tipo de producto
       - Nivel de fidelidad del cliente
       - Temporada
    3. Cálculo y visualización inmediata del resultado:
       - Precio base
       - % y monto descontado por cada variable
       - Precio final
    4. Tabla de configuración editable para definir reglas de descuento:
       - % por temporada
       - % por fidelidad
       - % por tipo de producto
    5. Validaciones mínimas de negocio:
       - Campos obligatorios
       - Descuentos permitidos entre 0% y 100%
       - El precio final no puede ser negativo
    6. Guardado de configuración con confirmación visible al usuario.

- OUT
   1. No incluye cuentas reales de usuario: registro, inicio de sesión y gestión avanzada de permisos o roles.
   2. No incluye historial completo de operaciones ni auditoría detallada de compras.
   3. No incluye análisis avanzado del negocio, como tableros de indicadores o reportes personalizados.
   4. No incluye sugerencias automáticas para definir qué productos conviene poner en descuento, ni modelos predictivos.

## Riesgos de negocio y técnicos

### Riesgos de negocio
1. Reglas de descuento ambiguas
   - Impacto: decisiones promocionales inconsistentes, menor conversión y pérdida de confianza por parte del comercio.
   - Mitigación QA: prueba de aceptación temprana de criterios de negocio con usuarios objetivo y validación de criterios de aceptación antes del despliegue.

2. Cambios frecuentes en descuentos dinámicos sin evaluación de impacto.
   - Impacto: retrabajo continuo y defectos de regresión.
   - Mitigación QA: control formal de cambios, prueba de sistema de extremo a extremo y regresión focalizada por riesgo en cada ajuste de reglas.

3. Desglose del descuento poco claro para el usuario final.
   - Impacto: abandono del flujo de compra, aumento de reclamos y percepción de falta de transparencia.
   - Mitigación QA: prueba de sistema funcional de UX y prueba de aceptación con usuarios para validar claridad del desglose, descuento aplicado y precio final.

### Riesgos técnicos
1. Cálculo incorrecto del descuento total por orden de aplicación o acumulación de reglas.
   - Impacto: precio final erróneo, pérdida de margen para el comercio o sobreprecio para el cliente, y aumento de reclamos.
   - Mitigación QA: prueba de sistema extremo a extremo y validación de aceptación con ejemplos aprobados por negocio.


2. Validaciones incompletas o inconsistentes de datos de entrada.
   - Impacto: ingreso de valores inválidos (nulos, negativos, fuera de rango).
   - Mitigación QA: pruebas de validación en frontend y backend, casos negativos y de frontera, y prueba de integración de sistemas para asegurar consistencia de rechazos entre servicios e interfaces externas.


3. Rendimiento insuficiente en la simulación de precio bajo uso concurrente.
   - Impacto: tiempos de respuesta altos o inestables en horas pico, degradación de la experiencia, abandono del flujo y menor conversión de promociones.
   - Mitigación QA: ejecutar pruebas de carga y estrés con concurrencia progresiva en entorno representativo de sistema y monitorear latencia y estabilidad antes de despliegue.
