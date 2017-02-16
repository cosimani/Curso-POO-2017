.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 02 - POO 2016
===================

Utilidades de la biblioteca estándar de C++
===========================================

vector
^^^^^^

- Mantiene sus elementos en un área contigua de memoria.
- El acceso aleatorio es eficiente.
- La inserción en cualquier posición distinta a la última es ineficiente.
- Se encuentra en #include <vector> en el namespace std

.. code-block:: c

	vector<int> v1;    // vector vacío
	vector<int> v2(15);    // vector de 15 elementos
	vector<string> v3(18, "cadena");    // 18 elemento con valor inicial
	vector<string> v4(v3);    // v4 es una copia v3

**Algunas operaciones**

.. code-block:: c

	size()    // Tamaño
	bool empty()    // Está vacío?
	void clear()    // Limpia el vector
	front()    // Acceso al primero
	back()    // Al último
	push_back(x)    // Inserción al último
	pop_back()    // Elimina
	w = v    // Asignación
	v == w    v < w    // Comparaciones
	v.at(i)    // Acceso con verificación de rango (lanza out_of_range)
	v[i]    // Acceso sin verificación de rango

Cadena de caracteres
^^^^^^^^^^^^^^^^^^^^

- Al estilo C	

.. code-block:: c

	#include <string.h>

	char cadena1[30], cadena2[30];
	strcpy(cadena1, "Hola");
	cin >> cadena2;
	
- Con C++ usamos   

.. code-block:: c

	#include<string>

	Asignación			s1 = s2		s1 = "Hola"
	Concatenación		s1 = s2 + s3	
	Comparación			if (s1 == s2)
	Subcadenas			s1.substr(3, 5)
	Longitud			s1.length()	s2.size()  // Son lo mismo
	Acceso a char		s1[2]			s2.at(2)  // Lanza out_of_range
	Limpiar				s1.clear()
	Busca cadena		s1.find("cadena");    s1.find(s2);
	Puntero a char		const char *c = s1.c_str()

**Ejercicio:**

- Crear un vector de 100 números enteros.
- Los valores serán aleatorios y positivos menores o iguales a 10.
- Utilizar un algoritmo para ordenar de menor a mayor estos números.

Clases
======

.. code-block:: c

	class ClaseEjemplo  {
	    // Lista de miembros (generalmente funciones y datos)
	    // Los datos no pueden ser inicializados (es una declaración)
	    // Si las funciones se definen fuera, se usa el operador :: 
	    // :: es el operador de acceso a ámbito
	};

**Ejemplo:**

.. code-block:: c

	#include <iostream>
	using namespace std;

	class Punto  {
	private:
	    // Datos miembro de la clase "Punto"
	    int a, b;
		
	public:
	    // Funciones miembro de la clase "Punto"
	    void getDatos(int &a2, int &b2);
	    void setDatos(int a2, int b2)  {
	        a = a2;
	        b = b2;
	    }
	};

	void Punto::getDatos(int &a2, int &b2)  {
	    a2 = a;
	    b2 = b;
	}

	int main()  {
	    Punto punto1;
		int x, y;  // Variables donde se copiarán los valores de punto1

	    punto1.setDatos(12, 32);
	    punto1.getDatos(x, y);

	    cout << "(" << x << “, ” << y << “)” << endl;
	}
	
	// La función "setDatos()" se definió en el interior de la clase (lo haremos sólo cuando
	// la definición sea muy simple, ya que dificulta la lectura y comprensión del programa). 

**Constructor**

.. code-block:: c

	class Punto  {
	public:
	    Punto(int a2, int b2);

	    void getDatos(int &a2, int &b2);
	    void setDatos(int a2, int b2);
		
	private:
	    // Datos miembro de la clase "Punto"
	    int a, b;
	};

	Punto::Punto(int a2, int b2)  {
	    a = a2;
	    b = b2;
	}

	void Punto::getDatos(int &a2, int &b2)  {
	    a2 = a;
	    b2 = b;
	}

	void Punto::setDatos(int a2, int b2)  {
	    a = a2;
	    b = b2;
	}

**Cuestiones sobre declaraciones**

.. code-block:: c

	Punto punto1;  // Llama al constructor sin parámetros. En esta última versión 
	               // de Punto, esto no serviría, ya que no hay constructor sin parámetros. 
				   // Si no se especifica un constructor, el compilador crea uno (igual que 
				   // en Java). Por lo tanto, esta declaración sirve para una clase Punto 
				   // donde el programador no escriba constructor.

	Punto punto1();  // Se entiende como el prototipo de una función sin parámetros que 
	                 // devuelve un objeto Punto. Es decir, no sirve para instanciar un 
					 // objeto con el contructor sin parámetros de Punto.

	Punto punto1(12,43);  // Válido
	Punto punto2(45,34);  // Válido


**Inicialización de objetos**

.. code-block:: c

	Punto(int a2, int b2)  {
	    a = a2;
	    b = b2;
	}

	// O también se permite:

	Punto::Punto(int a2, int b2) : a(a2), b(b2)  {  }

	Punto::Punto() : a(0), b(0)  {  }

**El puntero this**

.. code-block:: c

	#include <iostream>
	using namespace std;

	class Punto  {
	public:
	    // Constructor
	    Punto(int a2, int b2)  {  }
	
	    // Funciones miembro de la clase "Punto"
	    void getDatos(int &a2, int &b2)  {  }
	    void setDatos(int a2, int b2);
	
	private:
	    // Datos miembro de la clase "Punto"
	    int a, b;
	};

	void Punto::setDatos(int a2, int b2) {
	    a = a2;
	    b = b2;
	}

	// O lo podemos hacer con this:

	void Punto::setDatos(int a2, int b2) {
	    this->a = a2;
	    this->b = b2;
	}


**Constructores con argumentos por defecto**

.. code-block:: c

	class ClaseA  {
	public:
	    ClaseA(int a = 10, int b = 20) : a(a), b(b)  {  }
	
	    void verDatos(int &a, int &b)  {
	        a = this->a;
	        b = this->b;
	    }

	private:
	    int a, b;
	};

	int main(int argc, char** argv)  {
	    ClaseA* objA = new ClaseA;

	    int a, b;
	    objA->verDatos(a, b);
	
	    std::cout << "a = " << a << " b = " << b << std::endl;

	    return 0;
	}

	// Probar con:	
	
	ClaseA(int c, int a = 10, int b = 20) : a(a), b(b), c(0)  {  }

	ClaseA(int a = 10, int b = 20, int c) : a(a), b(b), c(0)  {  }

**Destructor**

.. code-block:: c

	ClaseA::~ClaseA()  {
	    a = 0;
	    b = 0;
	}
