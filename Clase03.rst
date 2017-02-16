.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 03 - POO 2016
===================

Punteros
========

**Declaración**

.. code-block:: c

	int* entero;     // entero es un puntero a int
	char* caracter;  // puntero a char

	entero 	es el puntero
	*entero 	es el contenido


**Punteros a variables**

.. code-block:: c

	int entero;         // entero es una variable int
	int* pEntero;       // pEntero es un puntero a int
	pEntero = &entero;  // &entero es la dirección de memoria donde se almacena entero

**Arrays y punteros**

.. code-block:: c

	int miArray[10];	// miArray es como un puntero al primer elemento
	int* puntero;

	puntero = miArray;  // similar a:  puntero = &miArray[0];
	(*puntero)++;       // equivale a miArray[0]++;  // incrementa
	puntero++;          // equivale a &miArray[1];  // se mueve una posición

	puntero = puntero + 3;  // se desplaza 3 posiciones int

**Array como parámetro en funciones**

.. code-block:: c

	#include <iostream>
	using namespace std;

	void funcion(int miArray[]);
	// Le estamos pasando un puntero al primer elemento del array.

	int main()  {
	    int miA[5] = {0, 1, 2, 3, 4};

	    funcion(miA);

	    cout << miA[0] << miA[1] << miA[2] << miA[3] << miA[4];
	}

	void funcion(int miArray[])  {
	    miArray[0] = 5;  // Las modificaciones quedarán.

	    miArray[3] = 5; 
	} 

**Ejercicio:** Escribir la salida por consola de la siguiente aplicación:

.. code-block:: c

	#include <QApplication>
	#include <QDebug>

	int main(int argc, char** argv)  {
	    QApplication app(argc, argv);

	    int a = 10, b = 100, c = 30, d = 1, e = 54;
	    int m[10] = {10, 9, 80, 7, 60, 5, 40, 3, 20, 1};
	    int *p = &m[3], *q = &m[6];

	    ++q;
	    qDebug() << a + m[d/c] + b-- / *q + 10 + e--;

	    p = m;
	    qDebug() << e + *p + m[9]++;

	    return 0;
	}

**Función con número indefinido de parámetros**

- Requiere:

.. code-block:: c

	#include <cstdarg>

- Imprime los enteros que se pasen como parámetro
- Se puede comprender la sintaxis de:

.. code-block:: c

	int printf(const char* format, ...)

.. code-block:: c

	void imprimirParametros(int cantidad, ...)  {

	    // En cstdarg se define un tipo va_list y define tres macros (va_start, va_arg y va_end)
	    // para moverse por la lista de argumentos cuyo numero y tipo no son conocidos.

	    // Aqui se declara la lista de parametros
	    va_list argumentos; 
				
	    // La macro va_start inicializa 'argumentos' para ser usado por va_arg y va_end.
	    // 'cantidad' es el nombre del ultimo parametro antes de la lista de argumentos.
	    va_start(argumentos, cantidad); 

	    for (int i=0 ; i<cantidad ; i++)  {

		    // La macro va_arg contiene el tipo y el valor del proximo argumento. 
			// Cada llamada a va_arg devuelve el resto de los argumentos.

	        int valor = va_arg( argumentos, int );  // Devuelve en formato de int

	        cout << valor << endl;
	    }

	    // A cada invocacion de va_start le corresponde una invocacion de va_end
	    // en la misma funcion. 	   
	    va_end(argumentos);  // Para limpiar la pila de parametros
	}
	
**Ejercicio:** 

- Definir una función (que se llame mi_printf) que realice el mismo trabajo que la famosa printf. 
- Investigar qué tipos de datos se pueden utilizar en va_arg

.. ..

 <!---  
 - Se puede pasar cualquier tipo siempre que sea con punteros:
 
 #include <QApplication>
 #include <QString>
 #include <QDebug>
 #include <cstdarg>

 void imprimirParametros(int cantidad, ...)  {
     va_list argumentos; // esta linea declara la lista de parametros
     va_start(argumentos, cantidad);

     for (int i=0 ; i<cantidad ; i++)  {
         QString *str = va_arg( argumentos, QString* );
         qDebug() << *str;
     } 

     va_end(argumentos);  // Para limpiar la pila de parametros
 }
 
 int main(int argc, char** argv)  {
     QApplication app(argc, argv);
 
     imprimirParametros(3, new QString("uno"), new QString("dos"), new QString("tres"),
                        new QString("cuatro"), new QString("cinco"));

     return 0;
 }

 --->
 
 


.. code-block:: c
	
	int printf(const char* format, ...)

Primer aplicación en Qt con interfaz gráfica
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Qt(Quasar Toolkit) 
	- Biblioteca para desarrollo de software de Quasar Technologies
	- Se llamó también Trolltech
	- Biblioteca multiplataforma
	- En el 2008 lo compró Nokia
	- Aplicaciones escritas con C++ (Qt)
		- KDE
		- VLC Media Player
		- Skype
		- VirtualBox
		- Google Earth 
		- Spotify para Linux
	- En 2012 Digia compra Qt y comercializa las licencias 
	- Digia desarrolló herramientas para usar Qt en iOS, Android y Blackberry.
		
.. code-block:: c

	#include <QApplication>	
	// - Administra los controles de la interfaz
	// - Procesa los eventos
	// - Existe una única instancia
	// - Analiza los argumentos de la línea de comandos

	int main(int argc, char** argv)  {	
	    // app es la instancia y se le pasa los parámetros de la línea
	    // de comandos para que los procese.
	    QApplication app(argc, argv); 

	    QLabel hola("<H1 aling=right> Hola </H1>");
	    hola.resize(200, 100);
	    hola.setVisible(true);

	    app.exec();  // Se le pasa el control a Qt
	    return 0;
	}

Signals y slots
^^^^^^^^^^^^^^^

- signal y slot son funciones.
- Las signals de una clase se comunican con los slots de otra.
- Se deben conectar con la función connect de QObject.
- Un evento puede generar una signal.
- Los slots reciben estas signals.
- SIGNAL() y SLOT() son macros (convierten a cadena).
- emisor y receptor son punteros a QObject:

.. code-block:: c

	QObject::connect(emisor, SIGNAL(signal), receptor, SLOT(slot));
	
- Se puede remover la conexión:

.. code-block:: c

	QObject::disconnect(emisor, SIGNAL(signal), receptor, SLOT(slot));

**Ejemplo:** QPushButton para cerrar la aplicación.

.. code-block:: c

	#include <QApplication>
	#include <QPushButton>

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);
	    QPushButton* boton = new QPushButton("Salir");

	    QObject::connect(boton, SIGNAL(clicked()), &a, SLOT(quit()));
	    boton->setVisible(true);
		
	    return a.exec();
	}

