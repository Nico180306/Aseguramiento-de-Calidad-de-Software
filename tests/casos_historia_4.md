# Caso de Prueba Positivo: Flujo Normal
## ID: TC-007
## Título: Carga asíncrona exitosa, centrado en Quito y despliegue de Info Window

**Objetivo:** 
Validar que el mapa se inicialice correctamente centrado en Quito (zoom 14), que la carga de los marcadores se realice de forma asíncrona sin congelar la interfaz, y que el popup emergente muestre la información exacta de la parcela con su enlace de redirección.

**Precondiciones:**
* El usuario debe haber iniciado sesión exitosamente en el sistema.
* Deben existir al menos dos parcelas activas registradas en la base de datos con coordenadas geográficas válidas en la ciudad de Quito.
* La API del proveedor de mapas (ej. Mapbox o Google Maps) debe estar operativa y con la clave de acceso (API Key) vigente.

**Datos de prueba:**
* **Parcela Objetivo:** `Huerto Comunitario La Carolina`
* **Responsable asignado:** `Laura Mendoza`
* **Coordenadas:** Latitud `-0.1807`, Longitud `-78.4678` (Quito).

**Pasos:**
1. Hacer clic en la opción "Mapa de Parcelas" en el menú principal de navegación.
2. Observar el comportamiento de la página durante el primer segundo (verificar si el menú y el *header* responden mientras el mapa se dibuja).
3. Confirmar que la vista inicial del mapa abarca la ciudad de Quito.
4. Identificar el marcador correspondiente a las coordenadas del "Huerto Comunitario La Carolina" y hacer clic sobre él.
5. Leer la información desplegada en el *popup* (Info Window).
6. Hacer clic en el botón o enlace "Ver Detalle" que se encuentra dentro del popup.

**Resultado esperado:**
La navegación hacia la vista es fluida gracias a la petición asíncrona. El mapa se centra en Quito automáticamente en nivel de zoom 14. Al hacer clic en el marcador objetivo, se abre un popup que muestra los textos: "Huerto Comunitario La Carolina" y "Responsable: Laura Mendoza". Al hacer clic en "Ver Detalle", el sistema abandona el mapa y redirige de manera exitosa a la vista de inventario específica de esa parcela.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar capturas de pantalla del mapa centrado en Quito y del Info Window desplegado con el botón "Ver Detalle"]

# Caso de Prueba Negativo: Flujo Alterno
## ID: TC-008
## Título: Manejo amigable de errores por timeout o caída del proveedor de mapas

**Objetivo:** 
Validar que el sistema aplique un mecanismo de tolerancia a fallos (*fallback*) cuando el servicio externo de mapas o el endpoint de coordenadas dejen de responder, asegurando que la aplicación no sufra una excepción crítica que bloquee la navegación del usuario.

**Precondiciones:**
* El usuario debe estar autenticado en el sistema.
* Se debe utilizar la consola de herramientas de desarrollador del navegador (F12) o un software de intercepción de tráfico (ej. Postman/Fiddler) para bloquear temporalmente las peticiones de red hacia el proveedor de mapas.

**Datos de prueba:**
* **Condición simulada:** Simular estado "Offline" en la pestaña de red del navegador o bloquear el dominio de la API de mapas (ej. `api.mapbox.com` o `maps.googleapis.com` forzando un error 500 o Timeout).

**Pasos:**
1. Abrir las herramientas de desarrollador del navegador (F12) y habilitar el bloqueo de peticiones de red para la API del mapa.
2. Navegar a la sección "Mapa de Parcelas" utilizando el menú lateral del sistema.
3. Esperar a que se cumpla el tiempo máximo de respuesta (*timeout*).
4. Observar la reacción de la interfaz general (menú, encabezado, pie de página).
5. Observar el contenedor específico donde debería cargarse el lienzo del mapa.
6. Intentar hacer clic en otro módulo del menú (ej. "Inventario de Plantas") para comprobar si la plataforma sigue interactiva.

**Resultado esperado:**
La página no debe colapsar ni mostrar pantallas blancas o rastros de código de error de servidor (ej. Error 500 YSOD). El sistema captura la excepción de red de manera controlada y despliega dentro del contenedor del mapa un recuadro amigable con un mensaje similar a: *"Servicio de mapas temporalmente inactivo. Por favor, intente más tarde"*. El menú de navegación se mantiene 100% operativo, permitiendo al usuario salir de la pantalla sin problemas.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar captura de pantalla del mensaje amigable de error y de las peticiones fallidas simuladas en la consola de red]
