# Comment intégrer une application dans Selenium 

Dans cette documentation, il sera présenté une méthode pour intégrer une application dans Selenium. Pour cela, 3 sujets seront abordés  :  comment écrire des tests, comment les exécuter et finalement comment récupérer les résultats des tests effectués.

Mais tout d'abord, qu'est-ce que Selenium ?

## Qu'est-ce que Selenium ?

Selenium est un ensemble d'outils de tests automatisés qui permet de tester des applications WEB. Son composant principal est __Selenium WebDriver__, qui permet de piloter un navigateur web et d'effectuer des actions dessus que nous détaillerons dans les parties suivantes.  

Pour intégrer une application dans Selenium, nous utiliserons l'IDE Aqua développé par Jetbrains qui a été spécifiquement conçu pour ce cas d'usage. En effet, l'IDE Aqua dispose d'un environnement de développement intégré qui permet de créer, d'exécuter et d'analyser des tests avec selenium. L'avantage principal est qu'il ne nécessite pas 
de télécharger de webdriver pour le navigateur que vous souhaitez utiliser.

## Ecriture des tests
Il est possible d'écrire des tests en utilisant plusieurs langages de programmation, dont Java, Python, C#, Ruby, etc. Dans cette documentation, nous utiliserons python et la librairie pytest. 
Pour cela, l'IDE Aqua propose un environnement préconfiguré qui permet de créer des tests en python. Il suffit donc de sélectionner cette option lorsque l'on crée un nouveau projet comme illustré dans la figure suivante.

![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/New_Project_Aqua.png)  
<u>  **Figure 1 : Initialisation du projet** </u>

Une fois le projet créé, voici l'arborescence de fichiers que l'on obtient.   

![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/Arborescence_du_projet.png)  
<u>  **Figure 2 : Arborescence du projet** </u>

Par défaut, les scripts de tests se situent dans le fichier test.py.
Cependant, pour des raisons pratiques, nous allons créer un répertoire nommé ``tests`` dans lequel tous les scripts de test de notre application WEB seront stockés.
Le répertoire ``reports`` contiendra les rapports de tests générés par pytest dont nous parlerons dans la dernière partie de cette documentation.

La documentation officielle de [Selenium](https://www.selenium.dev/documentation/) recommande d'utiliser le design pattern [Page Object Model (POM)](https://www.selenium.dev/documentation/test_practices/encouraged/page_object_models/) pour écrire des tests. Ce design pattern permet de séparer la logique de test de la logique de l'application. Il permet également de réduire la duplication de code et de faciliter la maintenance des tests.
Voici à quoi ressemble l'arborescence du projet avec ce design pattern :    

![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/Arborescence_du_projet_avec_POM.png)   
<u>  **Figure 3 : Arborescence du projet avec le design pattern POM** </u>   

Comme illustré dans la figure ci-dessus, le répertoire ``pages`` contient des classes qui représentent chacunes des pages de l'application. Chaque classe dispose de méthodes qui permettent d'interagir avec les éléments de la page.  

Dans l'exemple suivant, nous avons la classe AdminPage qui représente la page d'administration de notre application. Cette classe dispose de méthodes qui permettent de se connecter, de se déconnecter, de naviguer vers la page des utilisateurs, de supprimer un utilisateur, etc. La librairie selenium contient un package nommé [**By**](https://www.selenium.dev/selenium/docs/api/java/org/openqa/selenium/By.html) qui permet de sélectionner des éléments de la page en utilisant des sélecteurs CSS, XPATH, etc. L'IDE Aqua quant à lui propose une fonctionnalité qui permet de générer automatiquement les sélecteurs CSS et XPATH des éléments de la page : c'est le __*Web Inspector*__. 

```python
# pages/AdminPage.py
from pages import By, webdriver, DEFAULT_PASSWORD, ADMIN_USERNAME

class AdminPage:
    def __init__(self, driver: webdriver):
        self.driver = driver
        self.driver.get("http://127.0.0.1:8000/admin")
        self.username_input = self.driver.find_element(By.CSS_SELECTOR, "#id_username")
        self.password_input = self.driver.find_element(By.CSS_SELECTOR, "#id_password")
        self.log_in_button = self.driver.find_element(By.CSS_SELECTOR, "input[value$='in']")

    def log_in(self):
        self.username_input.send_keys(ADMIN_USERNAME)
        self.password_input.send_keys(DEFAULT_PASSWORD)
        self.log_in_button.click()

    def get_title(self):
        h1 = self.driver.find_element(By.CSS_SELECTOR, "h1")
        return h1.text

    def go_to_users_page(self):
        users_page = self.driver.find_element(By.XPATH, "//*[text() = 'Users']")
        users_page.click()

    def get_user(self, username):
        return self.driver.find_element(By.XPATH, f"//*[text() = '{username}']")
        
    def delete_user(self, username):
        user = self.get_user(username)
        user.click()
        delete_button = self.driver.find_element(By.CSS_SELECTOR, "a[class='deletelink']")
        delete_button.click()
        self.driver.find_element(By.CSS_SELECTOR, "input[value$='sure']").click()
    
    def log_out(self):
        button_log_out = self.driver.find_element(By.XPATH, "//button[@type='submit']")
        button_log_out.click()

```

#### Web Inspector  
Pour utiliser le __*Web Inspector*__, il faut cliquer sur son icône à droite dans la barre d'outils de l'IDE Aqua. Ensuite, il suffit de cliquer sur l'élément de la page que vous souhaitez inspecter. L'IDE Aqua affiche alors les sélecteurs CSS et XPATH de l'élément sélectionné comme illustré dans la figure suivante. En cliquant sur le bouton **+**, l'élément sera ajouté directement dans le script de test.

![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/Web_Inspector.png)    
<u>  **Figure 4 : Web Inspector** </u>   

Dans la suite, il faut rédiger les scripts de test. Pour ce faire, il suffit de créer un fichier python dans le répertoire ``tests``. Le nom du fichier doit soit commencer par le mot clef ``test_``, soit se terminer par ``_test`` afin qu'il soit reconnu comme un fichier qui exécute des tests. Par exemple, ``test_admin_page.py`` ou ``admin_page_test.py`` sont des noms de fichier valides. 


Voici un exemple de script de test qui utilise la classe AdminPage pour tester la page d'administration de notre application ainsi qu'une autre page qui permet d'inscrire un utilisateur dans notre application WEB. 
Il y a donc deux tests : 
- Le premier test __*(test_admin_login(self))*__ vérifie si l'administrateur peut se connecter à la page d'administration.
- Le second test __*(test_sign_up_with_vue(self))*__ vérifie si un utilisateur peut s'inscrire dans notre application WEB et si cet utilisateur est bien ajouté à la base de données. Après le test, l'utilisateur est supprimé de la base de données.    

<u>Remarques :</u> Les méthodes de test commencent toutes par le mot clef **test_**. De plus, le driver utilisé est celui de Chrome mais il est possible de changer le driver en fonction du navigateur que vous souhaitez utiliser. Enfin, la méthode __*(browser_setup_and_teardown)*__ est une [__fixture__](https://docs.pytest.org/en/stable/explanation/fixtures.html) qui permet de configurer le driver avant et après chaque test.  

```python
# tests/test_application.py
import time
import pytest
from selenium import webdriver
from pages.AdminPage import AdminPage
from pages.SignUpPage import SignUpPage


class TestApp:
    # 1. Check driver configuration in browser_setup_and_teardown
    # 2. Run 'Selenium Tests' configuration
    # 3. Test report will be created in reports/ directory
    username = "Marcus Brown"
    password = "password123"

    @pytest.fixture(autouse=True)
    def browser_setup_and_teardown(self):
        self.driver = webdriver.Chrome()

        self.driver.maximize_window()
        self.driver.implicitly_wait(10)

        yield

        self.driver.close()
        self.driver.quit()

    def test_admin_login(self):
        admin_page = AdminPage(self.driver)
        admin_page.log_in()
        assert admin_page.get_title() == "Site administration"

    def test_sign_up_with_vue(self):
        sign_up_page = SignUpPage(self.driver)
        sign_up_page.sign_up(self.username)
        time.sleep(5)

        # check if the user has been added to the database
        admin_page = AdminPage(self.driver)
        admin_page.log_in()
        admin_page.go_to_users_page()
        assert admin_page.get_user(self.username) is not None
        admin_page.delete_user(self.username)
        admin_page.log_out()

```

## Exécution des tests
L'exécution des test se fait en utilisant la commande suivante : 
```bash
pytest tests/ 
```
Cette commande permet d'exécuter tous les tests qui se trouvent dans le répertoire ``tests``. Pour que cette commande fonctionne, il faut que les noms des fichiers et des fonctions de test respectent le format ( *test_nom_de_fichier.py ou nom_de_fichier_test.py* ). Il est également possible d'exécuter les tests individuellement en spécifiant le nom du fichier de test. Par exemple, pour exécuter les tests du fichier 
``test_application.py``, il suffit de taper la commande suivante : 

```bash 
pytest tests/test_application.py
```

Pour ne pas avoir à taper la commande sur le terminal, l'IDE Aqua propose une fonctionnalité qui permet d'exécuter les tests directement depuis l'IDE. Pour cela, il suffit de cliquer sur l'icône de la flèche verte sur la barre supérieure de la fenêtre de l'application.

![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/Run_Tests.png)

Il est nécessaire d'éditer la configuration de l'éxécution des tests pour spécifier le répertoire dans lequel se trouvent les tests. Pour cela, il faut cliquer sur l'icône des 3 points à droite de la flèche verte, puis sur **Edit Configurations**. Ensuite, il faut spécifier le répertoire dans lequel se trouvent les tests comme illustré dans la figure suivante.

![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/Edit_Configuration.png)

## Récupération des résultats
En ce qui concerne la récupération des résultats des tests, il est possible de le faire en rajoutant l'option ``--html=reports/report.html`` à la commande de test. Par exemple, pour exécuter les tests du fichier ``test_application.py`` et générer un rapport de test, il suffit de taper la commande suivante : 

```bash
pytest tests/test_application.py --html=reports/report.html
```

Cette commande permet à pytest de générer un rapport qui contient des informations sur les tests qui ont été exécutés. Ce rapport est généré dans le répertoire ``reports``. Pour visualiser le rapport, il suffit d'ouvrir le fichier ``report.html`` avec un navigateur web.
Les résultats sont tout de même affichés dans la console après l'exécution des tests.

La figure suivante montre un exemple de rapport de test généré par pytest.
![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Selenium%20DOCS%20img/Test_Report.png)

On peut voir que les deux tests ont été exécutés. Le premier test (*__test_admin_login()__*) a réussi tandis que le second (__*test_sign_up_with_vue()*__) a échoué. Le rapport contient également des informations sur le temps d'exécution des tests, le nom du fichier de test, le nom de la méthode de test, etc.