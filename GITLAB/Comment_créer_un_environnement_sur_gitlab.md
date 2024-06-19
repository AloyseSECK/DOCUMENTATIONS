# Configuration du projet pour un déploiement automatique CI/CD
Pour assurer un déploiement automatique sur Gitlab il faut passer par un certain nombre d'étapes.

1. <u>__Création du fichier **`.gitlab-ci.yml`**__</u>  
Le fichier ___.gitlab-ci.yml___ est un fichier de configuration qui servira à définir les étapes du pipeline de notre projet. Par conséquent, il doit être à la racine de ce dernier.

2. <u>__Configuration des étapes du pipeline__</u>  
Après avoir créé le fichier de configuration, il faut définir les étapes du pipeline comme la *compilation*, les *tests*, le *déploiement* etc. Ces étapes sont appelées __stages__ et dans le fichier de configuration, nous définirons plusieurs **jobs** dont chacun correspond à une étape précise.  
A noter que les **stages** s'exécutent dans l'ordre défini dans le fichier `.gitlab-ci.yml` et les **jobs** peuvent s'exécuter parallèlement s'ils appartiennent au même *stage*.


3. <u>__Configuration des déclencheurs__ </u>  
La dernière étape consiste à configurer les déclencheurs pour lancer automatiquement le pipeline CI/CD lorsqu'un commit est effectué sur une branche spécifique par exemple.

```yaml
stages:
  - build
  - test
  - deploy

variables:
  ENVIRONMENT: "production"

building:
  stage: build
  script:
    - echo "Building the application..."
    # Commandes de compilation
testing:
  stage: test
  script:
    - echo "Running tests..."
    # Commandes de test

merge_validation:
  stage: test
  script:
    - echo "Validating after merge..."
    # Commandes pour valider les changements après la fusion des branches
  only:
    - merge_requests  # Exécuter cette étape uniquement pour les demandes de fusion (merge requests)

deployment:
  stage: deploy
  script:
    - echo "Deploying to $ENVIRONMENT..."
    # Commandes de déploiement
  environment:
    name: production
    url: https://example.com
  only:
    - master  # Déployer uniquement depuis la branche master

```
Dans cet exemple nous avons 3 étapes : __build__, __test__ et __deploy__. Les jobs *testing* et *merge_validation* appartiennent à l'étape de <u>test</u> tandis que *building* et *deployment* appartiennent respectivement aux étapes <u>build</u> et <u>deploy</u>. Cet exemple est à adapter en fonction du projet. En effet, ici on fait uniquement des affichages dans les scripts mais il faudra écrire les vraies instructions de test, de compilation ... afin d'assurer le déploiement automatique de l'application.  

# Création d'un environnement sur gitlab

Un environnement est soit **<u>statique</u>** soit **<u>dynamique</u>**.

+ **Environnements statiques**  
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

+ **Environnements dynamiques**
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
Dans l'exemple ci-dessus, chaque fois que le job *deploy_review_app* est exécuté, le nom de l'environnement est défini en utilisant la variable  `$CI_COMMIT_REF_SLUG`.

