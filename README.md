# nginx-fancyindex
用于构建docker镜像的dockerfile，让nginx支持fancyindex模组
##下载源码
```
wget http://nginx.org/download/nginx-1.27.5.tar.gz
wget https://github.com/aperezdc/ngx-fancyindex/releases/download/v0.5.2/ngx-fancyindex-0.5.2.tar.xz
tar -xzvf nginx-1.27.5.tar.gz
tar -xvJf ngx-fancyindex-0.5.2.tar.xz
```
## 构建镜像
```
docker build -t nginx-fancyindex:alpine .
```
## Docker-compose.yml
```
services:
  nginx:
    image: nginx-fancyindex:alpine
    container_name: nginx
    restart: always
    ports:
      - "80:80"
      - "443:443"
      - "443:443/udp"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./conf.d:/etc/nginx/conf.d
      - ./certs:/etc/nginx/certs
      - ./html:/var/www/html
      - ./log/nginx:/var/log/nginx
      - php-socket-php:/run/php
      - php-socket-php74:/run/php74
    tmpfs:
      - /var/cache/nginx:rw,noexec,nosuid,size=2048m
```

