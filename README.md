## Install latest docker and docker compose

### Cleaning Up

```
docker system prune -af --volumes
```

### Arm on AWS

```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.27.1/docker-compose-linux-armv7" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### x86

```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.27.1/docker-compose-linux-x86_64" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce
sudo systemctl enable --now docker
```

## `nginx` files are in `/etc/nginx/sites-available/`

## [lobe-chat](https://github.com/lobehub/lobe-chat)

url: [lobe.jimchen.me](https://lobe.jimchen.me)

```
sudo docker run -d -p 3210:3210 --env-file .env --restart always --name lobe-chat lobehub/lobe-chat
sudo certbot certonly --standalone -d lobe.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/chat.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [chatgpt-next-web](https://github.com/ChatGPTNextWeb/ChatGPT-Next-Web)

url: [chat.jimchen.me](https://chat.jimchen.me)

```
sudo docker run -d -p 3000:3000 --env-file .env --restart always yidadaa/chatgpt-next-web
sudo certbot certonly --standalone -d chat.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/chat.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [vaultwarden](https://github.com/dani-garcia/vaultwarden)

url: [vault.jimchen.me](https://vault.jimchen.me)

```
sudo docker run -d --name vaultwarden -v /vw-data/:/data/ --restart always -p 3001:80 vaultwarden/server:latest
sudo certbot certonly --standalone -d vault.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/vault.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [uptime-kuma](https://github.com/louislam/uptime-kuma)

url: [status.jimchen.me](https://status.jimchen.me)

```
sudo docker run -d --restart=always -p 3002:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1
sudo certbot certonly --standalone -d status.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/status.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [immich](https://github.com/immich-app/immich)

url: [immich.jimchen.me](https://immich.jimchen.me)

```sh
mkdir ./immich-app
cd ./immich-app

# wget -O docker-compose.yml https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml
#wget -O .env https://github.com/immich-app/immich/releases/latest/download/example.env

sudo docker-compose up -d
sudo certbot certonly --standalone -d immich.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/immich.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [portainer](https://github.com/portainer/portainer)

url: [portainer.jimchen.me](https://portainer.jimchen.me)

```
sudo docker volume create portainer_data
sudo docker run -d -p 3003:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
sudo certbot certonly --standalone -d portainer.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/portainer.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [mongodb]

```bash
# add mongod.conf, dockercompose
docker-compose up -d
# expose port 27017
# mongosh "mongodb://admin:[]@3.228.73.172:27017/" --authenticationDatabase admin
# connecting admin only works when specifying admin ?authSource=admin
```

## [mongodb-to-s3](https://github.com/jimchen2/mongodb-to-s3)

```bash
docker run --env-file .env --restart always jimchen2/mongodb-s3-backup
```

## [alist](https://github.com/alist-org/alist)

url: [bucket.jimchen.me](https://bucket.jimchen.me)

```
docker run -d --restart=always -v /etc/alist:/opt/alist/data -p 5244:5244 -e PUID=0 -e PGID=0 -e UMASK=022 --name="alist" xhofe/alist:latest
docker exec -it alist ./alist admin set password
sudo certbot certonly --standalone -d bucket.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/bucket.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [jimchen.me](https://github.com/jimchen2/My-Website-New)

url: [jimchen.me](https://jimchen.me)

```bash
# configure .env
# double quote leads to errors
docker run -d --restart always --env-file .env -p 3010:3000 jimchen2/my-website:latest
sudo certbot certonly --standalone -d jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/jimchen.me.conf /etc/nginx/sites-enabled/
```

## [task-manager-nextjs](https://github.com/jimchen2/task-manager-nextjs)

url: [task.jimchen.me](https://task.jimchen.me)

```bash
# configure .env
docker run -d --restart always --env-file .env -p 3025:3000 jimchen2/task-manager-nextjs:latest
sudo certbot certonly --standalone -d task.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/task.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [markdown-parser](https://github.com/jimchen2/markdown-parser)

url: [markdown.jimchen.me](https://markdown.jimchen.me)

```bash
# configure .env
docker run -d --restart always --env-file .env -p 3025:3000 jimchen2/markdown-parser:latest
sudo certbot certonly --standalone -d markdown.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/markdown.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [nocodb](https://github.com/nocodb/nocodb)

url: [nocodb.jimchen.me](https://nocodb.jimchen.me)

```bash
# configure docker-compose.yml
docker-compose up -d
sudo certbot certonly --standalone -d nocodb.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/nocodb.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [actual](https://github.com/actualbudget/actual)

url: [actual.jimchen.me](https://actual.jimchen.me)

```

docker run --pull=always --restart=unless-stopped -d -p 3037:5006 -v /data:/data --name actual-server actualbudget/actual-server:latest
sudo certbot certonly --standalone -d actual.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/actual.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [nezha](https://github.com/naiba/nezha)

url: [nezha.jimchen.me](https://nezha.jimchen.me)

```bash
curl -L https://raw.githubusercontent.com/naiba/nezha/master/script/install.sh -o nezha.sh && chmod +x nezha.sh && sudo ./nezha.sh
# expose port 8008 and 5555
sudo certbot certonly --standalone -d nezha.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/nezha.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [stirling-pdf](https://github.com/Stirling-Tools/Stirling-PDF)

url: [pdf.jimchen.me](https://pdf.jimchen.me)

```bash
docker run -d --restart always \
  -p 8033:8080 \
  -v ./trainingData:/usr/share/tessdata \
  -v ./extraConfigs:/configs \
  -v ./logs:/logs \
  -e DOCKER_ENABLE_SECURITY=false \
  -e INSTALL_BOOK_AND_ADVANCED_HTML_OPS=false \
  -e LANGS=en_GB \
  --name stirling-pdf \
  frooodle/s-pdf:latest
sudo certbot certonly --standalone -d pdf.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/pdf.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [rsshub](https://github.com/DIYgod/RSSHub)

url: [rss.jimchen.me](https://rss.jimchen.me)

```bash
docker run -d --name rsshub -p 1200:1200 --restart always diygod/rsshub:chromium-bundled
sudo certbot certonly --standalone -d rss.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/rss.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [freshrss](https://github.com/FreshRSS/FreshRSS)

url: [feed.jimchen.me](https://feed.jimchen.me)

```
docker run -d --restart always --log-opt max-size=10m \
  -p 8092:80 \
  -e TZ=Europe/Paris \
  -e 'CRON_MIN=1,31' \
  -v freshrss_data:/var/www/FreshRSS/data \
  -v freshrss_extensions:/var/www/FreshRSS/extensions \
  --name freshrss \
  freshrss/freshrss
sudo certbot certonly --standalone -d feed.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/feed.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [linktree](https://github.com/jimchen2/linktree)

url: [link.jimchen.me](https://link.jimchen.me)

```bash
docker run -d --restart always -p 3069:3000 jimchen2/linktree:latest
sudo certbot certonly --standalone -d link.jimchen.me --email jimchen4214@gmail.com --non-interactive --agree-tos
sudo ln -sf /etc/nginx/sites-available/link.jimchen.me.conf /etc/nginx/sites-enabled/
```

## [gitlab](https://about.gitlab.com/install/#amazonlinux-2023)

url: [git.jimchen.me](https://git.jimchen.me)

Note: This is on another instance

GitLab uses significant RAM

```
# Add Ram or use at least 4 GB RAM
sudo apt-get update && sudo apt upgrade -y
sudo apt-get install -y curl openssh-server ca-certificates tzdata perl
sudo apt-get install -y postfix
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
sudo EXTERNAL_URL="https://git.jimchen.me" apt-get install gitlab-ee
```

Then configure [S3 Storage](https://docs.gitlab.com/ee/administration/object_storage.html#amazon-s3) in `/etc/gitlab/gitlab.rb`

```
gitlab_rails['object_store']['enabled'] = true
gitlab_rails['object_store']['proxy_download'] = false
gitlab_rails['object_store']['connection'] = {
  'provider' => 'AWS',
  'region' => 'us-east-1',
  'aws_access_key_id' => 'YOUR_ACCESS_KEY',
  'aws_secret_access_key' => 'YOUR_SECRET_KEY'
}

gitlab_rails['object_store']['objects']['artifacts']['bucket'] = 'jimchen4214-git'
gitlab_rails['object_store']['objects']['artifacts']['prefix'] = 'artifacts'

gitlab_rails['object_store']['objects']['external_diffs']['bucket'] = 'jimchen4214-git'
gitlab_rails['object_store']['objects']['external_diffs']['prefix'] = 'external_diffs'

gitlab_rails['object_store']['objects']['lfs']['bucket'] = 'jimchen4214-git'
gitlab_rails['object_store']['objects']['lfs']['prefix'] = 'lfs'

gitlab_rails['object_store']['objects']['uploads']['bucket'] = 'jimchen4214-git'
gitlab_rails['object_store']['objects']['uploads']['prefix'] = 'uploads'

gitlab_rails['object_store']['objects']['packages']['bucket'] = 'jimchen4214-git'
gitlab_rails['object_store']['objects']['packages']['prefix'] = 'packages'

gitlab_rails['object_store']['objects']['dependency_proxy']['bucket'] = 'jimchen4214-git'
gitlab_rails['object_store']['objects']['dependency_proxy']['prefix'] = 'dependency-proxy'

gitlab_rails['object_store']['objects']['terraform_state']['bucket'] = 'jimchen4214-git'
gitlab_rails['object_store']['objects']['terraform_state']['prefix'] = 'terraform-state'
```

Then `sudo gitlab-ctl reconfigure`
