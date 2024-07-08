# Paso 1: Crear y activar el entorno virtual
python -m venv nombre_entorno
nombre_entorno\Scripts\activate  # Para Windows
source nombre_entorno/bin/activate  # Para Unix/MacOS

# Paso 2: Ver las dependencias e instalar lo necesario
pip list
pip install django

# Paso 3: Instalar el driver de la base de datos (PostgreSQL) en nuestro entorno virtual
pip install psycopg2
pip install --upgrade pip
pip list

# Paso 4: Crear el proyecto e ingresar a la carpeta
django-admin startproject nombre_proyecto
cd nombre_proyecto

# Paso 4.5: Crear la base de datos

## Base de Datos (Terminal Bash)

CREATE DATABASE nombre_bd;
\l                     -- lista bases de datos creadas 
\c nombre_bd           -- conectarse a la base de datos 
\q                     -- salir

## Vincular en settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'nombre_bd',
        'USER': 'postgres',
        'PASSWORD': 'Admin1234',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}

# Paso 5: Agregar la app al proyecto
python manage.py startapp nombre_aplicacion

## En settings.py
INSTALLED_APPS = [
    ...,
    'nombre_aplicacion',
]

# Paso 6: TEMPLATES
- Crea la carpeta templates en la app.
- Crea los archivos HTML con estructura básica.
- Crea un método que despliegue el HTML.
- Crea una ruta que enlace a views.py de la app.

# Paso 7: MODELOS
- Crea el modelo en models.py
- Agrégalo al admin.py

from .models import Nombre_Modelo
admin.site.register(Nombre_Modelo)

- Crea un superusuario
python manage.py createsuperuser

# Paso 8: Ejecutar las migraciones
python manage.py makemigrations
python manage.py migrate

## Revisar en la base de datos (Terminal Bash)
\d     -- verificar el modelo creado en la lista

# Ejecutar el servidor
python manage.py runserver

# Conocer todas las migraciones y saber cuáles se han ejecutado en la Base de Datos
python manage.py showmigrations
python manage.py showmigrations nombre_aplicacion

# Revertir una migración específica
python manage.py migrate nombre_aplicacion 0001_initial

# Entrar a la shell de Django desde la terminal
python manage.py shell  # Inicia una sesión interactiva de Django
