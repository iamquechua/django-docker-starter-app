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

## Deployment

* [Sign up](https://signup.heroku.com/) for a Heroku account (if you don’t already have one)
* Install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) (if you haven't already done so)
* Create a new app: `heroku create`

Log in to the [Heroku Container Registry](https://devcenter.heroku.com/articles/container-registry-and-runtime):
```
$ heroku create
```

Provision a new Postgres database with the [hobby-dev](https://devcenter.heroku.com/articles/heroku-postgres-plans#hobby-tier) plan:
```
$ heroku addons:create heroku-postgresql:hobby-dev --app <app_name>
```
Now, we need to build the production Docker image and tag it with the following format `registry.heroku.com/<app>/<process-type>`:

```
$ cd app
$ docker build -f Dockerfile.prod -t registry.heroku.com/<app_name>/web .
```

Update the `DJANGO_ALLOWED_HOSTS` environment variable in _Dockerfile.prod_:
```
ENV DJANGO_ALLOWED_HOSTS .herokuapp.com
```
Build the image again:
```
$ docker build -f Dockerfile.prod -t registry.heroku.com/<app_name>/web .
```
Push the image to the registry:
```
$ docker push registry.heroku.com/<app_name>/web:latest
```
Release the image:
```
$ heroku container:release web --app <app_name>
```
This will run the container. You should be able to view the app at `https://<app_name>.herokuapp.com/`

Apply the migrations:
```
$ heroku run python manage.py migrate --app <app_name>
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

###  Code Quality Commands:

| Tasks | Commands |
|--|--|
| Run Flake8 | `$ $ docker-compose exec movies flake8 .`  |
| Format code with Black | `$ docker-compose exec movies black --exclude=migrations .`  |
| Check if there is code to format with Black | `$ docker-compose exec movies black --check --exclude=migrations .`  |
| Show the difference before and after formatting with Black | `$ docker-compose exec movies black --diff --exclude=migrations .`  |
| Sort imports with isort | `$ docker-compose exec movies isort .`  |
| Check if there are imports that need sorting with Black | `$ docker-compose exec movies isort . --check-only`  |
| Show the difference before and after sorting imports with isort | `$ docker-compose exec movies isort . --diff`  |

###  Common Docker Commands:

| Tasks | Commands |
|--|--|
| Build an image | `$ docker-compose build`  |
| Start a container | `$ docker-compose up`  |
| Start a container (in detached mode) | `$ docker-compose up -d`  |
| Build and image and start a container (in detached mode) | `$ docker-compose up -d --build`  |
| Inspect a volume | `$ docker volume inspect django-backend-starter_postgres_data`  |
| Run migrations | `$ docker-compose exec backend python manage.py migrate`  |
