# Proyecto 08: Gestor de Inventario y Alerta de Reposición

## Resumen
Este proyecto consiste en validar y transformar registros operativos diarios para convertir datos sin procesar en información confiable para el control de inventario y la toma de decisiones. En esencia, el script en Python puro procesa movimientos diarios (`venta` y `devolucion`) sobre un diccionario `inventario` y una lista `transacciones`, revisa posibles inconsistencias o registros anómalos, calcula el valor total del stock disponible y detecta qué productos quedan por debajo de su `stock_minimo` al cierre de operaciones.

Desde el enfoque de análisis de datos, muestra cómo traducir reglas de negocio y controles de calidad de datos en una lógica clara, trazable y reproducible sin interrumpir el flujo ante entradas inválidas.

## Reglas de negocio y lógica
- **Validación de SKU:** Si el `sku` de una transacción no existe en `inventario`, se registra una incidencia en `incidencias` y no se modifica el stock.
- **Ventas (`venta`):** Solo se descuenta `cantidad` de `stock_actual` si hay unidades suficientes (`disponible >= cantidad`); si no alcanza, se rechaza la operación y se guarda en `incidencias` sin alterar el stock.
- **Devoluciones (`devolucion`):** Suma las unidades devueltas (`cantidad`) al `stock_actual` del producto correspondiente.
- **Valoración total del inventario:** Tras procesar las transacciones, acumula `stock_actual * costo_unitario` de cada producto en `valor_total` (`+=`).
- **Alertas de reposición:** Al cierre del ciclo, revisa qué productos tienen `stock_actual < stock_minimo` y los añade a `alertas_reposicion` (`.append()`).

## Cómo ejecutarlo en Google Colab
1. Abre [Google Colab](https://colab.research.google.com/) y crea un nuevo notebook.
2. Ejecuta los datos iniciales (`inventario`, `transacciones` y `incidencias = []`) y luego el bloque de procesamiento de transacciones, cálculo de valor total y alertas de reposición (`Shift + Enter`).
3. Revisa las salidas impresas (`incidencias`, `valor_total` y `alertas_reposicion`).

## Conclusión
Este proyecto me permitió practicar la lógica base de Python puro—estructuras de datos (`diccionarios` y `listas`), bucles (`for`), condicionales (`if`/`elif`/`else`), acumuladores (`+=`) y validación de casos límite—aplicada a un escenario cotidiano de control de inventario y revisión de registros, dejando el flujo documentado y listo en GitHub para futuras mejoras.
