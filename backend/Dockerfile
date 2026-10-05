# Stage 1: install production dependencies
FROM node:20-alpine AS dependencies

WORKDIR /app

COPY package*.json ./

RUN npm ci --omit=dev


# Stage 2: minimal production runtime
FROM node:20-alpine AS runtime

WORKDIR /app

ENV NODE_ENV=production

RUN apk add --no-cache curl

COPY --from=dependencies /app/node_modules ./node_modules
COPY --chown=node:node . .

EXPOSE 8080

USER node

CMD ["node", "server.js"]
