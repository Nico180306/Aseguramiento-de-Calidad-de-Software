# HU-06: Dashboard Estadístico

* **ID:** HU-06
* **Módulo:** Frontend / ChartJS
* **Prioridad:** Media
* **Estimación:** 8 Puntos

## Descripción de la HU
Como supervisor, quiero ver gráficos estadísticos sobre el estado de los huertos para tomar decisiones basadas en datos de productividad.

## Flujo guiado
1. El supervisor inicia sesión en el sistema.
2. Es dirigido automáticamente al "Dashboard Principal".
3. Visualiza los gráficos interactivos poblados con la información actual de la base de datos.

## Criterios de aceptación
* **Gráfico de Barras (Productividad):** Debe renderizar un gráfico de barras mostrando "Cosechas por Mes". El eje X representará los meses del año actual y el eje Y la cantidad de plantas cosechadas. Al posicionar el cursor sobre una barra, un *tooltip* debe mostrar el valor numérico exacto.
* **Gráfico de Pastel (Salud del Huerto):** Debe incluir un gráfico circular que categorice el "Estado de Salud de Plantas" (ej. Sana, En Tratamiento, Enferma), mostrando visualmente la proporción y calculando automáticamente el porcentaje de cada estado.
* **Manejo de Estados Vacíos (Empty States):** Si un huerto es nuevo y no tiene suficientes registros para generar estadísticas, en lugar de renderizar un gráfico vacío o roto, el sistema debe mostrar un contenedor con el mensaje: *"Aún no hay datos suficientes para generar este gráfico"*.
* **Carga de Datos (Optimización):** Para no sobrecargar la memoria del servidor, las agrupaciones y sumatorias de datos deben realizarse a nivel de base de datos (usando funciones de agregación en SQL/LINQ) y no en la memoria de la aplicación (C#).
* **Responsividad del Canvas:** Los elementos `<canvas>` de ChartJS deben estar configurados para redimensionarse automáticamente. En pantallas de escritorio se mostrarán lado a lado, mientras que en pantallas móviles deberán apilarse verticalmente (uno debajo del otro) manteniendo su legibilidad.
