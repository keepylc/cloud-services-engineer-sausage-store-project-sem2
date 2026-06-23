FROM node:16-alpine AS build

WORKDIR /usr/src/app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build -- --prod

FROM nginx:stable-alpine

COPY --from=build /usr/src/app/dist/frontend /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]