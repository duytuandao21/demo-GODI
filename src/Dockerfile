# syntax=docker/dockerfile:1

FROM node:24-alpine AS build

WORKDIR /app

# COPY package.json package-lock.json ./
COPY . .
RUN npm ci

# COPY index.js ./
# COPY routes ./routes
# COPY server ./server
# COPY tests ./tests

RUN npm test -- --runInBand
RUN npm prune --omit=dev && npm cache clean --force


FROM node:24-alpine AS runtime

ENV NODE_ENV=production \
    PORT=3000

WORKDIR /app

COPY --from=build --chown=node:node /app/node_modules ./node_modules
COPY --chown=node:node package.json package-lock.json index.js ./
COPY --chown=node:node routes ./routes
COPY --chown=node:node server ./server

USER node

EXPOSE 3000

CMD ["node", "index.js"]
