# Bitácora de aprendizaje de la unidad 6


## Actividad 06

### Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?

El patrón Observer sirve para que un objeto pueda avisarle a varios otros cuando algo cambia, sin necesidad de estar directamente conectado con ellos. El problema que resuelve es el acoplamiento fuerte, pues en lugar de que el Sujeto conozca todos los detalles de cada observador , simplemente dispara una notificación y cada Observador decide cómo reaccionar. Esto hace que el sistema sea más flexible y fácil de ampliar

### Diagrama de la relación entre Subject, Observer, ofApp y Particle



<img width="850" height="594" alt="image" src="https://github.com/user-attachments/assets/292ffb29-a17d-4d40-8f36-74064886d467" />



### Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.



<img width="1059" height="580" alt="image" src="https://github.com/user-attachments/assets/9ee2abeb-e4e9-4b8a-abe8-b5db9db4911d" />






### ¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.

Usar el patrón Observer en esta aplicación trae varias ventajas. En primer lugar, reduce el acoplamiento entre las clases, ya que ofApp no necesita conocer los detalles internos de cada partícula ni recorrerlas una por una para cambiar su comportamiento; simplemente lanza una notificación y cada partícula decide qué hacer con ella. Esto también mejora la extensibilidad, porque si en el futuro quiero agregar nuevos tipos de objetos que reaccionen a los eventos, puedo hacerlo sin tener que modificar el código de ofApp. Además, el código resulta más limpio y fácil de mantener, pues cada clase se enfoca en su propia responsabilidad. Finalmente, el patrón facilita la escalabilidad, ya que un solo evento enviado desde el sujeto puede llegar automáticamente a todas las partículas, sin necesidad de escribir más lógica en el controlador principal.


