# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_BASE = "ubuntu/focal64" # VM Operating System
BOX_CPU = 2 # Number of virtual cpu assigned to VM
BOX_MEMORY = "1024" # Amount of memory assigned to VM
IP = "192.168.2.105"

Vagrant.configure("2") do |config|
    config.vm.box = BOX_BASE
    config.vm.network "private_network", ip: IP
    config.vm.hostname = "docker"
    config.vm.provider "virtualbox" do |vb|
        vb.memory = BOX_MEMORY
        vb.cpus = BOX_CPU
    end
    config.vm.provision "shell", inline: $install_docker
end

$install_docker = <<-SCRIPT
sudo apt-get update && \
sudo apt-get install -y ca-certificates curl gnupg lsb-release && \
sudo mkdir -p /etc/apt/keyrings && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg && \
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && \
sudo apt-get update && \
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin && \
sudo usermod -aG docker $USER && \
newgrp docker && \
docker run --rm hello-world && \
sudo sed -i 's@--containerd=/run/containerd/containerd.sock@-H=tcp://0.0.0.0:2375@g' /lib/systemd/system/docker.service && \
sudo systemctl daemon-reload && \
sudo systemctl restart docker
SCRIPT