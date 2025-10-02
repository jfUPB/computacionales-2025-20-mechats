# Bitácora de aprendizaje de la unidad 6



## Actividad 01

### ¿Cómo puedes interactuar con la aplicación? Menciona específicamente las teclas y qué efecto parecen tener sobre las partículas

al presionar la tecla a las partículas se acercan al cursor, con la tecla r se alejan, al usar la tecla s se quedan quietas y con la tecla n vuelven a moverse de manera normal

### ¿Observas los diferentes tipos de “partículas”? ¿Se comportan todas igual inicialmente?

a primera vista no noté ningún cambio, al inicio aparecen tres clases diferentes de partículas que son star, planet y shooting star

###  Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas

pues, yo diria que es una forma de polimorfismo en la que en vez de cambiar el comportamiento segun el tipo de particula sea que cambie segun el estado en el que se encuentran las particulas



N: se mueven de maanera aleatoria


<img width="1102" height="805" alt="image" src="https://github.com/user-attachments/assets/0ed950e7-9c1c-48d7-98d5-8adc88db2d61" />


S: estan quietas

<img width="1899" height="919" alt="image" src="https://github.com/user-attachments/assets/c8e7a635-bd9a-4f2c-8e2e-a70f150dbe91" />


A: se dirigen al puntero

<img width="1102" height="609" alt="image" src="https://github.com/user-attachments/assets/fc8c7476-da89-4bf8-99c5-5ae0c205c902" />


R: se alejan del puntero

<img width="1023" height="749" alt="image" src="https://github.com/user-attachments/assets/9d02f6b4-bdee-41f5-a3c2-fa8202d10b82" />





## Actividad 02

### Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?

El patrón observer sirve para que un objeto pueda avisarle a varios otros cuando algo cambia, sin necesidad de estar directamente conectado con ellos. El problema que resuelve es el acoplamiento fuerte, pues en lugar de que el Sujeto conozca todos los detalles de cada observador , simplemente dispara una notificación y cada Observador decide cómo reaccionar. Esto hace que el sistema sea más flexible y fácil de ampliar

### Diagrama de la relación entre Subject, Observer, ofApp y Particle



<img width="850" height="594" alt="image" src="https://github.com/user-attachments/assets/292ffb29-a17d-4d40-8f36-74064886d467" />



### Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.



<img width="1059" height="580" alt="image" src="https://github.com/user-attachments/assets/9ee2abeb-e4e9-4b8a-abe8-b5db9db4911d" />

## Actividad 03

### Explica con tus propias palabras el propósito del patrón Factory Method (o Simple Factory, en este caso). ¿Qué problema principal aborda en la creación de objetos?

es separar la creación de objetos del código que los usa. Esto significa que ofApp no necesita saber cómo se construye un objeto ni qué configuración específica debe tener, solo pide el objeto y la fábrica se encarga de devolverlo ya configurado. El problema que resuelve es el acoplamiento fuerte: evita que el código cliente dependa de clases concretas y de toda la lógica de inicialización

### ¿Qué ventajas aporta el uso de ParticleFactory en ofApp::setup en comparación con instanciar y configurar las partículas directamente allí? Piensa en términos de organización del código (SRP - Single Responsibility Principle), legibilidad y facilidad para añadir nuevos tipos de partículas en el futuro.

el uso de particlefactory en ofapp setup trae varias ventajas primero permite que el codigo este mas ordenado y facil de leer ya que la logica de crear particulas no queda mezclada con la configuracion de la aplicacion segundo sigue el principio de responsabilidad unica porque cada clase se enfoca en lo que debe hacer ofapp organiza la aplicacion y particlefactory crea las particulas tercero facilita mucho cuando se quieren agregar nuevos tipos de particulas porque solo se modifica la fabrica sin tener que tocar otras partes del codigo esto hace que el mantenimiento sea mas facil y el programa sea mas escalable en el futuro

### Imagina que quieres añadir un nuevo tipo de partícula llamada "black_hole" que tiene tamaño grande, color negro y velocidad muy lenta. Describe los pasos que necesitarías seguir para implementar esto utilizando la ParticleFactory existente. ¿Tendrías que modificar ofApp::setup? ¿Por qué sí o por qué no?
Para añadir la partícula "black_hole" tendría que:

pues, para eso yo creo que habria que hacer una serie de pasos:

1 ir a la clase ParticleFactory.

2 en el método createParticle, agregar un nuevo caso para "black_hole".

3 crear un objeto Particle con las propiedades: tamaño grande, color negro y velocidad muy lenta.

4 devolver esa partícula como resultado.

### El método createParticle en el ejemplo es estático. ¿Qué implicaciones (ventajas/desventajas) tiene esto comparado con tener una instancia de ParticleFactory y un método de instancia createParticle()?

las ventajas son que el método estático hace que sea muy fácil de usar, porque no hay que crear objetos adicionales, solo se llama directamente desde la clase, esto reduce la cantidad de código repetido y hace que la lógica de creación esté toda en un mismo punto, también mejora el rendimiento en cierta medida porque no hay que manejar instancias extra, y ayuda a que el código cliente sea más limpio y directo, otra ventaja es que, al ser centralizado, es fácil mantener o cambiar las reglas de creación sin ir a buscar en muchas partes del programa

las desventajas son que, al ser estático, la factory no se puede extender tan fácilmente, por ejemplo, no puedes hacer subclases de la factory para crear variaciones distintas de partículas, tampoco puedes aprovechar patrones más avanzados como inyección de dependencias porque no tienes una instancia configurable, además, se pierde flexibilidad si en el futuro quieres tener varias factories con configuraciones diferentes, por ejemplo, una factory que cree partículas rápidas y otra de partículas lentas, no sería tan fácil con métodos estáticos, finalmente, si el proyecto crece demasiado, la dependencia en un método estático puede hacer el código menos modular y más difícil de probar en unit tests

## Actividad 04

### Explica con tus propias palabras el propósito del patrón State. ¿Cuándo es útil aplicarlo?

el patrón state sirve para que un objeto pueda cambiar su comportamiento dependiendo de su estado interno sin necesidad de llenar el código de condicionales gigantes lo que se hace es encapsular cada comportamiento en una clase separada y la clase principal delega la lógica al estado actual es muy útil cuando un objeto puede tener múltiples comportamientos y estos dependen de su estado por ejemplo una partícula que puede moverse normalmente ser atraída al mouse repelerse o detenerse


### Dibuja un diagrama de estados simple para la clase Particle. Muestra los diferentes estados (Normal, Attract, Repel, Stop) como nodos y las transiciones entre ellos como flechas etiquetadas con el evento que las causa (p. ej., la tecla presionada: ‘n’, ‘a’, ‘r’, ‘s’).


<img width="787" height="582" alt="image" src="https://github.com/user-attachments/assets/ec5118cc-ef98-4fbd-8d9b-d4012e28903a" />










### Describe las ventajas de usar el patrón State en Particle en lugar de tener un miembro std::string estadoActual y usar un gran if/else if/else o switch dentro de Particle::update() para cambiar el comportamiento. Piensa en cohesión, extensibilidad (añadir nuevos estados) y el Principio Abierto/Cerrado (Open/Closed Principle).

primero mejora la cohesión porque cada clase de estado tiene su lógica bien organizada y no se mezcla con las demás segundo hace que el código sea más fácil de mantener y extender porque si quiero agregar un nuevo estado solo creo una nueva clase sin tocar el código existente esto sigue el principio abierto cerrado tercero el código de particle queda más limpio porque no necesita saber qué hacer en cada estado solo delega la responsabilidad al objeto de estado actual

### Qué responsabilidad tienen los métodos onEnter y onExit en el patrón State? Proporciona un ejemplo de por qué podrían ser útiles (incluso si no se usan mucho en todos los estados de este caso de estudio). Por ejemplo, ¿Qué podrías hacer en onEnter para AttractState o en onExit para StopState?

los métodos onenter y onexit sirven para ejecutar acciones específicas al entrar o salir de un estado por ejemplo en este caso normalstate usa onenter para asignar una nueva velocidad aleatoria a la partícula podrían ser útiles en otros casos como en attractstate para inicializar una fuerza especial al entrar o en stopstate para reiniciar la velocidad a cero al salir así se asegura que cada transición se maneje correctamente sin dejar restos de un estado anterior










### ¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.

 En primer lugar, reduce el acoplamiento entre las clases, ya que ofApp no necesita conocer los detalles internos de cada partícula ni recorrerlas una por una para cambiar su comportamiento, simplemente lanza una notificación y cada partícula decide qué hacer con ella. Esto también mejora la extensibilidad, porque si en el futuro quiero agregar nuevos tipos de objetos que reaccionen a los eventos, puedo hacerlo sin tener que modificar el código de ofApp. Además, el código resulta más limpio y fácil de mantener, pues cada clase se enfoca en su propia responsabilidad. Finalmente, el patrón facilita la escalabilidad, ya que un solo evento enviado desde el sujeto puede llegar automáticamente a todas las partículas, sin necesidad de escribir más lógica en el controlador principal.

 ## Actividad 05

 ```cpp
OfApp.cpp

#include "ofApp.h"
#include <algorithm>

void Subject::addObserver(Observer * observer) {
	if (!observer) return;
	if (std::find(observers.begin(), observers.end(), observer) == observers.end()) {
		observers.push_back(observer);
	}
}

void Subject::removeObserver(Observer * observer) {
	if (!observer) return;
	observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
}

void Subject::notify(const std::string & event) {
	for (Observer * observer : observers) {
		observer->onNotify(event);
	}
}

Particle::Particle()
	: state(nullptr) {
	position = ofVec2f(ofRandomWidth(), ofRandomHeight());
	velocity = ofVec2f(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
	size = ofRandom(2.0f, 5.0f);
	color = ofColor(255);

	state = new NormalState();
	state->onEnter(this);
}

Particle::~Particle() {
	if (state) {
		state->onExit(this);
		delete state;
		state = nullptr;
	}
}

void Particle::setState(State * newState) {
	if (state) {
		state->onExit(this);
		delete state;
	}
	state = newState;
	if (state) {
		state->onEnter(this);
	}
}

void Particle::update() {
	if (state) {
		state->update(this);
	}
	keepInsideWindow();
}

void Particle::draw() {
	ofPushStyle();
	ofSetColor(color);
	ofDrawCircle(position, size);
	ofPopStyle();
}

void Particle::onNotify(const std::string & event) {
	if (event == "attract") {
		setState(new AttractState());
	} else if (event == "repel") {
		setState(new RepelState());
	} else if (event == "stop") {
		setState(new StopState());
	} else if (event == "normal") {
		setState(new NormalState());
	}
}

void Particle::keepInsideWindow() {
	const float W = static_cast<float>(ofGetWidth());
	const float H = static_cast<float>(ofGetHeight());

	if (position.x < 0.0f) {
		position.x = 0.0f;
		velocity.x *= -1.0f;
	} else if (position.x > W) {
		position.x = W;
		velocity.x *= -1.0f;
	}
	if (position.y < 0.0f) {
		position.y = 0.0f;
		velocity.y *= -1.0f;
	} else if (position.y > H) {
		position.y = H;
		velocity.y *= -1.0f;
	}
}

void NormalState::onEnter(Particle * particle) {
	particle->velocity.set(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
}

void NormalState::update(Particle * particle) {
	particle->position += particle->velocity;
}

static void steer(Particle * particle, const ofVec2f & toward, float accel, float vmax, float posScale) {
	ofVec2f dir = toward - particle->position;
	float len = dir.length();
	if (len > 1e-6f) {
		dir /= len;
		particle->velocity += dir * accel;
	}
	particle->velocity.limit(vmax);
	particle->position += particle->velocity * posScale;
}

void AttractState::update(Particle * particle) {
	ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
	steer(particle, mouse, 0.05f, 3.0f, 0.2f);
}

void RepelState::update(Particle * particle) {
	ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
	ofVec2f away = particle->position - mouse;
	float len = away.length();
	if (len > 1e-6f) {
		away /= len;
		particle->velocity += away * 0.05f;
	}
	particle->velocity.limit(3.0f);
	particle->position += particle->velocity * 0.2f;
}

void StopState::update(Particle * particle) {
	particle->velocity *= 0.80f;
	if (particle->velocity.lengthSquared() < 1e-4f) {
		particle->velocity.set(0.0f, 0.0f);
	}
	particle->position += particle->velocity;
}

void BlackHoleState::onEnter(Particle * particle) {
	particle->velocity.set(ofRandom(-0.1f, 0.1f), ofRandom(-0.1f, 0.1f));
	particle->color = ofColor(0, 0, 0);
}

void BlackHoleState::update(Particle * particle) {
	particle->position += particle->velocity * 0.05f;
}

BlackHole::BlackHole() {
	setState(new BlackHoleState());
	size = ofRandom(15.0f, 25.0f);
	color = ofColor(0, 0, 0);
}

Particle * ParticleFactory::createParticle(const std::string & type) {
	if (type == "black_hole") {
		return new BlackHole();
	}

	Particle * particle = new Particle();

	if (type == "star") {
		particle->size = ofRandom(2.0f, 4.0f);
		particle->color = ofColor(255, 0, 0);
	} else if (type == "shooting_star") {
		particle->size = ofRandom(3.0f, 6.0f);
		particle->color = ofColor(0, 255, 0);
		particle->velocity *= 3.0f;
	} else if (type == "planet") {
		particle->size = ofRandom(5.0f, 8.0f);
		particle->color = ofColor(0, 0, 255);
	}
	return particle;
}

ofApp::~ofApp() {
	for (Particle * p : particles) {
		removeObserver(p);
		delete p;
	}
	particles.clear();
}

void ofApp::setup() {
	ofBackground(0);
	particles.reserve(100 + 5 + 10 + 2);

	for (int i = 0; i < 100; ++i) {
		Particle * p = ParticleFactory::createParticle("star");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 5; ++i) {
		Particle * p = ParticleFactory::createParticle("shooting_star");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 10; ++i) {
		Particle * p = ParticleFactory::createParticle("planet");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 2; ++i) {
		Particle * p = ParticleFactory::createParticle("black_hole");
		particles.push_back(p);
		addObserver(p);
	}
}

void ofApp::update() {
	for (Particle * p : particles) {
		p->update();
	}
}

void ofApp::draw() {
	for (Particle * p : particles) {
		p->draw();
	}
}

void ofApp::keyPressed(int key) {
	switch (key) {
	case 's':
		notify("stop");
		break;
	case 'a':
		notify("attract");
		break;
	case 'r':
		notify("repel");
		break;
	case 'n':
		notify("normal");
		break;
	default:
		break;
	}
}
```

```cpp
ofapp.h

#pragma once

#include "ofMain.h"
#include <string>
#include <vector>

class Observer {
public:
	virtual ~Observer() = default;
	virtual void onNotify(const std::string & event) = 0;
};

class Subject {
public:
	void addObserver(Observer * observer);
	void removeObserver(Observer * observer);

protected:
	void notify(const std::string & event);

private:
	std::vector<Observer *> observers;
};

class Particle;

class State {
public:
	virtual ~State() = default;
	virtual void update(Particle * particle) = 0;
	virtual void onEnter(Particle * particle) { }
	virtual void onExit(Particle * particle) { }
};

class Particle : public Observer {
public:
	Particle();
	~Particle() override;

	Particle(const Particle &) = delete;
	Particle & operator=(const Particle &) = delete;

	void update();
	void draw();
	void onNotify(const std::string & event) override;

	void setState(State * newState);

	ofVec2f position;
	ofVec2f velocity;
	float size;
	ofColor color;

private:
	void keepInsideWindow();
	State * state;
};

class NormalState : public State {
public:
	void update(Particle * particle) override;
	void onEnter(Particle * particle) override;
};

class AttractState : public State {
public:
	void update(Particle * particle) override;
};

class RepelState : public State {
public:
	void update(Particle * particle) override;
};

class StopState : public State {
public:
	void update(Particle * particle) override;
};

class BlackHoleState : public State {
public:
	void update(Particle * particle) override;
	void onEnter(Particle * particle) override;
};

class BlackHole : public Particle {
public:
	BlackHole();
};

class ParticleFactory {
public:
	static Particle * createParticle(const std::string & type);
};

class ofApp : public ofBaseApp, public Subject {
public:
	~ofApp() override;
	void setup() override;
	void update() override;
	void draw() override;
	void keyPressed(int key) override;

private:
	std::vector<Particle *> particles;
};
```

el patron factory lo use para poder crear la nueva particula sin tener que escribir todo el codigo de configuracion en ofapp, lo que hice fue agregar un nuevo caso en el metodo createparticle dentro de la clase particlefactory, ahi defini las caracteristicas especificas de la particula como su tamaño, su color y su velocidad, de esta forma solo con llamar a createparticle pasando el nombre de la particula se crea automaticamente con sus propiedades, esto hace que el codigo quede mas ordenado, mas facil de leer y que sea sencillo agregar mas tipos de particulas en el futuro sin modificar otras partes del programa

para implementar el patron observer en la nueva particula lo que hice fue aprovechar que la clase particle ya hereda de observer, entonces la nueva particula automaticamente puede recibir notificaciones de los eventos que manda el sujeto que en este caso es ofapp, al crear la particula con el factory la agregue como observador usando addobserver, de esa forma cuando en ofapp se presiona una tecla y se llama a notify la nueva particula recibe el mensaje y cambia su estado segun el evento, igual que las demas particulas

para aplicar el patron state en la nueva particula no tuve que crear un sistema diferente, sino que reutilice el que ya estaba en la clase particle, lo que hice fue que la nueva particula tambien empieza en un estado normal y luego puede cambiar a attract, repel o stop cuando recibe las notificaciones del observer, cada estado define su propio comportamiento en el metodo update, por ejemplo mover hacia el mouse, alejarse o detenerse, gracias a esto la nueva particula puede tener distintos comportamientos dinamicos segun su estado interno, sin necesidad de usar if o switch grandes

PDDT: si no se alcanza a apreciar bien la nueva particula que cree es porque me dio curiosidad ver si se veria una particula de color negro, y aunque es medio dificil en el modo attract se pueden apreciar con mas claridad, incluso como son mas grandes que las demas particulas pareciera que cuando activas attract un agujero negro las absorbe, increible

<img width="784" height="531" alt="image" src="https://github.com/user-attachments/assets/e83d3a50-c017-405a-8c9b-6d3f4528a78d" />




## Autoevaluacion


### Actividad 01

nota propuesta: 5

Creo que me aventure mucho con la hipotesis, tecnicamente no estaba en lo correcto. Pero decir que era una especie de polimorfismo pero que funcionaba con estados y no con objetos demostraba como aplicaba lo que ya se a dar una hipotesis inicial de como funcionaba el codigo

### Actividad 2

nota propuesta: 4.5

en la segunda actividad aprendí a identificar los patrones observer y factory en el código, entendí cómo observer permite que las partículas reaccionen a eventos externos sin acoplarse directamente a la clase principal, y cómo factory me permitió crear diferentes tipos de partículas sin duplicar código, gracias a eso comprendí mejor la importancia de la modularidad y la reutilización en la programación, siento que el diagrama que hice esta bastante claro y esperaria yo que este correcto

### Actividad 3

nota propuesta: 4

en la segunda actividad entendí cómo funciona el patrón factory, aprendí que su propósito es centralizar la creación de objetos para no llenar el código de instanciaciones repetidas, vi que con la clase particlefactory el método createparticle se encarga de configurar cada partícula según su tipo, esto mejora la organización del código y sigue el principio de responsabilidad única, también comprendí que si quiero crear nuevos tipos de partículas es mucho más fácil porque solo modifico la fábrica y no el resto de la aplicación, pienso que me merezco buena nota porque demostré que sé diferenciar entre instanciación directa y el uso de una fábrica y cómo eso mejora la extensibilidad del sistema

### Actividad 4 

nota propuesta: 4
en la tercera actividad aprendí a profundidad cómo funciona el patrón state, entendí que lo más importante es que permite que un objeto cambie de comportamiento dependiendo de su estado sin necesidad de tener un montón de condiciones dentro de la misma clase, ademas es mas facil usarlo en comparación con un switch o muchos if, porque con state el código se vuelve más cohesivo, cada clase tiene una sola responsabilidad, y además se cumple el principio abierto cerrado ya que si quiero agregar un nuevo estado no tengo que modificar la clase particle sino simplemente crear una nueva clase que extienda state

### Actividad 05

nota propuesta: 4.5
 
esta actividad fue la más completa porque integré los tres patrones en una nueva partícula, logré usar la fábrica para crearla, el observer para que recibiera eventos y el state para definir su comportamiento, sin embargo aquí tuve más dificultades, por ejemplo  me costó integrar el nuevo tipo en la factory sin romper lo que ya estaba, tuve que rehacer esa parte para que funcionara bien, a pesar de esos errores pude resolverlos y ahora entiendo mejor cómo combinar varios patrones en un mismo sistema


 


