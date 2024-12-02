FROM node:alpine

ENV MONGO_DB_USERNAME=root \
    MONGO_DB_PWD=password

WORKDIR /src

COPY ./src/app-server/src/package.json .
RUN npm install

COPY ./src/app-server/src/server.js .

CMD ["node", "server.js"]