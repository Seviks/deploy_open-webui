# Create a new user
```
adduser sammy
usermod -aG sudo sammy
rsync --archive --chown=sammy:sammy ~/.ssh /home/sammy
```

# Set up firewall
```
ufw allow ssh
ufw allow http
ufw allow https
ufw enable

# ufw allow from 203.0.113.0/24
```

# Install Docker
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

# Set up compose
```
git clone https://github.com/Seviks/deploy_open-webui.git -b ssl
cd deploy_open_webui
```
## Comment 443 Block
`nano nginx.conf`

## Create ssl certificate
```
docker compose up -d --force-recreate
docker-compose run --rm certbot certonly --webroot --webroot-path /var/www/certbot/ --dry-run --agree-tos --no-eff-email -d bassllm.ddns.net
docker-compose exec nginx nginx -s reload
```


## Update
apt update && apt upgrad -y
docker pull ghcr.io/open-webui/open-webui:main
docker compose up -d --force-recreate
docker image prune -a

