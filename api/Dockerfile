# 1. Imagem base: Node 22 no Alpine (leve)
FROM node:22-alpine

# 2. Diretório de trabalho dentro do container
WORKDIR /app

# 3. Dependências de sistema para compilar o bcrypt (módulo nativo)
RUN apk add --no-cache python3 make g++

# 4. Copiar arquivos de dependência PRIMEIRO (otimiza cache do Docker)
COPY package*.json ./
COPY prisma ./prisma/
COPY prisma.config.ts ./

# 5. Instalar dependências
RUN npm ci

# 6. Gerar o Prisma Client
RUN npx prisma generate

# 7. Copiar o restante do código
COPY . .

# 8. Build do TypeScript
RUN npm run build

# 9. Porta que a aplicação vai escutar
EXPOSE 3000

# 10. Comando para iniciar
CMD ["node", "dist/server.js"]
