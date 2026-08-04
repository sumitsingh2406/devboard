#stage1
FROM node:24 as builder

WORKDIR /app

COPY package*.json ./

RUN npm install
RUN npm run build

#stage2
FROM node:24-alpine

WORKDIR /app

COPY --from=builder /app/dist ./dist

RUN npm install -g vite

CMD ["vite", "preview", "--port", "3000", "--host"]