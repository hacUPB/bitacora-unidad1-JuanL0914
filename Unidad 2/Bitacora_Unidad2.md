
Actividad 1 — Suma de dos enteros
```


//Define una función sum(a, b) que retorna la suma de dos enteros, y en main() la llama con a=5 y b=7, imprimiendo el resultado por consola. Es el ejemplo más básico: declarar una función, pasar parámetros por valor y usar cout.

#include <iostream>
int sum(int a, int b) {
	return a + b;
}
 
int main() {
	int a = 5;
	int b = 7;
	std::cout << "La suma de " << a << " y " << b << " es " << sum(a, b) << "\n";
}
```

<img width="967" height="51" alt="image" src="https://github.com/user-attachments/assets/ccc7ac97-6ee9-4e64-aa1e-7074f03bfd01" />

 

●	Resultado: 'La suma de 5 y 7 es 12' — correcto.
●	No hay errores porque el código es sintácticamente simple y no maneja memoria dinámica.

Actividad 2 — Paso de parámetros: valor, referencia y puntero
```


//Compara las tres formas de pasar un argumento a una función en C++

#include <iostream>
using namespace std;
 
// Función que modifica el parámetro pasado por valor
void modificarPorValor(int n) {
    cout << "Dentro de modificarPorValor, valor inicial: " << n << endl;
    n += 5;
    cout << "Dentro de modificarPorValor, valor modificado: " << n << endl;
}
 
// Función que modifica el parámetro pasado por referencia
void modificarPorReferencia(int& n) {
    cout << "Dentro de modificarPorReferencia, valor inicial: " << n << endl;
    n += 5;
    cout << "Dentro de modificarPorReferencia, valor modificado: " << n << endl;
}
 
// Función que modifica el parámetro utilizando punteros
void modificarPorPuntero(int* n) {
    cout << "Dentro de modificarPorPuntero, valor inicial: " << *n << endl;
    *n += 5;
    cout << "Dentro de modificarPorPuntero, valor modificado: " << *n << endl;
}
 
int main() {
    int a = 10;    int b = 10;    int c = 10;
    cout << "Valor inicial de a (paso por valor): " << a << endl;
    cout << "Valor inicial de b (paso por referencia): " << b << endl;
    cout << "Valor inicial de c (paso por puntero): " << c << endl;
    cout << "\nLlamando a modificarPorValor(a)..." << endl;
    modificarPorValor(a);
    cout << "Después de modificarPorValor, valor de a: " << a << endl;
    cout << "\nLlamando a modificarPorReferencia(b)..." << endl;
    modificarPorReferencia(b);
    cout << "Después de modificarPorReferencia, valor de b: " << b << endl;
    cout << "\nLlamando a modificarPorPuntero(&c)..." << endl;
    modificarPorPuntero(&c);
    cout << "Después de modificarPorPuntero, valor de c: " << c << endl;
    return 0;
}
```

<img width="968" height="386" alt="image" src="https://github.com/user-attachments/assets/a1747e43-24e2-4d33-8620-3572a1106f63" />



Actividad 3 — Regiones de memoria (stack, heap, globales, estáticas, solo lectura)
 ```


//Imprime direcciones de memoria de distintos tipos de variables para visualizar en qué región vive cada una: variables locales (stack), variables globales inicializadas y no inicializadas, una constante de solo lectura, una variable static dentro de una función, y un arreglo reservado dinámicamente con new (heap), liberado al final con delete[].
Error a propósito #1 — conflicto de Git sin resolver
El archivo tal como está en el repositorio contiene marcadores de conflicto de fusión (<<<<<<< HEAD, ======= y >>>>>>> ...) que nunca se resolvieron. Un marcador de conflicto es un carácter no válido en C++

#include <iostream>
#include <cstdlib>
using namespace std;
// Variables globales
int global_inicializada = 42;
int global_no_inicializada;
// Constante global
const char* const mensaje_ro = "Hola, memoria de solo lectura";
// Función de ejemplo que muestra la dirección de su variable local estática
void funcionConStatic() {
    static int var_estatica = 100;
    cout << "Dirección de var_estatica (static): " << &var_estatica << endl;
}
// Función que asigna memoria dinámica (heap)
int* crearArrayHeap(int tam) {
    int* arr = new int[tam];
    for (int i = 0; i < tam; i++) {
        arr[i] = i;
    }    return arr;
}
// Una función simple para representar el código (se encontrará en la región de código)
int suma(int a, int b) {
    int c = a + b; // "c" es una variable local (stack)
    return c;
}
int main() {
    // Variable local (stack)
    int a = 10;
    int b = 20;
    int c = suma(a, b);
    cout << "Resultado de suma(a, b): " << c << endl;
    cout << "Dirección de variable local 'a': " << &a << endl;
    cout << "Dirección de variable local 'b': " << &b << endl;
    cout << "Dirección de la variable local 'c' (resultado): " << &c << endl;
    // Variables globales
    cout << "Dirección de 'global_inicializada': " << &global_inicializada << endl;
    cout << "Dirección de 'global_no_inicializada': " << &global_no_inicializada << endl;
    // Constante global (solo lectura)
    cout << "Dirección de 'mensaje_ro' (zona de solo lectura): " << static_cast<const void*>(mensaje_ro) << endl;
    // Llamada a función que tiene variable estática
    funcionConStatic();
    // Uso del Heap: asignación dinámica
    int tamArray = 10;
    int* arrayHeap = crearArrayHeap(tamArray);
    cout << "Dirección del primer elemento del array asignado en Heap: " << arrayHeap << endl;
    for (int i = 0; i < tamArray; i++) {
        cout << "arrayHeap[" << i << "] = " << arrayHeap[i] << " en " << (arrayHeap + i) << endl;
    }
    delete[] arrayHeap; // Liberamos la memoria dinámica
    return 0;
}
```
 

 <img width="969" height="289" alt="image" src="https://github.com/user-attachments/assets/dc021286-b40a-4bfc-a7a0-75d195978fb0" />

 
Actividad 4 — Experimentos de memoria (use-after-free)
```
//#include <iostream>
//#include <cstdlib>
//using namespace std;
//
//int main() {
//    // Variable local (stack)
//    int a = 10;
//    int b = 20;
//    /**********************************************************
//    EXPERIMENTO 1
//    ***********************************************************/
//    void* ptr = reinterpret_cast<void*>(&main);
//    cout << "Voy a modificar la memoria en la dirección: " << ptr << endl;
//    *reinterpret_cast<int*>(ptr) = 0;
//    /********************************************************/
//    return 0;
//}
//
 
//#include <iostream>
//#include <cstdlib>
//using namespace std;
//// Constante global
//const char* const mensaje_ro = "Hola, memoria de solo lectura";
//
//int main() {
//    // Variable local (stack)
//    int a = 10;
//    int b = 20;
//
//    /**********************************************************
//    EXPERIMENTO 2
//    ***********************************************************/
//    char* ptr = (char*)&mensaje_ro;
//    cout << "Voy a modificar la memoria en la dirección: " << ptr << endl;
//    *ptr = 0;
//    /********************************************************/
//    return 0;
//}
 
// el puntero esta duplicado por ende no va a arrancar porque esta detectando 2 punteros
 
//#include <iostream>
//#include <cstdlib>
//using namespace std;
//// Variables globales
//int global_inicializada = 42;
//int global_no_inicializada;
//
//int main() {    // Variable local (stack)
//    int a = 10;
//    int b = 20;
//    /**********************************************************
//    EXPERIMENTO 3
//    ***********************************************************/
//    cout << "global_inicializada: " << global_inicializada << endl;
//    cout << "global_no_inicializada: " << global_no_inicializada << endl;
//
//    global_inicializada = 69;
//    global_no_inicializada = 666;
//    cout << "global_inicializada: " << global_inicializada << endl;
//    cout << "global_no_inicializada: " << global_no_inicializada << endl;
//    /********************************************************/
//    return 0;
//} 
 
//#include <iostream>
//#include <cstdlib>
//using namespace std;
//// Función de ejemplo que muestra la dirección de su variable local estática
//void funcionConStatic() {
//    static int var_estatica = 100;
//    cout << "Dirección de var_estatica (static): " << &var_estatica << endl;
//}
//
//int main() {    // Variable local (stack)
//    int a = 10;
//    int b = 20;
//    /**********************************************************
//    EXPERIMENTO 4
//    ***********************************************************/
//    static int var_estatica = 42;
//    cout << "var_estatica: " << var_estatica << endl;
//    /********************************************************/
//    return 0;
//}
 
//
 
//#include <iostream>
//#include <cstdlib>
//using namespace std;
//// Función de ejemplo que muestra la dirección de su variable local estática
//void funcionConStatic() {
//	static int var_estatica = 100;
//	cout << "var_estatica: " << var_estatica << endl;
//	var_estatica++;
//}
//
//void funcionSinStatic() {
//	int var_no_estatica = 100;
//	cout << "var_no_estatica: " << var_no_estatica << endl;
//	var_no_estatica++;
//}
//
//int main() {    // Variable local (stack)
//	int a = 10;
//	int b = 20;
//	/**********************************************************
//	EXPERIMENTO 5
//	***********************************************************/
//	for (int i = 0; i < 5; i++) {
//		cout << "Iteración " << i << endl;
//		funcionSinStatic();
//		funcionConStatic();
//	}
//	/********************************************************/
//	return 0;
//}
 
#include <iostream>
using namespace std;
int main() {    // Tamaño del arreglo dinámico
    int tam = 5;
    // Asignar memoria en el Heap para un arreglo de enteros
    int* arrayHeap = new int[tam];
    // Inicializar y mostrar los valores y direcciones de memoria
    for (int i = 0; i < tam; i++) {
        arrayHeap[i] = (i + 1) * 10;
        cout << "arrayHeap[" << i << "] = " << arrayHeap[i] << " en dirección " << (arrayHeap + i) << endl;
    }
    // Liberar la memoria asignada en el Heap
    delete[] arrayHeap;
    /**********************************************************
    EXPERIMENTO 6
    ***********************************************************/
    cout << arrayHeap[0] << endl;
 
    /********************************************************/
    return 0;
}

 
```

 
Actividad 5 — Copia de objetos (constructor de copia por defecto)
```
//Define la clase Punto con constructor y destructor que imprimen mensajes. En main() se crea un objeto 'original', se copia en 'copia' (invocando el constructor de copia generado por el compilador) y se guarda un puntero p que apunta al mismo 'original'. Al modificar 'copia' y luego 'p->...', se observa la diferencia entre una copia independiente y un alias (puntero) al mismo objeto.

// Actividad 5.cpp : Este archivo contiene la función "main". La ejecución del programa comienza y termina ahí.
#include <iostream>
#include <string>
using namespace std;
class Punto {
public:   string name;
      int x;
      int y;
      // Constructor
      Punto(string _name, int _x, int _y) : name(_name), x(_x), y(_y) {
          cout << "Constructor: Punto " << name << " (" << x << ", " << y << ") creado." << endl;
      }
      // Destructor
      ~Punto() {
          cout << "Destructor: Punto " << name << "(" << x << ", " << y << ") destruido." << endl;
      }
      // Método para imprimir valores
      void imprimir() {
          cout << "Punto " << name << "(" << x << ", " << y << ")" << endl;
      }
};
 
int main() {    // Objeto original
    Punto original("original", 70, 80);
    original.imprimir();
    Punto* p = &original;
    // Copia del objeto
    Punto copia = original;
    copia.name = "copia";
    copia.x = 100;
    copia.y = 200;
    copia.imprimir();
    original.imprimir();
    p->name = "p";
    p->x = 300;
    p->y = 400;
    p->imprimir();
    original.imprimir();
    return 0;
}
 ```

 
Actividad 6 — Ciclo de vida de un objeto en el stack
```
Ubicación: Unidad 2/Sesion 3/Actividad 6
Qué hace el código
Crea un objeto Punto p(10, 20) en el stack (pensado para inspeccionarse con el depurador de Visual Studio, colocando un breakpoint). Al salir de main(), el destructor se llama automáticamente porque el objeto vive en el stack.
#include <iostream>
using namespace std;
class Punto {
public:   int x;
	  int y;
	  // Constructor
	  Punto(int _x, int _y) : x(_x), y(_y) {
		  cout << "Constructor: Punto(" << x << ", " << y << ") creado." << endl;
	  }
	  // Destructor
	  ~Punto() {
		  cout << "Destructor: Punto(" << x << ", " << y << ") destruido." << endl;
	  }
	  // Método para imprimir valores
	  void imprimir() {
		  cout << "Punto(" << x << ", " << y << ")" << endl;
	  }
};
int main() {
	// Coloca un breakpoint en la siguiente línea
	Punto p(10, 20);
	// Muestra el contenido del objeto
	p.imprimir();
	// Utiliza el depurador para inspeccionar 'p', observa la dirección de memoria y el valor de x e y.
	return 0;
}
```
Compilación y ejecución
 
 
Actividad 7 — Objetos en stack vs. objetos en heap
```
Ubicación: Unidad 2/Sesion 3/Actividad 7
Qué hace el código
Crea un objeto Punto en el stack (pStack) y otro en el heap con new (pHeap, accedido mediante un puntero). Se libera manualmente pHeap con delete. La diferencia clave: pStack se destruye solo al salir de main(); pHeap solo se destruye si el programador llama a delete explícitamente (si se olvida, hay fuga de memoria).
#include <iostream>
using namespace std;
class Punto {
public:    int x;    int y;
      // Constructor
      Punto(int _x, int _y) : x(_x), y(_y) {
          cout << "Constructor: Punto(" << x << ", " << y << ") creado." << endl;
      }
      // Destructor
      ~Punto() {
          cout << "Destructor: Punto(" << x << ", " << y << ") destruido." << endl;
      }
      // Método para imprimir valores
      void imprimir() {
          cout << "Punto(" << x << ", " << y << ")" << endl;
      }
};
int main() {
    // Objeto en el stack
    Punto pStack(30, 40);
    pStack.imprimir();
    // Objeto en el heap
    Punto* pHeap = new Punto(50, 60);
    pHeap->imprimir();
    // Coloca breakpoints en la creación de pStack y pHeap
    // Inspecciona las direcciones de memoria de ambos objetos:
    // - pStack: dirección obtenida directamente.
    // - pHeap: la variable pHeap es un puntero que contiene la dirección del objeto en el heap.
    // Recuerda liberar la memoria del heap
    delete pHeap;
    return 0;
}
Compilación y ejecución
 
Actividad 8 — Paso de objetos por valor (copias temporales)
Ubicación: Unidad 2/Sesion 3/Actividad 8
Qué hace el código
La función cambiarNombre(Punto p, string nuevoNombre) recibe el objeto Punto por valor, es decir, trabaja sobre una copia temporal. Cambia el nombre de esa copia, pero el objeto 'original' en main() permanece intacto. Al terminar la función, la copia temporal se destruye (se ve el destructor extra en la salida).
#include <iostream>
#include <string>
using namespace std;
class Punto {
public:   string name;
	  int x;
	  int y;
	  // Constructor
	  Punto(string _name, int _x, int _y) : name(_name), x(_x), y(_y) {
		  cout << "Constructor: Punto " << name << " (" << x << ", " << y << ") creado." << endl;
	  }
	  // Destructor
	  ~Punto() {
		  cout << "Destructor: Punto " << name << "(" << x << ", " << y << ") destruido." << endl;
	  }
	  // Método para imprimir valores
	  void imprimir() {
		  cout << "Punto " << name << "(" << x << ", " << y << ")" << endl;
	  }
};
void cambiarNombre(Punto p, string nuevoNombre) {
	p.name = nuevoNombre;
}
int main() {    // Objeto original
	Punto original("original", 70, 80);
	original.imprimir();
	cambiarNombre(original, "cambiado");
	original.imprimir();
	return 0;
}
```
Compilación y ejecución
 
Actividad 9 — Miembros estáticos (compartidos entre instancias)
```
Ubicación: Unidad 2/Sesion 4/Actividad 9
Qué hace el código
La clase Contador tiene un atributo de instancia 'valor' y un atributo static 'total', compartido por todos los objetos de la clase (una sola copia en memoria, no una por objeto). Cada vez que se construye un Contador, 'total' se incrementa. Se crean c1, c2 (en el stack) y c3 (dinámico, con new), y se observa cómo 'total' refleja el conteo global.
#include <iostream>
using namespace std;
class Contador {
public:   int valor;
      static int total;
      // Constructor
      Contador(int v = 0) : valor(v) {
          total++;
          cout << "Contador creado. total de Contadores = " << total << endl;
      }
      // Destructor
      ~Contador() {
          cout << "Contador destruido. valor = " << valor << endl;
      }
      // Método para incrementar el contador de instancia
      void incrementar() {
          valor++;
      }
};
// Definición e inicialización del miembro estático
int Contador::total = 0;
int main() {
    // Crea varios objetos en el stack
    Contador c1(5);
    Contador c2(10);
    // Inspecciona con el depurador las direcciones de c1 y c2.
    // Observa que 'total' es compartido entre todos los objetos.
    c1.incrementar();
    c2.incrementar();
    cout << "c1.valor = " << c1.valor << endl;    cout << "c2.valor = " << c2.valor << endl;
    cout << "Contador::total = " << Contador::total << endl;
    // Puedes también crear un objeto dinámico para comparar:
    Contador* c3 = new Contador(15);
    c3->incrementar();
    cout << "c3->valor = " << c3->valor << endl;
    // Coloca breakpoints en la creación de cada objeto y en las llamadas a 'incrementar()'
    // Observa cómo el miembro estático 'total' se comparte y no se almacena en el stack de cada objeto.
    delete c3;
    return 0;
}
```
Compilación y ejecución
 

