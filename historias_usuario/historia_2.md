# HU-02: CRUD Plantas e Inventario

* **ID:** HU-02
* **Módulo:** Base de Datos / Inventario
* **Prioridad:** Alta
* **Estimación:** 8 Puntos

## Descripción de la HU
Como administrador, quiero registrar, editar y listar las plantas disponibles para mantener un inventario digital actualizado.

## Flujo guiado
1. El administrador accede al módulo de "Inventario de Plantas".
2. Selecciona la opción "Nueva Planta" o el icono de edición sobre un registro existente.
3. Completa o modifica el formulario con los datos requeridos.
4. Hace clic en "Guardar" y visualiza el catálogo actualizado.

## Criterios de aceptación
* **Validaciones obligatorias:** Los campos "Nombre Común" y "Especie (Nombre Científico)" deben ser requeridos. El formulario no debe procesar la solicitud si estos están vacíos o exceden los 50 caracteres.
* **Control de duplicidad:** El sistema debe verificar en la base de datos que no se ingrese una planta con el mismo "Nombre Científico" ya existente; de ser así, mostrará la alerta: *"Esta especie ya se encuentra registrada"*.
* **Listado y paginación:** La tabla principal del inventario debe mostrar un máximo de 10 registros por página e incluir una barra de búsqueda funcional por nombre de planta.
* **Borrado Lógico (Soft Delete):** La acción de "Eliminar" no debe borrar el registro de la base de datos relacional para no romper la integridad de datos históricos. En su lugar, debe cambiar el estado del registro a "Inactivo" u "Oculto".
* **Retroalimentación de la interfaz:** Al completarse cualquier acción de crear, editar o eliminar lógicamente, el sistema mostrará una notificación temporal (Toast/Alerta verde) confirmando la acción exitosa.
