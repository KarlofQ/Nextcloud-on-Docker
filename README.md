# Nextcloud Docker Quick Setup

## 1. Create directory for Nextcloud

```sh
sudo mkdir -p /opt/stacks/nextcloud
cd /opt/stacks/nextcloud
```

## 2. Set up Docker NGINX proxy

```sh
sudo mkdir proxy
sudo nano proxy/Dockerfile
```
Paste:
```Dockerfile
FROM nginxproxy/nginx-proxy:alpine
COPY uploadsize.conf /etc/nginx/conf.d/uploadsize.conf
```

```sh
sudo nano proxy/uploadsize.conf
```
Paste:
```
client_max_body_size 10G;
proxy_request_buffering off;
```

## 3. Generate MySQL password

```sh
gpg --gen-random --armor 1 24 | base64
```

## 4. Create .env file

```sh
sudo nano .env
```
Paste and fill in:
```
MYSQL_PASSWORD=<SQLPASS>
STORAGE_LOCATION=<STORAGELOCATION>
DOMAIN_NAME=<HOSTNAME>
LETS_ENCRYPT_EMAIL=<EMAIL>
```

## 5. Download Docker Compose file

With domain (Let's Encrypt):
```sh
sudo wget https://git.pimylifeup.com/compose/nextcloud/signed/compose.yaml
```
Without domain (self-signed):
```sh
sudo wget https://git.pimylifeup.com/compose/nextcloud/selfsigned/compose.yaml
```

## 6. Start Nextcloud

```sh
docker compose up -d
```

## 7. Access Nextcloud

Get IP:
```sh
hostname -I
```
Go to:
```
https://<IPADDRESS OR DOMAINNAME>/
```
