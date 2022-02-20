# Projet Docker avec une architecture backend / frontend

L’objectifs de ce projet est d’intégrer le déploiement d’une API Rest avec Docker afin de pouvoir l’intégrer dans un système d’intégration continue.

## Backend

```
FROM node:current-alpine3.15
> permet de définir notre image de base

COPY package.json /app/package.json
> copie les dépendances

WORKDIR /usr/src/app
> permet de définir notre répertoire de travail

COPY . .
> copie les fichiers dans le répertoire précédent

RUN npm install
> permet d'exécuter une commande à l'intérieur de notre image, installation des dépendances

EXPOSE 8080
> permet d'indiquer quel port nous souhaitons partager

CMD [ "npm", "start"]
> indiquer quelle instruction doit s'exécuter au lancement de notre conteneur

```


## Frontend

```
FROM node:current-alpine3.15
> permet de définir notre image de base

COPY package.json /app/package.json
> copie les dépendances

WORKDIR /usr/src/app
> permet de définir notre répertoire de travail

COPY . .
> copie les fichiers dans le répertoire précédent

RUN npm install
> permet d'exécuter une commande à l'intérieur de notre image, , installation des dépendances

EXPOSE 3000
> permet d'indiquer quel port nous souhaitons partager

CMD [ "npm", "start"]
> indiquer quelle instruction doit s'exécuter au lancement de notre conteneur

```
