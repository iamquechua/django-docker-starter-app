# Django Backend Starter
A starter project for a Django backend.

## Setup Instructions

Clone the repository:
```
$ git clone https://github.com/douno/django-backend-starter.git
```

Ensure you have Docker and Docker Compose installed:
```
$ docker -v
$ docker-compose -v
```

Start Docker if not already.

Build the image and start a container:
```
$ docker-compose up -d --build
```

You can open the app in the browser at `localhost:8009`

To stop the container and remove associated volumes, run the command:

```
$ docker-compose down -v
```

## Useful Commands:

### Django Commands with Docker Compose:

| Tasks | Commands |
|--|--|
| Create migrations | `$ docker-compose exec backend python manage.py makemigrations`  |
| Run migrations | `$ docker-compose exec backend python manage.py migrate`  |

###  PostgreSQL Commands with Docker Compose:

| Tasks | Commands |
|--|--|
| Connect to a specific database | `$ docker-compose exec backend-db psql --username=backend --dbname=backend_dev`  |

###  Common Docker Commands:

| Tasks | Commands |
|--|--|
| Build an image | `$ docker-compose build`  |
| Start a container | `$ docker-compose up`  |
| Start a container (in detached mode) | `$ docker-compose up -d`  |
| Build and image and start a container (in detached mode) | `$ docker-compose up -d --build`  |
| Inspect a volume | `$ docker volume inspect django-backend-starter_postgres_data`  |
| Run migrations | `$ docker-compose exec backend python manage.py migrate`  |
