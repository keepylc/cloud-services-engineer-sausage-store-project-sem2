# build
FROM node:16-alpine AS builder

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm install

COPY . .

RUN npm run build -- --prod

# release
FROM nginx:stable-alpine

WORKDIR /opt/html
COPY --from=builder /app/dist/frontend ./
RUN chown -R 101:101 /opt/html

ENTRYPOINT ["sh", "-c", "cp -a /opt/html/. /mnt/ && exit 0"]
