# Etapa 1: Build
FROM node:20-slim AS build
WORKDIR /usr/src/app

COPY package*.json tsconfig.json ./
RUN npm install --legacy-peer-deps

COPY . .

RUN npm run build

# Etapa 2: Servir com Nginx
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

RUN rm -rf ./*
COPY --from=build /usr/src/app/dist .

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]