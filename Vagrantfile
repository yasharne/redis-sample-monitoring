# -*- mode: ruby -*-
# vi: set ft=ruby :

REDIS1_IP = "172.28.128.11"
REDIS2_IP = "172.28.128.12"
REDIS3_IP = "172.28.128.13"
REDIS_EXPORTER_IP = "172.28.128.14"
PROMETHEUS_IP = "172.28.128.15"
GRAFANA_IP = "172.28.128.16"

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = 512
  end
  config.vm.synced_folder ".", "/vagrant"
  config.vm.box_check_update = false
  
  config.vm.define "redis1" do |redis1|
    redis1.vm.box = "hashicorp/bionic64"
    redis1.vm.network "private_network", ip: REDIS1_IP
  end

  config.vm.define "redis2" do |redis2|
    redis2.vm.box = "hashicorp/bionic64"
    redis2.vm.network "private_network", ip: REDIS2_IP
  end

  config.vm.define "redis3" do |redis3|
    redis3.vm.box = "hashicorp/bionic64"
    redis3.vm.network "private_network", ip: REDIS3_IP
  end

  config.vm.define "redis_exporter1" do |redis_exporter1|
    redis_exporter1.vm.box = "hashicorp/bionic64"
    redis_exporter1.vm.network "private_network", ip: REDIS_EXPORTER_IP
  end

  config.vm.define "prometheus1" do |prometheus1|
    prometheus1.vm.box = "hashicorp/bionic64"
    prometheus1.vm.network "private_network", ip: PROMETHEUS_IP
  end

  config.vm.define "grafana1" do |grafana1|
    grafana1.vm.box = "hashicorp/bionic64"
    grafana1.vm.network "private_network", ip: GRAFANA_IP
  end
  
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.extra_vars = {
      redis1_ip: REDIS1_IP,
      redis2_ip: REDIS2_IP,
      redis3_ip: REDIS3_IP,
      redis_exporter_ip: REDIS_EXPORTER_IP,
      prometheus_ip: PROMETHEUS_IP,
      grafana_ip: GRAFANA_IP
    }
    ansible.groups = {
      "redis_master" => ["redis1"],
      "redis_replicas" => ["redis2", "redis3"],
      "redis:children" => ["redis_master", "redis_replicas"],
      "redis_exporter" => ["redis_exporter1"],
      "prometheus" => ["prometheus1"],
      "grafana" => ["grafana1"]
    }
  end

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
  vagrant_synced_folder_default_type = ""
end
