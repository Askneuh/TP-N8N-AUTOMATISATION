# Guide d'installation

1. [Installation Prérequis](#1-prérequis)
2. [Installation de n8n en self-host avec Docker](#-2-installation-de-n8n-en-self-host-avec-docker)
    1. [Docker](#avec-docker)
    2. [Docker Compose](#avec-docker-compose)

## 1. Prérequis

Pour pouvoir utiliser n8n, il vous faudra ces prérequis : 
> - Docker Desktop ou docker,
> - Une connexion internet,
> - Git pour le contenu du TP.

Avant de commencer le TP il faudra le cloner.

```
git clone https://github.com/Askneuh/TP-N8N-AUTOMATISATION.git
```

## 🛠 2. Installation de n8n en self-host avec Docker

### Avec Docker

#### Prérequis

Avoir docker sur sa machine

#### Lancement de l'instance

Ouvrez un terminal et collez la commande suivante :
```
docker volume create n8n_data

docker run -it --rm \
 --name n8n \
 -p 5678:5678 \
 -v n8n_data:/home/node/.n8n \
 docker.n8n.io/n8nio/n8n
```

Une fois le conteneur démarré, accédez à l'interface sur : [http://localhost:5678](http://localhost:5678)

### Avec Docker Compose

Dans le dossier ``DOCKER`` vous allez retrouver un ficher ``.env`` et un fichier ``docker-compose.yaml`` il s'agit d'un docker compose pour tester n8n pour le développement. 

**Attention ! :  Vos port 80 et 8080 devront être libres !**

```
cd DOCKER

docker compose up -d
```
---

A partir de ce stade, vous devriez voir cela dans docker desktop ou dans ``docker ps`` : 

|![docker-desk](./TUTORIAL_IMAGES/image.png)|![term](./TUTORIAL_IMAGES/image2.png)|
|--|--|

Avec Docker compose il vous suffira d'allez sur [http://localhost](http://localhost)