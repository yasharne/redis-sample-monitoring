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
  vagrant_synced_folder_default_type = ""
end
