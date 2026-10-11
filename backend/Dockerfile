FROM node:18-alpine AS deps

WORKDIR /app

COPY package.json package-lock.json ./
COPY backend/package.json backend/package.json

RUN npm ci -w backend --include-workspace-root=false --omit=dev

FROM node:18-alpine

WORKDIR /app
ENV NODE_ENV=production

COPY --from=deps /app/node_modules /app/node_modules
COPY backend/ backend/

WORKDIR /app/backend

EXPOSE 8000

CMD ["node", "index.js"]
