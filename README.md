# Ejercicio data engineering

# Primeros pasos

- Descargar la data (excel con 3 hojas con datos).
- Tener DataGrip
- Tener una consola instalada con GitBash

## Comandos de la consola

cd cambiar la ruta para algun archivo

cd .. devolverse

mkdir , crear carpeta

cat muestra el contenido

ls lista el contenido de las carpetas

pip install (instala cosas en el Python)

## PASO A PASO

1. Crear desde la consola una carpeta para almacenar el proyecto.

Emplear Snake_case : usar _ en vez de espacio y todo en minus.

```sql
mkdir reto_ds
```

1. Una vez creada, descargar el excel con la base de datos en esa misma carpeta.
2. Crear un ambiente virtual.
    
    Los ambientes virtuales o venv permiten que las instalaciones o afectaciones a Python solo se ejecuten en ese proyecto en específico y no en el Windows en general.
    
    Desde la consola creamos el venv (es el segundo venv mostrado), se recomienda que se mantenga ese mismo nombre.
    

```sql
python -m venv venv
```

1. Procedemos a activarlo para que se muestre en la parte superior del path de la consola.

```sql
source venv/Scripts/activate
```

Se verá algo así: 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bc4ab2cd-633b-40f8-9d09-00ba73d59fa2/Untitled.png)

1. Creamos el repositorio.

### Creando el git

Primero vamos a crear el repo desde el disco local, para posterior a finalizar, hacer un push de manera remota a la página de GitHub.

Desde la consola, ubicados en la ruta de nuestro venv:

```sql
git init
```

ahora nos aparece en la ruta de la consola, la palabra (master) que nos indica que se ha creado esa rama de manera local donde se almacenará el proyecto.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ee4403d0-7833-4aeb-b601-caeb358101b2/Untitled.png)

una vez creado el repo, se crean tambien algunas carpetas por defecto dentro de nuestra carpeta principal del proyecto, entre ellos un archivo .gitignore, que nos permitirá meter allí todo aquello que no queremos sea accesado desde el repo remoto (en GitHub), usualmente allí meteremos el venv, para ello procedemos a:

1. Abrir el archivo .gitignore desde la consola

```sql
vim .gitignore
```

Nos aparece ahora algo así:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/08962e60-e1b9-406e-88ac-3671bd9a194a/Untitled.png)

1. Damos la tecla **I = INSERT** y pondremos la palabra **venv/** para decirle que no queremos que el ambiente virtual sea visible desde el repo remoto.
2. Una vez puesto ponemos **esc** para dejar de editar y luego **:wq**, que guarda y cierra
3. Listo ya no va a aparecer nuestro venv en el repo.
4. TIP: Si quisieramos ver que tenemos instalado en el Python de nuestro proyecto ponemos

```sql
pip freeze
```

Nos listará lo que tenemos, si es que contamos con algo.

## Pasando los datos de Excel a Python

Link a Jupyter:

@[http://localhost:8888/notebooks/retods.ipynb](http://localhost:8888/notebooks/retods.ipynb)

Este paso intermedio requiere el uso de la herramienta Jupyter, para ello vamos a la consola de nuevo a instalarlo para poder usarlo.

```sql
pip install jupyter
```

Tomará cerca de 5 minutos completar todo el proceso.

una vez instalado, debemos abrir una nueva pestaña de la consola, ya que la actual estará corriendo el Jupyter y no permitirá hacer nada diferente.

1. ponemos de nuevo la palabra Jupyter en la consola y nos abrirá desde Chrome, el programa.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6fb97d63-0bc6-4f18-8586-afd3dab0574a/Untitled.png)

Podemos visualizar desde la url, que trabajamos aun desde el disco local.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/43cff453-7b40-4ba1-a88c-218472223ce5/Untitled.png)

1. Procedemos a crear una ventana de trabajo de Python desde New.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/049fa1b1-ab8e-4f33-98cf-8dc3f8abbe9e/Untitled.png)

1. Procedemos entonces a utilizar Jupyter para pasar los datos de Excel a Python y posterior a ello visualizar los datos en DataGrip.

## Utilizando Jupyter

1. Vamos primero a llamar las librerias que necesitaremos:

```python
import pandas as pd
import os
import openpyxl
```

pandas: Esencia para trabajar con datos en Python

os: Para trabajar con el sistema operativo del pc en temas de acceso a dir y carpetas

openpyxl: Tiene funcionalidades para trabajar excel en python

1. NOTA: Como estas librerias no existian en nuestro venv, debemos instalarlas tambien desde la consola

```python
pip install pandas
pip install os
pip install openpyxl
```

Desde Jupyter:

1. vamos a listar ahora lo que contiene el directorio (nuestra carpeta del proyecto)

```python
os.listdir()
```

1. Una vez identificamos el archivo excel, vamos a abrir cada hoja necesaria para trabajar:
- Definimos la variable
- le pedimos que con pandas lea el excel
- Damos el nombre del archivo
- y el nombre de la hoja

```python
df_bd = pd.read_excel(r'BD_Gestion.xlsx', sheet_name='BD')
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/842ea49a-82fe-4c93-8303-8c846380084f/Untitled.png)

1. Luego vamos a mirar qué contiene cada hoja, usamos

```python
df_bd.head()
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/349bde30-6462-4919-9e86-3d022323f373/Untitled.png)

LISTO, YA TENEMOS EN PYTHON LOS DATOS NECESARIOS, PROCEDEMOS A ENVIARLOS A POSTGRESQL PARA MANEJARLOS CON DATAGRIP 

Desde Jupyter:

1. Importamos la librería psycopg2 y también lo hacemos en la consola:
2. En Jupyter:

```python
import psycopg2
```

1. En la consola

```python
pip install psycopg2
```

1. Una vez instalados:
2. Creamos desde DataGrip una nueva base de datos que llamaremos retods,

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6dc79c8f-4eed-4180-882c-464e410fca57/Untitled.png)

1. Una vez creada, vamos a acceder a sus propiedades para tener las credenciales y parametros de acceso:

Desde la bases de datos principal, damos clic derecho > properties

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7dce9a3b-0e31-4824-bf4e-97ddea460291/Untitled.png)

1. Podemos visualizar ahora:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2ae2894c-7ee8-4533-9df4-174735367fd3/Untitled.png)

1. Desde Jupyter, vamos a crear la conexión a la base de datos 

```python
pgcon = psycopg2.connect(
	host = 'localhost',
database = 'retods',
user = 'postgres'
port = 5433,
password = 'admin',
)
```

1. Probamos ahora la conexión.

```python
pgcursor = pgcon.cursor()
pgcon.close()
```

1. Importamos ahora una librería que nos permite conectarnos a las bases de datos.

Consola:

```python
pip install sqlalchemy
```

1. Jupyter: sqlalchemy ya está “preinstalada”, solo debemos llamarla

```python
from sqlalchemy import create_engine
engine = create_engine('postgresql+psycopg2://postgres:admin@localhost:5433/retods')
```

1. Por ultimo vamos a pasar la hoja de geston a sql, usando el engine creado anteriormente:

```python
df_bd.to_sql('gestion',engine,if_exists='replace',index=False)
```

Ya podemos visualizar desde Datagrip los datos, e iniciar a trabajar y consultar.

## IMPORTANTE:

Si cerramos el proyecto, para abrirlo:

1. Desde la consola ubicarnos en la carpeta de nuestro proyecto
2. Activar el venv
3. debe verse el master del repo, si no poner git status.
4. poner en la consola jupyter notebook si lo necesitamos para que corra

### Próximos pasos:

1. Normalizar los nombres de las columnas con snake_case

## Normalizando nombres de campos en el dataframe Gestión

Inicializamos desde consola

## Desde DataGrip con SQL

vamos a DataGrip

desde la consola vamos a cambiar cada uno de los nombres:

```python
ALTER TABLE nombre_Tabla 
	RENAME COLUMN "nombre_actual_columna"
	TO "nuevo_nombre_columna";

-- En nuestro caso la tabla es gestion y todos los nombres van en minus y los espacios con _
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dbb9474d-81d6-4957-958a-6fe2e04d188d/Untitled.png)

## Desde Jupyter usando Python

```python
# Renombrar columnas
df_bd.rename(
    columns=({'IdCanal':'id_Canal', 'Fecha':'fecha', 'Intervalo 2 horas':'intervalo_2_horas', 
              'Intervalo Hora':'intervalo_hora', 'Intervalo Medias Hora':'intervalo_medias_hora', 
              'Entrantes':'entrantes', 'IdPrograma':'id_programa', 'Contestadas':'contestadas', 
              'SumaNS':'suma_ns', 'SumaPromResp':'suma_prom_resp', 'SumaPromAbandono':'suma_prom_abandono', 
              'Tot_ConversandoEntrada':'tot_conversando_entrada', 'Tot_ConversandoSalida':'tot_conversando_salida', 
              'Tot_Documentando':'tot_documentando', 'TotalDisponible':'total_disponible'}),
    inplace=True, 
)
print(df_bd.columns)
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c19ac83e-975d-4163-a140-79cd0b28e4e8/Untitled.png)

### Próximos pasos:

1. Agregar constraints a las tablas, llave primaria y relaciones foráneas entre las 3 tablas.

inplace = True visualizar solo durante la ejecución del código.

Se puede ejecutar y asignarlo a otra variable.