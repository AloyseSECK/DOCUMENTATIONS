# Comment Intégrer Une Application Dans Selenium 

Dans cette documentation, il sera présenté une méthode pour intégrer une application dans Selenium. Pour cela, 3 sujets seront abordés  :  comment écrire des tests, comment les exécuter et finalement comment analyser les résultats.

Mais tout d'abord, qu'est-ce que Selenium ?

## Qu'est-ce que Selenium ?

Selenium est un ensemble d'outils de tests automatisés qui permet de tester des applications web. Son composant principal est __Selenium WebDriver__, qui permet de piloter un navigateur web et d'effectuer des actions dessus que nous détaillerons dans les parties suivantes.  

Pour intégrer une application dans Selenium, nous utiliserons l'IDE Aqua développé par Jetbrains qui a été spécifiquement conçu pour ce cas d'usage. En effet, l'IDE Aqua dispose d'un environnement de développement intégré qui permet de créer, d'exécuter et d'analyser des tests avec selenium. L'avantage principal est qu'il ne nécessite pas 
de télécharger de webdriver pour le navigateur que vous souhaitez utiliser.

## Ecriture des tests
Il est possible d'écrire des tests en utilisant plusieurs langages de programmation, dont Java, Python, C#, Ruby, etc. Dans cette documentation, nous utiliserons python et la librairie pytest. 
Pour cela, l'IDE Aqua propose un environnement préconfiguré qui permet de créer des tests en python. Il suffit donc de sélectionner cette option lorsqu'on crée un nouveau projet comme illustré dans la figure suivante.

![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/New_Project_Aqua.png)  
<u>  **Figure 1 : Choix du projet** </u>

Une fois le projet sélectionné, voici l'arborescence de fichiers que l'on obtient.   

![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Arborescence_du_projet.png)  
<u>  **Figure 2 : Arborescence du projet** </u>

Par défaut, les scripts de tests se situent dans le fichier test.py.
Pour des raisons pratiques, nous allons créer un répertoire nommé ``tests`` dans lesquels tous les scripts de test de notre application WEB vont figurer.
Le répertoire ``reports`` contiendra les rapports de tests générés par pytest dont nous parlerons à la dernière partie de cette documentation.

La documentation officielle de [Selenium](https://www.selenium.dev/documentation/) recommande d'utiliser le design pattern [Page Object Model](https://www.selenium.dev/documentation/test_practices/encouraged/page_object_models/) pour écrire des tests. Ce design pattern permet de séparer la logique de test de la logique de l'application. Il permet également de réduire la duplication de code et de faciliter la maintenance des tests.
Voici à quoi ressemble l'arborescence du projet avec le design pattern Page Object Model : 
![image](https://raw.githubusercontent.com/AloyseSECK/DOCUMENTATIONS/main/Images/Arborescence_du_projet_avec_POM.png)

Pour écrire un test, il suffit de créer un fichier python dans le répertoire ``tests``. Voici un exemple de test qui permet de vérifier si le titre de la page d'accueil de notre application est correct.


```python
from selenium import webdriver


```

## Exécution des tests

## Analyse des résultats


