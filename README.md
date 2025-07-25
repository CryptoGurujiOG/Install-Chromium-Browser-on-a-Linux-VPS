# Install-Chromium-Browser-on-a-Linux-VPS
This guide provides step-by-step instructions to install Chromium Browser on a Linux VPS, making it suitable for web automation, testing, scraping, or general browser-based tasks in a server environment.

---

**Buy & Set up VPS using this 👉 Guide**

---

**Install Docker**

```
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Docker version check
docker --version

```

**Check Timezone**

```
realpath --relative-to /usr/share/zoneinfo /etc/localtime
```

## Install Chromium

**Create directory**

```
mkdir chromium
cd chromium
```

**Create `docker-compose.yaml` file**

```
nano docker-compose.yaml
```

**Paste the following code in the GNU nano**

```
services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined #optional
    environment:
      - CUSTOM_USER=     #Replace username
      - PASSWORD=    #Replace password
      - PUID=1000
      - PGID=1000
      - TZ=TZ=Asia/Kolkata
      - CHROME_CLI=https://x.com/CryptoGurujiOG #optional
    volumes:
      - /root/chromium/config:/config
    ports:
      - 3010:3000   #Change 3010 to your favorite port if needed
      - 3011:3001   #Change 3011 to your favorite port if needed
    shm_size: "1gb"
    restart: unless-stopped
```

- `CUSTOM_USER` & `PASSWORD`: Set username and password to login to Chromium
- `TZ`: Replace with your server timezone
- `CHROME_CLI`: The main page when you open the browser
- `ports`: You can replace 3010 & 3011 if they have conflict

- Save and exit: `Ctrl+X+Y+Enter`

## Run Chromium

```
cd $HOME && cd chromium

docker compose up -d
```

## Chromium application can be accessed by going to one of these addresses in any browser

1. http://Server_IP:3010/
2. https://Server_IP:3011/

- Replace Server_IP with your VPS IP

## Optional: Stop and Delete Chromium

```
docker stop chromium
docker rm chromium
docker system prune
```

## My All Socials:

- Twitter: https://x.com/CryptoGurujiOG
- Youtube: https://www.youtube.com/@CryptoGurujiOG
- Telegram: https://www.telegram.me/cryptogurujiog

