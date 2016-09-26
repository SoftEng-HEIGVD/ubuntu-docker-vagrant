Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 3000, host: 3000

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update -qq

    # Install Docker
    apt-get install -q -y apt-transport-https ca-certificates
    apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
    echo deb https://apt.dockerproject.org/repo ubuntu-trusty main > /etc/apt/sources.list.d/docker.list
    apt-get update -qq
    apt-get purge lxc-docker
    apt-get install -q -y linux-image-extra-$(uname -r) linux-image-extra-virtual
    apt-get install -q -y docker-engine
    service docker start

    # Install Docker Compose
    curl -L https://github.com/docker/compose/releases/download/1.8.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose

    usermod -a -G docker vagrant
  SHELL
end
