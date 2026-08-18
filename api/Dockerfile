# 1. Imagem base: Node 22 no Alpine
FROM node:22-alpine

# 2. Diretório de trabalho dentro do container
WORKDIR /app

# 3. Copiar arquivos de dependência PRIMEIRO
COPY package*.json ./
COPY prisma ./prisma/

# 4. Instalar todas as dependências (incluindo devDependencies para o TypeScript/tsx se necessário, ou use npm ci)
RUN npm ci

# 5. Gerar o Prisma Client
RUN npx prisma generate

# 6. Copiar o restante do código
COPY . .

# 7. Porta que a aplicação vai escutar
EXPOSE 3000

# 8. Comando para iniciar usando o tsx (já que está nos seus scripts)
CMD ["npx", "tsx", "src/server.ts"]