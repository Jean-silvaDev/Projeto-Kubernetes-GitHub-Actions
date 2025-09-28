# Etapa 1: Build com Node
FROM node:18 AS build
WORKDIR /app

COPY package*.json tsconfig.json ./
RUN npm install
COPY . .

# Compila o TypeScript + copia estáticos
RUN npm run build

# Etapa 2: Servir com Nginx
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

# Limpa arquivos antigos do Nginx
RUN rm -rf ./*

# Copia os artefatos do build
COPY --from=build /app/dist .

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]