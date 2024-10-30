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
## 7. Retrieve the data from the previous database by launching this script in the Django shell
```python
import json

# Load the JSON data
with open('datadump.json', 'r') as file:
    data = json.load(file)

# Filter out the database data
database_data = [entry for entry in data if entry['model'] not in ['auth.permission', 'contenttypes.contenttype', 'sessions.session']]

# Write the filtered data to a new JSON file
with open('filtered_data.json', 'w') as outfile:
    json.dump(database_data, outfile, indent=4)
```

## 8. Load the data from the previous database
```bash
python manage.py loaddata filtered_data.json
```