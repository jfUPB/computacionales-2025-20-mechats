# Unidad 3


## 🛠 Fase: Apply

### ACTIVIDAAD INTEGRADORA

#### compilación de codigo

<img width="1887" height="869" alt="image" src="https://github.com/user-attachments/assets/94ff1ed3-99bd-461a-90ce-02216b536bd6" />

#### identificacion y explicacion de errores

1. Hay una fuga de memoria, porque hay un new [] pero no hay un delete [].

   estadisticas = new int[3] nunca se libera, no tiene un destructor, ese arreglo vive en el heap; al salir de simularEncuentro los objetos se destruyen  pero el bloque del heap queda sin liberar y entonces hace que cada personaje pierda su bloque

2. Hay una copia superficial

   Personaje copiaHeroe = heroe; usa el constructor de copia implícito, que copia el puntero, no los datos y por eso ahora dos objetos apuntan al mismo arreglo en el heap . No existe un dueño único ni reglas de copia.


#### Solucion y refactorizacion

En la refactorización de la clase Personaje añadí un destructor que libera la memoria reservada dinámicamente con delete[] estadisticas, ya que en la versión original esa memoria nunca se liberaba y producía fugas de memoria. Además, señalé que la copia por defecto de objetos (Personaje copiaHeroe = heroe;) era peligrosa porque hacía una copia superficial del puntero, dejando a dos objetos apuntando al mismo bloque de memoria, lo que llevaría a errores graves al destruirlos. Para evitarlo, la solución propuesta es no usar la copia automática y, en su lugar, crear nuevos personajes explícitamente con sus propios datos. Con estos cambios, la clase gestiona correctamente la memoria y se evitan tanto fugas como accesos inválidos.

```cpp
#include <iostream>
#include <string>

class Personaje {
public:
    std::string nombre;
    int* estadisticas;

    Personaje(std::string n, int vida, int ataque, int defensa) {
        nombre = n;
        estadisticas = new int[3];
        estadisticas[0] = vida;
        estadisticas[1] = ataque;
        estadisticas[2] = defensa;
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

    ~Personaje() {
        delete[] estadisticas;
        std::cout << "Destructor: muere " << nombre << std::endl;
    }

    void imprimir() {
        std::cout << "Personaje " << nombre
            << " [Vida: " << estadisticas[0]
            << ", ATK: " << estadisticas[1]
            << ", DEF: " << estadisticas[2]
            << "]" << std::endl;
    }
};

void simularEncuentro() {
    std::cout << "\n--- Iniciando encuentro ---" << std::endl;
    Personaje heroe("Aragorn", 100, 20, 15);

    std::cout << "Saliendo del encuentro..." << std::endl;
}

int main() {
    simularEncuentro();
    std::cout << "\nSimulación terminada." << std::endl;
    return 0;
}
```

#### Justificación de la solucion

