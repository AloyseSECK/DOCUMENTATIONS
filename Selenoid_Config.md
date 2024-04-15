# COMMENT CONFIGURER SELENOID POUR EXECUTER DES TESTS SUR DOCKER

[Documentation officielle](https://aerokube.com/cm/latest/)
[Autre Documentation](https://www.jetbrains.com/help/aqua/selenium.html#selenoid-cross-browser-testing)

## Installation de Selenoid
1. Récupérer le binaire du configuration manager sur [github](https://github.com/aerokube/cm/releases/tag/1.8.7) puis taper les commandes suivantes:
- Pour permettre l'exécution du binaire et de docker en mode utilisateur normal 
```bash	
sudo usermod -aG docker $USER
```
Redémarrer la machine pour que les changements prennent effet
- Pour donner les droits d'exécution au binaire
```bash
chmod +x cm_darwin_amd64
```
- Ensuite tapez : 
```bash
./cm_darwin_amd64 selenoid start --vnc
```
