# chromium-docker-setup
How to set up chromium browser for desktop nodes
Step 2: Clone Your Repository to Your VPS
Log in to your VPS using SSH and clone your GitHub repository:

bash
Copy
Edit
ssh <YOUR_USERNAME>@<YOUR_SERVER_IP>
git clone https://github.com/<YOUR_GITHUB_USERNAME>/chromium-docker-setup.git
cd chromium-docker-setup
Step 3: Create and Edit the README File
Run the following to create a README.md file:

bash
Copy
Edit
nano README.md
Then, paste this user-friendly guide inside README.md:

Dockerized Chromium Setup on VPS
This guide helps you deploy Chromium in a Docker container on any Linux VPS.

🚀 Features
No GUI needed (Runs in a container).
Secure login via custom credentials.
Easy access through your browser.
Persistent storage with Docker volumes.
🔹 Step 1: Connect to Your VPS
Log in to your VPS using SSH:

bash
Copy
Edit
ssh <YOUR_USERNAME>@<YOUR_SERVER_IP>
🔹 Step 2: Install Docker
Update packages and install Docker:

bash
Copy
Edit
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
🔹 Step 3: Verify Installation
Check if Docker is installed:

bash
Copy
Edit
docker --version
Check the system timezone:

bash
Copy
Edit
realpath --relative-to /usr/share/zoneinfo /etc/localtime
🔹 Step 4: Set Up Chromium
Create a directory for Chromium:

bash
Copy
Edit
mkdir chromium
cd chromium
Create a docker-compose.yaml file:

bash
Copy
Edit
nano docker-compose.yaml
🔹 Step 5: Paste This Configuration
Replace USERNAME, PASSWORD, TIMEZONE with your values.

yaml
Copy
Edit
services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined # optional
    environment:
      - CUSTOM_USER=<YOUR_USERNAME>   # Change this
      - PASSWORD=<YOUR_PASSWORD>      # Change this
      - PUID=1000
      - PGID=1000
      - TZ=<YOUR_TIMEZONE>            # Example: Europe/London
      - CHROME_CLI=https://www.google.com # Default homepage
    volumes:
      - /root/chromium/config:/config
    ports:
      - 3010:3000   # Change 3010 if needed
      - 3011:3001   # Change 3011 if needed
    shm_size: "1gb"
    restart: unless-stopped
Save and exit: Ctrl + X, then Y, then Enter.
🔹 Step 6: Run Chromium
bash
Copy
Edit
docker compose up -d
Check if the container is running:

bash
Copy
Edit
docker ps
🔹 Step 7: Access Chromium
Now, open your browser and go to:

HTTP: http://<YOUR_SERVER_IP>:3010/
HTTPS: https://<YOUR_SERVER_IP>:3011/
Login using your username and password from docker-compose.yaml.

🔹 Optional: Stop and Remove Chromium
To stop Chromium:

bash
Copy
Edit
docker stop chromium
To remove the container:

bash
Copy
Edit
docker rm chromium
To clean up unused Docker resources:

bash
Copy
Edit
docker system prune
Step 4: Commit and Push to GitHub
Now, push everything to GitHub:

bash
Copy
Edit
git add README.md docker-compose.yaml
git commit -m "Added Chromium Docker setup guide"
git branch -M main
git push origin main
Your guide is now live on GitHub! 🎉

Final GitHub Link
Go to https://github.com/<YOUR_GITHUB_USERNAME>/chromium-docker-setup and share it! 🚀

Let me know if you need any changes! 😊








You said:
i created reposity what is next
ChatGPT said:
Great! Now that you’ve created the GitHub repository, follow these steps to upload your Chromium setup files to GitHub.

🔹 Step 1: Install Git (if not installed)
On your VPS, make sure Git is installed:

bash
Copy
Edit
sudo apt update
sudo apt install git -y
🔹 Step 2: Clone Your Repository
Replace <YOUR_GITHUB_USERNAME> and <YOUR_REPO_NAME> with your actual GitHub details:

bash
Copy
Edit
git clone https://github.com/<YOUR_GITHUB_USERNAME>/<YOUR_REPO_NAME>.git
cd <YOUR_REPO_NAME>
For example, if your repository is chromium-docker-setup, run:

bash
Copy
Edit
git clone https://github.com/your-username/chromium-docker-setup.git
cd chromium-docker-setup
🔹 Step 3: Move Your Files Into the Repository
If you already created docker-compose.yaml and README.md, move them into your cloned repository:

bash
Copy
Edit
mv ~/chromium/docker-compose.yaml .
mv ~/chromium/README.md .
(If you didn’t create a README.md yet, follow this guide.)

🔹 Step 4: Add Your Files to Git
Now, add the files to Git:

bash
Copy
Edit
git add .
🔹 Step 5: Commit the Files
Commit your changes with a message:

bash
Copy
Edit
git commit -m "Added Chromium Docker setup files"
🔹 Step 6: Push to GitHub
Send the files to your GitHub repository:

bash
Copy
Edit
git branch -M main
git push origin main
🔹 Step 7: Verify on GitHub
Go to https://github.com/<YOUR_GITHUB_USERNAME>/<YOUR_REPO_NAME>
You should see docker-compose.yaml and README.md uploaded.
🔹 Step 8: Share Your Repository
Now, anyone can access your setup by visiting your GitHub repository! 🎉

Let me know if you run into any issues! 🚀







You said:
how do i add the process as a post on my github profile ffs
ChatGPT said:
To add the Chromium Docker setup guide as a post on your GitHub profile, you need to create a special README.md file in a pinned repository. Follow these steps:

🔹 Step 1: Create a Special GitHub Repository
Go to GitHub and click on New Repository.
Repository name: Must be exactly your GitHub username (e.g., wavy → wavy).
Make it public and check “Add a README file”.
Click Create Repository.
🔹 Step 2: Clone Your Profile Repository
On your VPS or local machine, clone the repo:

bash
Copy
Edit
git clone https://github.com/<YOUR_GITHUB_USERNAME>/<YOUR_GITHUB_USERNAME>.git
cd <YOUR_GITHUB_USERNAME>
🔹 Step 3: Edit the Profile README
Open the README.md file:

bash
Copy
Edit
nano README.md
Paste the following Markdown content:

md
Copy
Edit
# 🚀 Chromium Docker Setup Guide  

This guide will help you deploy **Chromium in a Docker container** on a Linux VPS!  

## **Step 1: Connect to VPS**
```bash
ssh <YOUR_USERNAME>@<YOUR_SERVER_IP>
Step 2: Install Docker
bash
Copy
Edit
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
Step 3: Set Up Chromium
bash
Copy
Edit
mkdir chromium
cd chromium
nano docker-compose.yaml
Paste This in docker-compose.yaml:
yaml
Copy
Edit
services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined
    environment:
      - CUSTOM_USER=<YOUR_USERNAME>
      - PASSWORD=<YOUR_PASSWORD>
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - CHROME_CLI=https://www.google.com
    volumes:
      - /root/chromium/config:/config
    ports:
      - 3010:3000
      - 3011:3001
    shm_size: "1gb"
    restart: unless-stopped
Step 4: Run Chromium
bash
Copy
Edit
docker compose up -d
Step 5: Access Chromium
HTTP: http://<YOUR_SERVER_IP>:3010/
HTTPS: https://<YOUR_SERVER_IP>:3011/
Step 6: Stop Chromium
bash
Copy
Edit
docker stop chromium
docker rm chromium
docker system prune
🔗 Full Guide
Check the full setup guide here: GitHub Repo

🔥 Like this guide? Give it a ⭐ on my GitHub!

yaml
Copy
Edit

---

## **🔹 Step 4: Commit & Push the Changes**
```bash
git add README.md
git commit -m "Added Chromium Docker setup guide"
git push origin main
🔹 Step 5: Check Your GitHub Profile
Go to https://github.com/<YOUR_GITHUB_USERNAME>
Your README.md will now be displayed as a post on your GitHub profile! 🎉

🔥 Now your guide is publicly visible on your GitHub profile! Let me know if you need any help! 🚀😎







