.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 25 - POO 2016
===================

Declaraciones friend
====================

- Miembros privados no son accesibles para funciones y clases externas
- Podemos usar friend en caso de necesitar acceder
- Se pueden aplicar a clases o métodos
- Inhabilitan el sistema de protección (protected o private)
- La amistad no es transferible

.. code-block:: c
	
	A es amigo de B     B amigo de C     No por eso A es amigo de C

- No se hereda

.. code-block:: c

	A amigo de B     C derivada de B     No por eso A es amigo de C

- No simétrica

.. code-block:: c

	A amigo de B     No por eso B es amigo de A

**Funciones amigas**

.. code-block:: c

	#include <iostream>
	using namespace std;

	class ClaseA  {
	public:
	    ClaseA(int i) : a(i)  {  }
	    void verA()  {  cout << a << endl;  }

	protected:
	    int a;
	    friend void mostrarA(ClaseA);  // mostrarA es amiga de ClaseA
	};

	void mostrarA(ClaseA cA)  {  // Esta función no pertenece a ClaseA
	    cout << cA.a << endl;   // Pero al ser amiga puede acceder a 'a'
	}

	int main(int argc, char** argv)  {
	    ClaseA objetoA(10);
	    mostrarA(objetoA);
	    objetoA.verA();

	    return 0;
	}
 
**Función amiga en otra clase**

.. code-block:: c

	#include <iostream>
	using namespace std;

	class ClaseA;	// Declaración

	class ClaseB  {
	public:
	    ClaseB(int i) : b(i)  {  }
		
	    void ver()  { cout << b << endl;  }
		
	    bool esMayor(ClaseA cA)  {  // Compara
	        return b > cA.a;
	    }
		
	private:
	    int b;
	};

	class ClaseA  {
	public:
	    ClaseA(int i) : a(i)  {  }
	    void ver()  { cout << a << endl; }

	private:
	    friend bool ClaseB::esMayor(ClaseA);
	    int a;
	};

	int main(int argc, char** argv)  {
	    ClaseA objetoA(10);
	    ClaseB objetoB(2);

	    objetoA.ver();	
	    objetoB.ver();

	    if (objetoB.esMayor(objetoA))
	        cout << "objetoB > objetoA" << endl;
	    else
	        cout << "objetoB < objetoA" << endl;

	    return 0;
	}
	
Levantar base de datos a QTableView
===================================

- Colocar con el QtDesigner un QTableView

.. code-block:: c

	QSqlRelationalTableModel * tableModelAlumnos;
	tableModelAlumnos = new QSqlRelationalTableModel(this, adminDB->getDB()); 

	tableModelAlumnos->setTable("alumnos");  // Tabla de la base

	// Para modificar como una planilla de excel
	tableModelAlumnos->setEditStrategy(QSqlTableModel::OnManualSubmit); 

	// Otra relación. En lugar de mostrar el id_carrera que muestre el nombre de la carrera.
	tableModelAlumnos->setRelation(5, QSqlRelation("carreras", "id", "nombre"));

	tableModelAlumnos->select();  // Hace la consulta.

	// Títulos de las columnas en el widget.
	tableModelAlumnos->setHeaderData(1, Qt::Horizontal, "Legajo");
	tableModelAlumnos->setHeaderData(2, Qt::Horizontal, "Nombre");
	tableModelAlumnos->setHeaderData(3, Qt::Horizontal, "Apellido");
	tableModelAlumnos->setHeaderData(4, Qt::Horizontal, "Mail");
	tableModelAlumnos->setHeaderData(5, Qt::Horizontal, "Carrera"); 

	// Seteamos el QSqlTableModel sobre el QTableView
	ui->tableViewAlumnos->setModel(tableModelAlumnos);

	// Lista desplegable con el nombre de la carrera, esto cuando se modifique la celda.
	ui->tableViewAlumnos->setItemDelegate(new QSqlRelationalDelegate(ui->tableViewAlumnos));

	// Ocultamos la columna id de la tabla alumnos.
	ui->tableViewAlumnos->setColumnHidden(0, true);

	// Ajusta el ancho de la celda con el texto en su interior. Para todas las columnas.
	ui->tableViewAlumnos->resizeColumnsToContents(); 
	
.. code-block:: c

	void Principal::slot_guardarCambios()  {    // Guada todos los cambios 
	    tableModelAlumnos->submitAll();
	}

	void Principal::slot_deshacer()  {  // Deshace todos los cambios que hizo el usuario.
	    tableModelAlumnos->revertAll();
	}

**Ejercicio**

- Hacerlo funcionar mostrando la tabla usuarios y su relación con tabla carreras
- Tabla alumnos: id, legajo, nombre, apellido, mail, id_carrera
- Tabla carreras: id, nombre
- Usar QtDesigner
		


	





