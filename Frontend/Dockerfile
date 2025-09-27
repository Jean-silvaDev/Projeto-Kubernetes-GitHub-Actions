# Etapa 1 - Compila o TypeScript
FROM node:20-alpine as build
WORKDIR /
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build   # compila para /dist

# Etapa 2 - Servir os arquivos compilados
FROM nginx:alpine
COPY --from=build /dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]