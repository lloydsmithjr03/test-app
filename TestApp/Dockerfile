FROM node:lts-alpine AS builder

WORKDIR /app

COPY package.json .
RUN npm install -g @angular/cli
RUN npm install

COPY . .
RUN ng build

FROM nginx:alpine

COPY --from=builder /app/dist/TestApp/* /usr/share/nginx/html/
COPY nginx.conf /etc/nginx/conf.d/default.conf