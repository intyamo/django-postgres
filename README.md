# Django + PostgreSQL

## Setup

1. Virtualenv and dependencies

We'll manage this stuff via awesome [poetry](https://python-poetry.org):

```sh
# run in the root of our project
poetry init
poetry add django ~=3.2
poetry add psycopg2-binary
```

2. Database

Run `psql` and:

```sql
CREATE DATABASE myshop;

CREATE USER vpupkin WITH ENCRYPTED PASSWORD 'admin';

GRANT ALL PRIVILEGES ON DATABASE myshop TO vpupkin;
```

3. Django

```sh
django-admin startproject config .
```

Edit database settings `config/settings.py`:

```py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'myshop',
        'USER': 'vpupkin',
        'PASSWORD': 'admin',
        'HOST': 'localhost',
        'PORT': '5432'
    },

    'sqlite': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

4. Let's go :rocket:

```sh
# apply database migrations
python manage.py migrate

# create superuser for our site
python manage.py createsuperuser

# start our Django project
python manage.py runserver

# open site + Admin Panel in the browser
firefox http://locahost:8000/
firefox http://localhost:8000/admin
```

## Reference

- https://wiki.archlinux.org/title/PostgreSQL#Installation
- https://djangocentral.com/using-postgresql-with-django

