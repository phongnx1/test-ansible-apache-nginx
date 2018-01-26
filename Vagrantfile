# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  
  config.vm.box = "centos-6.5"
  config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"
  
  $script = "
sudo yum update -y --disablerepo=\* --enablerepo=base,updates ca-certificates
sudo yum install -y epel-release
sudo yum install -y --enablerepo=epel sshpass git
sudo yum install -y --enablerepo=epel-testing ansible
cd ansible-playbook
cp vagrant/insecure_private_key /home/vagrant/.ssh/id_rsa
cp vagrant/ssh_config /home/vagrant/.ssh/config
chmod -R og-rwx /home/vagrant/.ssh
chown -R vagrant.vagrant /home/vagrant/.ssh
cp vagrant/ansible.cfg /etc/ansible/ansible.cfg
  "

  $consumer_script = "
  sudo adduser oneid
  "
  
  config.vm.define :ci do |ci|
    ci.vm.hostname = "ci"
    ci.vm.box = "centos-6.5"
    ci.vm.network :private_network, ip: "192.168.33.50"
    ci.vm.network :forwarded_port, guest: 22, host: 2250, id: "ssh"
    ci.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", "1024"]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
    ci.ssh.private_key_path = "./vagrant/insecure_private_key"
    ci.ssh.insert_key = false
    ci.vm.synced_folder ".", "/home/vagrant/ansible-playbook", owner: "vagrant", group: "vagrant", :create => true, :mount_options => ["fmode=600"]
    ci.vm.provision :shell, inline: $script
  end
  
  config.vm.define :consumer do |consumer|
    consumer.vm.hostname = "consumer"
    consumer.vm.box = "centos-6.5"
    consumer.vm.network :private_network, ip: "192.168.33.51"
    consumer.vm.network :forwarded_port, guest: 22, host: 2251, id: "ssh"
	consumer.vm.synced_folder "./gmopoint", "/var/www/gmo/frontend/current", mount_options: ['dmode=777','fmode=777'], owner: "vagrant", group: "vagrant"
    consumer.vm.synced_folder "./gmopoint", "/var/www/gmo/backend/current", mount_options: ['dmode=777','fmode=777'], owner: "vagrant", group: "vagrant"
    consumer.vm.synced_folder "./gmopoint", "/var/www/gmo/console/current", mount_options: ['dmode=777','fmode=777'], owner: "vagrant", group: "vagrant"
    consumer.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", "1024"]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
    consumer.ssh.private_key_path = "./vagrant/insecure_private_key"
    consumer.ssh.insert_key = false
    consumer.vm.provision :shell, inline: $consumer_script
  end

  config.vm.define :consumer1 do |consumer1|
    consumer1.vm.hostname = "consumer1"
    consumer1.vm.box = "centos-6.5"
    consumer1.vm.network :private_network, ip: "192.168.33.52"
    consumer1.vm.network :forwarded_port, guest: 22, host: 2252, id: "ssh"
    consumer1.vm.synced_folder "./gmopoint", "/var/www/gmo/frontend/current", mount_options: ['dmode=777','fmode=777'], owner: "vagrant", group: "vagrant"
    consumer1.vm.synced_folder "./gmopoint", "/var/www/gmo/backend/current", mount_options: ['dmode=777','fmode=777'], owner: "vagrant", group: "vagrant"
    consumer1.vm.synced_folder "./gmopoint", "/var/www/gmo/console/current", mount_options: ['dmode=777','fmode=777'], owner: "vagrant", group: "vagrant"
    consumer1.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", "256"]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
    consumer1.ssh.private_key_path = "./vagrant/insecure_private_key"
    consumer1.ssh.insert_key = false
    consumer1.vm.provision :shell, inline: $consumer_script
  end

  config.vm.define :consumer2 do |consumer2|
    consumer2.vm.hostname = "consumer2"
    consumer2.vm.box = "centos-6.5"
    consumer2.vm.network :private_network, ip: "192.168.33.53"
    consumer2.vm.network :forwarded_port, guest: 22, host: 2253, id: "ssh"
    consumer2.vm.synced_folder "./gmopoint", "/var/www/gmo/frontend/current", mount_options: ['dmode=777','fmode=777'], owner: "vagrant", group: "vagrant"
    consumer2.vm.synced_folder "./gmopoint", "/var/www/gmo/backend/current", mount_options: ['dmode=777','fmode=777'], owner: "vagrant", group: "vagrant"
    consumer2.vm.synced_folder "./gmopoint", "/var/www/gmo/console/current", mount_options: ['dmode=777','fmode=777'], owner: "vagrant", group: "vagrant"
    consumer2.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", "256"]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
    consumer2.ssh.private_key_path = "./vagrant/insecure_private_key"
    consumer2.ssh.insert_key = false
    consumer2.vm.provision :shell, inline: $consumer_script
  end
end
