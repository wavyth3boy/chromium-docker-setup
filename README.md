🔹 Step 1: Connect to Your VPS on command prompt or git bash
Log in to your VPS using SSH:
ssh <YOUR_USERNAME>@<YOUR_SERVER_IP>

🔹 Step 2: Install Docker
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

Step 3: Set Up Chromium
Create a directory for Chromium:

mkdir chromium
cd chromium

Create a docker-compose.yaml file:
nano docker-compose.yaml


step 4  Paste the following code in it

CUSTOM_USER & PASSWORD: Replace your favorite credentials to login to chromium
TZ: Replace with your server timezone
CHROME_CLI: The main page when you open browser
ports: You can replace 3010 & 3011 if they have conflict

version: "3.8"  # Always define the version

services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined  # Optional
    environment:
      - CUSTOM_USER= #replaceusername
      - PASSWORD= #newpassword
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - CHROME_CLI=https://docs.google.com/document/d/1l8vVKX3LZWcx5lanuNINmAw7CJYrydxMDOt2P2Uod7g/edit?usp=sharing
    volumes:
      - /root/chromium/config:/config
    ports:
      - "3010:3000"
      - "3011:3001"
    shm_size: "1gb"
    restart: unless-stopped


To save and exit: Ctrl+X+Y+Enter

Run Chromium
cd $HOME && cd chromium

docker compose up -d
The application can be accessed by going to one of these addresses in your local PC browser

http://Server_IP:3010/
https://Server_IP:3011/
Optional: Stop and Delete Chromium
docker stop chromium
docker rm chromium
docker system prune
