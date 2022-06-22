FROM node:17-alpine AS builder
WORKDIR /app
ARG clientId
ARG productionURL
ENV REACT_APP_GOOGLE_CLIENT_ID=${clientId}
ENV REACT_APP_SERVER_URL=${productionURL}
ENV REACT_APP_SOCKET_PROD_URL=${productionURL}
COPY ./capslol_frontend/package*.json ./
RUN npm install --legacy-peer-deps
COPY ./capslol_frontend/ ./
RUN npm run build

# production environment
FROM nginx:1.19.10-alpine AS server
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 80
EXPOSE 8080
EXPOSE 443
CMD ["nginx", "-g", "daemon off;"]