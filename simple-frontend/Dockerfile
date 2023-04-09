FROM node:18.15.0-buster as build-stage

WORKDIR /app

COPY package.json package.json
COPY package-lock.json package-lock.json

RUN npm ci --production

COPY . .

#EXPOSE 3000

RUN npm run build

#NGINX Web Server
FROM nginx:1.22.1-alpine as production-stage

COPY --from=build-stage /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]