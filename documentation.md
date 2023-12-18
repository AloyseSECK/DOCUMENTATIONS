# Comment créer un environnement sur gitlab 

### Deux solutions :  

## Création de l'environnement dans l'interface de gitlab

- Cliquer sur le bouton `Operations`
- Puis `Environments`
- Enfin `New Environment`  

**Il suffit de suivre les différentes étapes de création**

## Création dans un fichier de configuration yaml
Dans un fichier yml, il faut spécifier le nom de l'environnement comme suit : 

```
deploy: 
    stage: deploy
    when: manual 
    script: 
        - echo "Deploy to production"
    environment: 
        name: production
    only: 
        - main          
```
Dans cet exemple le nom de l'environnement est production et le script exécuté est un simple affichage mais en pratique il faudra exécuter les commandes nécessaires pour déployer l'application.


# Création d'un environnement Gitlab (Django, Vue JS, PostgreSQL)

## 1ère étape : Initialiser les projets Django et Vue JS