# ---- Stage 1: Build ----
FROM node:22-alpine AS builder

WORKDIR /app

# 1. Copiar arquivos de dependências primeiro
COPY package*.json ./

# 2. Instalar dependências
RUN npm install --force

# 3. COPIAR TODO O RESTANTE DO CÓDIGO (incluindo tsconfig.json e src) ANTES DO BUILD
COPY . .

# 4. Executar o build do TypeScript/Vite
RUN npm run build

# ---- Stage 2: Serve ----
FROM nginx:alpine

# Copiar os arquivos gerados pelo build para o Nginx
COPY --from=builder /app/dist /usr/share/nginx/html

# Configuração do Nginx para SPA (React Router)
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]