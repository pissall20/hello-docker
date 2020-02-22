# hello-docker

Following is the directory structure of this project.
```
.
├── Dockerfile
├── Pipfile
├── README.md
├── config
│   ├── db
│   │   └── db1_env
│   └── nginx
│       └── conf.d
│           └── local.conf
├── docker-compose.yml
├── hello
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
└── requirements.txt
```

**Dockerfile**: Contains how the Django application is dockerized
**docker-compose.yml**: Contains services info for our app, and other related services like nginx, db, etc. 
**config**: This folder contains config for various services like nginx, and the database. You can use multiple databases for a Django app and have different environments set up for the same.
**Pipfile**: We used Pipenv to manage the requirements of the project, so that no extra packages get installed.
**settings.py**: DB settings in this file get updated according to the services in the docker-compose.yml (Left comments wherever needed)


## To use the boilerplate

As we are using Django, we need to “migrate” the database first. To do this, we will simply use Docker Compose to start our djangoapp service and run the migration command inside it:
```
docker-compose build 
docker-compose run --rm djangoapp /bin/bash -c "./manage.py migrate"
```

To run the app:
```
docker-compose up
```

To collect static files each time you need to update them:
```
docker-compose run djangoapp hello/manage.py collectstatic --no-input
```
