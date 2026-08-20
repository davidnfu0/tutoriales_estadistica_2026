# Tutorial de Gestión de Proyecto de Datos

En este tutorial se mostrará cómo hacer la gestión básica de un proyecto de datos. Para ello estudiaremos cómo crear un entorno de Conda, cómo gestionar librerías de requerimientos, como versionar el código usando y Git y cómo hacer código colaborativo usando Github.

Todas las tareas del curso se van a trabajar en un mismo repositorio (carpeta). Que tiene que seguir la estructura de este tutorial.

## Estructura del Proyecto

Un proyecto de datos ordenado facilita el trabajo propio y el de sus compañeros. Le recomendamos utilizar una estructura similar a la siguiente:

```
tareas_estadistica/
├── data/               # Datos utilizados en el proyecto
│   ├── raw/            # Datos originales, nunca se modifican
│   └── processed/      # Datos ya limpios o transformados
├── notebooks/          # Jupyter notebooks de exploración y análisis
├── src/                # Funciones y scripts reutilizables
├── results/            # Gráficos, tablas y salidas del análisis
├── requirements.txt    # Librerías necesarias para el proyecto
├── .gitignore          # Archivos que Git debe ignorar
└── README.md           # Descripción del proyecto
```

La idea principal es separar los datos, el código y los resultados. Así, cualquier persona que reciba su proyecto sabe dónde buscar cada cosa.

## Positron

Positron es un editor de código basado en visual studio code, enfocado en ciencia de datos que incorpora varias comodidades para trabajar con Python y R. Para este curso, le recomendamos instalar Positron en su computador. Puede descargarlo desde [este enlace](https://positron.posit.co/download.html).

## Entornos de Conda

Los entornos en programación son una herramienta fundamental, tienen como objetivo aislar las dependencias de un proyecto para evitar conflictos y garantizar la reproducibilidad del entorno. En el mundo de los datos la herramienta fundamental de gestión de entornos es [Conda](https://docs.conda.io/en/latest/). 

### ¿Qué es Conda y Cómo Instalarlo?

Conda es un gestor de entornos y paquetes para lenguajes de programación como Python, R, y otros. Permite crear, mantener y compartir entornos aislados con diferentes versiones de librerías y dependencias.

Para este curso va a ser necesario que usted instale Conda en su sistema. Recomendamos instalar Miniconda, un versión de la mínima de la aplicación que tiene todo lo necesario para este curso. Para instalarlo, utilice [este enlace](https://www.anaconda.com/docs/getting-started/installation).

### Entornos en Conda

Una vez instalado Conda, puede crear un nuevo entorno de python utilizando el siguiente comando en su terminal:
```
conda create --name tareas_estadistica python=3.12
```
Este comando crea un entorno de python 3.12 llamado tareas_estadistica, les aconsejamos utilizar este entorno para realizar las actividades del curso.

Una vez creado el entorno, lo puede activas usando el siguiente comando:
```
conda activate tareas_estadistica
```
Una vez activado el entorno, puede instalar las librerías necesarias para su proyecto. Hay dos formas principales de intalar librerías:

```
pip install numpy
```

```
conda install numpy
```

Usted debe leer la documentación de la librería que desee instalar para saber cuál es la mejor forma de instalarla en su entorno. Con la mayoría de librerías estándar ambos métodos funcionan. **Sin embargo, en este curso le pediremos que instale siempre con `pip`**, por las razones que se explican en la siguiente sección.

### Exportar y Replicar un Entorno

Para que otra persona pueda replicar su entorno, debe entregarle la lista de librerías que usted instaló. La forma estándar de hacerlo es con un archivo llamado `requirements.txt`. Con su entorno activo, ejecute:

```
pip freeze > requirements.txt
```

El resultado es un archivo de texto simple, con una librería por línea y su versión exacta:

```
matplotlib==3.9.2
numpy==2.1.3
pandas==2.2.3
```

Si otra persona recibe este archivo, puede reproducir su entorno en dos pasos. Primero crea un entorno vacío con la misma versión de Python, y luego instala las librerías:

```
conda create --name tareas_estadistica python=3.12
conda activate tareas_estadistica
pip install -r requirements.txt
```

Cada vez que instale una librería nueva, recuerde volver a exportar el archivo.

Algunos comandos adicionales que le pueden ser útiles:

```
conda env list          # Muestra todos sus entornos
conda list              # Muestra las librerías del entorno activo
conda deactivate        # Sale del entorno activo
```

## Git

Cuando uno trabaja en un proyecto es común terminar con archivos como `tarea1_final.py`, `tarea1_final_v2.py` o `tarea1_final_ahora_si.py`. Git existe justamente para evitar eso.

### ¿Qué es Git y Cómo Instalarlo?

Git es un sistema de control de versiones: una herramienta que guarda el historial de los cambios de su proyecto. Con Git usted puede ver qué cambió, cuándo cambió y volver a una versión anterior si algo se rompe.

Para instalarlo, siga las instrucciones para su sistema operativo en [este enlace](https://git-scm.com/downloads). Para verificar que quedó bien instalado, ejecute en su terminal:

```
git --version
```

### Configuración Inicial

Antes de usar Git por primera vez, debe indicarle quién es usted. Esta información quedará asociada a cada cambio que registre:

```
git config --global user.name "Su Nombre"
git config --global user.email "su_correo@ejemplo.com"
```

### Comandos Básicos

Para empezar a versionar un proyecto, ubíquese en la carpeta del proyecto y ejecute:

```
git init
```

Esto crea un repositorio de Git en su carpeta. A partir de ahora Git observará los archivos que hay en ella.

El flujo de trabajo básico en Git tiene tres pasos. Primero, revise el estado de sus archivos:

```
git status
```

Segundo, seleccione los archivos cuyos cambios desea guardar:

```
git add tarea1.py
```

Si desea agregar todos los archivos modificados, puede usar:

```
git add .
```

Tercero, registre los cambios con un mensaje que describa lo que hizo:

```
git commit -m "Agrego la lectura de datos de la tarea 1"
```

Cada `commit` es una fotografía del estado de su proyecto. Le recomendamos hacer commits pequeños y frecuentes, con mensajes claros. Para revisar el historial de commits:

```
git log --oneline
```

### El Archivo .gitignore

Hay archivos que no conviene versionar: bases de datos pesadas, archivos temporales o credenciales. Para que Git los ignore, cree un archivo llamado `.gitignore` en la raíz del proyecto con un contenido similar a este:

```
__pycache__/
*.pyc
.ipynb_checkpoints/
data/raw/
```

## Github

Git funciona de manera local, en su propio computador. Github es un servicio en la nube que permite guardar sus repositorios en internet, compartirlos y trabajar con otras personas sobre el mismo código.

### Crear una Cuenta y un Repositorio

Primero, cree una cuenta gratuita en [github.com](https://github.com). Luego, desde la página principal, haga clic en el botón **New** para crear un repositorio nuevo. Elija un nombre (por ejemplo, `tareas_estadistica`), decida si será público o privado y créelo.

### Conectar su Proyecto Local con Github

Github le mostrará las instrucciones para conectar un proyecto existente. En esencia, debe indicarle a Git dónde está el repositorio remoto y luego subir sus cambios:

```
git remote add origin https://github.com/su_usuario/tareas_estadistica.git
git branch -M main
git push -u origin main
```

De ahora en adelante, cada vez que quiera subir sus commits a Github, basta con:

```
git push
```

### Descargar un Repositorio

Si quiere obtener una copia de un repositorio que ya existe (por ejemplo, el del curso), use:

```
git clone https://github.com/usuario/nombre_repositorio.git
```

Y si un compañero subió cambios y usted quiere traerlos a su computador:

```
git pull
```

### Resumen del Flujo de Trabajo

En resumen, un día típico de trabajo en su proyecto se ve así:

```
conda activate tareas_estadistica   # Activa el entorno
git pull                            # Trae los cambios de sus compañeros
# ... trabaja en su código ...
git add .                           # Selecciona los cambios
git commit -m "Descripción clara"   # Registra los cambios
git push                            # Sube los cambios a Github
```

Con esto ya tiene las herramientas mínimas para gestionar un proyecto de datos de forma ordenada y reproducible.

Este flujo de trabajo se puede realizar utilizando la UI que ofrece Positron, que permite hacer todo esto sin necesidad de usar la terminal. Puede ver cómo hacer esto siguiendo el tutorial.
