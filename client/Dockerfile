FROM node:16-alpine as builder

RUN npm install -g npm

WORKDIR '/app'

COPY package*.json .
RUN npm install

COPY ./ ./
RUN npm run build

# copy all the files from the build
# into an nginx container
FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/shar/nginx/html

