# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
    # Sync Directory
    config.vm.synced_folder "/Users/yasuaki640/PhpstormProjects", "/home/vagrant/workspace", create:"true", mount_options: ['dmode=777','fmode=777']
    # portマッピング
    config.vm.network "forwarded_port", guest: 8000, host: 8000
    config.vm.network "forwarded_port", guest: 3306, host: 3306
    config.vm.network "forwarded_port", guest: 8080, host: 8080
    config.vm.network "forwarded_port", guest: 4572, host: 4572
    config.vm.network "private_network", ip: "192.168.33.10"
    # ssh-agent起動
    config.vm.provision "shell", run: "always", inline: <<-SHELL
    echo 'eval `ssh-agent`' > /home/vagrant/.bash_profile
  SHELL
  # setup
  config.vm.provision "shell", inline: <<-SHELL
    apt-get -y upgrade
    apt-get -y update
    # docker, docker-compose
    curl -fsSL https://get.docker.com -o get-docker.sh
    sh get-docker.sh
    curl -fsSL https://github.com/docker/compose-cli/releases/download/v2.0.0-beta.3/docker-compose-linux-amd64 -o .docker/cli-plugins/docker-compose --create-dirs
    chmod 755 .docker/cli-plugins/docker-compose
    chown -R vagrant:vagrant .docker
    usermod -aG docker vagrant
    gpasswd -a vagrant docker
    systemctl enable --now docker
    systemctl restart docker
    echo 'eval `ssh-agent`' > /home/vagrant/.bash_profile
  SHELL
  config.vm.box = "bento/ubuntu-20.04"
end
