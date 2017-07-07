# Initialize the application
docker-compose run web django-admin.py startproject hello .

# Change the database connection and redis settings
In hello/settings.py

Replace the DATABASES section with this:

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
    }
}

And add a CACHES section like this:

CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://redis:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient"
        },
        "KEY_PREFIX": "hello"
    }
}

# Start the application

docker-compose up

# Validate

Test [http://localhost:8080](http://localhost:8080)
