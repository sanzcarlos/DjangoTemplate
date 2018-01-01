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

El proyecto esta preparado para tener varios entornos a la vez y que sólo tengamos que modificar el archivo docker-compose.yml.

Como vamos a utilizar postgresql como base de datos para el proyecto de [Django](https://www.djangoproject.com/), tenemos que modificar los
