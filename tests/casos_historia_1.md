# Caso de Prueba Positivo: Flujo Normal
## ID: TC-001
## Título: Autenticación exitosa de cuenta Administrador y redirección de rol

**Objetivo:** 
Validar que un usuario con privilegios de Administrador pueda acceder al sistema ingresando credenciales válidas (cuya contraseña está encriptada en la base de datos) y sea redirigido a la vista de gestión que le corresponde según su rol.

**Precondiciones:**
* El usuario debe existir en la base de datos con el rol de `Administrador` asignado.
* La contraseña del usuario debe estar almacenada mediante un algoritmo de Hash seguro (ej. BCrypt).
* El sistema debe encontrarse en la pantalla inicial de Login (`/Login`).
* El usuario no debe tener bloqueos activos en su cuenta.

**Datos de prueba:**
* **Usuario (Correo):** `admin_huertos_norte@huertos.com`
* **Contraseña:** `P@ssw0rd_Global2026!`

**Pasos:**
1. Ingresar a la URL del portal del Huerto Comunitario.
2. Hacer clic o enfocar el campo de "Usuario/Correo electrónico".
3. Digitar el usuario: `admin_huertos_norte@huertos.com`.
4. Hacer clic o enfocar el campo de "Contraseña".
5. Digitar la contraseña: `P@ssw0rd_Global2026!`.
6. Presionar el botón "Iniciar Sesión" o la tecla Enter.

**Resultado esperado:**
El sistema procesa la solicitud, verifica exitosamente el hash de la contraseña en la base de datos y concede el acceso. El usuario es redirigido automáticamente a la "Vista de gestión global", sin mostrar vistas destinadas a Voluntarios.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar capturas de pantalla de la base de datos mostrando el hash y del Dashboard de gestión global tras el login]

# Caso de Prueba Negativo: Flujo Alterno
## ID: TC-002
## Título: Bloqueo temporal de cuenta por fuerza bruta y ocultamiento de fallos

**Objetivo:** 
Validar que el sistema aplique la política de seguridad de bloqueo de cuenta (15 minutos) al registrar 3 intentos fallidos consecutivos, y comprobar que en todo momento se mantenga un mensaje de error genérico para prevenir ataques de enumeración de usuarios.

**Precondiciones:**
* El usuario de prueba debe existir en la base de datos y tener estado "Activo" (sin bloqueos previos).
* El sistema debe encontrarse en la pantalla inicial de Login (`/Login`).

**Datos de prueba:**
* **Usuario (Correo válido):** `voluntario_zona_sur@huertos.com`
* **Contraseña 1 (Inválida):** `ClaveEquivocada1`
* **Contraseña 2 (Inválida):** `ClaveEquivocada2`
* **Contraseña 3 (Inválida):** `ClaveEquivocada3`
* **Contraseña 4 (Válida):** `ClaveVoluntario2026*`

**Pasos:**
1. Ingresar al formulario de Login.
2. Ingresar el usuario `voluntario_zona_sur@huertos.com` y la Contraseña 1. Clic en "Iniciar Sesión".
3. Observar el mensaje de error devuelto por el sistema.
4. Repetir el paso 2 utilizando la Contraseña 2 y luego la Contraseña 3.
5. Inmediatamente después del tercer intento fallido, ingresar el usuario `voluntario_zona_sur@huertos.com` y su Contraseña 4 (la cual es la correcta).
6. Clic en "Iniciar Sesión".

**Resultado esperado:**
* En los intentos 1, 2 y 3: El sistema debe denegar el acceso y mostrar ESTRICTAMENTE el mensaje genérico: *"Usuario o contraseña incorrectos"*. No debe revelar si el error fue en el correo o en la clave.
* En el intento 4 (a pesar de ingresar la clave correcta): El sistema debe rechazar el inicio de sesión y mostrar una alerta visual indicando que la cuenta se encuentra bloqueada temporalmente por 15 minutos por motivos de seguridad.

**Resultado obtenido:** 
[Espacio para completar tras la ejecución]

**Estado:** 
Pendiente

**Notas/Evidencias:**
[Adjuntar capturas del mensaje de error genérico en el intento 1 y del mensaje de cuenta bloqueada en el intento 4]
