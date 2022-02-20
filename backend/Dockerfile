FROM node:current-alpine3.15

COPY package.json /app/package.json

WORKDIR /usr/src/app

COPY . .

RUN npm install

EXPOSE 8080

CMD [ "npm", "start"]