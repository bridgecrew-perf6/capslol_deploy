FROM node:17-alpine AS builder
WORKDIR /app
COPY ./capslol_frontend/package*.json ./
RUN npm install --production
ENV NODE_OPTIONS=”–max_old_space_size=2048″
COPY ./capslol_frontend/ ./
RUN npm run build

# production environment
FROM nginx:1.19.10-alpine AS server
COPY --from=builder /app/build /usr/share/nginx/html
ENV NODE_OPTIONS=”–max_old_space_size=2048″
EXPOSE 80
EXPOSE 8080
EXPOSE 443
CMD ["nginx", "-g", "daemon off;"]