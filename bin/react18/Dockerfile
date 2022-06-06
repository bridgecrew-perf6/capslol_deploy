
FROM node:17
WORKDIR /app
COPY ./capslol_frontend/package*.json ./
RUN npm install
COPY ./capslol_frontend/ ./
EXPOSE 3000
CMD [ "npm","run","start" ]