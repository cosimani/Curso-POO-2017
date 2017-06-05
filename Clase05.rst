.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 05 - POO 2017
===================
	
**Ejemplo:** Control de volumen

.. code-block:: c

	#include <QApplication>
	#include <QWidget>
	#include <QHBoxLayout>
	#include <QSlider>
	#include <QSpinBox>

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);

	    QWidget* ventana = new QWidget;  // Es la ventana padre (principal)
	    ventana->setWindowTitle("Volumen"); 
	    ventana->resize(300, 50);

	    QSpinBox* spinBox = new QSpinBox;
	    QSlider* slider = new QSlider(Qt::Horizontal);
	    spinBox->setRange(0, 100);
	    slider->setRange(0, 100);

	    QObject::connect(spinBox, SIGNAL(valueChanged(int)), slider, SLOT(setValue(int)));
	    QObject::connect(slider, SIGNAL(valueChanged(int)),  spinBox, SLOT(setValue(int)));

	    spinBox->setValue(15);

	    QHBoxLayout* layout = new QHBoxLayout;
	    layout->addWidget(spinBox);
	    layout->addWidget(slider);
	    ventana->setLayout(layout);
	    ventana->setVisible(true);	

	    return a.exec();
	}

**Ejercicio 3**
^^^^^^^^^^^^^^^

- Cuando el valor del QSlider se modifique, colocar como título de la ventana el mismo valor (de 0 a 100). 
	
QLineEdit
^^^^^^^^^

.. code-block:: c

	QLineEdit* le = new QLineEdit;
	le->setEchoMode(QLineEdit::Password);
	le->setEnabled(false);

	// QLineEdit::Normal  // Se visualizan al escribir
	// QLineEdit::NoEcho  // No se visualiza nada
	// QLineEdit::Password  // Se escribe como asteriscos
	// QLineEdit::PasswordEchoOnEdit  // Se escribe normal y al dejar de editar	se convierten en asteriscos

**Señales**

.. code-block:: c

	// void returnPressed()  // Detecta cuando el usuario presiona Enter.

	// void editingFinished()  // Cuando pierde foco.

	// void textChanged(const QString &text)  // Texto modificado por código o por usuario desde la interfaz.

	// void textEdited(const QString &text)  // Sólo por el usuario.

QGridLayout
^^^^^^^^^^^

- Ubica los widgets en una grilla
- Con setColumnMinimumWidth() podemos setear el ancho mínimo de columna
- Separación entre widget con setVerticalSpacing(int)
- void addWidget(QWidget* widget, int fila, int columna, int spanFila, int spanCol)

Macro Q_OBJECT
^^^^^^^^^^^^^^

- Convierte a una clase cualquiera en una clase Qt.
- Una clase Qt permitirá trabajar con signals y slots.
- Con la macro Q_OBJECT en la declaración de la clase la convertimos.

**Ejercicio 4**
^^^^^^^^^^^^^^^

- Construir un login.
- Usar asteriscos para la clave.
- Detectar enter para simular la pulsación del botón.
- Si la clave ingresada es admin:admin, la aplicación se cerrará.
- Si se ingresa otra clave se borrará el texto de los QLineEdit.

- Tener en cuenta que este ejercicio requiere conocer cómo se define un slot propio.

QGridLayout
^^^^^^^^^^^

- Ubica los widgets en una grilla
- Con setColumnMinimumWidth() podemos setear el ancho mínimo de columna
- Separación entre widget con setVerticalSpacing(int)
- void addWidget(QWidget* widget, int fila, int columna, int spanFila, int spanCol)





