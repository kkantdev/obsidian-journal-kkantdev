---
{"dg-publish":true,"permalink":"/documents/n8n-workflow/self-hosted-installation-guide/self-hosted-n8-n-aws-guide/","dg-note-properties":{}}
---


 --install Docker & Docker Compose

```
sudo apt update && sudo apt upgrade -y

```

```
sudo apt install docker.io -y  
```

```
sudo systemctl enable docker 
```


```
sudo systemctl start docker 
```


```
sudo usermod -aG docker ubuntu 
```


```
newgrp docker  
```

```
sudo apt install docker-compose -y
```


docker -v

docker-compose --version  
or
docker compose version

--Create n8n Setup

```
mkdir n8n && cd n8n  
```

```
sudo nano docker-compose.yml

```

--Create docker-compose.yml:  

```
version: "3"
services:
  n8n:
    image: n8nio/n8n:latest
    restart: always
    ports:
      - "5678:5678"
    environment:
      - DB_TYPE=postgresdb
      - DB_POSTGRESDB_HOST=your-postgres-host-here       # <-- Put your database IP/Host here
      - DB_POSTGRESDB_PORT=5432
      - DB_POSTGRESDB_DATABASE=postgres
      - DB_POSTGRESDB_USER=your-db-user-here             # <-- Put your database username here
      - DB_POSTGRESDB_PASSWORD=your-db-password-here     # <-- Put your database password here
      - DB_POSTGRESDB_SSL=true
      - DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED=false
      - N8N_SECURE_COOKIE=true                           # <-- Changed to true for better HTTPS security
      - N8N_HOST=n8n.kkzero.site                          # <-- Use your actual domain
      - N8N_PROTOCOL=https
      - WEBHOOK_URL=https://n8n.kkzero.site/              # <-- Use your actual domain
      - N8N_DB_HEALTH_CHECK_INTERVAL=0
      - N8N_DB_HEALTH_CHECK_TIMEOUT=30000
      - EXECUTIONS_DATA_PRUNE=true                        # <-- auto delete log
      - EXECUTIONS_DATA_MAX_AGE=168                       # <-- 7day * 24 =168
      - EXECUTIONS_DATA_PRUNE_MAX_COUNT=50000             # <-- auto delete if it full before 7 days
    volumes:
      - ~/.n8n:/home/node/.n8n

```


# Start n8n

```

```
docker compose up -d
```
docker compose up -d
or
docker-compose up -d

```


--Stop n8n  

```
docker compose down
```

  
--Permissions

```
sudo chown -R 1000:1000 ~/.n8n
```

--Check Logs

```
docker compose logs -f
```


Check Docker Status
docker ps

```

sudo fallocate -l 512M /swapfile


sudo chmod 600 /swapfile


sudo mkswap /swapfile


sudo swapon /swapfile

```


#  Install Nginx

**1.Install Nginx and Certbot:**~2 mins.

First, update your packages and install both Nginx and the Certbot SSL tools at the same time so everything you need is ready.

Bash

```
sudo apt update
sudo apt install nginx certbot python3-certbot-nginx -y
```

**2.Create your Nginx Config:**Replace placeholders.

Instead of using a placeholder name, name the file after your actual subdomain so it stays organized. Run this command:

Bash

```
sudo nano /etc/nginx/sites-available/domain.com
```

Paste the following updated configuration inside it (press `Ctrl+O` then `Enter` to save, and `Ctrl+X` to exit):

Nginx

```
server {
    listen 80;
    listen [::]:80;

    server_name domain.com;

    location / {
        proxy_pass http://localhost:5678; 
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        
        # Crucial for n8n WebSockets / Webhooks
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

**3.Link and Clean up Configs:**Enable your site.

Link your new configuration to the `sites-enabled` folder and delete the default Nginx placeholder config so it doesn't conflict.

Bash

```
sudo ln -s /etc/nginx/sites-available/domain.com /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default
```

**4.Test and Restart Nginx:**Verify syntax.

Always check your Nginx syntax before restarting it. If it says "syntax is ok", restart the service.

Bash

```
sudo nginx -t
sudo systemctl restart nginx
```

**5.Generate the SSL Certificate:**Secure with HTTPS.

Now that Nginx is running and pointing to your domain, run Certbot. It will automatically talk to Let's Encrypt, issue the certificate, and update your Nginx file for you.

Bash

```
sudo certbot --nginx -d domain.com
```

_(Follow the on-screen prompts, enter your email, and agree to the terms)._

for checking if its working 

```
sudo systemctl status nginx
  
```
