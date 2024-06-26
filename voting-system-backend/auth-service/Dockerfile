FROM node:18.19.0

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm install bcrypt --build-from-source

EXPOSE 5001

CMD ["node", "index.js"]
