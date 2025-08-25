# Stage 1: Build mit Node.js
FROM node:lts-alpine AS builder

WORKDIR /app

# Nur die Abhängigkeitsdateien kopieren
COPY package*.json ./

# Reproduzierbare, saubere Installation
RUN npm ci

# Restlichen Code kopieren
COPY . .

# Vite-Build starten
RUN npm run build

# Stage 2: Runtime mit Nginx
FROM nginx:alpine

# Standard-HTML-Seiten löschen
RUN rm -rf /usr/share/nginx/html/*

# Build-Ergebnis vom Builder kopieren
COPY --from=builder /app/dist /usr/share/nginx/html

# Port dokumentieren
EXPOSE 80

# Healthcheck (optional)
HEALTHCHECK --interval=30s --timeout=10s \
  CMD wget --no-verbose --tries=1 --spider http://localhost || exit 1
