.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 06 - POO 2016
===================

Sutilezas con punteros
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char cadena[10] = "hola";  
	// Funciona? sí. Qué hace con el sobrante?
	// Los completa a todos con \000

	char cadena[4] = "hola";   // Por qué no compila?

	char cadena[5] = "hola";   // Y por qué esto sí compila?

	// Porque la última posición se usa para el carácter nulo que el
	// compilador lo agrega (si tiene lugar).

	//    \000  (octal)
	//    \x0   (hexadecimal)    

Usando puntero para cadenas
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char* cadena = "hola";      // el compilador agrega \000
	char* cadena = "ho\000la";  // Imprime  ho

- Asignamos memoria dinámicamente.
- No necesitamos especificar la longitud máxima.

Notación octal y hexadecimal
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	cout << 3 + 4 + 11;      // Imprime 18
	cout << 3 + 4 + 011;     // ?

	//    octal    hexadecimal    decimal
	//    0121     0x51           81
	//    011      0x9            9
	//    '\000'   '\x0'          nulo
	//    '\063'   '\x33'         carácter 3

Punteros a punteros
^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char cadena[2][3];
	cadena[0][0] = 'f';
	cadena[0][1] = 'u';
	cadena[0][2] = 'e';
	cadena[1][0] = 'f';
	cadena[1][1] = 'u';
	cadena[1][2] = 'i';

	//    Mejor así

	char cadena[2][3];
	cadena[0][0] = 's';
	cadena[0][1] = 'i';
	cadena[0][2] = '\000';
	cadena[1][0] = 'n';
	cadena[1][1] = 'o';
	cadena[1][2] = '\000';
 
Array ≡ puntero
^^^^^^^^^^^^^^^

- Cuando declaramos un array
- Estamos declarando un puntero al primer elemento.

.. code-block:: c

	char arreglo[5];
	char* puntero;
	puntero = arreglo;  // Equivale a puntero = &arreglo[0];

Volviendo a puntero a puntero
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char cadena[2][3] = {{'s', 'i', '\000'}, {'n', 'o', '\000'}};
	// Y si fuera char cadena[2][3] = {{'s', 'i', '-'}, {'n', 'o', '\000'}};
	char* p1;
	char* p2;

	p1 = cadena[0];   // p1 = &cadena[0][0];
	p2 = cadena[1];   // p2 = &cadena[1][0];

	cout << p1;  // si  
	cout << p2;  // no
	
	cout << *p1;  // ?
	cout << *p2;  // ?

	// Es decir:
	//    El identificador de un arreglo unidimensional 
	//    es considerado un puntero a su primer elemento.

**Ejemplo**

.. code-block:: c

	char p1[] = {'a', 'b', 'c', 'd', 'e'};
	cout << "Letra " << *p1;   // Letra a
	cout << "Letra " << p1[0];   // Letra a

	char m2[][5] = {{'a', 'b', 'c', 'd', 'e'}, {'A', 'B', 'C', 'D', 'E'}};
	cout << "Letra " << **m2;          // Letra a
	cout << "Letra " << m2[0][0];      // Letra a
	cout << "Letra " << m2[1][3];      // Letra D
	cout << "Letra " << *(*(m2+1)+3);  // Letra D

**Extendiendo a arreglos de cualquier dimensión**

.. code-block:: c

	m[a] == *(m+a)
	m[a][b] == *(*(m+a)+b)
	m[a][b][c] == *(*(*(m+a)+b)+c)

	//    Si nos referimos al primer elemento

	m[0] == *m
	m[0][0] == **m
	m[0][0][0] == ***m

QByteArray
^^^^^^^^^^

- Se podría decir que es administrador de un char*
- Se puede usar el operador []
- Almacena \000 al final de cada objeto QByteArray

QTextEdit
^^^^^^^^^

- Un QWidget que muestra texto plano o enriquecido
- Puede mostrar imágenes, listas y tablas
- La barra de desplazamiento es automática
- Interpreta tags HTML
- Seteamos texto con setPlainText()

**Ejercicio:**

- Crear una aplicación que inicie con un login validando el usuario admin:123
- Luego de ingresar el usuario válido, mostrar un nuevo QWidget con las siguientes características:
	- Definida en la clase Editor
	- Contendrá un QTextEdit vacío, un QPushButton "Buscar" y un QLabel
	- El usuario podrá escribir cualquier texto en el QTextEdit
	- Al presionar "Buscar" se detectará automáticamente la cantidad de letras 'a' en el texto y colocará el resultado en el QLabel.
- Luego de dejar funcionando lo anterior, agregar lo siguiente:
	- Un QLineEdit y un QPushButton "Borrar"
	- En este QLineEdit el usuario puede colocar una palabra o frase
	- Al presionar Borrar se buscará en el texto y se eliminarán


