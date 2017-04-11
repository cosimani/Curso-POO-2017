.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 10 - POO 2017
===================

Polimorfismo
^^^^^^^^^^^^

- Lo utilizamos con punteros.
- Nos permite acceder a objetos de la clase derivada usando un puntero a la clase base.
- Sin embargo, sólo podemos acceder a datos y funciones que existan en la clase base.
- Los datos y funciones propias de la derivada quedan inaccesibles.

.. code-block:: c

	class Persona  {
	public:
	    Persona(QString nombre) : nombre(nombre)  {  }
	    QString verNombre()  {  return "Nombre: " + nombre;  }

	protected:  // Para acceso desde las clases derivadas
	    QString nombre;
	};

	class Empleado : public Persona  {
	public:
	    Empleado(QString nombre) : Persona(nombre)  {  }
	    QString verNombre()  {  return "Empleado: " + nombre;  }
	    void mostrarAlgo()  {  qDebug() << "Algo";  }
	};

	class Estudiante : public Persona  {
	public:
	    Estudiante(QString nombre) : Persona(nombre)  {  }
	    QString verNombre()  {  return "Estudiante: " + nombre;  }
	};


	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);

	    {
	    Persona *jose = new Estudiante("Jose");
	    Persona *carlos = new Empleado("Carlos");

	    qDebug() << carlos->verNombre();
	    qDebug() << jose->verNombre();
	    carlos->mostrarAlgo();  // Muestra algo? 

	    delete jose;
	    delete carlos;
	    }

	    return a.exec();
	}
	
**Para todo hay un mexicano que también lo explica** 

- Clic sobre el GIF para abrir video 

|ImageLink|_

.. |ImageLink| image:: /images/clase10/explicacion_mexicana.gif
.. _ImageLink: https://www.youtube.com/watch?v=6lIGfzZ4oqo
	
Funciones virtuales
^^^^^^^^^^^^^^^^^^^

- Puede ser interesante llamar a la función de la derivada (en polimorfismo).
- Al declarar una función como virtual en la clase base, si se superpone en la derivada, al invocar usando el puntero a la clase base, se ejecuta la versión de la derivada.

.. code-block:: c

	class Persona  {
	public:
	    Persona(QString nombre) : nombre(nombre)  {  }
	    virtual QString verNombre()  {  return "Persona: " + nombre;  }  // Y si no fuera virtual?

	protected:  
	    QString nombre;
	};

	class Empleado : public Persona  {
	public:
	    Empleado(QString nombre) : Persona(nombre)  {  }
	    QString verNombre()  {  return "Empleado: " + nombre;  }
	};


	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);

	    {
	    Persona *carlos = new Empleado("Carlos");

	    qDebug() << carlos->verNombre();  // Qué publica?

	    delete carlos;
	    }

	    return a.exec();
	}

		
		
		
**Volviendo a base de datos**

- Definir una clase AdminDB para administrar la base de datos
- Crear el siguiente método:

.. code-block:: c
	
	bool conectar(QString archivoSqlite); 

- En un proyecto nuevo y desde la función main() intentar la conexión.

.. code-block:: c

	// --- adminDB.h ---------------
	#include <QSqlDatabase>
	#include <QString>
	#include <QObject>

	class AdminDB : public QObject  {
	    Q_OBJECT

	public:
	    AdminDB();
	    bool conectar(QString archivoSqlite);
	    QSqlDatabase getDB();

	private:
	    QSqlDatabase db;
	};

	// --- adminDB.cpp ------------
	#include "adminDB.h"

	AdminDB::AdminDB()  {
	    db = QSqlDatabase::addDatabase("QSQLITE");
	}

	bool AdminDB::conectar(QString archivoSqlite)  {
	    db.setDatabaseName(archivoSqlite);

	    if(db.open())
	        return true;

	    return false;
	}

	QSqlDatabase AdminDB::getDB()  {
	    return db;
	}

	// --- main.cpp  ----------------
	#include <QApplication>
	#include "adminDB.h"

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);

	    qDebug() << QDir::currentPath();

	    AdminDB adminDB;
	    if (adminDB.conectar("C:/Qt/db/test"))
	        qDebug() << "Conexion exitosa";
	    else
	        qDebug() << "Conexion NO exitosa";

	return 0;
	}

- Para independizar del SO

.. code-block:: c

	AdminDB adminDB;
	QString nombreSqlite;

	#ifdef __APPLE__
	    nombreSqlite = "/home/cosimani/db/test";
	#elif __WIN32__
	    nombreSqlite = "C:/Qt/db/test";
	#elif __linux__
	    nombreSqlite = "/home/cosimani/db/test";
	#else
	    nombreSqlite = "/home/cosimani/db/test";
	#endif

	if (adminDB.conectar(nombreSqlite))
	    qDebug() << "Conexion exitosa";

Consulta a la base de datos
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	QSqlDatabase db = QSqlDatabase::addDatabase("QSQLITE");

	db.setDatabaseName("C:/Qt/db/test"); 

	if (db.open())  {
	    QSqlQuery query = db.exec("SELECT nombre, apellido FROM usuarios");

	    while(query.next())  {
	        qDebug() << query.value(0).toString() << " " << query.value(1).toString();
	    }
	}

**Ejemplo**: slot de la clase Login para que valide usuarios contra la base

.. code-block:: c

	void Login::slot_validar()  {
	    bool usuarioValido = false;

	    if (adminDB->getDB().isOpen())  {  
	        QSqlQuery* query = new QSqlQuery(adminDB->getDB());

	        query->exec("SELECT nombre, apellido FROM usuarios WHERE usuario='" + 
	        leUsuario->text() + "' AND clave='" + leClave->text() + "'");

	        // Si los datos son consistentes, devolverá un único registro.
	        while (query->next())  {

	            QSqlRecord record = query->record();

	            // Obtenemos el número de la columna de los datos que necesitamos.
	            int columnaNombre = record.indexOf("nombre");
	            int columnaApellido = record.indexOf("apellido");

	            // Obtenemos los valores de las columnas.
	            qDebug() << "Nombre=" << query->value(columnaNombre).toString();
	            qDebug() << "Apellido=" << query->value(columnaApellido).toString();

	            usuarioValido = true;
	        }

	        if (usuarioValido)  {
	            QMessageBox::information(this, "Conexión exitosa", "Válido");
	        }
	        else  {
	            QMessageBox::critical(this, "Sin permisos", "Usuario inválido");
	        }
	    }
	}

**Ejercicio**

- Diseñar una aplicación para una galería de fotos
- Debe tener una base con una tabla 'imagenes' que tenga las URLs de imágenes
- Un botón >> y otro << para avanzar o retroceder en la galería de fotos
- Se podrá navegar sobre las fotos que se descargarán desde internet
	
	
	





