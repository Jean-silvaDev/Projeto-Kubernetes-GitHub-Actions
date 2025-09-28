# Etapa 1: Construção (Build)
# Use a versão slim para uma imagem menor, e nomeie esta etapa como 'build'
FROM node:20-slim AS build

# Define o diretório de trabalho dentro do container
WORKDIR /usr/src/app

# Copia package.json e package-lock.json para instalar as dependências
# Isso permite que o Docker armazene a camada de 'install' em cache
COPY package*.json ./

# Instala as dependências (tsc está incluído aqui)
RUN npm install

# Mude para o usuário 'node' (um usuário não-root) para maior segurança
# Este é o ponto onde o erro de permissão geralmente ocorre se o tsc não for acessível
USER node

# Copia o restante dos arquivos da aplicação
COPY . .

# Executa o build usando o script atualizado (agora usando 'npx tsc')
# Como 'npx' é usado, a permissão e o caminho são resolvidos corretamente
RUN npm run build

# O Nginx stage (Etapa 2) que você forneceu continua abaixo deste.
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

RUN rm -rf ./*

COPY --from=build /usr/src/app/dist .

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]