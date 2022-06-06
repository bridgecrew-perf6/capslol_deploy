FROM node:17-alpine AS builder
WORKDIR /app
COPY ./capslol_frontend/package*.json ./
RUN npm install
COPY ./capslol_frontend/ ./
RUN npm run build --openssl-legacy-provider

# production environment
FROM nginx:1.19.10-alpine AS server
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 80
EXPOSE 8080
EXPOSE 443
CMD ["nginx", "-g", "daemon off;"]