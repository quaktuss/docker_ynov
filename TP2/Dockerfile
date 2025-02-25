FROM node:12-alpine3.9

COPY package.json .
COPY ./src/index.js src/index.js

RUN npm install

CMD ["node", "src/index.js"]