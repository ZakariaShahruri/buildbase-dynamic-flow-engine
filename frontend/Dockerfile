FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm ci

ARG VITE_API_URL
ENV VITE_API_URL=$VITE_API_URL

COPY . .

RUN npm run build

FROM nginx:stable-alpine AS runner

RUN rm -rf /usr/share/nginx/html/*
COPY --from=build /app/dist /usr/share/nginx/html

RUN cat > /etc/nginx/nginx.conf <<'EOF'
worker_processes  1;
error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;

events {
    worker_connections  1024;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    keepalive_timeout  65;

    client_body_temp_path /tmp/nginx_client_temp;

    gzip on;

    server {
        listen       8080;
        listen       [::]:8080;
        server_name  _;
        root /usr/share/nginx/html;
        index index.html;

        location / {
            try_files $uri $uri/ /index.html;
        }

        location ~* \.(?:css|js|jpg|jpeg|gif|png|svg|ico|woff2?)$ {
            try_files $uri =404;
            expires 30d;
            access_log off;
        }
    }
}
EOF

RUN mkdir -p /var/cache/nginx /var/run /var/log/nginx /etc/nginx/conf.d && \
    chown -R 0:0 /var/cache/nginx /var/run /var/log/nginx /usr/share/nginx/html /etc/nginx && \
    chmod -R g+rwX /var/cache/nginx /var/run /var/log/nginx /usr/share/nginx/html /etc/nginx

EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]