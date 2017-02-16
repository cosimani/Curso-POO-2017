.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 15 - POO 2016
===================

Enumeraciones
^^^^^^^^^^^^^

- Es un tipo especial de variable
- Sus valores son constantes enteras
- Estos valores pueden ser autogenerados (0, 1, 2, 3, ...)

.. code-block:: c	

	enum los_dias { DOM, LUN, MAR, MIE, JUE, VIE, SAB } dia;

	enum los_dias { DOM = 7, LUN = 1, MAR, MIE, JUE = 0, VIE, SAB };

- Las variables de este tipo pueden adoptar sólo valores DOM, LUN, ...
- Es decir, la variable "dia" puede tomar DOM o LUN o MAR ...
- Las enumeraciones declaradas dentro de una clase tiene la visibilidad de la clase

.. code-block:: c	

	class Dia  {
	public:
	    enum los_dias { LUN, MAR, MIE, JUE, VIE };
	    int un_dia;
	};

	int main(int argc, char** argv)  {
	    Dia d1;
	    d1.un_dia = Dia::LUN;
	}

const
.....

- Una variable definida como const no podrá ser modificada a lo largo del programa (se crea como sólo lectura)
- Se puede aplicar a cualquier tipo:

.. code-block:: c	

	const float pi = 3.14;
	const peso = 67;	// Si no se indica el tipo entonces es int
					    // Ojo: Sólo en compiladores viejos


const con punteros
^^^^^^^^^^^^^^^^^^

.. code-block:: c	

	int x = 10;
	int* px = &x;		// normal

	const int y = 10;
	int* py = &y;	// El compilador dirá: "invalid conversion from const int*
					// to int*". La inversa sí se permite

	int y = 10;
	const int* py = &y;	// permitido (pero el contenido es de sólo lectura)

	*py = 6;  // No permitido. El contenido apuntado es de sólo lectura


const en parámetros de funciones
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Cuando los parámetros son punteros, decimos que no podrá modificar los objetos referenciados

.. code-block:: c	

	int funcion(const char* ch)

- Lo mismo sucede con referencias

.. code-block:: c	

	int funcion(const char& ch)

const en clases
^^^^^^^^^^^^^^^

.. code-block:: c	

	class ClaseA  {
	    const int i;
	    int x;

	public:
	    int funcion(ClaseA cA, const ClaseA &c)  {
	        cA.x = 1;
	        cA.i = 2;  // No compila. i es de sólo lectura.
	        c.x = 3;  // No compila. El objeto c es de sólo lectura.

	        return cA.x;
	    }
	}; 

.. code-block:: c	

	// A la variable i sólo la puede inicializar el constructor y sólo con la forma:
	ClaseA() : i(8)  {  }   

	// Si en el cuerpo del constructor se hace:
	ClaseA()   { 
	    i = 8;  // Compila? i es de solo lectura o no
	}   

- Aplicado a métodos de una clase no permite modificar ninguna propiedad de la clase

.. code-block:: c	

	class ClaseB  {
	    int x;

	    void funcion(int i) const  {
	        x = x + i;  // Compila?
	    }
	};

Clase QFileDialog
^^^^^^^^^^^^^^^^^

- Permite abrir un cuadro de diálogo para buscar un archivo en disco

.. code-block:: c	

	QString file = QFileDialog::getOpenFileName(this, "Abrir", "./", "Imagen (*.png *.jpg)");

**Ejercicio:**

- Elegir un archivo de imagen del disco con ``QFileDialog`` y dibujarlo en un ``QWidget``.
- Agregar un botón "Iniciar rotación" que genere la rotación de la imagen sobre su centro.




