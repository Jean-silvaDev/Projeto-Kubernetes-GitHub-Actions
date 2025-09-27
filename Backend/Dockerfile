# Usar imagem oficial do Node
FROM node:20-alpine

# Criar diretório da aplicação
WORKDIR /app

# Copiar package.json e instalar dependências
COPY package*.json ./
RUN npm install

# Copiar código da aplicação
COPY . .

# Expor a porta
EXPOSE 5000

# Rodar a aplicação
CMD ["npm", "start"]