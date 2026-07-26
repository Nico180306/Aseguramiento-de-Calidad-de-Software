# Caso de Prueba Positivo: Flujo Normal
## ID: TC-005
## Título: Visualización interactiva del calendario, tooltips y resolución de tareas superpuestas

**Objetivo:** 
Validar que el calendario renderice correctamente la leyenda y los códigos de color (azul y verde), identifique adecuadamente los días con cargas de trabajo dobles (riego y cosecha simultáneos) mediante un indicador dual, y despliegue el nivel de detalle correcto a través de los *tooltips*.

**Precondiciones:**
* El usuario debe estar autenticado en el sistema.
* El usuario debe tener asignada la "Parcela Norte".
* La base de datos debe tener pre-cargadas para el mes actual las siguientes tareas en la "Parcela Norte": 
  * Un Riego programado para dentro de 2 días.
  * Una Cosecha programada para dentro de 4 días.
  * Un Riego y una Cosecha programados *para el mismo día* (dentro de 6 días).

**Datos de prueba:**
* **Tarea 1 (Riego):** "Regar Lechugas" (Fecha: Hoy + 2 días)
* **Tarea 2 (Cosecha):** "Cosechar Rábanos" (Fecha: Hoy + 4 días)
* **Tareas 3 y 4 (Doble):** "Regar Tomates" y "Cosechar Fresas" (Fecha: Hoy + 6 días)

**Pasos:**
1. Navegar al módulo "Calendario" desde el menú principal.
2. Comprobar la presencia de la leyenda estática de colores en la pantalla.
3. Observar el día agendado para la "Tarea 1" y verificar que la celda esté resaltada en color azul.
4. Observar el día agendado para la "Tarea 2" y verificar que la celda esté resaltada en color verde.
5. Observar el día agendado para las "Tareas 3 y 4". Verificar que posea un indicador visual dual (mitad azul, mitad verde o un icono de alerta de doble carga).
6. Posicionar el cursor (*hover*) sobre el día de las "Tareas 3 y 4" sin hacer clic.
7. Hacer clic en la flecha de navegación para ir al mes siguiente, y luego hacer clic en el botón "Hoy".

**Resultado esperado:**
* La leyenda es visible y clara. 
* Los colores azul y verde se aplican estrictamente según el tipo de tarea. 
* El día con doble tarea muestra un indicador visual combinado. 
* Al hacer *hover* en el día de doble carga, se despliega un *tooltip* flotante detallando exactamente las dos acciones ("Regar Tomates en Parcela Norte" y "Cosechar Fresas en Parcela Norte").
* Al hacer clic en "Hoy", el calendario regresa instantáneamente a la vista del mes y día en curso.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar capturas de pantalla del indicador dual, el tooltip desplegado y la leyenda del calendario]


# Caso de Prueba Negativo: Flujo Alterno
## ID: TC-006
## Título: Restricción de agenda en fechas históricas y adaptación responsiva

**Objetivo:** 
Validar que el sistema impida la creación o manipulación de tareas en fechas pasadas mostrando un estado visual deshabilitado, y comprobar que la interfaz colapse correctamente a un diseño de "Agenda/Lista" en resoluciones de pantalla pequeñas.

**Precondiciones:**
* El usuario debe estar autenticado en el sistema.
* El sistema debe contar con tareas históricas finalizadas en el mes anterior.

**Datos de prueba:**
* **Fecha objetivo de prueba:** Cualquier día perteneciente al mes anterior al actual.
* **Resolución de pantalla emulada:** Dispositivo móvil (ej. iPhone 13 / Ancho <= 768px).
* **Acción simulada:** Intentar arrastrar una nueva tarea desde un panel o hacer doble clic para crear "Riego de Emergencia".

**Pasos:**
1. Ingresar al sistema desde un dispositivo móvil o utilizar las herramientas de desarrollador del navegador (F12) para emular una pantalla de teléfono celular.
2. Navegar al módulo "Calendario".
3. Verificar que la vista mensual de cuadrícula haya cambiado automáticamente a una vista vertical de "Agenda" o "Lista".
4. Utilizar la navegación para retroceder al mes calendario anterior.
5. Observar el color de los días y tareas pasadas.
6. Intentar agendar, hacer doble clic o arrastrar un nuevo evento en un día del mes pasado.

**Resultado esperado:**
* El sistema detecta el *viewport* de tamaño móvil y reemplaza la cuadrícula tradicional por una vista en lista vertical, permitiendo hacer *scroll* de manera fluida y legible sin necesidad de zoom.
* Todos los días anteriores a la fecha actual se renderizan en tonos grises o con opacidad reducida. 
* El sistema bloquea cualquier intento de interacción para crear tareas en el pasado (no se abren modales de creación, o se muestra una alerta indicando "No se pueden programar tareas en fechas anteriores"). El usuario solo puede consultar el historial en modo lectura.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar capturas de pantalla de la vista móvil "Agenda" y el intento fallido de crear un evento en un día sombreado en gris]
