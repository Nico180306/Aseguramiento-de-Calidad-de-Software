# Caso de Prueba Positivo: Flujo Normal
## ID: TC-011
## Título: Renderizado exitoso de gráficos interactivos, tooltips y adaptabilidad responsiva

**Objetivo:** 
Validar que el Dashboard renderice correctamente los gráficos de Barras y Pastel basándose en consultas optimizadas, despliegue tooltips numéricos precisos al interactuar con los elementos, y adapte la disposición de los contenedores `<canvas>` (lado a lado vs. apilado vertical) según la resolución del dispositivo.

**Precondiciones:**
* El usuario debe estar autenticado con el rol de `Administrador`.
* La base de datos debe contener un volumen representativo de registros históricos para el año en curso (ej. 2026), incluyendo plantas en distintos estados de salud y un conteo variado de cosechas en meses anteriores.
* Se debe contar con una herramienta de monitoreo de consultas (ej. SQL Server Profiler o consola de Entity Framework) para validar la optimización.
* La vista inicial debe ejecutarse en una pantalla de escritorio (ej. resolución 1920x1080).

**Datos de prueba:**
* **Datos esperados en BD para el mes de Abril:** `42` plantas cosechadas.
* **Proporciones esperadas de Salud:** `Sana` (120 plantas), `En Tratamiento` (50 plantas), `Enferma` (30 plantas).

**Pasos:**
1. Iniciar sesión y navegar al "Dashboard Principal".
2. Monitorear los logs de base de datos para verificar que las sumatorias se resolvieron mediante funciones de agregación (`GROUP BY`, `COUNT`) a nivel de SQL.
3. Observar la disposición visual de los gráficos en la pantalla de escritorio.
4. Posicionar el cursor (*hover*) sobre la barra correspondiente al mes de "Abril" en el Gráfico de Productividad.
5. Observar el Gráfico de Pastel y verificar que las proporciones correspondan a los estados de salud y calculen el porcentaje correctamente.
6. Utilizar las herramientas de desarrollador del navegador (F12) para emular una pantalla móvil (ej. ancho de 375px).

**Resultado esperado:**
* El motor de base de datos ejecuta la carga de datos de manera optimizada, sin trasladar toda la tabla a la memoria de la aplicación.
* En escritorio, los gráficos se muestran lado a lado de forma clara. Al hacer *hover* sobre "Abril", un *tooltip* dinámico muestra el valor numérico exacto: "42".
* El gráfico de pastel renderiza correctamente los tres estados y sus porcentajes proporcionales.
* Al emular la pantalla móvil, los elementos `<canvas>` detectan el cambio de *viewport* y se redimensionan fluidamente, apilándose uno debajo del otro sin recortar las leyendas ni distorsionar la información.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar capturas de pantalla de la vista escritorio con el tooltip visible, captura de la vista móvil apilada y fragmento del log de la consulta SQL ejecutada]

# Caso de Prueba Negativo: Flujo Alterno
## ID: TC-012
## Título: Intercepción de ausencia de datos y manejo de "Empty States"

**Objetivo:** 
Validar que el sistema procese adecuadamente la falta de datos estadísticos en un huerto de reciente creación, evitando el renderizado de gráficos vacíos, errores de división por cero y mostrando los contenedores de advertencia (*Empty States*) especificados.

**Precondiciones:**
* El usuario debe estar autenticado con el rol de `Administrador`.
* Se debe haber asignado al supervisor un huerto totalmente nuevo (ej. "Huerto Piloto Bicentenario").
* La base de datos debe tener exactamente `0` registros de plantas sembradas, `0` cosechas y `0` historiales de salud para dicho huerto.

**Datos de prueba:**
* **Identificador del huerto:** Huerto Piloto Bicentenario (ID: 999).
* **Registros asociados:** `null` o `Count = 0`.

**Pasos:**
1. Iniciar sesión en el sistema con la cuenta del administrador asignado al "Huerto Piloto Bicentenario".
2. Ser redirigido o navegar manualmente al "Dashboard Principal".
3. Observar el área de la pantalla destinada al Gráfico de Barras ("Cosechas por Mes").
4. Observar el área destinada al Gráfico de Pastel ("Estado de Salud de Plantas").
5. Abrir la consola de JavaScript del navegador (F12) para buscar posibles excepciones.

**Resultado esperado:**
* El sistema evalúa correctamente la ausencia de registros antes de inicializar la librería ChartJS.
* No se renderiza ningún elemento `<canvas>` en blanco ni con ejes en valor `0`.
* En su lugar, se dibujan contenedores estéticos en las posiciones de los gráficos que muestran explícitamente el texto: *"Aún no hay datos suficientes para generar este gráfico"*.
* La consola del navegador no registra errores de ejecución, excepciones de tipo *NullReference*, ni errores matemáticos como división por cero al intentar calcular los porcentajes del gráfico circular.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar capturas de pantalla de los contenedores de "Empty State" desplegados en la interfaz del Dashboard]
