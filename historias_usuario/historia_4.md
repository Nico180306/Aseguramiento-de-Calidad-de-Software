# HU-04: Geolocalización y Mapas

* **ID:** HU-04
* **Módulo:** API / Frontend
* **Prioridad:** Media
* **Estimación:** 8 Puntos

## Descripción de la HU
Como usuario, quiero visualizar la ubicación de las parcelas en un mapa interactivo para identificar mi zona de trabajo y rutas de acceso.

## Flujo guiado
1. El usuario selecciona la opción "Mapa de Parcelas" en el menú principal.
2. El sistema renderiza un mapa interactivo poblado con marcadores correspondientes a las parcelas activas.
3. El usuario interactúa con un marcador para visualizar información emergente sobre esa parcela específica.

## Criterios de aceptación
* **Inicialización y Centrado:** Al cargar la vista, el mapa debe centrarse automáticamente en las coordenadas base de los huertos (Quito), con un nivel de zoom adecuado (ej. nivel 14) para tener una visión panorámica inicial.
* **Información Emergente (Info Window):** Al hacer clic sobre un marcador, el *popup* debe mostrar explícitamente el nombre de la parcela y el responsable asignado. Adicionalmente, debe incluir un botón o enlace ("Ver Detalle") para redirigir a la vista de inventario de esa parcela específica.
* **Carga Asíncrona (Rendimiento):** La solicitud de los puntos geográficos a la base de datos debe realizarse de forma asíncrona (AJAX) una vez que la vista base ya esté renderizada. El tiempo de pintado de los marcadores no debe interferir con la navegación de la página.
* **
