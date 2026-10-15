---
{"dg-publish":true,"permalink":"/documents/n8n-workflow/self-hosted-installation-guide/self-hosted-docploy-aws-guide/","dg-note-properties":{}}
---

**Requirements**

- Ubuntu 22.04 or Ubuntu 24.04
- EC2 instance (t3.small or larger recommended)
- Security Group:
    - TCP 22 (SSH)
    - TCP 80 (HTTP)
    - TCP 443 (HTTPS)
    - TCP 3000 (Dokploy Dashboard)
- An Elastic IP (recommended)
- A domain name (optional but recommended for SSL)

---

# Step 1 — SSH into your EC2

```
ssh -i your-key.pem ubuntu@YOUR_PUBLIC_IP
```

---

# Step 2 — Update Ubuntu

```
sudo apt update
sudo apt upgrade -y
sudo reboot
```

Reconnect after reboot.

---

# Step 3 — Become root

```
sudo -i
```

---

# Step 4 — Verify required ports are free

Dokploy needs ports **80**, **443**, and **3000** available.

```
ss -tulpn
```

If Nginx or Apache is running:

```
dpkg -l | grep -E 'nginx|apache2'

systemctl stop nginx
systemctl disable nginx

systemctl stop apache2
systemctl disable apache2
```

---

# Step 5 — Install Dokploy

The installer automatically installs Docker if it isn't already installed.

```
curl -sSL https://dokploy.com/install.sh | sh
```

Wait several minutes.

The installer configures:

- Docker
- Docker Swarm
- Traefik
- PostgreSQL
- Redis
- Dokploy UI

---

# Step 6 — Check everything is running

```
docker ps
```

You should see multiple containers running.

Also check Swarm:

```
docker node ls
```

---

# Step 7 — Open Dokploy

Visit:

```
http://YOUR_PUBLIC_IP:3000
```

Create your administrator account.

---

# Step 8 — Point a domain (Recommended)

Example:

```
dokploy.yourdomain.com
```

Create an **A Record** pointing to your EC2 public IP.

After adding the domain in Dokploy, Traefik can automatically obtain a Let's Encrypt SSL certificate.

---

# Step 9 — Enable firewall (Optional)

```
ufw allow 22
ufw allow 80
ufw allow 443
ufw allow 3000

ufw enable
```

---

# Step 10 — Verify installation

```
docker service ls
```

You should see services like:

```
dokploy
traefik
postgres
redis
```

---

# Update Dokploy

```
curl -sSL https://dokploy.com/install.sh | sh -s update
```

---

# Useful Commands

Restart Dokploy:

```
docker service update --force dokploy
```

Restart Docker:

```
systemctl restart docker
```

View running containers:

```
docker ps
```

View all services:

```
docker service ls
```

View logs:

```
docker service logs dokploy
```

---

# Recommended AWS Setup

|Setting|Value|
|---|---|
|AMI|Ubuntu Server 24.04 LTS|
|Instance|t3.small (minimum recommended)|
|Storage|20–30 GB gp3|
|Elastic IP|Yes|
|Security Group|22, 80, 443, 3000|
|Domain|Optional but recommended|

---

After Dokploy is running, you can deploy:

- Next.js apps
- Node.js APIs
- n8n
- Supabase
- PostgreSQL
- Redis
- Docker Compose applications
- Static websites
- Background workers

This gives you a self-hosted PaaS similar to Vercel, but on your own EC2 server.