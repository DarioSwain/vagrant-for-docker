# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.define "trusty64" do |trusty64|
  end

  #config.vm.box_check_update = false
  config.vm.network "private_network", ip: "192.168.33.50"
  config.vm.synced_folder "./../../", "/var/www/", disabled: true
  
  config.vm.provision "shell",
  inline: "apt-get update && apt-get install -y samba php5-cli \
			&& wget -qO- https://get.docker.com/ | sh && mkdir -p /var/www/ \
			&& curl -LsS http://symfony.com/installer -o /usr/local/bin/symfony \
			&& chmod a+x /usr/local/bin/symfony \
			&& curl -L https://github.com/docker/compose/releases/download/1.3.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose \
			&& chmod +x /usr/local/bin/docker-compose \
			&& echo '[share]' >> /etc/samba/smb.conf \
			&& echo '    comment = Vagrant share' >> /etc/samba/smb.conf \
			&& echo '    path = /var/www' >> /etc/samba/smb.conf \
			&& echo '    browsable = yes' >> /etc/samba/smb.conf \
			&& echo '    guest ok = yes' >> /etc/samba/smb.conf \
			&& echo '    read only = no' >> /etc/samba/smb.conf \
			&& echo '    create mask = 0755' >> /etc/samba/smb.conf \
			&& chown nobody:nogroup /var/www/ \
			&& service samba restart \
			&& symfony new project 2.6"

  config.vm.provider "virtualbox" do |v|
	v.memory = 1024
	v.cpus = 2
  end
  
end