
# Création d'un environnement Gitlab (Django, Vue JS, PostgreSQL)
Ce document répertorie les différentes étapes pour créer un environnement sur Gitlab.

## I- Initialiser les projets Django et Vue JS
- Pour initialiser le projet django, il faut d'abord s'assurer que la librairie est installée dans l'environnement actuel.  
Dans le cas échéant tapez la commande suivante sur le terminal :   
`$ django-admin startproject nom_du_projet`

    Cette commande génère une arborescence de fichiers python qui permettent de configurer notre application web. Pour lancer le serveur, il suffit de taper  
    `$ python manage.py runserver`

- Pour initialiser le projet VueJS plusieurs solutions sont possibles. Nous utiliserons [**Vue CLI**](https://cli.vuejs.org/#getting-started). Le lien qui précède documente clairement les différentes étapes à suivre.


## Instructions de déploiement
Dans cet extrait de code, on déploie la partie backend d'une application web dans un environnement appelé **`prod`**.

```yaml
(...)
deploy_backend_prod:
  stage: deploy
  extends: .aws_k8s
  script:
    - kubectl apply -f backend/deployment.yaml
  environment:
    name: prod
  only:
    - master   
(...)    
```