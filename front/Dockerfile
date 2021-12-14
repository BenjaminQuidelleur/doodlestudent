FROM node:16.13-alpine AS builder
WORKDIR /usr/src/app 
COPY . .
RUN npm install
RUN npm i -g @angular/cli
RUN npm run build

FROM bunkerity/bunkerized-nginx
COPY --from=builder /usr/src/app/dist/tlcfront /www/
COPY ./nginx.conf /server-confs/api.conf