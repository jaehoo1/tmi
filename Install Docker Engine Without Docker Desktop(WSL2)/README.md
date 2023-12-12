# Install Docker Engine Without Docker Desktop(WSL2)(Docker Desktop 없이 Docker Engine 설치하기)
Docker Desktop이 유료화 됨에 따라, Docker Engine을 Docker Desktop 없이 설치  
설치 환경 : Windows 10 WSL2 Ubuntu 22.04
```bash
sudo apt -y update && sudo apt -y upgrade
sudo apt -y install apt-transport-https ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt -y install docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker $USER
sudo service docker start
```