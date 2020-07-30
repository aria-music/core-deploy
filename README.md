# core-deploy
Aria-Core deploy made easy

# Dependent

- nginx
- certbot (Optional)
- docker
- docker-compose

# Prepare

```bash
certbot certonly --standalone
vim /etc/nginx/nginx.conf
nginx -t # test configuration and exit
```

# nginx config sample

```
user YOUR NAME;

events{};

http {
	server {
    listen 443 ssl;
    server_name YOUR DOMAIN;
    ssl_protocols TLSv1.2;
    ssl_certificate PATH TO FILE;
    ssl_certificate_key PATH TO FILE;

    location / {
      proxy_pass http://localhost:5577/;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";
    }
```

# How To Deploy

```bash
git clone https://github.com/ariamusic/core-deploy
cd core-deploy
vim config/core/config.json
vim config/database/
docker-compose up -d
```

# How To Update

```bash
git pull
git submodule update
docker-compose up --no-deps -d --build `module`
```

# How To google login

```bash
docker-compose exec core /bin/bash
# in docker container
python google_login.py
>GPM USER
>TOKEN
exit
```

use `updatedb` command to fetch gpm songs

# Log

```
docker-compose logs -f core
```
