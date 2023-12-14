# HOW TO INSTALL REQUIREMENTS.IN FILE

## Create a virtual environment  
### `$ python3 -m venv <environment_name>.env`

## Create **requirements.in** file and write all necessary packages you want to install. 
```
Exemple : 
django
djangorestframework
djoser
```

## Install **pip-tools**   
### `$ python -m pip install pip-tools`

## Create text file  
### `$ pip-compile`  

## Download all packages 
### `$ pip-sync` 