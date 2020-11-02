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

### Proxy Server conf.d

```cmd
├── conf.d
|  └── default.conf
├── docker-compose.yaml
└── public

```


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

### File Server conf.d

```conf
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;

        if ($request_method = OPTIONS) {
            return 204;
        }

        add_header Access-Control-Allow-Origin *;
        add_header Access-Control-Max-Age 3600;
        add_header Access-Control-Expose-Headers Content-Length;
        add_header Access-Control-Allow-Headers Range;
    }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```