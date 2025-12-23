# Stage 1: Build Angular app
FROM node:18-alpine AS builder
WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build -- --configuration production

# Stage 2: Nginx
FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*

# Copy Angular dist output
COPY --from=builder /app/dist/* /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
