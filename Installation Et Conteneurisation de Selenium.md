# Installation & Conteneurisation de Selenium 

## Installation de Selenium et initialisation du projet
Pour initialiser un projet selenium, il faut d'abord installer les dépendances nécessaires. Pour cela, deux options s'offrent à vous :
- Installer les dépendances manuellement en utilisant le fichier `requirements.txt` fourni dans cette documentation. Il est recommandé d'utiliser un environnement virtuel pour l'installation.
- Générer un template de projet "*selenium with pytest*" en utilisant l'IDE [Aqua](https://www.jetbrains.com/fr-fr/aqua/) de Jetbrains.


### Installation manuelle des dépendances
Voici le contenu du fichier `requirements.txt`. 
Créez un environnement virtuel et installez les dépendances en utilisant la commande suivante :
```bash
pip install -r requirements.txt
```
```requirements.txt
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
**NB** : Les versions des dépendances sont susceptibles de changer. Il est donc préférable de générer le template de projet avec l'IDE Aqua pour avoir les dernières versions. 

Une fois les dépendances installées, placez les dossiers `src` et `locale` fournis dans la documentation à la racine du projet. Enfin vous pouvez exécuter les tests en utilisant la commande suivante:
```bash
pytest --html="reports/test_report.html" src/tests
```
Pour une exécution sur la machine locale, mettre la variable **EXECUTE_ON_SELENOID** à **False** dans le fichier ``src/pages/config_file.py``


### Génération du projet avec Aqua
Dans l'IDE [Aqua](https://www.jetbrains.com/fr-fr/aqua/), cliquez sur `New Project` pour créer un nouveau projet. L'image suivante illustre les options pour  l'initialisation du projet.    

![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/New_Project_Aqua.png)  
<u>  **Figure 1 : Initialisation du projet** </u>

Une fois le projet créé, voici l'arborescence de fichiers que l'on obtient.   

![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/Arborescence_du_projet.png)  
<u>  **Figure 2 : Arborescence du projet** </u>

Suppprimez le fichier test.py et le répertoire reports puis chargez les dossiers `src` et `locale` fournis dans la documentation à la racine du projet. L'exécution des tests suit la même procédure que pour l'installation manuelle des dépendances.

## Conteneurisation de Selenium
Pour conteneuriser Selenium, il faut d'abord installer Docker sur votre machine. Pour cela, suivez les instructions sur le site officiel de [Docker](https://docs.docker.com/get-docker/).   
L'exécution des tests sur docker peut se faire en utilisant les images Selenoid et Selenoid-UI. La section suivante explique comment installer Selenoid et Selenoid-UI.

### Installation de Selenoid
Le *configuration manager* est un outil utilisé pour gérer automatiquement les conteneurs selenoid et selenoid-ui. Il permet de démarrer, arrêter et mettre à jour les conteneurs.
Voici les étapes à suivre pour lancer les conteneurs selenoid et selenoid-ui:

1. Récupérer le binaire du configuration manager sur [github](https://github.com/aerokube/cm/releases/tag/1.8.7).
2. Marquer le fichier binaire comme exécutable en utilisant la commande suivante:
```bash
chmod +x cm_darwin_amd64
```
3. Autoriser l'exécution du binaire et de docker en mode utilisateur normal en utilisant la commande suivante:
```bash
sudo usermod -aG docker $USER
```
Il faut redémarrer la machine pour que les changements puissent prendre effet

4. Démarrer le conteneur avec l'image de selenoid: 
```bash
./cm_darwin_amd64 selenoid start --vnc
```

5. Démarrer le conteneur avec l'image de selenoid-ui: 
```bash
./cm_darwin_amd64 selenoid-ui start 
```

Une fois les conteneurs démarrés, vous pouvez accéder à l'interface graphique de Selenoid en utilisant le lien http://localhost:8080.
 
Vérifiez que la variable EXECUTE_ON_SELENOID dans `src/pages/config_file.py` est à True puis lancer les tests en utilisant la commande suivante:
```bash
pytest --html="reports/test_report.html" src/tests
```