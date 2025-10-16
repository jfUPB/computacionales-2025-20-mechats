# Bitácora de aprendizaje de la unidad 7

## Actividad 01

### imagen

<img width="1919" height="1033" alt="image" src="https://github.com/user-attachments/assets/3356e517-9be8-43e0-8b85-aa0b719becbe" 


### preguntas

1. ¿por que se necesita tanto codigo solamente para generar un triangulo?

2. ¿que son los shaders?

3. ¿que parte del codigo es la que hace que cambie el tamaño de el triangulo segun el tamaño de la ventana?


### Actividad 02

Hasta donde recuerdo, descargamos tres dependencias externas (glad, glfw34 y glm-101-light), que contienen las librerías y archivos necesarios para crear un proyecto con OpenGL.

Después de descargarlas, configuramos Visual Studio para que supiera en qué carpetas buscar los archivos importantes, de modo que pudiera compilar y ejecutar correctamente los programas.

Personalmente, la que más me llamó la atención fue GLAD, porque actúa como una especie de intermediario que pasa las funciones de los drivers de la GPU al programa de OpenGL.

### Actividad 03
#### Primer experimento

Cuando modifico los parámetros de la línea

glViewport(0, 0, bufferWidth, bufferHeight);


la ventana mantiene su tamaño (lo que tiene sentido, ya que no cambiamos nada relacionado con ella), pero el triángulo cambia de tamaño proporcionalmente al valor por el que multiplico o divido bufferWidth y bufferHeight.

#### Segundo experimento

OpenGL nos proporciona herramientas para crear gráficos. El framebuffer es el espacio de memoria donde se pintan los píxeles que componen la imagen final. La GPU se encarga de renderizar estos píxeles, y el resultado se muestra en pantalla.

Me surge la curiosidad: ¿qué ocurriría si modifico la línea siguiente?

GLFWwindow* mainWindow = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "Ventana", NULL, NULL);

#### Tercer experimento

Antes de seguir, probé cambiar el número de vértices. Si es menor que tres, la figura desaparece (no se puede dibujar un polígono con menos de tres lados). Si es tres o más, se mantiene el triángulo.

Al cambiar la primitiva que se dibuja, también cambia la figura:

Si uso GL_LINES, se muestra una línea.

Si uso GL_POINTS, no aparece nada visible.

#### Cuarto experimento

¿Qué es el contexto OpenGL?
Es el entorno donde se ejecutan las operaciones gráficas, necesario para que la computadora pueda dibujar.

¿Cuál es el rol de la biblioteca GLFW y qué ventajas tiene?
GLFW facilita la creación y gestión de ventanas donde se mostrarán los gráficos, evitando tener que programar eso manualmente.

¿Por qué OpenGL necesita un contexto?
Porque sin él, no tendría un espacio donde ejecutar las órdenes gráficas (sería como un artista sin su taller).

¿Qué es el framebuffer y con qué se relaciona?
Es una zona de memoria donde se guardan los píxeles de la imagen que se va a mostrar. Me recuerda cómo en ensamblador escribíamos directamente en memoria para pintar píxeles.

¿Qué relación hay entre el viewport y el framebuffer?
El viewport define la porción visible en pantalla, mientras que el framebuffer almacena los píxeles que corresponden a esa parte.

¿Qué papel juegan los drivers y la GPU?
Los drivers contienen funciones necesarias para interactuar con la GPU, que es la encargada de procesar y dibujar los gráficos.

¿Por qué es importante activar el VSync?
Porque sincroniza los fotogramas con la tasa de refresco del monitor. Si no se activa, pueden aparecer parpadeos o desincronización visual.

¿Qué es OpenGL Legacy y en qué se diferencia del moderno?
El OpenGL Legacy usa un pipeline fijo, mientras que el moderno permite un pipeline programable, más flexible y potente.

¿Qué es el shader program y por qué es importante?
Es un conjunto de programas pequeños que transforman los vértices y determinan el color de los píxeles. Es esencial para el renderizado moderno.

¿Qué hace la función setupTriangle()? ¿Qué son VAO y VBO?
La función setupTriangle() probablemente define los vértices del triángulo, crea los buffers y asocia los datos.

El VAO (Vertex Array Object) guarda la configuración de los atributos de los vértices.

El VBO (Vertex Buffer Object) almacena los datos de los vértices en la memoria de la GPU


### Actividad 04

Diferencia entre CPU y GPU:
La CPU procesa instrucciones de forma secuencial, mientras que la GPU puede procesar muchas al mismo tiempo, lo que la hace ideal para gráficos.

Tres pasos claves del pipeline de OpenGL:

Vertex shading: Determina la posición de los objetos.

Rasterization: Colorea los objetos según su material.

Fragment shading: Aplica iluminación, sombras y otros efectos visuales.

Ventajas del pipeline programable:
Permite modificar o personalizar etapas del proceso gráfico, adaptándose a las necesidades de cada proyecto.

¿Qué es la rasterización?
Es el proceso en el que la GPU define el color de cada fragmento que compone los triángulos de la escena.

¿Qué son los fragmentos?
Son grupos de píxeles que provienen del mismo triángulo y comparten ciertas propiedades. No son lo mismo que un solo píxel.

¿Qué hace el Z-buffer y el depth test?
El depth test compara la profundidad de los objetos para determinar cuáles están más cerca de la cámara y deben mostrarse.

¿Qué es el aliasing y el anti-aliasing?
El aliasing genera bordes irregulares al representar figuras con píxeles.
El anti-aliasing suaviza estos bordes mediante cálculos matemáticos.

Relación entre iluminación y fragment shader:
El fragment shader puede calcular cómo afecta la luz a cada fragmento. Si no se usa iluminación, la escena se verá plana.

¿Qué implica tener varias fuentes de luz?
La GPU debe realizar más cálculos para cada triángulo, lo que incrementa el uso de recursos.

Resumen: cómo dibujar un triángulo en OpenGL

Definir los vértices.

Enviarlos a un buffer (VBO).

Configurar cómo se interpretan esos datos.

Usar un shader program para renderizar.

Resumen: cómo usar un shader en OpenGL
Crear un programa de shader con su ID, compilarlo, enlazarlo y activarlo antes de dibujar.


### Actividad 05

Básicamente, lo que hace el programa es obtener la posición del mouse en la ventana y dividirla entre el ancho y el alto, para que los valores estén entre 0 y 1.

Luego se ejecuta

```cpp

glUniform2f(offsetLocation, x*2 - 1, 1 - y*2);
```


Esto es necesario porque OpenGL trabaja en un sistema de coordenadas que va de -1 a 1, por lo que hay que transformar los valores del mouse para que coincidan.


### Actividad 06

El codigo lo cambie de esta manera: 

```cpp

#include <iostream>
#include <glad/glad.h>
#include <GLFW/glfw3.h>

// Callback: ajusta el viewport cuando cambie el tamaño de la ventana
void framebuffer_size_callback(GLFWwindow* window, int width, int height) {
    glViewport(0, 0, width, height);
}

// Procesa entrada simple: cierra con ESC
void processInput(GLFWwindow* window) {
    if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
        glfwSetWindowShouldClose(window, true);
}

// Tamaño de las ventanas
const unsigned int SCR_WIDTH = 400;
const unsigned int SCR_HEIGHT = 400;

// Fuentes de los shaders
const char* vertexShaderSrc = R"glsl(
    #version 460 core
    layout(location = 0) in vec3 aPos;
    void main() {
        gl_Position = vec4(aPos, 1.0);
    }
)glsl";

// Fragment shader dinámico (color cambia con el tiempo)
const char* fragmentShaderSrc = R"glsl(
    #version 460 core
    out vec4 FragColor;
    uniform float uTime;
    void main() {
        float green = (sin(uTime) / 2.0) + 0.5;
        FragColor = vec4(0.0, green, 1.0 - green, 1.0);
    }
)glsl";

// IDs globales
unsigned int VAO, VBO;
unsigned int shaderProg;

// Compila y linkea un programa de shaders, retorna su ID
unsigned int buildShaderProgram() {
    int success;
    char log[512];

    unsigned int vs = glCreateShader(GL_VERTEX_SHADER);
    glShaderSource(vs, 1, &vertexShaderSrc, nullptr);
    glCompileShader(vs);
    glGetShaderiv(vs, GL_COMPILE_STATUS, &success);
    if (!success) {
        glGetShaderInfoLog(vs, 512, nullptr, log);
        std::cerr << "ERROR VERTEX SHADER:\n" << log << "\n";
    }

    unsigned int fs = glCreateShader(GL_FRAGMENT_SHADER);
    glShaderSource(fs, 1, &fragmentShaderSrc, nullptr);
    glCompileShader(fs);
    glGetShaderiv(fs, GL_COMPILE_STATUS, &success);
    if (!success) {
        glGetShaderInfoLog(fs, 512, nullptr, log);
        std::cerr << "ERROR FRAGMENT SHADER:\n" << log << "\n";
    }

    unsigned int prog = glCreateProgram();
    glAttachShader(prog, vs);
    glAttachShader(prog, fs);
    glLinkProgram(prog);
    glGetProgramiv(prog, GL_LINK_STATUS, &success);
    if (!success) {
        glGetProgramInfoLog(prog, 512, nullptr, log);
        std::cerr << "ERROR LINKING PROGRAM:\n" << log << "\n";
    }

    glDeleteShader(vs);
    glDeleteShader(fs);
    return prog;
}

// Crea un VAO/VBO con los datos de un triángulo
void setupTriangle() {
    float vertices[] = {
        -0.5f, -0.5f, 0.0f,
         0.5f, -0.5f, 0.0f,
         0.0f,  0.5f, 0.0f
    };
    glGenVertexArrays(1, &VAO);
    glGenBuffers(1, &VBO);

    glBindVertexArray(VAO);
    glBindBuffer(GL_ARRAY_BUFFER, VBO);
    glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);
    glEnableVertexAttribArray(0);
    glBindVertexArray(0);
}

int main()
{
    // Inicializar GLFW
    if (!glfwInit()) {
        std::cerr << "Fallo al inicializar GLFW\n";
        return -1;
    }
    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 6);
    glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

    // Crear ventana
    GLFWwindow* mainWindow = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "Triangulo dinamico", nullptr, nullptr);
    if (!mainWindow) {
        std::cerr << "Error creando ventana\n";
        glfwTerminate();
        return -1;
    }

    glfwMakeContextCurrent(mainWindow);
    glfwSetFramebufferSizeCallback(mainWindow, framebuffer_size_callback);

    if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)) {
        std::cerr << "Fallo al cargar GLAD\n";
        return -1;
    }

    glfwSwapInterval(1); // V-Sync

    shaderProg = buildShaderProgram();
    setupTriangle();

    while (!glfwWindowShouldClose(mainWindow))
    {
        processInput(mainWindow);
        glClearColor(0.1f, 0.1f, 0.1f, 1.0f);
        glClear(GL_COLOR_BUFFER_BIT);

        glUseProgram(shaderProg);

        // Calcula tiempo y lo pasa al shader
        float timeValue = glfwGetTime();
        int timeLoc = glGetUniformLocation(shaderProg, "uTime");
        glUniform1f(timeLoc, timeValue);

        glBindVertexArray(VAO);
        glDrawArrays(GL_TRIANGLES, 0, 3);

        glfwSwapBuffers(mainWindow);
        glfwPollEvents();
    }

    glDeleteVertexArrays(1, &VAO);
    glDeleteBuffers(1, &VBO);
    glDeleteProgram(shaderProg);

    glfwDestroyWindow(mainWindow);
    glfwTerminate();
    return 0;
}
```

en este código se cumple el objetivo porque el color del triángulo cambia con el tiempo sin necesidad de interacción.
Se usa la función glfwGetTime() para obtener el tiempo transcurrido y se envía al fragment shader como una variable uniforme (uTime).
Dentro del shader, se usa una función sin() para modificar el valor del color verde de forma cíclica, creando un efecto pulsante

<img width="1263" height="871" alt="image" src="https://github.com/user-attachments/assets/1c780d07-d9c0-4f4f-8fed-8ffc7b97c2be" />


<img width="1014" height="737" alt="image" src="https://github.com/user-attachments/assets/6347dac0-9c19-4da2-a12a-a4a7d3685665" />


<img width="1057" height="693" alt="image" src="https://github.com/user-attachments/assets/16b184a1-2ea2-4b1c-8bd4-3ef648758984" />






   

