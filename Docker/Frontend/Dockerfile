FROM node:20.10.0 as build

WORKDIR /app

COPY package*.json ./

RUN sudo npm install

COPY . .

RUN npm run build --prod

FROM nginx:alpine

COPY nginx.conf /etc/nginx/nginx.conf

COPY --from=build /app/dist/patelbros/browser ./usr/share/nginx/html 

EXPOSE 80

