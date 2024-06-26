FROM node:20.10.0-alpine AS builder 

WORKDIR /app

COPY package*.json ./

RUN apk add --no-cache --virtual .build-deps nodejs npm  # Install dependencies using apk

RUN npm install

COPY . .

RUN npm run build --prod

FROM nginx:alpine

COPY nginx.conf /etc/nginx/nginx.conf

COPY --from=build /app/dist/patelbros/browser ./usr/share/nginx/html

EXPOSE 80