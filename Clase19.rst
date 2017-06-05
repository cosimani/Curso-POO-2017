.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 19 - POO 2017
===================

Uso de la Clase QGLWidget
^^^^^^^^^^^^^^^^^^^^^^^^^

- Se requiere lo siguiente en el .pro

.. code-block:: c

	QT += opengl

	win32:LIBS += -lopengl32
	win32:LIBS += -lglu32
	
	unix:LIBS += -lGLU

.. code-block:: c

	#include <QGLWidget>

	class MiOpenGL : public QGLWidget  {
	    Q_OBJECT
		
	public:
	    MiOpenGL();

	protected:
	    void initializeGL();	
	    void resizeGL(int w, int h);
	    void paintGL();
	};
	
	MiOpenGL::MiOpenGL()  {
	
	}

	void MiOpenGL::initializeGL()  { 
	    glClearColor(0,0,0,0);
	}

	void MiOpenGL::resizeGL(int w, int h)  {
	    // Porción de ventana donde puede dibujar.
	    glViewport(0, 0, w, h);

	    // Especifica la matriz actual: matriz de proyección (GL_PROJECTION), matriz de modelo
	    // (GL_MODELVIEW) y matriz de textura (GL_TEXTURE). 
	    glMatrixMode(GL_PROJECTION);

	    // Con esto cargamos en el "tipo" de matriz actual (matriz identidad - como resetear).
	    // Es una matriz 4x4 llena de ceros salvo la diagonal que contiene unos. 
	    glLoadIdentity();

	    // Para delimitar la zona de trabajo en una caja.
	    glOrtho(-1, 1, -1, 1, -1, 1);

	    // Se vuelve a este tipo de matrices, que afecta a las primitivas geométricas.
	    glMatrixMode(GL_MODELVIEW);
	}

	void MiOpenGL::paintGL()  {
	    // Borra un buffer.
	    glClear(GL_COLOR_BUFFER_BIT);

	    //  Carga la matriz identidad.
	    glLoadIdentity();

	    // Acá se inserta el código para dibujar 

	    // Volcamos en pantalla lo que se creó en memoria.
	    glFlush();
	}

**Ejercicio 30**

- Dibujar un triángulo en el plano ``z=-50``
- Utilizar el teclado para que al presionar la tecla C, el triángulo cambie de color.

Rotación de la escena
^^^^^^^^^^^^^^^^^^^^^

- Gira un ángulo en sentido contrario a las agujas del reloj.
- Sobre el eje formado desde el origen hasta el punto (x, y, z).

.. code-block:: c

	// glRotatef(angulo, x, y, z); 
	glRotatef(5, 0, 0, 1);  // gira 5° con respecto al eje z

Traslación de la escena
^^^^^^^^^^^^^^^^^^^^^^^

- Desplaza el punto (0, 0, 0) a la nueva posición (x, y, z).

.. code-block:: c

	// glTranslatef(x, y, z);
	glTranslatef(2, 0, 0);  // Desplaza 2 unidades en el eje x

Escalado de la escena
^^^^^^^^^^^^^^^^^^^^^

- Escala. Con valores mayores a 1, se amplía. Entre 0 y 1 se reduce.

.. code-block:: c

	// glScalef(x, y, z);
	glScalef(1, 2, 1);  // escala el doble en vertical
	
Objetos ocultos
^^^^^^^^^^^^^^^

- En 3D un objeto puede estar detrás de otro.
- Por defecto, OpenGL no tiene en cuenta esto. Pinta siguiendo el orden en el código fuente,.
- El siguiente código no se vería muy real:

.. code-block:: c

	glColor3f(0, 1, 0);
	glBegin(GL_TRIANGLES);
	    glVertex3f(-5, -5, 5);
	    glVertex3f(0, 0, 0);
	    glVertex3f(5, -5, 5);
	glEnd();

	glColor3f(0, 0, 1);
	glPointSize(5);
	glBegin(GL_POINTS);
	    glVertex3f(0, -1, 0);
	    glVertex3f(0, -2, 5);
	glEnd();

- Para solucionar activamos el buffer de profundidad

.. code-block:: c

	glEnable(GL_DEPTH_TEST); 

- Cada vez que se renderiza la escena, limpiamos la pantalla

.. code-block:: c

	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

Seguimiento continuo del mouse
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Al usar ``mouseMoveEvent`` ¿por qué sólo se sigue al mouse al presionar un botón?

.. code-block:: c

	setMouseTracking(bool enable)

- Es un método de la clase QWidget
- Activa el seguimiento continuo del mouse sobre un QWidget.
- Por defecto se encuentra desactivado.
- Cuando está desactivado sólo se reciben los eventos del movimiento del mouse cuando al menos se presiona un botón del mismo.

**Ejercicio 31**

- Dibujar un cajón deforme sin tapa con un color distinto en cada lado.
- Utilizar el teclado para hacerlo rotar sobre los tres ejes.







