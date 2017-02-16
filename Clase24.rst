.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 24 - POO 2016
===================

Funciones inline
================

- Cuando decimos que llamamos a una función es porque salta, ejecuta y retorna.
- Una función inline inserta su código.
- Ventaja de ejecutarse más rápidamente.
- Como desventaja tenemos un programa generado más extenso.

.. code-block:: c

	#include <QDebug>
	#include <QApplication>

	inline int calculo(int a, int b)  {
	    return a/2+b;
	}

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);

	    int x=2, y=3, z=0;
	    z = calculo(x, y);

	    return 0;
	}

**Funciones miembro inline dentro de clases**

- Un método se declara dentro del cuerpo de la clase y se puede definir dentro o fuera
- Si se declara y define dentro, se denomina función inline. En este caso, no hace falta indicar con inline (está implícito).
- Si se define fuera, deberá indicar inline. De lo contrario será offline.
- Se recomienda usar funciones inline para funciones pequeñas y de uso frecuente.

.. code-block:: c

	#include <QDebug>
	#include <QApplication>

	class ClaseA  {
	private:
	    int x;
	    int y;

	public:
	    ClaseA() : x(10), y(20)  {  }
	    int getX()  {  return x;  }     // inline implícito
	    int getY();
	};

	inline int ClaseA::getY()  {
	    return y;
	}

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);

	    ClaseA cA;
	    qDebug() << cA.getX();
	    qDebug() << cA.getY();

	    return 0;
	}
	
MiniExámenes
============

- Sin clases: 10 de junio (Expotrónica)
- Última semana (21 y 24 de junio) para recuperatorios y coloquios
- Se promediarán para la tercer nota de POO
- MiniExámenes previstos: Jun 14
- Tiempo: 30 minutos 
- Temas para el 14 de junio: 
	- Enumeraciones
	- Señales propias
	- const
	- QFile y QFileDialog
	- Dibujar con QPainter en paintEvent

	





