[[_TOC_]]

## DOCKER USEFUL COMMANDS

## `$ docker ps`
#### - Affiche une liste des conteneurs en cours d'exécution.

## `$ docker logs <container_id>`
#### - Affiche les logs (journaux) du conteneur spécifié.

## `$ docker exec -it <container_id> bash`
#### - Ouvres un terminal correspondant au conteneur qui a été créé.
NB : Attention pour que cette commande marche il faut bien récupérer l'id du conteneur et non celui de l'image. Il faut donc exécuter `docker ps` pour voir l'id et l'utiliser dans la commande exec. 

## `$ docker rmi <image_name_or_id>`
#### - Supprimes une image docker ; ajouter `-f` pour forcer la suppression 

## `$ docker build -t <image_name>:<version> <docker_file_directory>`
#### - Crées une image à partir du dockerfile trouvé dans le répertoire spécifié.


# `$ docker run -p  10000:8000 <container_id>`
#### - Cette commande permet de rediriger la sortie sur le port 10000 de la machine locale : expose le réseau du conteneur au réseau local
---     



# `$ docker stop $(docker ps -q)`
#### - Cette commande permet d'arrêter tous les conteneurs en cours d'exécution


---