# Comment déployer microsoft office localement et manuellement sur son PC

## Télécharger le [Office Deployment Tool](https://www.microsoft.com/en-us/download/details.aspx?id=49117)

## Indiquer puis télécharger les options de configuration xml à partir du site web https://config.office.com. Appuyer sur le bouton créer une configuration

## Une fois le fichier configuration.xml téléchargé, placez le dans un dossier OFFICE avec l'outil de déploiement.

## Exécuter l'outil de déploiement dans le dossier ; des fichiers seront produits dans le répertoire.

## Ouvrir le terminal en mode administrateur

## Accéder au répertoire OFFICE qui a été créé

## Enfin tapez la commande
```bash
setup.exe /configure Configuration.xml
```
Si tout se passe bien, l'utilitaire d'installation sera lancé.
