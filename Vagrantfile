$script = <<-SCRIPT
apt-get update
apt-get install git docker docker-compose -y
wget  -O Dynatrace-OneAgent-Linux-latest.sh "https://syb31902.sprint.dynatracelabs.com/api/v1/deployment/installer/agent/unix/default/latest?Api-Token=INSERT_API_TOKEN_HERE&arch=x86&flavor=default"
sudo /bin/sh Dynatrace-OneAgent-Linux-latest.sh APP_LOG_CONTENT_ACCESS=1 INFRA_ONLY=0
systemctl enable docker && systemctl start docker
chown -R vagrant:vagrant /media
git clone https://github.com/sebgl/htpc-download-box.git
chown -R vagrant:vagrant htpc-download-box
cd htpc-download-box
cp .env.example .env
sudo docker-compose up -d
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 4
  end

  config.vm.synced_folder "C:/Media", "/mediafiles"
  config.vm.box = "ubuntu/bionic64"
  config.vm.provision "shell", inline: $script
  config.vm.network "private_network", ip: "192.168.1.7"
end


