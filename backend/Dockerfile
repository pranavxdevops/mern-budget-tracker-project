# Stage 1 - Build dependencies
FROM node:18-alpine AS builder
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# Stage 2 - Production runtime
FROM node:18-alpine
WORKDIR /app

COPY --from=builder /app /app

EXPOSE 5000

# Load environment variables (docker-compose will override)
ENV NODE_ENV=production

CMD ["node", "server.js"]
