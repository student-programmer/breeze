FROM node:lts AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine AS runtime
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY --from=build /app/dist /usr/share/nginx/html

# Копирование SSL сертификата и закрытого ключа
COPY ./nginx/ssl/certificate.crt /etc/nginx/ssl/
COPY ./nginx/ssl/private.key /etc/nginx/ssl/



EXPOSE 443