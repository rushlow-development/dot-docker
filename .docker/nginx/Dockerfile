FROM nginx:alpine

RUN apk update && \
    apk add --no-cache openssl

RUN mkdir /etc/nginx/ssl

RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/nginx/ssl/nginx-UNSECURE.key \
    -out /etc/nginx/ssl/nginx-UNSECURE.crt \
    -subj '/C=US/ST=FL/L=DevTown/O=devDeveloper/CN=localhost'

CMD ["nginx"]
