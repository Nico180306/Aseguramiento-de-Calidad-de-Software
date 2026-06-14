# HU-01: Login y Seguridad

* **ID:** HU-01
* **Módulo:** Seguridad
* **Prioridad:** Alta
* **Estimación:** 3 Puntos

## Descripción de la HU
Como administrador, quiero iniciar sesión con credenciales seguras (Hash) para proteger la información sensible de los huertos.

## Flujo guiado
1. El usuario ingresa a la página de inicio (Login).
2. Introduce su nombre de usuario y contraseña.
3. El sistema valida las credenciales contra la base de datos verificando el hash.
4. En caso de éxito, el sistema redirige a la vista principal correspondiente al rol. En caso de error, muestra un mensaje de advertencia.

## Criterios de aceptación
* **Encriptación:** Las contraseñas deben estar encriptadas en la BDD usando un algoritmo seguro (ej. BCrypt o el nativo de .NET Identity).
* **Bloqueo de seguridad:** Tras 3 intentos fallidos consecutivos, la cuenta debe bloquearse temporalmente por 15 minutos.
* **Mensajes de error:** Por motivos de seguridad, el error debe ser genérico: *"Usuario o contraseña incorrectos"*, sin especificar cuál de los dos falló.
* **Redirección por Rol:** Si es Administrador va a la vista de gestión global; si es Usuario/Voluntario, va al calendario de su huerto.
