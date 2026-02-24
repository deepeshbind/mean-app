FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
# The app listens on 8080 as per your server.js
EXPOSE 8080
CMD ["node", "server.js"]