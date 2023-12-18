# Comment créer un environnement sur gitlab

Cette documentation a pour but de montrer les différentes étapes pour créer un environnement sur Gitlab.  
Pour appuyer cette doc, nous allons créer un environnement avec du [Django](https://www.djangoproject.com/) en backend et du [VueJS](https://vuejs.org/) en frontend.  
Cette documentation suppose que vous avez déjà connaisance  des deux frameworks.


### Initialisation des projets
- **Django**   
Pour initialiser le projet django, nous utiliserons la commande suivante :  
`django-admin startproject <nom_du_projet>`   
Cette commande génère une arborescence de fichiers qui permet de lancer une application web minimaliste avec quelques fonctionnalités.  
    
    *<u>NB</u>* : IL faudra s'assurer au préalable que toutes les librairies nécessaires sont installées. On pourra utiliser un [environnement virtuel python](https://docs.python.org/fr/3/library/venv.html) pour éviter les conflits de dépendances. 

- **VueJS**   
Plusieurs solutions sont possibles pour créer une application VueJS, nous utiliserons le gestionnaire de paquets **<u>npm</u>** et l'outil [Vue CLI](https://cli.vuejs.org/#getting-started).       
Ce [tutoriel](https://vuejs.org/guide/quick-start.html) montre les différentes étapes à suivre.


### Création des dockerfile
Chaque projet doit contenir son **dockerfile**. Ce fichier permet de créer une image de notre application qu'on pourra construire puis déployer dans un serveur de notre choix.  

Pour notre projet la partie django sera appelée `backend` et la partie VueJS, `frontend`.

Voici par exemple le dockerfile du backend.
```
FROM python:3.10-slim-buster

# Set working directory (inside image)
WORKDIR /app

# Install dependencies
COPY requirements.txt .

RUN apt-get update \
    && apt-get -y install libpq-dev gcc \
    && apt-get -y install python3-dev \
    && pip install psycopg2

RUN pip install --no-cache-dir -r requirements.txt


# Copy the source code
COPY ../ .


# Start the server

CMD ["gunicorn", "--preload", "--bind", "0.0.0.0:8000", "backend.wsgi:application"]
```