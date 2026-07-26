# Caso de Prueba Positivo: Flujo Normal
## ID: TC-009
## Título: Consulta exitosa de consejo específico y validación de caché (Rendimiento)

**Objetivo:** 
Validar que el microservicio devuelva correctamente un consejo técnico estructurado en JSON cruzando la "Especie" y la "Etapa", y comprobar que las solicitudes repetidas se sirven desde la caché temporal en menos de 1 segundo.

**Precondiciones:**
* El usuario debe estar autenticado y tener acceso a la vista de detalles de una parcela.
* El microservicio de consejos debe estar en ejecución y accesible.
* La base de datos debe contener un consejo específico redactado para la especie y etapa seleccionadas.
* Las herramientas de desarrollador (F12 - pestaña de Red/Network) del navegador deben estar abiertas para medir tiempos y revisar el payload JSON.

**Datos de prueba:**
* **Especie:** `Zanahoria`
* **Etapa:** `Crecimiento`
* **Respuesta JSON esperada:** `{"especie": "Zanahoria", "etapa": "Crecimiento", "consejo": "Mantener suelo suelto y riego profundo para evitar deformación de la raíz.", "status": 200}`

**Pasos:**
1. Navegar a la vista de detalle de la planta "Zanahoria".
2. Seleccionar la etapa de "Crecimiento" en el menú desplegable de la interfaz.
3. Observar en la pestaña de "Red" de las herramientas de desarrollador la petición al endpoint `GET /api/consejos/Zanahoria/Crecimiento`.
4. Verificar en pantalla que el consejo específico se muestre correctamente.
5. Recargar la página o volver a seleccionar la misma etapa para forzar una segunda petición idéntica.
6. Revisar el tiempo de respuesta de esta segunda petición en la pestaña de "Red".

**Resultado esperado:**
La primera petición retorna el JSON estructurado correctamente y el texto se inyecta en la vista del usuario. En la segunda petición, el microservicio intercepta la llamada y responde utilizando la caché temporal, reflejando un tiempo de respuesta de red consistentemente inferior a 1 segundo (ej. 20ms - 50ms), optimizando el rendimiento general.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar captura de pantalla de la pestaña Network mostrando el JSON devuelto y el tiempo de respuesta (Time < 1s) para validar la caché]

# Caso de Prueba Negativo: Flujo Alterno
## ID: TC-010
## Título: Manejo de datos nulos y tolerancia a caídas del microservicio (Resiliencia)

**Objetivo:** 
Validar el comportamiento del sistema ante condiciones adversas: primero, cuando se consultan variables sin consejo redactado en la base de datos (fallback genérico), y segundo, cuando el microservicio experimenta una caída total o lentitud severa (resiliencia de la interfaz principal).

**Precondiciones:**
* El usuario debe estar autenticado en el sistema.
* La base de datos NO debe tener consejos redactados para la especie "Espinaca" en la etapa "Producción".
* Se debe utilizar un bloqueador de peticiones (ej. herramientas de red del navegador o un software intermediario) para simular la caída del microservicio.

**Datos de prueba:**
* **Caso Nulo:** Especie: `Espinaca`, Etapa: `Producción`.
* **Caso Caída:** Endpoint `GET /api/consejos/*` bloqueado o forzando un error `500 Internal Server Error`.

**Pasos:**
1. Navegar a la vista de detalle de la planta "Espinaca".
2. Seleccionar la etapa de "Producción".
3. Validar el mensaje desplegado en la sección de consejos.
4. Utilizando las herramientas de desarrollador (F12), aplicar una regla para bloquear la URL del microservicio (`/api/consejos/*`) o establecer el estrangulamiento de red (*throttling*) a modo "Offline".
5. Refrescar la vista principal de la planta "Espinaca" u otra del inventario.
6. Observar el comportamiento de renderizado de la página principal (datos de la planta, humedad, botones de acción) y el contenedor de consejos.

**Resultado esperado:**
* **Para el paso 3:** El sistema captura correctamente la ausencia de datos en la BDD y, en lugar de mostrar un error de servidor, retorna de manera silenciosa el mensaje genérico por defecto: *"Asegure riego moderado y luz adecuada"*.
* **Para los pasos 5 y 6:** Ante la caída simulada del microservicio, la página de detalles de la planta debe renderizarse de forma fluida y normal. La interfaz no debe bloquearse ni mostrar un error 500 ("Pantalla de la muerte"). La sección de "Consejos" debe ocultarse por completo de la vista de forma elegante o mostrar un indicador de "Servicio no disponible temporalmente", aislando el fallo y garantizando que la experiencia del usuario principal permanezca intacta.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar captura del mensaje genérico de fallback y captura de la vista principal cargando exitosamente a pesar de que la petición al API marque estado rojo/fallido en la consola]
