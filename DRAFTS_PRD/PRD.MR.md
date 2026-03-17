# PRD

## Visión
En LOYALTY buscamos crear la mejor calculadora de descuentos dinámicos para e-commerce, ayudando a comercios de cualquier tamaño a tomar decisiones promocionales inteligentes basadas en temporada, fidelidad del cliente y tipo de producto, para construir relaciones más justas, sostenibles y duraderas con sus clientes.

## Objetivos
1. Durante las primeras 8 semanas del MVP, lograr que al menos 90% de los comercios clientes configure una promoción completa (temporada, fidelidad y tipo de producto) en menos de 3 minutos.
2. En los primeros 90 días del MVP, aumentar en al menos 8% las compras de productos en promoción, comparado con el nivel inicial.
3. Aumentar en al menos 10% la tasa de recompra de clientes fidelizados en los comercios clientes durante el primer trimestre de uso.
4. Desde el lanzamiento del MVP, lograr que 95% de las simulaciones de precio muestren claramente el detalle del descuento (temporada, fidelidad y tipo de producto) antes de confirmar el precio final.

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