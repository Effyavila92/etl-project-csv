# Creación de ETL con Python,  PostgreSQL y visualización de datos con Microsoft Power BI

Este proyecto pretende tomar la información de un archivo .csv con datos de prueba para crear un proceso de ETL desde Jupyter con Python, almacenando los datos en una DB empleando PostgreSQL y finalmente visualizando en Power BI, todo a través de una arquitectura simple, como se muestra a continuación.

## Arquitectura:

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled.png)

## Visualización en Power BI

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled.gif)

# 1. Herramientas ideales

- Descargar la data (Archivo Ms. Excel).
- Tener una IDE para los datos, Ej: JetBrains - DataGrip ([https://www.jetbrains.com/es-es/datagrip/](https://www.jetbrains.com/es-es/datagrip/))
- Tener consola con GitBash.

## Comandos importantes en la consola:

- **cd:** Cambiar la ruta para algún archivo
- **cd .. :** Devolverse
- **mkdir:** Crear carpeta
- **cat:** Muestra el contenido
- **ls:** Lista el contenido de las carpetas
- **pip install:** (Instalar librerías en Python)

## PASO A PASO

1. Crear desde la consola una carpeta para almacenar el proyecto.

*NOTA: Emplear snake_case : usar _ en vez de espacio y todo en minus.*

```sql
mkdir reto_ds
```

1. Una vez creada, descargar el archivo Excel con la base de datos en esa misma carpeta.
2. Crear un ambiente virtual.

*NOTA: Los ambientes virtuales o **venv** permiten que las instalaciones o afectaciones a Python solo se ejecuten en ese proyecto en específico y no en Windows en general.*

1. Desde la consola crear el venv (es el segundo venv mostrado el primero es el comando), se recomienda que se mantenga ese mismo nombre.

```sql
python -m venv venv
```

1. Proceder a activarlo para que se muestre en la parte superior del path de la consola, para ello ejecutar:.

```sql
source venv/Scripts/activate
```

Se verá algo así:

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%201.png)

1. Una vez creado el venv, se debe crear el repositorio.

### Creando el repositorio:

Primero se debe crear el repo desde el disco local del pc, para luego, hacer un git push de manera remota a GitHub.

Desde la consola, ubicarse en la ruta del venv creado y luego ejecutar:

```sql
git init
```

ahora aparece en la ruta de la consola, la palabra (master) que nos indica que se ha creado esa rama de manera local donde se almacenará el proyecto.

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%202.png)

A partir de la creación local del repositorio, se crean con el algunas carpetas por default en la carpeta del proyecto, entre ellos el archivo .gitignore, este permite ingresar todo aquello que no debe ser accesado desde el repo remoto en GitHub, es allí donde se debe poner el venv, para ello:

1. Abrir el archivo .gitignore desde la consola:

```sql
vim .gitignore
```

Aparece así:

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%203.png)

1. Oprimir la tecla **I = INSERT** y poner la palabra **venv/** para ingresarlo y evitar que el ambiente virtual sea visible desde el repo remoto.
2. Dar a **esc** para dejar de editar y luego **:wq**, (guarda y cierra).

NOTA: Para ver que tenemos instalado en Python del proyecto ejecutar:

```python
pip freeze
```

Listará librerías existentes, si se cuenta con alguna.

## Pasando los datos de Excel a Python

Link a Jupyter:

@[http://localhost:8888/notebooks/retods.ipynb](http://localhost:8888/notebooks/retods.ipynb)

1. Este paso intermedio requiere el uso de la herramienta Jupyter, para ello se debe instalar desde la consola para usarlo.

```sql
pip install jupyter
```

*NOTA: Tomará cerca de 5 minutos completar todo el proceso.*

1. Luego de instalar, abrir una nueva pestaña en la consola, ya que la actual estará corriendo el Jupyter y no permitirá hacer nada diferente a ello.
2. Desde la consola escribir la palabra Jupyter para abrir desde Google Chrome, el programa.

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%204.png)

NOTA: Desde la URL del navegador se puede identificar que se está trabajando desde el disco local.

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%205.png)

1. Desde Jupyter, crear una ventana de trabajo de Python desde el botón New:

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%206.png)

## Jupyter

Ahora desde Jupyter, pasar los datos del archivo de Excel a Python para luego visualizarlos en DataGrip, para ello:

1. Importar las librerias necesarias para el proyecto:

```python
import pandas as pd
import os
import openpyxl
```

Relevancia de las librerías en el proyecto:

- Pandas: Esencial para trabajar con datos en Python.
- os: Para trabajar con el sistema operativo del pc en temas de acceso a dir y carpetas.
- openpyxl: Tiene funcionalidades para trabajar archivos Excel desde Python.

*NOTA: Como estas librerías no existian en el venv, deben instalarse tambien desde la consola en local:*

```python
pip install pandas
pip install os
pip install openpyxl
```

**Volviendo a Jupyter:**

1. Listar el contenido del directorio (la carpeta del proyecto):

```python
os.listdir()
```

1. Ya identificado el archivo Excel con el paso anterior, se debe abrir cada una de las hojas necesarias para trabajar:
- Definir la variable
- Trabajar los datos de Excel con la librería pandas
- Asignar el nombre del archivo y el nombre de la hoja

```python
df_bd = pd.read_excel(r'BD_Gestion.xlsx', sheet_name='BD')
```

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%207.png)

1. Identificar el contenido (campos y parte de los registros) de cada hoja usando:

```python
df_bd.head()
```

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%208.png)

Una vez ejecutado lo anterior, se enviarán los datos a PostgreSQL para manejarlos con la UI DataGrip.

**Desde Jupyter:**

1. Importar la librería psycopg2 tanto ej Jupyter como en la consola local:
2. En Jupyter:

```python
import psycopg2
```

1. En la consola:

```python
pip install psycopg2
```

Una vez instalados:

1. Crear desde DataGrip una nueva base de datos = retods,

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%209.png)

1. Una vez creada, acceder a sus propiedades para tener las credenciales y parámetros de acceso:

Para ello, desde la base de datos principal, dar *clic derecho > properties*

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%2010.png)

1. Se visualiza ahora:

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%2011.png)

1. Desde Jupyter, crear la conexión a la base de datos usando las credenciales identificadas en el paso anterior: 

```python
pgcon = psycopg2.connect(
	host = 'localhost',
database = 'retods',
user = 'postgres'
port = 5433,
password = 'admin',
)
```

1. Probar la conexión:

```python
pgcursor = pgcon.cursor()
pgcon.close()
```

1. Importar una librería que permita conectarse a las bases de datos.

Desde la Consola:

```python
pip install sqlalchemy
```

1. Desde Jupyter: sqlalchemy ya está “preinstalada”, solo debe llamarse

```python
from sqlalchemy import create_engine
engine = create_engine('postgresql+psycopg2://postgres:admin@localhost:5433/retods')
```

1. Pasar la hoja de gestion a sql, usando el engine creado anteriormente:

```python
df_bd.to_sql('gestion',engine,if_exists='replace',index=False)
```

Ya se pueden visualizar desde DataGrip los datos, e iniciar a trabajar y ejecutar consultas.

## IMPORTANTE:

En caso de cerrar el proyecto, para abrirlo de nuevo:

1. Desde la consola ubicarse en la carpeta del proyecto
2. Activar el venv
3. Debe verse la rama master del repo, en caso contrario poner en la consola git status.
4. En caso de necesitar Jupyter, poner en la consola: jupyter notebook

### Trabajando los datos:

1. Normalizar los nombres de las columnas con snake_case

## Normalizando nombres de campos en el dataframe Gestión

Iniciar desde consola

## Desde DataGrip con SQL

1. Desde la consola en DataGrip, cambiar cada uno de los nombres de los campos:

```sql
ALTER TABLE nombre_Tabla 
	RENAME COLUMN "nombre_actual_columna"
	TO "nuevo_nombre_columna";

-- La tabla es gestion y todos los nombres van en minus y los espacios con _
```

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%2012.png)

## Desde Jupyter usando Python

Antes de enviar los datos a Postgres se efectúa este paso para poder ser visible en la base de datos (es importante efectuarlo antes de ejecutar la conexión).

```python
# Renombrar columnas
df_bd.rename(
    columns=({'IdCanal':'id_canal', 'Fecha':'fecha', 'Intervalo 2 horas':'intervalo_2_horas', 
              'Intervalo Hora':'intervalo_hora', 'Intervalo Medias Hora':'intervalo_medias_hora', 
              'Entrantes':'entrantes', 'IdPrograma':'id_programa', 'Contestadas':'contestadas', 
              'SumaNS':'suma_ns', 'SumaPromResp':'suma_prom_resp', 'SumaPromAbandono':'suma_prom_abandono', 
              'Tot_ConversandoEntrada':'tot_conversando_entrada', 'Tot_ConversandoSalida':'tot_conversando_salida', 
              'Tot_Documentando':'tot_documentando', 'TotalDisponible':'total_disponible'}),
    inplace=True,   
)
print(df_bd.columns)
```

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%2013.png)

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%2014.png)

### Próximos pasos:

1. Agregar constraints a las tablas, llave primaria y relaciones foráneas entre las 3 tablas.

## Creando las llaves primarias para las tablas

NOTA: Todo puede ser visualizado en Postgres, dando refresh a la base de datos, en este caso es retods

1. Crear una sentencia corta para presentar las columnas, situarse sobre el nombre de la tabla, dar ctrl y clic y se presenta el desglose de las columnas y sus constraints asignados.

Para lograr esto, se debe tener creado el engine, de lo contrario no se podrá establecer la conexión.

### Creando una columna nueva en la tabla gestion para volverla PK

1. Como esta tabla no tiene ningún campo que pueda volverse una llave primaria, se debe emplear el índice, empleando pandas:

```python
#Primero dar reset_index para visualizar con el inplace en las tablas
df_bd.reset_index(inplace=True)

#Ahora renombrar para poder volverlo PK
df_bd.rename(
    columns=({'index':'id_gestion'}),
    inplace=True,
)
```

1. Ahora la será la PK empleando sqlalchemy, para ello llamando la función execute desde engine, se indica la tabla a alterar y el campo que será la PK:

```python
engine.execute('alter table gestion add primary key(id_gestion)')
```

1. Una vez ejecutado se puede visualizar desde Postgres ejecutando los pasos indicados al inicio de esta sección.

### Creando las PK en las tablas de canal y programa

Se crean de la misma manera que para la tabla de gestion, solo que en este caso las tablas ya contaban con un id, por lo que solo acudimos a la parte de engine:

```python
#Para canal
engine.execute('alter table canal add primary key(id_canal)')

#para programa
engine.execute('alter table programa add primary key(id_programa)')
```

## Creando las FK a partir de la relación de la tabla gestion con las tablas canal y programas

Todo puede ser visualizado en Postgres, dando refresh a la base de datos, en este caso es retods

Para establecer la llave foranea que es otro constraint, se debe emplear aparte del engine, una sentencia de SQL que se va a crear como función a fin de ser fácilmente replicable en casos mas extensos de asignación y creación de FKs.

```python
#La función
def add_foreing_key(table_name,fk_name,fk_column_name,parent_table,fk_column_parent):
    query=f"""
    ALTER TABLE {table_name}
    ADD CONSTRAINT {fk_name} 
    FOREIGN KEY ({fk_column_name}) 
    REFERENCES {parent_table} ({fk_column_parent});
    """
    engine.execute(query)
```

### Explicando las variables empleadas:

1. table_name
2. fk_name
3. (fk_column_name)
4. parent_table
5. (fk_column_parent)

### Estableciendo una función para la creación de las FK empleando sqlalchemy y una sentencia de SQL

## Importante

- inplace = True .Visualizar solo durante la ejecución del código.
- Todo lo que se vaya a ejecutar con pandas debe hacerse antes de enviar los datos a Postgres, de lo contrario no se van a ver los cambios efectuados, por ejemplo el nombre de los campos.
- Todo aquello que sea similar a SQL podemos tratarlo con otras librerías, por lo que se puede dejar despues de la visualización de los dataframes y la conexión a la DB.

Se puede ejecutar y asignarlo a otra variable.

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%2015.png)

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%2016.png)

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%2017.png)

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%2018.png)

## Utilizando GitHub

### Principales comandos

git add

git commit -m

git branch -m master main

git remote add origin (link SSH)

git pull origin main 

git push origin main 

git push origin main -f

## Creación de la SSH Key en GitBash

@[https://docs.github.com/es/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

![Untitled](Creacio%CC%81n%20de%20ETL%20con%20Python,%20PostgreSQL%20y%20visualiz%20f289a2160bfe448fb572041d291281c2/Untitled%2019.png)