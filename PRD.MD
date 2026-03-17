# 🛒 E-commerce: Calculadora de Descuentos Dinámicos (LOYALTY)
## Información del proyecto
* **Nombre del Producto:** LOYALTY (Calculadora de Descuentos Dinámicos) 
* **Autores:** Agustín Mites, Matias Regaló y Luis Ospino
* **Fecha:** 17 de Marzo de 2026 

## Visión y objetivos
### **Visión:** 
Para tiendas de e-commerce B2C en fase de escalamiento que necesitan optimizar sus estrategias promocionales sin comprometer su rentabilidad, LOYALTY es una plataforma de descuentos dinámicos que permite tomar decisiones promocionales inteligentes basadas en la temporada, la fidelidad del cliente y el tipo de producto. A diferencia de las herramientas básicas de descuentos que ofrecen las plataformas de e-commerce, nuestro producto determina el descuento mínimo viable para maximizar las conversiones mientras protege los margenes de ganancias proyectando relaciones más justas, sostenibles y duraderas con los clientes.
### Objetivos:
1. Mejorar la experiencia de configuración para que los ecommerce clientes puedan crear promociones completas en menos de 3 minutos.
2. Incrementar las compras de productos en promoción, comparado con el nivel inicial.
3. Fomentar la recompra de clientes fidelizados en los comercios clientes durante el primer trimestre de uso.

## **Alcance del MVP**
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
    
- OUT
   1. No incluye cuentas reales de usuario: registro, inicio de sesión y gestión avanzada de permisos o roles.
   2. No incluye historial completo de operaciones ni auditoría detallada de compras.
   3. No incluye análisis avanzado del negocio, como tableros de indicadores o reportes personalizados.
   4. No incluye sugerencias automáticas para definir qué productos conviene poner en descuento, ni modelos predictivos.

## Riesgos de negocio y técnicos

### Riesgos de negocio
1. Reglas de descuento ambiguas
   - Impacto: decisiones promocionales inconsistentes, menor conversión y pérdida de confianza por parte del comercio cliente.
   - Mitigación QA: prueba de aceptación temprana de criterios de negocio con usuarios objetivo y validación de criterios de aceptación antes del despliegue.

2. Cambios frecuentes en descuentos dinámicos sin evaluación de impacto.
   - Impacto: retrabajo continuo y defectos de regresión.
   - Mitigación QA: control formal de cambios, prueba de sistema de extremo a extremo y regresión focalizada por riesgo en cada ajuste de reglas.

3. Desglose del descuento poco claro para el usuario final.
   - Impacto: abandono del flujo de compra, aumento de reclamos y percepción de falta de transparencia.
   - Mitigación QA: prueba de sistema funcional de UX y prueba de aceptación con usuarios para validar claridad del desglose, descuento aplicado y precio final.

4. Rendimiento por debajo del objetivo definido
   - Impacto: Pérdida de credibilidad en el producto
   - Mitigación QA: Validar que el producto cumpla al 100% con los criterios de aceptación

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