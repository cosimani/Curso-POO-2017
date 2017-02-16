.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 05 - POO 2016
===================

QGridLayout
^^^^^^^^^^^

- Ubica los widgets en una grilla
- Con setColumnMinimumWidth() podemos setear el ancho mínimo de columna
- Separación entre widget con setVerticalSpacing(int)
- void addWidget(QWidget* widget, int fila, int columna, int spanFila, int spanCol)

QGroupBox
^^^^^^^^^ 

.. figure:: images/clase05/qgroupbox.png

.. code-block:: c

	QGroupBox* grupo = new QGroupBox("Texto");
	QGridLayout* layout = new QGridLayout;
	
	layout->addWidget(label, 0, 0);
	layout->addWidget(usuario, 1, 0, 1, 2);
	layout->addWidget(clave, 2, 0, 1, 2);
	
	grupo->setLayout(layout);

**Ejercicio:**

- Utilizar el login del ejercicio anterior en un proyecto nuevo.
- Definir la clase Formulario que será un QWidget
- Formulario tendrá QLabels y QLineEdits para Legajo, Nombre y Apellido y un QPushButton
- Si la clave ingresada es admin:1111, se cierra Login y se muestra Formulario



