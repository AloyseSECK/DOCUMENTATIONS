# Comment configurer un runner Gitlab
## Installation
### Installation du runner
```bash
sudo apt-get install gitlab-runner
```
### Enregistrement du runner
```bash
sudo gitlab-runner register
```
### Configuration du runner
```bash
sudo nano /etc/gitlab-runner/config.toml
```
```toml
[[runners]]
  name = "runner_name"
  url = "https://gitlab.com/"
  token
    executor = "shell"
    shell = "bash"
```
### Démarrage du runner
```bash
sudo gitlab-runner start
```
### Vérification du runner
```bash
sudo gitlab-runner verify
```
### Arrêt du runner
```bash
sudo gitlab-runner stop
```
### Suppression du runner
```bash
sudo gitlab-runner uninstall
```
