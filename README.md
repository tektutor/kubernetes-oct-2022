# Lab Setup

Our Lab machine is an Ubuntu 20.04 64-bit OS
Quad Core
32 GB RAM
500 GB HDD(Storage)

## For detailed installation instructions, you may refer the official documentation here
<pre>
https://docs.docker.com/engine/install/
</pre>

## Installing Docker Community Edition in Ubuntu 20.04 64-bit OS
```
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release -y
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
sudo apt-get update -y
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
sudo usermod -aG docker $USER
newgrp docker
docker --version
docker images
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ <b>docker --version</b>
Docker version 20.10.21, build baeda1f

jegan@tektutor.org:~/Desktop$ <b>docker images</b>
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
</pre>
