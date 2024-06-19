# Installation et Conteneurisation de Selenium

## Installation de Selenium et Initialisation du Projet
Pour mettre en place un projet Selenium, l'installation des dépendances est la première étape. Deux méthodes sont disponibles :

- **Installation Manuelle des Dépendances** :
  Pour cela, utilisez le fichier `requirements.txt` fourni dans cette documentation. Il est recommandé de créer un environnement virtuel pour l'installation. Voici le contenu du fichier `requirements.txt` :
  
  ```plaintext
  attrs==23.2.0
  certifi==2024.2.2
  charset-normalizer==3.3.2
  h11==0.14.0
  idna==3.6
  iniconfig==2.0.0
  Jinja2==3.1.3
  MarkupSafe==2.1.5
  outcome==1.3.0.post0
  packaging==24.0
  pluggy==1.4.0
  PySocks==1.7.1
  pytest==8.1.1
  pytest-base-url==2.1.0
  pytest-html==4.1.1
  pytest-metadata==3.1.1
  pytest-selenium==4.1.0
  pytest-variables==3.1.0
  python-dotenv==1.0.1
  requests==2.31.0
  selenium==4.19.0
  sniffio==1.3.1
  sortedcontainers==2.4.0
  tenacity==8.2.3
  trio==0.25.0
  trio-websocket==0.11.1
  typing_extensions==4.10.0
  urllib3==2.2.1
  webdriver-manager==4.0.1
  wsproto==1.2.0
  ```
  
  Après avoir créé l'environnement virtuel, installez les dépendances avec la commande :
  ```bash
  pip install -r requirements.txt
  ```
  
  Une fois les dépendances installées, placez les dossiers `src` et `locale` fournis dans la documentation à la racine du projet. Ensuite, vous pouvez exécuter les tests avec la commande suivante :
  ```bash
  pytest --html="reports/test_report.html" src/tests
  ```
  
  Pour une exécution en local, assurez-vous que la variable **EXECUTE_ON_SELENOID** dans le fichier `src/pages/config_file.py` est à **False**.

- **Génération du Projet avec Aqua** :
  Utilisez l'IDE [Aqua](https://www.jetbrains.com/fr-fr/aqua/) de Jetbrains pour générer un template de projet "*Selenium with Pytest*". Voici les étapes :
  
  1. Dans Aqua, cliquez sur `New Project` pour créer un nouveau projet.
  ![Initialisation du projet dans Aqua](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/New_Project_Aqua.png)
  
  2. Après la création, voici l'arborescence de fichiers obtenue :
  ![Arborescence du projet dans Aqua](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/Arborescence_du_projet.png)
  
  3. Supprimez le fichier `test.py` et le répertoire `reports`, puis importez les dossiers `src` et `locale` fournis dans la documentation à la racine du projet. L'exécution des tests suit la même procédure que pour l'installation manuelle des dépendances.

## Conteneurisation de Selenium
Pour conteneuriser Selenium, Docker doit être installé sur votre machine. Suivez les instructions sur le site officiel de [Docker](https://docs.docker.com/get-docker/).

L'exécution des tests avec Docker utilise les images Selenoid et Selenoid-UI. Voici les étapes pour installer Selenoid et Selenoid-UI :

### Installation de Selenoid
Le *configuration manager* est un outil essentiel pour gérer automatiquement les conteneurs Selenoid et Selenoid-UI. Il permet de démarrer, arrêter et mettre à jour les conteneurs. Suivez ces étapes :

1. Téléchargez le binaire du configuration manager depuis [github](https://github.com/aerokube/cm/releases/tag/1.8.7).
2. Rendez le fichier binaire exécutable avec la commande :
   ```bash
   chmod +x cm_darwin_amd64
   ```
3. Autorisez l'exécution du binaire et de Docker en mode utilisateur normal :
   ```bash
   sudo usermod -aG docker $USER
   ```
   Redémarrez la machine pour appliquer les changements.
4. Démarrez le conteneur avec l'image Selenoid :
   ```bash
   ./cm_darwin_amd64 selenoid start --vnc
   ```
5. Démarrez le conteneur avec l'image Selenoid-UI :
   ```bash
   ./cm_darwin_amd64 selenoid-ui start
   ```
Après le démarrage des conteneurs, accédez à l'interface graphique de Selenoid via le lien http://localhost:8080.

Assurez-vous que la variable **EXECUTE_ON_SELENOID** dans `src/pages/config_file.py` est à **True**, puis lancez les tests avec la commande :
```bash
pytest --html="reports/test_report.html" src/tests
```   
Sur l'interface web de Selenoid, vous pouvez observer les tests en cours d'exécution comme illustré dans l'image suivante :     

![Tests en cours d'exécution dans Selenoid-UI](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/selenoid-ui-running-test.png)