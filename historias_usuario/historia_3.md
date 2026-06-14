# HU-03: Calendario de Riego

* **ID:** HU-03
* **Módulo:** FullStack / UX
* **Prioridad:** Alta
* **Estimación:** 5 Puntos

## Descripción de la HU
Como usuario, quiero ver un calendario visual con fechas de riego y cosecha marcadas para no olvidar las tareas de mantenimiento.

## Flujo guiado
1. El usuario navega al módulo "Calendario".
2. El sistema despliega una vista mensual resaltando las fechas clave.
3. El usuario puede hacer clic en las flechas de navegación para explorar meses anteriores o futuros.

## Criterios de aceptación
* **Código de colores y leyenda:** Las fechas con tareas de riego programado deben resaltar visualmente en color azul, y las de cosecha en verde. Se debe incluir una leyenda permanente cerca del calendario para que los usuarios nuevos identifiquen qué significa cada color.
* **Superposición de tareas:** Si un mismo día contiene simultáneamente tareas de riego y de cosecha, la celda del calendario debe mostrar un indicador dual (mitad de cada color) o un ícono específico para alertar sobre la doble carga de trabajo.
* **Navegación ágil:** Además de las flechas para avanzar o retroceder de mes, debe existir un botón de acceso rápido denominado "Hoy" que devuelva al usuario instantáneamente al mes y día actuales.
* **Interacción de detalle (Tooltips):** Al pasar el cursor (*hover*) o hacer clic sobre un día marcado, el sistema debe desplegar un pequeño recuadro informativo detallando la acción exacta (ej. "Regar Tomates en Parcela 1").
* **Manejo de fechas pasadas:** Los días anteriores a la fecha actual deben mostrarse deshabilitados (en tonos grises), impidiendo que el usuario pueda arrastrar o agendar nuevas tareas en el pasado, pero permitiéndole consultar el historial.
* **Responsividad Móvil:** Dado que las cuadrículas mensuales no son legibles en pantallas pequeñas, el calendario debe adaptarse automáticamente a una vista tipo "Agenda" o "Lista" vertical cuando se acceda desde un teléfono celular.
