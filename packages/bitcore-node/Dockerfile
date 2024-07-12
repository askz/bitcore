FROM node:18-alpine AS builder


RUN set -x \
    && node -v \
    && npm -v


RUN npm i -g npm@8.19.3

RUN apk add --no-cache git python3 py3-setuptools alpine-sdk

WORKDIR /bitcore

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run tsc

FROM node:18-alpine

WORKDIR /app

COPY --from=builder /bitcore/build/src ./dist
COPY --from=builder /bitcore/node_modules ./node_modules

CMD ["node", "dist/server.js"]

