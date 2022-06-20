$script = <<-SCRIPT
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl apt-transport-https gnupg2

# terraform
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install terraform

# azure
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# vscodium
wget -O- https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg | sudo gpg --dearmor | sudo tee /usr/share/keyrings/vscodium.gpg
echo deb [signed-by=/usr/share/keyrings/vscodium.gpg] https://download.vscodium.com/debs vscodium main | sudo tee /etc/apt/sources.list.d/vscodium.list
sudo apt update

sudo apt-get install git
SCRIPT



Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: $script
    config.vm.box = "generic/ubuntu2204"
    #config.vm.box = "bento/ubuntu-18.04"
	config.vm.define "terraform" do |terraform|
		terraform.vm.hostname = "terraform"
		terraform.vm.provider "virtualbox" do |v|
			v.memory = 4096
			v.cpus = 2
			v.name = "terraform"
		end
	end
end