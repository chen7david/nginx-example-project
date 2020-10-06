# nginx-example-project

### docker-compose
```yaml
version: '3.2'

services:
    reverse-proxy:
        image: nginx:latest
        container_name: reverse-proxy
        volumes: 
            - ./conf.d:/etc/nginx/conf.d
        ports: 
            - 80:80
```

### conf.d

```conf
server {
    listen 80;
    server_name subdomain.domain.org localhost;
    location / {
        proxy_pass "http://192.168.50.251:8080";
    }
}

server {
    listen 80;
    server_name meta.localhost subdomain.domain.org;

    location / {
        proxy_pass "http://192.168.50.251:8000";
    }
}

server {
    listen 80;
    server_name file.localhost file.aox.hopto.org;

    location / {
        proxy_pass "http://192.168.50.251:9000";
    }
}
```