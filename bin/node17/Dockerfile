FROM node:17-alpine AS builder
WORKDIR /app
COPY ./capslol_backend/package*.json ./
RUN npm install
COPY ./capslol_backend/ ./
RUN npm run build
RUN  npm run seed:run


FROM node:17-alpine AS server
WORKDIR /app
COPY ./capslol_backend/package*.json ./
EXPOSE 3000
RUN npm install --production
RUN npm install pm2 -g
COPY --from=builder ./app/dist ./build
CMD ["pm2-runtime", "./build/main.js"]