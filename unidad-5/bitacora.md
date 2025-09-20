# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**


#### ¿Que es el encapsulamiento para mi?

Si mal no estoy, es una manera de hacer que el codigo no sea accesible para todo el mundo, es como una forma de protegerlo. Como tal no me ha servido en ningun ejemplo practico, pero si se que es muy util en aplicaciones que piden contraseñas, porque la contraseña queda guardada en el programa pero no se puede ver en otras clases

#### ¿Que es la herencia?

La herencia es una forma de copiar los atributos y metodos de una clase para ponerlos en otra, existen varios tipos de herencia, hay uno en el que no se pueden modificar los metodos ni los atributos desde la clase que hereda, otra que si se pueden modificar.

La herencia es muy util a la hora de resumir codigo, y no solo eso, si no de simplificar el proceso de codificacion a la hora de hacer que una clase implemente varios metodos diferentes, por ejemplo tenemos la clase avión o medio de transporte aereo, esta cuenta con metodos como despegar, volar, aterrizar. Ahora tenemos otras clases diferentes (helicoptero, avioneta, globo aereostatico) lo logico seria que estas subclases heredaran los metodos de la clase medio de transporte aereo

#### ¿Que es el polimorfismo?

La verdad no tengo el concepto claro, a mi el polimorfismo me suena a un codigo que puede ser independiente por si solo y se puede ensamblar en otra parte y ademas es modificable, por ejemplo, tenemos un programa que administra un lavadero de carros, pasa el timepo y el lavadero ahora tiene una nueva sucursal. El codigo deberia ser posible modificarlo para que se le añadan nuevas clases o metodos en funcion a la nueva sede

#### Señala una línea de código que sea un ejemplo claro de encapsulamiento y explica por qué lo es.

Pienso que aqui hay un encapsulamiento
```csharp
  protected set { nombre = value; }
```
se esta protegiendo el private string  nombre, aunque no tengo muy claro para que sirve pienso que puede funcionar para que el nombre nos ea modificable en otra parte del codigo

#### ¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?

Se evita que las clases hijas accedan directamente a nombre, y usando 

```csharp
 this.Nombre = nombre;
```

se hace que Nombre, que esta publico, adquiera ell valor de nombre que esta protegido por un get set (suposicion)

#### ¿Cómo se evidencia la herencia en la clase Circulo?

no lo tengo muy claro

#### Un objeto de tipo Circulo, además de Radio, ¿Qué otros datos almacena en su interior gracias a la herencia?

el nombre

#### Observa el bucle foreach. La variable fig es de tipo Figura, pero a veces contiene un Circulo y otras un Rectangulo. Cuando se llama a fig.Dibujar(), el programa ejecuta la versión correcta. En tu opinión, ¿Cómo crees que funciona esto “por debajo”? No necesitas saber la respuesta correcta, solo quiero que intentes razonar cómo podría ser.

En el foreach fig está declarado como Figura, pero  puede guardar un Circulo o un Rectangulo, no se muy bien como funcione pero siento que cuando llamo a fig.Dibujar(), mágicamente se ejecuta la versión correcta
Yo me lo imagino como si el objeto tuviera una especie de “etiqueta oculta” que dice qué tipo real es

#### Memoria y herencia: cuando creas un objeto Rectangulo, este tiene Base, Altura y también Nombre. ¿Cómo te imaginas que se organizan esos tres datos en la memoria del computador para formar un solo objeto?

Si creo un Rectangulo, en memoria se deberían guardar todos los datos juntos: primero la parte que corresponde a Figura (el Nombre), y después lo que es exclusivo de Rectangulo (Base y Altura) Me lo imagino como un bloque de memoria dividido en secciones, la primera guarda nombre y la otra los datos especificos de la figura


#### El mecanismo del polimorfismo: pensemos de nuevo en la llamada fig.Dibujar(). El compilador solo sabe que fig es una Figura. ¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo? Lanza algunas ideas o hipótesis.

creo que el programa mantiene una especie de tabla de métodos que dice: si es Círculo, usa esta función; si es Rectángulo, usa esta otra. Entonces cuando escribo fig.Dibujar() el compilador no decide en ese momento, sino que en ejecución el objeto consulta su tabla y escoge la función correcta

#### La barrera del encapsulamiento: ¿Cómo crees que el compilador logra que no puedas acceder a un miembro private desde fuera de la clase? ¿Es algo que se revisa cuando escribes el código, o es una protección que existe mientras el programa se ejecuta? ¿Por qué piensas eso?

pienso que la restricción de private la revisa principalmente el compilador, o sea, cuando escribo código y trato de acceder a algo privado, el compilador me bloquea y me diceesto no es permitido. Ya en la ejecución, seguramente el objeto sí tiene esos datos en memoria, pero el compilador se asegura de que yo nunca pueda escribir código que los toque directamente

#### Autoevaluacion y primeras preguntas

Me di cuenta que los conceptos que mas claros tengo o mejor dicho que menos peor tengo aprendidos son la herencia y el encapsulamiento, por otro lado el polimorfismo es un tema que la verdad no manejo completamente, siento que tengo una idea base pero no esta del todo desarrollada ni mucho menos certera







## 2.  Al final de esta unidad me gustaria saber... ¿Como funciona el polimorfismo durante la compilación y durante la ejecución?

## 3.  **Registro de exploración:** 

### En que consiste el programa

Este código es un sistema de partículas orientado a objetos que simula fuegos artificiales. Primero aparecen partículas que suben como cohetes y luego explotan en diferentes formas. Cada partícula es un objeto que tiene su posición, velocidad y tiempo de vida, y gracias a la herencia y al polimorfismo, el programa puede manejar diferentes tipos de partículas dentro de la misma estructura. El encapsulamiento protege esos datos y asegura que el programa solo las manipule de manera controlada, es como si el programa organizara a todas las partículas como familias que comparten un mismo apellido (Particle), pero cada una tiene su estilo propio (círculos, cuadrados, estrellas).



#### ¿Cómo maneja la aplicación el ciclo de vida de las partículas desde que nacen hasta que explotan y desaparecen?

##### Hipotesis
El sistema crea partículas ascendentes  que al llegar a cierta altura o superar su tiempo de vida explotan, generando nuevas partículas de distinto tipo (círculos, cuadrados o estrellas), las cuales cumplen un ciclo de vida por asi decirlo y desaparecen de la pantalla

##### Experimentación

<img width="1017" height="762" alt="image" src="https://github.com/user-attachments/assets/f99f5cfe-15c4-4350-ae87-1e477930588b" />



<img width="1015" height="759" alt="image" src="https://github.com/user-attachments/assets/27c99edb-9c71-4274-a22a-d05abac7b665" />


##### Hallazgos

El código implementa un sistema de partículas jerárquico,primero aparecen partículas ascendentes que se mueven hacia arriba, desaceleran y al llegar a cierta altura o edad se marcan como explosionadas. Cuando una partícula explota, se reemplaza por un conjunto de nuevas partículas con comportamientos visuales distintos: explosión circular (círculos que salen en todas direcciones), explosión aleatoria (cuadrados dispersos en direcciones random) y explosión en estrella (líneas que simulan rayos).

#### ¿De qué manera el polimorfismo permite que diferentes tipos de partículas (ascendentes y explosivas) compartan una misma interfaz de uso en el programa, y qué tan difícil sería escalar el sistema si no existiera polimorfismo?

##### Hipotesis

El polimorfismo en  permite que todas las partículas se manejen a través de un mismo puntero o referencia a la clase base. Osea que el programa puede almacenar en un mismo vector partículas ascendentes y de explosión, aunque cada una tenga comportamientos distintos. Si no existiera polimorfismo, habría que crear vectores separados o condicionales para cada tipo de partícula, lo cual haría el código más complejo, rígido y difícil de escalar.

##### Experimentación

Para validar cómo funciona el polimorfismo en el sistema de partículas, decidí usar breakpoints. La idea era comprobar si, al crear un objeto a través de un puntero de tipo Particle*, el programa realmente reconoce en tiempo de ejecución que se trata de una instancia de una clase hija como RisingParticle.

<img width="1893" height="277" alt="image" src="https://github.com/user-attachments/assets/0adc7217-b1a5-4531-9548-97daf6337888" />


en la captura se observa la ventana de variables locales de visual studio durante la ejecucion en modo debug se puede ver el puntero this apuntando a un objeto del tipo risingparticle y no simplemente a particle lo que confirma que el polimorfismo esta funcionando ademas se muestran los valores iniciales de sus atributos como posicion velocidad y color que fueron asignados al momento de crear la particula esto evidencia que aunque el programa maneja todas las particulas con un puntero generico en realidad reconoce en tiempo de ejecucion el tipo especifico del objeto

### Actividad 03

##### Hipotesis

antes de ejecutar el experimento espero ver que el objeto ofapp aparece en memoria con su vector de partículas y sus métodos asociados. en el caso de un objeto circularexplosion espero ver reflejada la jerarquía completa, es decir, primero los atributos heredados de particle, luego los de explosionparticle, y finalmente los propios de circularexplosion. también espero encontrar un puntero llamado _vptr que apunte a una tabla de funciones virtuales, donde se almacenan las direcciones de los métodos virtuales redefinidos por cada clase. mi hipótesis es que esta tabla cambia dependiendo del tipo exacto del objeto instanciado, aunque se use un puntero a la clase base.

##### Experimentacion

<img width="1903" height="322" alt="image" src="https://github.com/user-attachments/assets/8e7c9e96-b3dc-4253-bb45-b182752fe2d8" />

puedo observar que en memoria existe una instancia de la clase ofapp con su referencia this apuntando al objeto actual y que contiene tanto los atributos heredados de ofbaseapp como el vector particles, el depurador me proporciona la información sobre la estructura interna del objeto, sus miembros y la pila de llamadas que llevó a la ejecución, puedo concluir que un objeto en c++ no es abstracto sino una organización concreta en memoria que refleja la herencia, la composición y permite ver en qué estado está durante la ejecución

<img width="883" height="137" alt="image" src="https://github.com/user-attachments/assets/e4ab69f4-cb3f-4a2a-ad39-4bf09cca32fd" />


lo que se observa es una lista de direcciones en memoria, cada una corresponde a un puntero a funcion. esas entradas son la tabla de metodos virtuales del objeto. el depurador muestra que algunas de esas direcciones apuntan a metodos definidos en starexplosion (como su constructor, destructor o draw) y otras se mantienen heredadas desde explosionparticle o particle


<img width="868" height="111" alt="image" src="https://github.com/user-attachments/assets/85fba06b-89e5-4fbd-9c7a-64790335dff1" />

lo que puedo ver es que las dos tablas muestran direcciones diferentes en algunas entradas pero mantienen otras iguales eso me hace pensar que ciertas funciones son redefinidas en la clase derivada mientras que otras se heredan directamente sin cambio la conclusion es que la tabla de funciones virtuales guarda las referencias a los metodos que corresponden al tipo real del objeto y no al tipo declarado asi cuando el programa llama a un metodo virtual puede ejecutar la version correcta segun la clase que se este usando la relacion entre la tabla y los metodos virtuales es que cada entrada apunta a la direccion de la funcion que corresponde al metodo virtual ya sea heredado o sobreescrito una tabla de funciones virtuales sirve para que el compilador y el sistema sepan a que metodo llamar en tiempo de ejecucion esto es lo que permite el polimorfismo igual que en c# cuando usas interfaces o clases abstractas y puedes llamar a un metodo desde una referencia generica pero se ejecuta la version especifica de la clase real

##### Hallazgos

en memoria el objeto no es algo abstracto sino que tiene una estructura muy concreta formada por los atributos heredados y los propios de la clase tambien que el depurador permite ver como se refleja la jerarquia completa mostrando que un objeto puede contener tanto los elementos de su clase base como los de la clase derivada ademas confirme que existe un puntero especial llamado vfptr que apunta a la tabla de funciones virtuales y que esta tabla cambia segun el tipo real del objeto aunque se use un puntero de la clase base esto demuestra como se implementa el polimorfismo en c++ ya que gracias a esa tabla el sistema sabe que metodo ejecutar en tiempo de ejecucion segun la clase concreta por ultimo aprendi que el mecanismo es muy parecido a lo que pasa en c# cuando usamos interfaces o clases abstractas y podemos llamar metodos desde una referencia generica pero se ejecuta la version especifica del objeto real

##### Nota que el método HacerSonido se llama dos veces, una vez para el perro y otra vez para el gato. ¿Cómo se logra esto? ¿Qué relación existe entre los métodos virtuales y el polimorfismo? Al llamar HacerSonido cómo sabe esta función sobre cuál objeto debe actuar?


esto se logra porque en c# cuando una clase implementa una interfaz el compilador genera una tabla interna similar a la de funciones virtuales que vimos en c++ esa tabla guarda a que direccion de codigo debe ir cuando se invoque el metodo definido en la interfaz en este caso hacersonido por eso cuando recorres el arreglo de tipo ianimal y llamas animal.hacersonido el runtime busca en esa tabla del objeto concreto si es un perro o un gato y ejecuta la version que corresponde la relacion entre metodos virtuales y polimorfismo es directa porque el polimorfismo necesita que un mismo metodo pueda comportarse distinto segun el tipo real del objeto y eso solo se logra con metodos virtuales o con interfaces que internamente usan el mismo mecanismo cuando llamas hacersonido no es que la funcion sepa de antemano cual ejecutar sino que el objeto lleva consigo la referencia a su propia implementacion y ahi se decide cual codigo correr


### Actividad 04

Al ejecutar el codigo no sucede nada, sin embargo cuando descomentamos las dos lineas de codigo vemos que sucede esto

<img width="1820" height="979" alt="image" src="https://github.com/user-attachments/assets/bbec2b40-6a08-42e6-b859-49e7b7c884dc" />

esto pasa porque al descomentar las lineas que acceden a protectedVar y privateVar el compilador marca error porque esos miembros no son accesibles desde main ya que no pertenecen al ambito publico de la clase

Al ejecutar el siguiente codigo tenemos esto:

<img width="1848" height="893" alt="image" src="https://github.com/user-attachments/assets/4063b066-6c99-4352-8727-c622a7a50a3d" />

ocurre un error de compilacion porque secret1 es privado y no puede ser accedido fuera de la clase, la unica manera valida es usar un metodo publico como printMembers

Por ultimo, con el codigo final  al compilarlo no hay errores y funciona con normalidad. El programa compila y al ejecutarlo imprime los valores de secret1, secret2 y secret3 accediendo directamente a memoria, lo que demuestra que el encapsulamiento en c++ puede romperse en tiempo de ejecucion.

Despues de estos 3 breves ejercicios puedo decir que el encapsulamiento es ocultar los detalles internos de una clase y exponer solo lo necesario al exterior sirve para proteger los datos y evitar que el programador los use mal tambien hace que el codigo sea mas ordenado y facil de mantener porque solo se accede a lo que la clase permite. Sin embargo, hay cosas que quiesiera experimentar y resolver, por ejemplo


#### ¿podria usarse este truco de reinterpret_cast para hackear un programa o leer datos sensibles de un objeto?

Para esto usaremos de experimento este codigo generado por IA

```cpp
#include <iostream>
#include <cstddef>
#include <cstdint>
#include <cstring>

class MyClass {
private:
    int secret1;
    float secret2;
    char secret3;

public:
    MyClass(int s1, float s2, char s3) : secret1(s1), secret2(s2), secret3(s3) {}

    void printMembers() const {
        std::cout << "printMembers -> secret1: " << secret1 << "\n";
        std::cout << "printMembers -> secret2: " << secret2 << "\n";
        std::cout << "printMembers -> secret3: " << secret3 << "\n";
    }

    // metodos para calcular offsets relativos a 'this' (son legales dentro de la clase)
    std::size_t offset_secret1() const {
        return reinterpret_cast<const char*>(&(this->secret1)) - reinterpret_cast<const char*>(this);
    }
    std::size_t offset_secret2() const {
        return reinterpret_cast<const char*>(&(this->secret2)) - reinterpret_cast<const char*>(this);
    }
    std::size_t offset_secret3() const {
        return reinterpret_cast<const char*>(&(this->secret3)) - reinterpret_cast<const char*>(this);
    }
};

int main() {
    MyClass obj(42, 3.14f, 'A');

    std::cout << "direccion de obj: " << &obj << "\n";
    std::cout << "offset secret1: " << obj.offset_secret1() << "\n";
    std::cout << "offset secret2: " << obj.offset_secret2() << "\n";
    std::cout << "offset secret3: " << obj.offset_secret3() << "\n";

    obj.printMembers();

    std::cout << "presiona enter para continuar..." << std::endl;
    std::cin.get();

    // acceso directo usando aritmetica de bytes
    unsigned char* base = reinterpret_cast<unsigned char*>(&obj);

    // opcion A: leer directo mediante punteros (simple, comun en estos experimentos)
    int* ptrInt = reinterpret_cast<int*>(base + obj.offset_secret1());
    float* ptrF = reinterpret_cast<float*>(base + obj.offset_secret2());
    char* ptrCh = reinterpret_cast<char*>(base + obj.offset_secret3());

    std::cout << "acceso directo -> secret1: " << *ptrInt << "\n";
    std::cout << "acceso directo -> secret2: " << *ptrF << "\n";
    std::cout << "acceso directo -> secret3: " << *ptrCh << "\n";

    // opcion B (mas "defensiva"): copiar bytes con memcpy a variables locales
    int valInt = 0; float valF = 0.0f; char valCh = 0;
    std::memcpy(&valInt, base + obj.offset_secret1(), sizeof(valInt));
    std::memcpy(&valF, base + obj.offset_secret2(), sizeof(valF));
    std::memcpy(&valCh, base + obj.offset_secret3(), sizeof(valCh));
    std::cout << "acceso memcpy -> secret1: " << valInt << "\n";
    std::cout << "acceso memcpy -> secret2: " << valF << "\n";
    std::cout << "acceso memcpy -> secret3: " << valCh << "\n";

    std::cout << "presiona enter para salir..." << std::endl;
    std::cin.get();
    return 0;
}
```

##### Hipotesis

mi hipotesis es que aunque el compilador impida acceder directamente a los atributos privados de una clase, en tiempo de ejecucion es posible leerlos usando punteros y conversiones de tipo como reinterpret_cast. espero que de esta manera pueda acceder a los valores privados almacenados en memoria, lo cual demostraria que el encapsulamiento en c++ no es absoluto sino una convencion de compilacion

##### Experimentacion

para comprobarlo compile un programa donde defino una clase con tres atributos privados y un metodo publico que los imprime. luego en la funcion main cree una instancia y use punteros con reinterpret_cast sumando desplazamientos con sizeof para recorrer directamente la memoria del objeto. al ejecutar el programa primero verifique los valores con el metodo publico y despues accedi a los mismos valores pero leyendo directamente la memoria del objeto. tambien use la ventana de memoria y de inspeccion del depurador para confirmar que los miembros privados estaban ahi de forma contigua y accesible

<img width="1918" height="821" alt="image" src="https://github.com/user-attachments/assets/05a75ab7-1a9b-4d3d-9db2-86dff2773959" />

<img width="1919" height="378" alt="image" src="https://github.com/user-attachments/assets/a59bc48e-13bb-460c-8c96-958741f4d3cf" />


##### Hallazgos

descubri que el encapsulamiento en c++ solo protege en tiempo de compilacion y evita que el programador acceda por error a los atributos privados, pero en realidad en memoria los datos estan ahi y se pueden leer con tecnicas como reinterpret_cast. esto significa que el encapsulamiento no debe considerarse un mecanismo de seguridad, sino una herramienta de diseño que organiza el acceso a los datos y mejora la claridad del codigo. tambien confirme que al analizar la memoria con el depurador se pueden observar los miembros privados aun cuando el compilador prohibe usarlos directamente en el codigo


### Actividad 05

Cuando depuras un objeto de tipo CircularExplosion en Visual Studio, el depurador te muestra que este objeto contiene en memoria todos los campos heredados desde ExplosionParticle y, a su vez, los de Particle (aunque Particle no tiene atributos, sí tiene las tablas virtuales vtable para métodos virtuales).

<img width="1911" height="408" alt="image" src="https://github.com/user-attachments/assets/2f60f983-8a55-456d-9ee8-e976bc573fb6" />

La clase CircularExplosion no declara nuevos atributos propios, pero en memoria tiene todos los atributos de ExplosionParticle: position, velocity, color, age, lifetime, size. Además, el depurador deja ver que hay punteros ocultos a las vtables, lo que confirma que la herencia en C++ incluye la tabla de métodos virtuales para resolución dinámica. En el depurador puedo ver que  un objeto hijo realmente contiene la memoria de su clase padre, Que la jerarquía de clases se traduce en una estructura anidada de datos en memoria y que aunque no accedas a ciertos campos directamente, el compilador los incluye en el objeto.

De esto se puede concluir que La herencia en C++ se implementa incrustando la memoria del padre dentro del hijo. Eso significa que un CircularExplosion es un ExplosionParticle y también es un Particle,esto explica por qué puedes usar polimorfismo: un puntero Particle* puede apuntar a cualquier subclase.


### Actividad 06

Se puede observar que cuando uso el depurador y analizo el ciclo for, donde se llama particles[i]->update(dt), puedo ver que aunque todos los elementos son tratados como particle*, en realidad cada uno ejecuta el metodo update de su clase concreta, por ejemplo risingparticle, circularexplosion o randomexplosion, esto pasa porque cada objeto guarda internamente un puntero a su tabla virtual y gracias a esto el programa, en tiempo de ejecucion, sabe que funcion debe llamar, observo que el mismo codigo se comporta diferente dependiendo del tipo real del objeto, eso es lo que se llama polimorfismo en tiempo de ejecucion, el depurador me muestra que se invoca el metodo especifico de cada clase y ademas me deja ver los valores de los atributos del objeto en ese momento, esto confirma que la resolucion de la llamada no se hace en compilacion sino en ejecucion, puedo concluir que el polimorfismo funciona porque los metodos virtuales permiten que exista una tabla de funciones virtuales que almacena la direccion de las implementaciones correspondientes y asi la llamada se dirige a la version correcta, la relacion es que los metodos virtuales son la base del polimorfismo, sin ellos no seria posible que una misma llamada se comporte diferente segun el objeto real.

#### ¿Qué relación existe entre los métodos virtuales y el polimorfismo?

el polimorfismo en tiempo de ejecucion se implementa gracias a la combinacion de vptr y vtable lo que permite que la llamada se resuelva dinamicamente, la relacion entre los metodos virtuales y el polimorfismo es que los metodos virtuales son el mecanismo que habilita el polimorfismo dinamico ya que sin ellos todas las llamadas se resolverian de forma estatica en compilacion


#### Dibujo

<img width="1254" height="580" alt="image" src="https://github.com/user-attachments/assets/e8e9801e-0be8-45e6-abf3-08256d272138" />


El polimorfismo es uno de los temas que mas me genera dudas, asi que realizaremos los siguientes experimentos para salir de toda duda

#### ¿puede un mismo puntero de tipo base invocar en tiempo de ejecucion distintas implementaciones de un metodo virtual segun el tipo real del objeto y como evidenciamos esto con el depurador?

##### Hipotesis

si tengo un vector de punteros a una clase base con metodos virtuales y guardo alli distintos tipos de objetos derivados, entonces al recorrerlos con un ciclo y llamar al mismo metodo, cada objeto deberia ejecutar la version especifica de su clase, y con el depurador deberia poder ver como la llamada se resuelve en tiempo de ejecucion gracias a la tabla de funciones virtuales.

##### Experimentacion

Mediante este codigo genreado por IA creamos un vector de punteros a la clase base figura y almacenamos objetos de las clases derivadas circulo rectangulo y triangulo, luego recorrimos el vector llamando figuras[i]->dibujar() y usamos el depurador para detener la ejecucion en la llamada y observar la resolucion dinamica de metodos mediante la tabla de funciones virtuales, para ello compilamos en modo debug y desactivamos optimizaciones, colocamos un breakpoint en la llamada a dibujar, cuando el programa se detuvo inspeccionamos en autos o watch el puntero figuras[i] y expandimos el objeto para ver su tipo real, abrimos la ventana de memoria y pegamos la direccion del objeto para localizar el vptr y navegar por la vtable, despues continuamos la ejecucion paso a paso y observamos en el call stack que la invocacion entraba en circulo::dibujar o rectangulo::dibujar segun el objeto real, repetimos este proceso para cada elemento del vector y verificamos que las entradas de la vtable apuntaban a funciones distintas segun la clase derivada, hallazgos, observe que aunque el tipo declarado era figura* la llamada se ejecutaba en la implementacion concreta de cada clase, el depurador mostro el metodo especifico en el call stack y permitio ver el puntero a la vtable dentro del objeto, confirmando que el polimorfismo dinamico se implementa consultando la tabla de funciones virtuales en tiempo de ejecucion

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Figura {
public:
    virtual void dibujar() { cout << "dibujar figura generica\n"; }
    virtual ~Figura() {}
};

class Circulo : public Figura {
public:
    void dibujar() override { cout << "dibujar circulo\n"; }
};

class Rectangulo : public Figura {
public:
    void dibujar() override { cout << "dibujar rectangulo\n"; }
};

class Triangulo : public Figura {
public:
    void dibujar() override { cout << "dibujar triangulo\n"; }
};

int main() {
    vector<Figura*> figuras;
    figuras.push_back(new Circulo());
    figuras.push_back(new Rectangulo());
    figuras.push_back(new Triangulo());

    for (int i = 0; i < figuras.size(); i++) {
        figuras[i]->dibujar(); // llamada polimorfica
    }

    // limpiar memoria
    for (auto f : figuras) delete f;
    return 0;
}
```


<img width="1913" height="850" alt="image" src="https://github.com/user-attachments/assets/b44735f7-69ab-4651-a36e-06f572327ec5" />

<img width="1919" height="792" alt="image" src="https://github.com/user-attachments/assets/daad76f2-3f17-4d09-aab4-571170c2578d" />

<img width="1880" height="361" alt="image" src="https://github.com/user-attachments/assets/2b034834-d57e-427e-ad41-37bd6868e078" />

##### Hallazgos

el polimorfismo permite escribir codigo generico que se comporta segun el tipo real del objeto en ejecucion y los metodos virtuales son el mecanismo que habilita esta flexibilidad, implicaciones, comprender esto ayuda a depurar comportamientos inesperados, optimizar llamadas criticas y ser consciente del coste de la resolucion dinamica en tiempo de ejecucion

















