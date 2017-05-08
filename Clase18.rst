.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 18 - POO 2016 (No preparada aún)
===================

Clase QFile
^^^^^^^^^^^

- Permite leer y escribir en archivos. 
- Puede ser utilizado además con ``QTextStream`` o ``QDataStream``.

.. code-block:: c	

	QFile(const QString & name)
	viod setFile(const QString & name)

- Existe un archivo? y lo eliminamos.

.. code-block:: c	

	bool exists() const
	bool remove()

- Lectura de un archivo línea por línea:

.. code-block:: c	

	QFile file("c:/in.txt");
	if ( !file.open (QIODevice::ReadOnly | QIODevice::Text) )
	    return;

	while ( !file.atEnd() )  {
	    QByteArray linea = file.readLine();
	    qDebug() << linea;
	}

**Ejercicio:**

- Elegir un archivo de texto cualquiera con ``QFileDialog`` y mostrarlo sobre un ``QTextEdit``.
- Agregar dos ``QLineEdit``, uno acompañado con el ``QLabel`` "Buscar" y otro con el "Reemplazar por".
- Un botón "Reemplazar" realizará la busqueda reemplazará todas las coincidencias encontradas.

**Ejercicio:**

- En el ejercicio anterior emitir la señal ``signal_reemplazosFinalizados(int cantidad)`` al finalizar la acción.
- ``int cantidad`` indicará la cantidad de reemplazos realizados, incluyendo el cero si no hubo reemplazos.
- Conectar esta señal con algún slot cualquiera para probar su funcionamiento.

**Ejercicio:**

- Usar QtDesigner
- Definir la clase Ventana que herede de QWidget
- Usar const.
- Buscar una imagen de un fútbol con formato PNG (para usar transparencias).
- Ventana tendrá un formulario que pide al usuario:
	- Diámetro del fútbol (píxeles):
	- Velocidad (mseg para ir de lado a lado):
	- QPushButton para actualizar el estado.
- El fútbol irá golpeando de izquierda a derecha en Ventana.




Clase QWebView
^^^^^^^^^^^^^^

- Es un QWidget que tiene todas las características de un navegador
- Dispone del método load() para cargar un sitio web
- Requiere la inclusión del siguiente módulo 

.. code-block:: c

	QT += webkitwidgets

**Ejercicio:** Diseñar la siguiente interfaz de usuario:

.. figure:: images/clase09/descarga.png 
 
- Mostrar el código fuente del sitio en el QTextEdit
- También incluir un QLabel para indicar el porcentaje de descarga

**Ejercicio:** Navegador - Diseñar la siguiente interfaz de usuario:

.. figure:: images/clase09/navegador.png 

- Utilizar sólo 2 widgets: un QLineEdit y un QWebView (ningún QPushButton)
- Por defecto se cargará la página de Google
- Filtrar el acceso a los dominios terminados en: edu.ar y gov.ar
- Cuando un sitio se haya filtrado mostrar el mensaje "Sitio bloqueado"


.. figure:: images/clase16/imagenes-para-reirse-en-los-examenes.jpg

****

.. figure:: images/clase16/yeah.gif

****

Aplicación para replicar en Primer Parcial
..........................................

Usuario válido: cgomez:123456

- `Ejecutable (Windows 7 o superior - 64 bits) <https://drive.google.com/file/d/0B3bNJFNPgLHnTVd6SGl2cERReWc/view?usp=sharing>`_

- `Ejecutable (Linux - 64 bits) <https://drive.google.com/file/d/0B3bNJFNPgLHneUhiQmNjTFdldkU/view?usp=sharing>`_







