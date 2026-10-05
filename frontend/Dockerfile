FROM nginx:alpine

RUN apk add --no-cache curl \
    && rm -rf /usr/share/nginx/html/*

COPY public/ /usr/share/nginx/html/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
