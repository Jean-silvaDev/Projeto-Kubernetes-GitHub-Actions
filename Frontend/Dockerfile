# Etapa 1: Build
FROM node:20-slim AS build
WORKDIR /usr/src/app

# copia package.json / tsconfig
COPY package*.json tsconfig.json ./

# instala dependências (unsafe-perm evita problemas quando rodando como root)
RUN npm install --legacy-peer-deps --unsafe-perm=true

# copia código
COPY . .

# garante permissões razoáveis em node_modules (opcional, mas útil)
RUN chmod -R a+rX node_modules || true

# compilação: chama tsc via node (não precisa do bit executável)
RUN node ./node_modules/typescript/bin/tsc

# copia estáticos para dist (caso não esteja já no script)
RUN mkdir -p dist && cp -n index.html dist/ || true && cp -n styles.css dist/ || true

# Etapa 2: Nginx
FROM nginx:alpine
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*

COPY --from=build /usr/src/app/dist .

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]