FROM node:17-alpine AS builder
WORKDIR /app
ARG host
ARG port
ARG databaseName
ARG username
ARG password
ENV DATABASE_HOST=${host}
ENV DATABASE_PORT=${port}
ENV DATABASE_NAME=${databaseName}
ENV DATABASE_USERNAME=${username}
ENV DATABASE_PASSWORD=${password}
COPY ./capslol_backend/package*.json ./
RUN npm install
COPY ./capslol_backend/ ./
RUN npm run migration:run
RUN npm run build


FROM node:17-alpine AS server
WORKDIR /app
COPY ./capslol_backend/package*.json ./
EXPOSE 3000
RUN npm install --production
RUN npm install pm2 -g
COPY --from=builder ./app/dist ./build
CMD ["pm2-runtime", "./build/main.js"]