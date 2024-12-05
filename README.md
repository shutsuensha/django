- django-admin startproject src
- python3 manage.py startapp myapp
- Add myapp in src/settings.py
- Add templates/, forms.py, urls.py in myapp

## Postgres
- pip3 install psycopg2-binary
```sh
sudo systemctl status postgresql
sudo -i -u postgres
psql

CREATE DATABASE mydatabase;
CREATE USER myuser WITH ENCRYPTED PASSWORD 'mypassword';
GRANT ALL PRIVILEGES ON DATABASE mydatabase TO myuser;

psql -U myuser -d mydatabase
```

- src/settings.py
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.getenv('DB_NAME'),
        'USER': os.getenv('DB_USER'),
        'PASSWORD': os.getenv('DB_PASS'),
        'HOST': os.getenv('DB_HOST'),
        'PORT': os.getenv('DB_PORT')
    }
}
```

## .env file in root project
- pip install python-dotenv
- generate secret key
```sh
python3 -c 'from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())'
```
### src/settings.py
```python
import os
from dotenv import load_dotenv

load_dotenv()

SECRET_KEY = os.getenv('SECRET_KEY')
```

- python3 manage.py migrate
- python3 manage.py createsuperuser
- python3 manage.py runserver