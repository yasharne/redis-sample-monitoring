# Simple Redis monitoring scenario using vagrant
This repository creates a simple scenario of redis master/slave and sentinel implementation and monitores the instances.
## Architecture
This scenario contains 3 redis servers (1 master and 2 slaves), with a sentinel service on each, A [redis_exporter](https://github.com/oliver006/redis_exporter) instance, a prometheus instance and a grafana instance. Grafana dashboard is imported from [here](https://github.com/oliver006/redis_exporter/blob/master/contrib/grafana_prometheus_redis_dashboard.json).
## prerequisites
In order to run this scenario you need three things installed on your system:
1. [Ansible](https://www.ansible.com/)
2. [Vagrant](https://www.vagrantup.com/)
3. [VirtualBox](https://www.virtualbox.org/)
## How to run
Running this project is as simple as cloning the project and running the following command in the terminal:
```
vagrant up
```
After deployment, you can access the grafana dashboard using this URL:
```
http://<GRAFANA_IP>:3000
```
Where `GRAFANA_IP` is defined in the Vagrantfile.