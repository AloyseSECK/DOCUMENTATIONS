# HOW TO INSTALL REQUIREMENTS.IN FILE

- First you need to create a virtual environment  
Generally `$ python3 -m venv <environment_name>.env`

- Then create your **requirements.in** file and write all the things you want to install. 

```
Exemple : 
django
djangorestframework
djoser
```

- Next you need to install **pip-tools** with the following command  
`$ python -m pip install pip-tools`

- To finish run `$ pip-compile` to create the text file and `$ pip-sync` to download everything.