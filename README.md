# Plantilla para proyectos de Django
Es una plantilla para los proyectos de Django, que esta basada en Docker

# Prerequisitos
Tenemos que tener instalado docker y docker-compose para poder utilizar este repositorio

# Instalación
Tenemos que clonar el repositorio y crearnos el archivo .env que tendrá el siguiente contenido

```
POSTGRES_DB=<database_name>
POSTGRES_USER=<database_username>
POSTGRES_PASSWORD=<database_password>
DB_HOST=<database_host>
DB_PORT=5432
PGDATA=/var/lib/postgresql/data/pgdata
DJANGO_SECRET_KEY=<django_secre_key>
```

## Creación del proyecto
Lo primero que tenemos que hacer es crearnos el volumen que hemos defindo, en el caso del proyecto será db_data

```
docker volume create --name=db_data
```

A continuación tenemos que hacer es crearnos el proyecto en django:

```
docker-compose run web django-admin.py startproject <project_name> .
```

El proyecto esta preparado para tener varios entornos a la vez (desarrollo, prepoducción y producción) y que sólo tengamos que modificar el archivo docker-compose.yml.

Como vamos a utilizar postgresql como base de datos para el proyecto de [Django](https://www.djangoproject.com/). Vamos a crearnos un directorio llamado:

```
mkdir -p <project_name>/settings/
```

Tenemos que crear el archivo __init__.py con el comando:

```
touch <project_name>/settings/__init__.py
```

Movemos el archivo settings.py a este directorio y le cambiamos el nombre:

```
mv <project_name>/settings.py <project_name>/settings/base.py
```

Modificamos el contenido del fichero base.py 

```
...
SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY')
...
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('POSTGRES_DB'),
        'USER': os.environ.get('POSTGRES_USER'),
        'PASSWORD': os.environ.get('POSTGRES_PASSWORD'),
        'HOST': os.environ.get('DB_HOST'),
        'PORT': os.environ.get('DB_PORT'),
    }
}
...
```

Creamos un fichero dev.py para nuestro entorno de desarrollo con el siguiente contenido, es este archivo vamos a instalar todos los paquetes que necesitemos en nuestro entorno de desarrollo::

```
from .base import *

INSTALLED_APPS += [
]
```

Tenemos que modificar el fichero <project_name>/settings/base.py, para añadir la variable STATIC_ROOT:

```
STATIC_ROOT = '/<project_name>/static'
```

```
docker-compose exec web python manage.py collectstatic
```
