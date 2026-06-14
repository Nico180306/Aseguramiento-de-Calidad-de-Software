# HU-07: Reportes PDF Mensuales

* **ID:** HU-07
* **Módulo:** Backend / Reporting
* **Prioridad:** Baja
* **Estimación:** 5 Puntos

## Descripción de la HU
Como administrador, quiero descargar reportes en PDF con el resumen mensual para presentarlos a la comunidad y documentar el avance operativo del huerto.

## Flujo guiado
1. El administrador navega al módulo de "Reportes".
2. Selecciona el rango de fechas a evaluar (por defecto, el mes en curso) y pulsa el botón "Generar Reporte".
3. El sistema compila la información de la base de datos y renderiza la vista en formato documento.
4. El navegador del usuario inicia la descarga automática del archivo `.pdf`.

## Criterios de aceptación
* **Formato Institucional:** El documento PDF generado debe contar con un encabezado estándar que incluya el logotipo del proyecto, la fecha y hora de generación, y el nombre del administrador que lo solicitó.
* **Paginación y Estructura:** El reporte debe tener márgenes adecuados para impresión física (A4), mostrando una tabla resumen de cosechas y riegos del mes. Si los registros exceden una página, los encabezados de la tabla deben repetirse automáticamente al inicio de cada hoja nueva.
* **Nomenclatura del Archivo:** El archivo descargado debe generarse con un nombre semántico y dinámico para facilitar el orden en el equipo del usuario (ej. `Reporte_Huerto_Mayo2026.pdf`).
* **Feedback de Carga (UX):** Dado que la compilación de datos y renderizado del PDF puede demorar, al hacer clic en "Generar", el botón debe cambiar a un estado visual de "Procesando..." (deshabilitándose temporalmente) para evitar que el usuario haga múltiples clics y sature el servidor. El tiempo total de descarga no debe exceder los 5 segundos.
* **Autorización Estricta:** El endpoint o controlador encargado de compilar el reporte debe estar protegido a nivel de código (`[Authorize(Roles = "Administrador")]`). Si un usuario con rol de "Voluntario" intenta forzar la URL de descarga, el sistema bloqueará la acción devolviendo un error de acceso denegado.
