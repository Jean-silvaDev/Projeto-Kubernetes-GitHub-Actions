# Etapa 1: Build com Node
FROM node:20-slim AS build

WORKDIR /usr/src/app

# Copia configs e instala dependências
COPY package*.json tsconfig.json ./
RUN npm install --legacy-peer-deps

# Copia código-fonte
COPY . .

# Compila TypeScript
RUN npm run build
# Copia os arquivos estáticos pro dist
RUN cp index.html dist/ && cp styles.css dist/

# Etapa 2: Servir com Nginx
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

# Limpa pasta padrão
RUN rm -rf ./*

# Copia build gerado
COPY --from=build /usr/src/app/dist .

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]