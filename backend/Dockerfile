# Этап сборки
FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Финальный этап
FROM node:16-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY --from=builder /app/dist ./dist
COPY ecosystem.config.js ./ 
RUN npm install -g pm2
EXPOSE 4000
CMD ["pm2-runtime", "start", "ecosystem.config.js"]