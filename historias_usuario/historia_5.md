# HU-05: Microservicio de Consejos

* **ID:** HU-05
* **Módulo:** Backend / Lógica
* **Prioridad:** Media
* **Estimación:** 5 Puntos

## Descripción de la HU
Como usuario inexperto, quiero recibir consejos automáticos sobre el cuidado de cada planta para evitar errores en el cultivo y mejorar la producción.

## Flujo guiado
1. El usuario accede al detalle de una planta específica en su parcela.
2. Selecciona la etapa de crecimiento actual.
3. El sistema consulta el microservicio y retorna en pantalla un consejo agronómico útil.

## Criterios de aceptación
* **Contrato de Interfaz (API):** El servicio debe exponer un endpoint (ej. `GET /api/consejos/{especie}/{etapa}`) que retorne la recomendación estructurada en formato estándar JSON.
* **Lógica de Negocio:** El sistema debe devolver un texto distinto y específico cruzando obligatoriamente dos variables: la Especie (ej. Tomate) y la Etapa (Siembra, Crecimiento, Cosecha).
* **Manejo de Casos Nulos:** Si se consulta una especie o etapa que aún no tiene consejos redactados en la base de datos, el servicio debe retornar un mensaje genérico por defecto (ej. *"Asegure riego moderado y luz adecuada"*), evitando generar errores técnicos (excepciones 500) en pantalla.
* **Rendimiento y Caché:** Dado que los consejos agronómicos son información estática que no cambia diariamente, el sistema debe implementar una política de caché temporal para garantizar que el tiempo de respuesta del servicio sea consistentemente inferior a 1 segundo y así reducir consultas repetitivas a la base de datos.
* **Tolerancia a Fallos (Resiliencia):** Si este microservicio específico experimenta una caída o lentitud severa, la vista principal del inventario de la planta debe seguir cargando con normalidad, simplemente ocultando la sección de "Consejos", para no bloquear la experiencia del usuario.
