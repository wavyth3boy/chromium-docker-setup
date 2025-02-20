# 🚀 Responsive Guide to Setting Up Chromium on a VPS

## 📌 **Step 1: Connect to Your VPS**
Log in to your VPS using SSH via Command Prompt or Git Bash:
```sh
ssh <YOUR_USERNAME>@<YOUR_SERVER_IP>
```

---

## 📌 **Step 2: Install Docker**
Update and upgrade packages, remove old Docker packages, and install the latest version:

```sh
sudo apt update -y && sudo apt upgrade -y

for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do 
    sudo apt-get remove $pkg;
done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg -y

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo $VERSION_CODENAME) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

# Check Docker version
docker --version
```

---

## 📌 **Step 3: Set Up Chromium**
Create a directory for Chromium and navigate into it:

```sh
mkdir chromium && cd chromium
```

Create a `docker-compose.yaml` file:
```sh
nano docker-compose.yaml
```

---

## 📌 **Step 4: Paste the Following Code**
Fill in the placeholders with your credentials and configuration.

```yaml
version: "3.8"  # Always define the version

services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined  # Optional
    environment:
      - CUSTOM_USER=your_username  # Replace with your username
      - PASSWORD=your_password    # Replace with your password
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London          # Replace with your timezone
      - CHROME_CLI=https://docs.google.com/document/d/1l8vVKX3LZWcx5lanuNINmAw7CJYrydxMDOt2P2Uod7g/edit?usp=sharing
    volumes:
      - /root/chromium/config:/config
    ports:
      - "3010:3000"
      - "3011:3001"
    shm_size: "1gb"
    restart: unless-stopped
```

**To save and exit:** Press `Ctrl + X`, then `Y`, and hit `Enter`.

---

## 📌 **Step 5: Run Chromium**

```sh
cd $HOME/chromium
docker compose up -d
```

The application can be accessed by going to one of these addresses in your local browser:
- **`http://<Server_IP>:3010/`**
- **`https://<Server_IP>:3011/`**

---

## 📌 **Optional: Stop and Delete Chromium**
```sh
docker stop chromium
docker rm chromium
docker system prune
```

---

### ✅ **All done!** Now your Chromium container is up and running with a 24-hour uptime without compromising your PC! 🕒
