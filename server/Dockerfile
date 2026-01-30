FROM node:18-alpine AS builder
WORKDIR /app

COPY package*.json ./
RUN npm install --legacy-peer-deps

COPY . .
RUN npm run build


FROM node:18-alpine
WORKDIR /app

COPY package*.json ./
RUN npm install --production

COPY --from=builder /app/build ./build


COPY --from=builder /app/ormconfig.js ./ormconfig.js

EXPOSE 5000
CMD ["npm", "run", "start"]
