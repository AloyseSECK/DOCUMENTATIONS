# Création d'un environnement sur gitlab

Un environnement est soit **<u>statique</u>** soit **<u>dynamique</u>**.

- **Environnements statiques**  
    Les environnements statiques ont 3 particularités : 
    - Leur nom est fixe, ils ne subissent pas de modifications lorsqu'on effectue un déploiement. Par exemple, *preproduction*, *test* et *production* sont des noms d'environnements statiques.
    - Ils sont souvent réutilisés par plusieurs déploiements.
    - Ils sont créés manuellement.  

    Leur création peut se faire soit dans **`l'interface gitlab`** soit dans le fichier **`.gitlab-ci.yml`**
    - **Dans l'interface gitlab** :   
    Sur le volet latéral de notre projet, il suffit de cliquer sur   
    `Operate` ,  
    `Environments` puis   
    `Create an environment`  
    
        Une fenêtre contextuelle s'affiche et on remplit les champs.
    
    - **Dans le fichier .gitlab-ci.yml** :  
    L'extrait de code suivant illustre un "job" appelé *deploy_backend_prod* qui déploie notre application `backend` dans un environnement appelé **`production`**.
    ```yaml
    deploy_backend_prod:
      stage: deploy
      extends: .aws_k8s
      script:
        - kubectl apply -f backend/deployment.yaml
      environment:
        name: production
      only:
        - master   
    ```

- **Environnements dynamiques**
Les environnements dynamiques eux, sont spécifiques à chaque déploiement et utilisent des variables CI/CD qui sont uniques pour chaque [pipeline](https://docs.gitlab.com/ee/ci/pipelines/).

Pour en créer, nous utiliserons le fichier **`.gitlab-ci.yml`**. 
```yaml
deploy_review_app:
  stage: deploy
  script: make deploy
  environment:
    name: review/$CI_COMMIT_REF_SLUG
    url: https://$CI_ENVIRONMENT_SLUG.example.com
  rules:
    - if: $CI_COMMIT_BRANCH == "main"
      when: never
    - if: $CI_COMMIT_BRANCH

```
Danc l'exemple ci-dessus, chaque fois que le job *deploy_review_app* est exécuté, le nom de l'environnement est défini en utilisant la variable  `$CI_COMMIT_REF_SLUG`.