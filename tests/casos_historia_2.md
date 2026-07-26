# Caso de Prueba Positivo: Flujo Normal
## ID: TC-003
## Título: Registro exitoso de nueva planta y verificación de listado

**Objetivo:** 
Validar que un administrador pueda registrar correctamente una nueva especie en el inventario utilizando datos válidos, y comprobar que el sistema proporciona la retroalimentación visual esperada y actualiza el catálogo.

**Precondiciones:**
* El usuario debe haber iniciado sesión con el rol de `Administrador`.
* El usuario debe encontrarse en la vista principal del módulo "Inventario de Plantas".
* La base de datos NO debe contener un registro previo con el nombre científico exacto que se va a ingresar.

**Datos de prueba:**
* **Nombre Común:** `Orégano Orejón`
* **Especie (Nombre Científico):** `Plectranthus amboinicus`

**Pasos:**
1. Hacer clic en el botón "Nueva Planta".
2. En el formulario desplegado, ingresar `Orégano Orejón` en el campo "Nombre Común".
3. Ingresar `Plectranthus amboinicus` en el campo "Especie (Nombre Científico)".
4. Hacer clic en el botón "Guardar".
5. Observar la esquina de la pantalla para identificar la notificación del sistema.
6. En la barra de búsqueda del listado principal, escribir `Orégano` y presionar Enter.

**Resultado esperado:**
El formulario se procesa sin errores. Inmediatamente después de guardar, el sistema muestra una notificación temporal (Toast/Alerta verde) confirmando la acción exitosa. Al buscar en el catálogo, el registro de "Orégano Orejón" aparece listado correctamente en la tabla de inventario.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar captura de pantalla del Toast verde de éxito y del listado actualizado mostrando la nueva planta]

# Caso de Prueba Negativo: Flujo Alterno
## ID: TC-004
## Título: Prevención de duplicidad de especie y rechazo por longitud excedida

**Objetivo:** 
Validar que el sistema aplique correctamente las restricciones de la base de datos y de la interfaz, impidiendo el registro de especies duplicadas y rechazando cadenas de texto que superen el límite permitido.

**Precondiciones:**
* El usuario debe haber iniciado sesión con el rol de `Administrador`.
* El usuario debe encontrarse en el formulario de "Nueva Planta".
* La base de datos DEBE contener un registro previo con la especie `Solanum lycopersicum` (Tomate).

**Datos de prueba:**
* **Intento 1 (Duplicidad):** 
  * Nombre Común: `Tomate Cherry`
  * Especie: `Solanum lycopersicum`
* **Intento 2 (Exceso de caracteres):** 
  * Nombre Común: `Esta cadena de texto es excesivamente larga y supera con creces el límite de cincuenta caracteres establecido para este campo de base de datos`
  * Especie: `Planta Test`

**Pasos:**
1. Ingresar los datos del "Intento 1" en los campos correspondientes.
2. Hacer clic en "Guardar" y observar la respuesta del sistema.
3. Limpiar los campos del formulario.
4. Ingresar los datos del "Intento 2". 
5. Hacer clic en "Guardar".

**Resultado esperado:**
* **Para el Intento 1:** El sistema bloquea el registro, no altera la base de datos y despliega exactamente la alerta visual: *"Esta especie ya se encuentra registrada"*.
* **Para el Intento 2:** El formulario no se procesa. El sistema indica que se ha superado el límite de 50 caracteres y exige corregir el campo antes de permitir el envío al servidor. 

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar captura de la alerta de especie registrada y del error de validación de longitud máxima en el campo de texto]
