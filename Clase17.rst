.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 17 - POO 2016
===================

Señales propias
^^^^^^^^^^^^^^^

- Si necesitamos enviar una señal se utiliza la palabra reservada ``emit``.

.. code-block:: c	

	int i = 5;
	emit signal_enviarEntero(i);

- La función ``enviarEntero(int a)`` debe estar declarada con el modificador de acceso ``signals``

.. code-block:: c	

	signals:
	    void signal_enviarEntero(int);

- No olvidarse de la macro ``Q_OBJECT`` para permitir a esta clase usar signals y slots.
- Las signals deben ser compatibles en sus parámetros con los slots a los cuales se conecten.
- Solamente se declara esta función (Qt se encarga de definirla).

**Ejercicio:** 

- Crear un login con un QLabel que funcione como un QPushButton
- Para esto incorporar al QLabel la señal ``void signal_clic()``

**Ejercicio:** 

- Incorporar a un Login una señal que se emita cada vez que un usuario se valide exitosamente
- Que la señal se llame ``void signal_usuarioLogueado(QString)``
- El QString que envía es el nombre de usuario




