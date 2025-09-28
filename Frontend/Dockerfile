# Etapa 1: Construção (Build)
FROM node:20-slim AS build

WORKDIR /usr/src/app

# Copia arquivos de dependência e instala
COPY package*.json tsconfig.json ./
RUN npm install --legacy-peer-deps

# Copia o restante do código
COPY . .

# Compila TypeScript e copia arquivos estáticos
RUN npx tsc && cp index.html dist/ && cp styles.css dist/

# Etapa 2: Servir com Nginx
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

# Limpa o conteúdo padrão do nginx
RUN rm -rf ./*

# Copia apenas o resultado do build
COPY --from=build /usr/src/app/dist .

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]