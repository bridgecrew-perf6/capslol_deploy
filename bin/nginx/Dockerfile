FROM node:16-alpine AS builder
ENV REACT_APP_GOOGLE_CLIENT_ID=""
ENV REACT_APP_PROD_SERVER_URL="http://159.223.13.78:8080/api/"
WORKDIR /app
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