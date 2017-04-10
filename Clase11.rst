.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 11 - POO 2016 (No preparada aún)
===================


	
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

