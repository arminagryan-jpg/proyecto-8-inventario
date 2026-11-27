## Análisis del proyecto 

### 1. Qué hice como analista
- **Revisé los datos antes de modificar el inventario:** Traté las transacciones (`venta` y `devolucion`) como datos operativos que podían tener errores o cantidades imposibles, en lugar de darlos por válidos sin comprobar.
- **Apliqué controles de calidad:** Verifiqué que el `sku` existiera en `inventario` antes de leer sus datos (evitando fallos con `SKU-99`) y comprobé que hubiera stock suficiente (`stock_actual >= cantidad`) antes de descontar una venta (evitando que `SKU-02` quedara en negativo).
- **Registré incidencias sin detener el proceso:** Guardé los casos problemáticos en `incidencias` y dejé que el resto de movimientos válidos continuaran.
- **Calculé métricas y alertas al cierre:** Al terminar las transacciones, sumé el valor económico del stock restante y marqué los productos por debajo de su `stock_minimo`.

### 2. Métricas y hallazgos principales
- **Incidencias en transacciones:** **2 de 5** operaciones (**40 %**) no se pudieron aplicar:
  - `SKU-99` (venta de 1 unidad): no existe en el catálogo (`inventario`).
  - `SKU-02` / *Monitor 24* (venta de 6 unidades): supera las **4** unidades disponibles.
- **Stock final por producto:**
  - `SKU-01` (*Teclado RGB*): de **16** a **4** unidades (mínimo: **5**).
  - `SKU-02` (*Monitor 24*): se mantiene en **4** unidades al rechazarse la venta (mínimo: **5**).
  - `SKU-03` (*Mouse Gamer*): sube de **8** a **11** unidades por una devolución de **3** (mínimo: **10**).
  - `SKU-04` (*Audifonos Pro*): baja de **2** a **0** unidades (mínimo: **4**).
- **Valor total del inventario (`valor_total`):** **1,035.00** (`(4 × 40.0) + (4 × 150.0) + (11 × 25.0) + (0 × 65.0)`). Solo `SKU-02` representa **600.00** (**~58 %**) de ese valor.
- **Alertas de reposición (`stock_actual < stock_minimo`):** **3 de 4** productos cierran por debajo de su mínimo (`SKU-01`, `SKU-02` y `SKU-04`). Solo `SKU-03` (`11` vs. `10`) queda por encima.

### 3. Conclusiones y siguientes pasos
- **Prioridad alta de reposición:** La mayor parte del catálogo queda por debajo del stock mínimo al cierre, con `SKU-04` agotado (**0** unidades).
- **Revisar reposiciones previas:** `SKU-02`, `SKU-03` y `SKU-04` ya empezaban por debajo de su `stock_minimo` antes de las transacciones del día, lo que sugiere demoras al reponer o umbrales mínimos que conviene ajustar.
- **Revisar códigos de venta:** La venta de `SKU-99` apunta a un posible error de código o a un producto aún no registrado en `inventario` que conviene verificar.
