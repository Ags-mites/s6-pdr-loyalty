# 🛒 E-commerce: Calculadora de Descuentos Dinámicos (LOYALTY)
## Información del proyecto
* **Nombre del Producto:** LOYALTY (Calculadora de Descuentos Dinámicos) 
* **Autores:** Agustín Mites, Matias Regaló y Luis Ospino
* **Fecha:** 17 de Marzo de 2026 

## Visión y objetivos
### **Visión:** 
Para tiendas de e-commerce B2C en fase de escalamiento que necesitan optimizar sus estrategias promocionales sin comprometer su rentabilidad, LOYALTY es una plataforma de descuentos dinámicos que permite tomar decisiones promocionales inteligentes basadas en la temporada, la fidelidad del cliente y el tipo de producto. A diferencia de las herramientas básicas de descuentos que ofrecen las plataformas de e-commerce, nuestro producto determina el descuento mínimo viable para maximizar las conversiones mientras protege los margenes de ganancias proyectando relaciones más justas, sostenibles y duraderas con los clientes.

### Contexto del proyecto:
En la actualidad, las tiendas de comercio electrónico B2C dependen de descuentos generales, estáticos y administrados manualmente, lo que genera ineficiencias operativas y financieras, además de fomentar un comportamiento perjudicial en el cliente, quien solo comprará cuando haya rebajas; por lo tanto, la marca perderá valor.  
Este modelo de promociones impacta directamente en el margen operativo bruto, ya que ofrece el mismo descuento a compradores recurrentes como a aquellos que solo buscan ofertas puntuales. A esto se suma la gestión manual de campañas, que dificulta reaccionar en tiempo real a cambios en la demanda, inventario o comportamiento del consumidor. Como resultado, los comercios subsidian ventas innecesariamente, aumentando el costo de adquisición y reduciendo su rentabilidad a largo plazo.  
En un contexto donde los costos de publicidad aumentan, las empresas han pasado de priorizar el crecimiento a toda costa a una estrategia de retención efectiva; como consecuencia, es necesaria una herramienta que proteja sus márgenes.
En este sentido, la rentabilidad y la retención son prioritarias, lo que impulsa la necesidad de una capa inteligente que permita personalizar y optimizar descuentos de forma dinámica. En función de ello, LOYALTY plantea una solución entre el catálogo y el checkout, que sea capaz de calcular e inyectar precios personalizados en tiempo real.

### Objetivos:
1. Lograr que el 80% de los usuarios que adopten la calculadora de descuentos puedan crear y activar promociones completas en la plataforma en menos de 3 minutos, durante el primer mes posterior a la implementación del software.
2. Mantener un margen de ganancia bruta promedio del 25% en productos con promociones, incrementando también en un 15% la tasa de conversión respecto al promedio previo a la implementación, durante los primeros 6 meses posteriores al lanzamiento.
3. Aumentar en un 20% la frecuencia de recompra de clientes frecuentes en los e-commerce durante el primer trimestre, mediante ofertas personalizadas basadas en su historial de compras. 


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