# ---- Build stage ----
FROM node:18-alpine AS builder
RUN apk add --no-cache openssl
WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY . .
RUN npx prisma generate --schema=src/prisma/schema.prisma
RUN npx nx build api --configuration=production

# ---- Runtime stage ----
FROM node:18-alpine
RUN apk add --no-cache openssl
WORKDIR /app
ENV NODE_ENV=production
ENV PORT=3000

COPY --from=builder /app/package.json ./package.json
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/dist/api ./dist/api
COPY --from=builder /app/src/prisma ./src/prisma

EXPOSE 3000

CMD ["sh", "-c", "npx prisma migrate deploy --schema=src/prisma/schema.prisma && node dist/api/main.js"]
