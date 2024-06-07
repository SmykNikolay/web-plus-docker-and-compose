# Этап сборки
FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build
RUN rm -rf ./src 

# Этап запуска nginx
FROM nginx:latest
COPY --from=builder /app/build /usr/share/nginx/html
COPY ./nginx/conf.d/default.conf /etc/nginx/conf.d
EXPOSE 8081
CMD ["nginx", "-g", "daemon off;"]