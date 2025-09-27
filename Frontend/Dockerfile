# Etapa 1 - Compila o TypeScript
FROM node:20-alpine as build
WORKDIR /app
COPY package*.json ./

# Adicione estas linhas para limpar o cache e o arquivo de bloqueio
RUN npm cache clean --force
RUN rm -f package-lock.json

RUN npm install
COPY . .
RUN npm run build  # compila para /app/dist

# Etapa 2 - Servir os arquivos compilados
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]