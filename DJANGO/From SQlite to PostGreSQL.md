# How to migrate sqlite database to postgresql database in Django

## 1. Install the required packages
```bash
pip install psycopg2-binary
``` 

## 2. Save the previous database
```bash
python manage.py dumpdata > db.json
```

## 3. Install Postgresql depending on your OS
```bash
sudo apt-get install postgresql # For Ubuntu
```

## 4. Create a user and a database in Postgresql
```bash
sudo -u postgres psql
CREATE DATABASE mydb;
CREATE USER myuser WITH PASSWORD 'mypass';
```

## 5. Change the database settings in settings.py
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydb',
        'USER': 'myuser',
        'PASSWORD': 'mypass',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```
## 6. Migrate the database
```bash
python manage.py migrate
```

## 7. Load the data from the previous database
```bash
python manage.py loaddata db.json
```