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

## Frontend

```
version: '3.8'
> 
services:
  mongo:
      > permet de spécifier l'image source pour le conteneur
      image: mongo
      > permet de définir le comportement du conteneur en cas d'arrêt du processus, ici reboot
      restart: always
      expose:
        - 27017

      ports:
        - 27017:27017

  backend:
    > permet de spécifier le Dockerfile source pour créer l'image du conteneur
    build: ./backend/
    
    > permet de définir les ports disponibles entre la machine host et le conteneur
    ports:
      - 8080:8080
      
    > permet de dire que le conteneur dépend d'un autre conteneur
    depends_on:
      - mongo
  
  frontend:
    build: ./frontend
   
    ports:
      - 3000:3000
```
