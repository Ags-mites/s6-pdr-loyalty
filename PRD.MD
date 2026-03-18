# 🛒 E-commerce: Calculadora de Descuentos Dinámicos (LOYALTY)
## Información del proyecto
* **Nombre del Producto:** LOYALTY (Calculadora de Descuentos Dinámicos) 
* **Autores:** Agustín Mites, Matias Regaló y Luis Ospino
* **Fecha:** 18 de Marzo de 2026 

### Introducción del problema:
En la actualidad, las tiendas de comercio electrónico B2C, dependen de descuentos generales y estáticos que se administran manualmente, ocasionando un comportamiento perjudicial en el cliente, quien solo comprará cuando haya rebajas, por lo tanto la marca perderá valor. El modelo tradicional de promociones reduce las ganancias, ya que ofrece el mismo descuento a un comprador recurrente que a uno que solo busca ofertas puntuales. Esto genera que aumenté el costo de adquisición y disminuye el valor del cliente a lo largo del tiempo.  
Dado el aumento de los costos de publicidad, la rentabilidad ha pasado de ser una estrategia de crecimiento a ser una estrategia enfocada en la retención efectiva. Como consecuencia, los comercios necesitan una herramienta que proteja sus márgenes.

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

## Riesgos de negocio y tecnicos

### Riesgos de negocio

| Descripción | Probabilidad | Impacto | Riesgo | Mitigación principal |
|-------------|--------------|---------|--------|----------------------|
| Retrasos en la entrega del MVP | 3 | 3 | 9 | Comunicar avances y antes de la fecha limite notificar a los clientes que se extenderá la fecha de entrega  |
| Cambios frecuentes en el alcance del MVP | 3 | 3 | 9 | Evaluar impacto en tiempo/costo y aprobar solo cambios críticos|
| Definición ambigua de criterios de aceptación | 2 | 3 | 6 | Documentar criterios en formato Given-When-Then y validar que esten centrados en el negocio antes de iniciar desarrollo. |
| Problemas de comunicación entre QA y DEV | 1 | 2 | 2 | Realizar reuniones cortas diarias para asignar responsables y fechas de solución. |
| Bajo uso inicial del MVP por parte de comercios clientes | 2 | 3 | 6 | Acompañar a los comercios en el uso del sistema durante las primeras 2 semanas y revisar cada semana el nivel de uso para aplicar mejoras. |

### Riesgos tecnicos

| Descripción | Probabilidad | Impacto | Riesgo | Mitigación principal |
|-------------|--------------|---------|--------|----------------------|
| Cálculo incorrecto del descuento total por orden de aplicación o acumulación de reglas | 3 | 3 | 9 | Definir reglas de cálculo claras y hacer pruebas completas con casos reales antes de publicar. |
| Validaciones incompletas o inconsistentes de datos de entrada | 3 | 3 | 9 | Validar datos, bloqueando valores vacíos, negativos o fuera de rango. |
| Rendimiento insuficiente en la simulación de precio bajo uso concurrente | 2 | 3 | 6 | Probar el sistema con alta concurrencia antes y optimizar consultas o procesos lentos detectados. |
| Interfaz de configuración poco clara para usuarios del comercio | 2 | 3 | 6 | Simplificar la pantalla principal, usar etiquetas claras y validar la usabilidad con pruebas rápidas con usuarios reales. |
| Cambios de reglas sin trazabilidad | 2 | 2 | 4 | Registrar quién, cuándo y qué regla se modificó, y mostrar un historial simple de cambios dentro del módulo. |
