# Etapa 1: Build com Node
FROM node:18 AS build
WORKDIR /app

COPY package*.json tsconfig.json ./
RUN npm install
COPY . .

# Compila o TypeScript
RUN npm run build

# Copia o index.html e styles.css pro dist
RUN cp index.html dist/ && cp styles.css dist/


# Etapa 2: Servir com Nginx
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

RUN rm -rf ./*

COPY --from=build /app/dist .

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]