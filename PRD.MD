# 🛒 E-commerce: Calculadora de Descuentos Dinámicos (LOYALTY)
## Información del proyecto
* **Nombre del Producto:** LOYALTY (Calculadora de Descuentos Dinámicos) 
* **Autores:** Agustín Mites, Matias Regaló y Luis Ospino
* **Fecha:** 17 de Marzo de 2026 

## Visión y objetivos
### **Visión:** 
Para tiendas de e-commerce B2C en fase de escalamiento que necesitan optimizar sus estrategias promocionales sin comprometer su rentabilidad, LOYALTY es una plataforma de descuentos dinámicos que permite tomar decisiones promocionales inteligentes basadas en la temporada, la fidelidad del cliente y el tipo de producto. A diferencia de las herramientas básicas de descuentos que ofrecen las plataformas de e-commerce, nuestro producto determina el descuento mínimo viable para maximizar las conversiones mientras protege los margenes de ganancias proyectando relaciones más justas, sostenibles y duraderas con los clientes.

### Contexto del proyecto:
En la actualidad, las tiendas de comercio electrónico B2C, dependen de descuentos generales y estáticos que se administran manualmente, ocasionando un comportamiento perjudicial en el cliente, quien solo comprará cuando haya rebajas, por lo tanto la marca perderá valor.  
Este modelo de promociones impacta directamente en el margen operativo bruto, ya que ofrece el mismo descuento a un comprador recurrente que a uno que solo busca ofertas puntuales. Como tal, los comercios subsidian ventas innecesariamente, lo que aumenta el costo de adquisición del cliente y disminuye su valor con el paso del tiempo.  
Dado que, debido a los actuales de publicidad, la rentabilidad se ha transformado de una estrategia de crecimiento a toda costa a una estrategia de retención efectiva, como consecuencia, los comercios necesitan una herramienta que proteja sus márgenes.
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

| Descripción | Probabilidad | Impacto | Riesgo | Mitigación principal |
|-------------|--------------|---------|--------|----------------------|
| Retrasos en la entrega del MVP | 3 | 3 | 9 | Comunicar avances y antes de la fecha limite notificar a los clientes que se extenderá la fecha de entrega  |
| Cambios frecuentes en el alcance del MVP | 3 | 3 | 9 | Evaluar impacto en tiempo/costo y aprobar solo cambios críticos|
| Definición ambigua de criterios de aceptación | 2 | 3 | 6 | Documentar criterios en formato Given-When-Then y validar que esten centrados en el negocio antes de iniciar desarrollo. |
| Problemas de comunicación entre QA y DEV | 2 | 2 | 4 | Realizar reuniones cortas diarias para asignar responsables y fechas de solución. |
| Bajo uso inicial del MVP por parte de comercios clientes | 2 | 3 | 6 | Acompañar a los comercios en el uso del sistema durante las primeras 2 semanas y revisar cada semana el nivel de uso para aplicar mejoras. |

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