# 🛒 E-commerce: Calculadora de Descuentos Dinámicos (LOYALTY)
## Información del proyecto
* **Nombre del Producto:** LOYALTY (Calculadora de Descuentos Dinámicos) 
* **Estado del Documento:** En fase de definición estratégica
* **Autores:** Agustín Mites, Matias Regaló y Luis Ospino
* **Fecha de Última Actualización:** 17 de Marzo de 2026 
* **Versión Objetivo:** MVP (v1.0)

## Visión y objetivos
### **Visión:** 
Para tiendas de e-commerce B2C en fase de escalamiento que necesitan optimizar sus estrategias promocionales sin comprometer su rentabilidad, LOYALTY es una plataforma de descuentos dinámicos que permite tomar decisiones promocionales inteligentes basadas en la temporada, la fidelidad del cliente y el tipo de producto. A diferencia de los servicios de cupones estáticos nativos de plataformas de e-commerce, nuestro producto determina el descuento mínimo viable para maximizar las conversiones mientras protege los margenes de ganancias proyectando  relaciones más justas, sostenibles y duraderas con los clientes.
### Objetivos:
1. Lograr que al menos 93% de los comercios clientes configure una promoción completa (temporada, fidelidad y tipo de producto) en menos de 3 minutos.
2. Aumentar en al menos 8% las compras de productos en promoción, comparado con el nivel inicial.
3. Aumentar en al menos 10% la tasa de recompra de clientes fidelizados en los comercios clientes durante el primer trimestre de uso.

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