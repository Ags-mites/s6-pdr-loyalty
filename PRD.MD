# 🛒 E-commerce: Calculadora de Descuentos Dinámicos (LOYALTY)
## Información del proyecto
* **Nombre del Producto:** LOYALTY (Calculadora de Descuentos Dinámicos) 
* **Autores:** Agustín Mites, Matias Regaló y Luis Ospino
* **Fecha:** 18 de Marzo de 2026 

## Visión y objetivos
### Visión:
Para tiendas de e-commerce B2C en fase de escalamiento que necesitan optimizar sus estrategias promocionales sin comprometer su rentabilidad, LOYALTY es una plataforma de descuentos dinámicos que permite tomar decisiones promocionales inteligentes basadas en la temporada, la fidelidad del cliente y el tipo de producto. A diferencia de las herramientas básicas de descuentos que ofrecen las plataformas de e-commerce, nuestro producto determina el descuento mínimo viable para maximizar las conversiones mientras protege los margenes de ganancias proyectando relaciones más justas, sostenibles y duraderas con los clientes.

### Problema a resolver y Contexto:
En la actualidad, las tiendas de comercio electrónico B2C dependen de descuentos generales, estáticos y administrados manualmente, lo que genera ineficiencias operativas y financieras, además de fomentar un comportamiento perjudicial en el cliente, quien solo comprará cuando haya rebajas; por lo tanto, la marca perderá valor.  
Este modelo de promociones impacta directamente en el margen operativo bruto, ya que ofrece el mismo descuento a compradores recurrentes como a aquellos que solo buscan ofertas puntuales. A esto se suma la gestión manual de campañas, que dificulta reaccionar en tiempo real a cambios en la demanda, inventario o comportamiento del consumidor. Como resultado, los comercios subsidian ventas innecesariamente, aumentando el costo de adquisición y reduciendo su rentabilidad a largo plazo.  
En un contexto donde los costos de publicidad aumentan, las empresas han pasado de priorizar el crecimiento a toda costa a una estrategia de retención efectiva; como consecuencia, es necesaria una herramienta que proteja sus márgenes.
En este sentido, la rentabilidad y la retención son prioritarias, lo que impulsa la necesidad de una capa inteligente que permita personalizar y optimizar descuentos de forma dinámica. En función de ello, LOYALTY plantea una solución entre el catálogo y el checkout, que sea capaz de calcular e inyectar precios personalizados en tiempo real.

### Objetivos:
1. Lograr que el 80% de los usuarios que adopten la calculadora de descuentos puedan crear y activar promociones completas en la plataforma en menos de 3 minutos, durante el primer mes posterior a la implementación del software.
2. Mantener un margen de ganancia bruta promedio del 25% en productos con promociones, incrementando también en un 15% la tasa de conversión respecto al promedio previo a la implementación, durante los primeros 6 meses posteriores al lanzamiento.
3. Aumentar en un 20% la frecuencia de recompra de clientes frecuentes en los e-commerce durante el primer trimestre, mediante ofertas personalizadas basadas en sus métricas de cantidad de compras y montos gastados. 


## Alcance del MVP

| In                                                                 | Out                                                                  |
|-----|-----|
| **API REST transaccional:** <br> Endpoint para cálculo en tiempo real que procesa un payload con datos de los productos del carrito y métricas de compras del usuario. | **Almacenamiento de usuarios finales:** <br> No se usará base de datos con historial de transacciones, nombres o datos personales de los clientes del e-commerce |
| **Dashboard de configuración UI:** <br> Interfaz web para que el administrador del e-commerce pueda definir las reglas de descuentos y los umbrales de clasificación de fidelidad. | **Integraciones nativas/plugins:** <br> No se desarrollarán apps para Shopify, VTEX O MAGENTO. La integración vía API recae en el cliente. |
| **Lógica de descuento combinada:** <br> Motor de reglas que utilice descuentos de temporada, fidelidad y tipo de producto. | **Modelos predictivos/IA:** <br> No tendrá sugerencias automáticas de optimización de precios o recomendaciones. |
| **Gestión de accesos:** <br> Generación y revocación de access tokens para autenticar las peticiones del e-commerce. | **Pasarela de pagos/Checkout:** <br> Loyalty no procesará pagos, solo devolverá el precio calculado al frontend del cliente. |

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
