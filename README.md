# nginx-example-project

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