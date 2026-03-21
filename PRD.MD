# 🛒 E-commerce: Calculadora de Descuentos Dinámicos (LOYALTY)
## Información del proyecto
* **Nombre del Producto:** LOYALTY (Calculadora de Descuentos Dinámicos) 
* **Autores:** Agustín Mites, Matias Regaló y Luis Ospino
* **Fecha:** 20 de Marzo de 2026 

## Visión y objetivos
### Visión:
Para tiendas de e-commerce B2C en fase de escalamiento que necesitan optimizar sus estrategias promocionales sin comprometer su rentabilidad, LOYALTY es una plataforma de descuentos dinámicos que permite tomar decisiones promocionales inteligentes basadas en la temporada, la fidelidad del cliente y el tipo de producto. A diferencia de las herramientas básicas de descuentos que ofrecen las plataformas de e-commerce, nuestro producto determina el descuento mínimo viable para maximizar las conversiones mientras protege los margenes de ganancias.

### Problema a resolver y Contexto:
En la actualidad, las tiendas de comercio electrónico B2C dependen de descuentos generales, estáticos y administrados manualmente, lo que genera ineficiencias operativas y financieras, además de fomentar un comportamiento perjudicial en el cliente, quien solo comprará cuando haya rebajas; por lo tanto, la marca perderá valor.  
Este modelo de promociones reduce la eficiencia del margen del negocio, ya que ofrece el mismo descuento a compradores recurrentes como a aquellos que solo buscan ofertas puntuales. A esto se suma la gestión manual de campañas, que dificulta reaccionar en tiempo real a cambios en la demanda, inventario o comportamiento del consumidor. Como resultado, los comercios pierde margen de ganancias innecesariamente, aumentando el costo de adquisición y reduciendo su rentabilidad a largo plazo.  
En un contexto donde los costos de publicidad aumentan, las empresas han pasado de priorizar el crecimiento a toda costa a una estrategia de retención efectiva; como consecuencia, es necesaria una herramienta que proteja sus márgenes.
En este sentido, la rentabilidad y la retención son prioritarias, lo que impulsa la necesidad de una capa inteligente que permita personalizar y optimizar descuentos de forma dinámica. En función de ello, LOYALTY plantea una solución entre el catálogo y el checkout, que sea capaz de calcular e inyectar precios personalizados en tiempo real.

### Objetivos:
1. Lograr que el 80% de los usuarios que adopten la calculadora de descuentos puedan crear y activar promociones completas en la plataforma en menos de 5 minutos, durante el primer mes posterior a la implementación del software.
2. Mantener un margen de ganancia bruta promedio del 25% en productos con promociones, incrementando también en un 15% la tasa de conversión respecto al promedio previo a la implementación, durante los primeros 6 meses posteriores al lanzamiento.
3. Aumentar en un 20% la frecuencia de recompra de clientes frecuentes en los e-commerce durante el primer trimestre, mediante ofertas personalizadas basadas en sus métricas de cantidad de compras y montos gastados. 


## Alcance del MVP

| In                                                                                                                                                                                                       | Out                                                                                                                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **API REST Stateless - S2S**: <br> Comunicación exclusiva entre servidores: el backend del e-commerce envía el payload con el carrito y las métricas; posteriormente recibe el descuento en tiempo real. | **Sincronización de datos históricos**: <br> No se usará ni se consumira datos con historial de transacciones, nombres o datos personales de las bases de datos de los compradores finales |
| **Validación de autenticación**: <br> El sistema solo procesará aquellas solicitudes que incluyan el API Key vinculada con el comercio.                                                                  | **SDKs de frontend**: <br> No se desarrollarán librerías de JavaScript para el navegador. La integración debe ser estrictamente de servidor a servidor.                                    |
| **Lógica de descuento combinada**: <br> Capacidad de sumar descuentos, de temporada, fidelidad y tipo de producto con la aplicación del límite máximo de descuento permitido                             | **Modelos predictivos/IA**: <br> No tendrá sugerencias automáticas de optimización de precios o recomendaciones.                                                                           |
| **Dashboard de configuración UI**: <br> Interfaz web para que el administrador del e-commerce pueda definir las reglas de descuentos, umbrales de clasificación de fidelidad y logs de aplicación.       | **Integraciones nativas/plugins**: <br> No se desarrollarán apps para Shopify, VTEX O MAGENTO. No se incluye análisis avanzados de negocio, tableros de indicadores ni reportes.           |
| **Autenticación al dashboard**: <br> Sistema de autenticación especifico para los gestores del e-commerce al dashboard de configuración.                                                                 | **Gestion de identidad B2C**: <br> No se gestionara perfiles, sesiones ni contraseñas de los compradores finales de los e-commerce.                                                        |
| **Persistencia de configuración y usuarios**: <br> Almacenamiento de las reglas, parámetros de fidelidad y credenciales de los usuarios administradores en base de datos.                                | **Persistencia de transacciones y perfiles B2C**: <br> No se almacenarán datos de transacciones, ni perfiles de los compradores finales, ni del detalle de carritos procesados.            |
| **Gestión de credenciales**: <br> Interfaz para generar, rotar y revocar API Keys de acceso para las peticiones del e-commerce restringida exclusivamente al perfil de administrador.                    | **Pasarela de pagos/Checkout**: <br> Loyalty no procesará pagos, solo devolverá el precio calculado al servidor del cliente.                                                               |
| **Logs de auditoría**: <br> Registro técnico de qué regla se aplicó a cada solicitud del e-commerce.                                                                                                     | **Almacenamiento de sesiones**: <br> No se guardara ni mantendra persistencia de la navegación del usuario final.                                                                          |

## Riesgos de negocio y técnicos

### Riesgos de negocio

| Descripción                                              | Probabilidad | Impacto | Riesgo | Mitigación principal                                                                                                                       |
| -------------------------------------------------------- | ------------ | ------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Retrasos en la entrega del MVP                           | 3            | 3       | 9      | Comunicar avances y antes de la fecha limite notificar a los clientes que se extenderá la fecha de entrega                                 |
| Cambios frecuentes en el alcance del MVP                 | 3            | 3       | 9      | Evaluar impacto en tiempo/costo y aprobar solo cambios críticos                                                                            |
| Definición ambigua de criterios de aceptación            | 2            | 3       | 6      | Definir criterios de aceptación claros y validar con QA antes de iniciar el sprint.                                                        |
| Problemas de comunicación entre QA y DEV                 | 1            | 2       | 2      | Realizar reuniones cortas diarias para asignar responsables y fechas de solución.                                                          |
| Bajo uso inicial del MVP por parte de comercios clientes | 2            | 3       | 6      | Acompañar a los comercios en el uso del sistema durante las primeras 2 semanas y revisar cada semana el nivel de uso para aplicar mejoras. |

### Riesgos técnicos

| Descripción                                                                            | Probabilidad | Impacto | Riesgo | Mitigación principal                                                                                                      |
| -------------------------------------------------------------------------------------- | ------------ | ------- | ------ | ------------------------------------------------------------------------------------------------------------------------- |
| Cálculo incorrecto del descuento total por orden de aplicación o acumulación de reglas | 3            | 3       | 9      | Definir reglas de cálculo claras y hacer pruebas completas con casos reales antes de publicar.                            |
| Validaciones incompletas o inconsistentes de datos de entrada                          | 3            | 3       | 9      | Validar datos, bloqueando valores vacíos, negativos o fuera de rango.                                                     |
| Cálculo e inyección de descuentos en el checkout                                       | 2            | 3       | 6      | Probar el sistema con alta concurrencia antes y optimizar consultas o procesos lentos detectados.                         |
| Interfaz de configuración poco clara para usuarios del comercio                        | 2            | 3       | 6      | Simplificar la pantalla principal, usar etiquetas claras y validar la usabilidad con pruebas rápidas con usuarios reales. |
| Cambios de reglas sin trazabilidad                                                     | 2            | 2       | 4      | Registrar quién, cuándo y qué regla se modificó, y mostrar un historial simple de cambios dentro del módulo.              |
