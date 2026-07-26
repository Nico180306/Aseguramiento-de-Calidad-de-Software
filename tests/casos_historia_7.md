# Caso de Prueba Positivo: Flujo Normal
## ID: TC-013
## Título: Generación exitosa del PDF, formato institucional y validación de tiempo de respuesta

**Objetivo:** 
Validar que un usuario con rol de Administrador pueda generar y descargar el reporte mensual, comprobando que el archivo contenga la nomenclatura dinámica correcta, aplique el formato institucional (encabezados repetidos, paginación A4, logotipo) y que la descarga inicie en menos de 5 segundos.

**Precondiciones:**
* El usuario debe estar autenticado con el rol de `Administrador`.
* La base de datos debe contener un volumen de registros de riegos y cosechas en el mes seleccionado lo suficientemente grande como para ocupar más de una página física (ej. > 40 registros).
* El módulo de generación de PDFs debe estar correctamente configurado en el servidor.

**Datos de prueba:**
* **Mes a evaluar:** Rango correspondiente a `Julio 2026`.
* **Nombre de Administrador activo:** `Nicolás S.`
* **Nombre de archivo esperado:** `Reporte_Huerto_Julio2026.pdf`

**Pasos:**
1. Navegar al módulo de "Reportes" desde el menú principal.
2. Seleccionar el rango de fechas correspondientes al mes de Julio de 2026.
3. Hacer clic en el botón "Generar Reporte".
4. Observar el cambio de estado del botón y cronometrar el tiempo desde el clic hasta que el navegador lanza la alerta de descarga.
5. Abrir el archivo `.pdf` descargado utilizando un lector de PDFs o el propio navegador.
6. Revisar el encabezado de la primera página y hacer *scroll* hacia la segunda página.

**Resultado esperado:**
* Al hacer clic, el botón cambia inmediatamente a "Procesando..." y se deshabilita, impidiendo más clics.
* La descarga del archivo inicia antes de transcurrir 5 segundos.
* El archivo se nombra dinámicamente como `Reporte_Huerto_Julio2026.pdf`.
* El documento tiene tamaño A4. En la parte superior de la primera hoja aparece el logotipo del proyecto, la fecha/hora de generación y el nombre "Nicolás S.".
* Al pasar a la segunda página, los encabezados de la tabla resumen de cosechas y riegos se repiten automáticamente para mantener la legibilidad de los datos.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar captura de pantalla del botón en estado "Procesando..." y el archivo PDF generado abierto mostrando la segunda página con los encabezados repetidos]

# Caso de Prueba Negativo: Flujo Alterno
## ID: TC-014
## Título: Seguridad de endpoint (Role-Based) y prevención de saturación del servidor

**Objetivo:** 
Validar que el controlador backend aplique estrictamente la etiqueta de autorización (`[Authorize(Roles = "Administrador")]`), impidiendo que usuarios sin privilegios fuercen la generación del PDF mediante manipulación de URLs, y asegurar que el frontend bloquee envíos múltiples.

**Precondiciones:**
* El sistema debe tener dos cuentas de prueba habilitadas: un `Administrador` y un `Voluntario`.
* Se debe conocer la URL exacta del endpoint que compila el PDF (ej. `https://dominio.com/api/Reportes/GenerarMesActual`).

**Datos de prueba:**
* **Usuario No Autorizado:** Cuenta con rol `Voluntario`.
* **Endpoint de prueba:** `/api/Reportes/GenerarMesActual` (o la ruta correspondiente en el proyecto).

**Pasos:**
1. Iniciar sesión con la cuenta de `Administrador`.
2. Navegar al módulo de Reportes y hacer clic repetidamente y muy rápido (doble o triple clic) en el botón "Generar Reporte".
3. Cerrar sesión (`Logout`).
4. Iniciar sesión con la cuenta de `Voluntario`.
5. Comprobar que el módulo de "Reportes" no sea visible en el menú.
6. Abrir la barra de direcciones del navegador, pegar la URL directa del endpoint del reporte (`/api/Reportes/GenerarMesActual`) y presionar Enter.

**Resultado esperado:**
* **Para el paso 2:** El sistema frontend intercepta el primer clic y desactiva instantáneamente el botón, previniendo que el doble o triple clic sature el backend con múltiples solicitudes de renderizado de PDF al mismo tiempo.
* **Para el paso 6:** Aunque el usuario `Voluntario` descubra la ruta directa del backend, el sistema verifica sus *claims* de seguridad y bloquea la ejecución del código. El sistema retorna un error HTTP 403 (Forbidden) o redirige a una vista de "Acceso Denegado", sin compilar ni descargar ningún archivo PDF.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar captura de pantalla mostrando la consola de red (Network) con el error 403 o la pantalla de Acceso Denegado al intentar vulnerar la URL]
