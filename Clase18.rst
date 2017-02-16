.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 18 - POO 2016
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

Uso de una clase propia con QtDesigner
======================================

- Deben heredar de algún QWidget
- Colocamos el widget (clase base) con QtDesigner
- Clic derecho "Promote to"

.. figure:: images/clase18/qtdesigner.png
					 
- Base class name: QLabel
- Promoted class name: MiLabel
- Header file: miLabel.h
- Add (y con esto queda disponible para promover)
- La clase MiLabel deberá heredar de QLabel
- El constructor debe tener como parámetro:

.. code-block::

	MiLabel(QWidget *parent = 0);  // Esto en miLabel.h

	MiLabel::MiLabel(QWidget *parent) : QLabel(parent)  {  // Esto en miLabel.cpp
	
	}

**Ejercicio:**
	- Definir la clase TuLabel que herede de QLabel
	- Agregar un QLabel a la GUI y promoverlo a TuLabel
	- Agregar un método void cambiarTexto(QString nuevoTexto)
	- Usar ese método desde la clase Principal de la siguiente forma:

.. code-block::

	ui->tuLabel->cambiarTexto("Sos un TuLabel?");
	
**Ejercicio:** 

- Crear un login con la clase TuLabel que herede de QLabel y que funcione como un QPushButton
- Para esto incorporar a TuLabel la señal ``void signal_clic()``







