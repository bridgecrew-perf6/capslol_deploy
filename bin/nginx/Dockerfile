FROM node:17-alpine AS builder
WORKDIR /app
ENV REACT_APP_GOOGLE_CLIENT_ID=361222498523-k30tc2octab8mtoahcbb899fqs5j53pa.apps.googleusercontent.com
ENV REACT_APP_SERVER_URL=http://159.223.1378:8080/
COPY ./capslol_frontend/package*.json ./
RUN npm install
COPY ./capslol_frontend/ ./
RUN npm run build

# production environment
FROM nginx:1.19.10-alpine AS server
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 80
EXPOSE 8080
EXPOSE 443
CMD ["nginx", "-g", "daemon off;"]