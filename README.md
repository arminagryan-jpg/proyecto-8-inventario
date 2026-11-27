Resumen del proyecto (enfoque Data Analyst)
Este proyecto consiste en validar y transformar registros operativos diarios para convertir datos sin procesar en información confiable para la toma de decisiones. A partir de una estructura base de datos y una lista de movimientos diarios, el flujo aplica reglas de calidad y control:

Validación y limpieza de registros: Detecta códigos o valores inconsistentes/inexistentes y bloquea operaciones inválidas (como cantidades que superan la disponibilidad real) para evitar errores o distorsiones en los resultados.

Seguimiento de incidencias: Registra las anomalías de forma trazable sin interrumpir el procesamiento del resto de los datos.

Cálculo de métricas y alertas: Consolida los valores resultantes al cierre del ciclo y señala los elementos que requieren atención o reposición prioritaria.

Valor analítico: Demuestra cómo traducir reglas de negocio y controles de calidad de datos en una lógica clara, reproducible y auditable, dejando el proyecto documentado y listo para su revisión en el repositorio.

Si quieres adaptarlo a un proyecto específico de tu bootcamp (por ejemplo, el de inventario o el de movilidad/vivienda), dime cuál es y lo ajustamos a sus datos exactos.# proyecto-8-inventario
El proyecto representa una revisión diaria para detectar fechas falsas o datos inconsistentes en el registro, y en esencia procesa transacciones diarias (venta y devolucion) sobre un diccionario inventario usando Python puro (sin atajos externos): valida si existe el sku, comprueba si hay stock suficiente antes de descontar, registra las incidencias sin detener el programa, acumula el valor total del inventario (stock_actual * costo_unitario) y detecta qué productos quedan por debajo de su stock_minimo al cierre de operaciones.
