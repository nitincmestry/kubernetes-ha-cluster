# Kubernetes High Availability Cluster with HAProxy (Ansible Role)
This Ansible role automates the deployment of a highly available (HA) Kubernetes cluster with HAProxy for load balancing the Kubernetes API server.

Features
Installs and configures Kubernetes on multiple master nodes.
Sets up HAProxy for load balancing traffic across the master nodes.
Provides a dynamic configuration that automatically adapts to changes in the number of master nodes.

## Requirements
1) Ansible >= 2.9
2) Kubernetes compatible Linux distribution on all nodes (masters, worker nodes, and HAProxy server)
3) DNS server configured to resolve hostnames (if using FQDNs in the inventory)
4) Inventory
  The inventory file should define three groups:
  * kubernetes_masters: A list of IP addresses or hostnames of the Kubernetes master nodes.
  * kubernetes_nodes: A list of IP addresses or hostnames of the worker nodes.
  * haproxy_server: The IP address or hostname of the HAProxy server.

HOSTS
Example Inventory (using IP addresses):
```
[kubernetes_masters]
192.168.1.10
192.168.1.11

[kubernetes_nodes]
192.168.1.20
192.168.1.21
192.168.1.22

[haproxy_server]
192.168.1.30
```

Example Inventory (using FQDNs):
```
[kubernetes_masters]
master1
master2

[kubernetes_nodes]
node1
node2
node3

[haproxy_server]
haproxy
```

Important Note: If using FQDNs, ensure your DNS server can resolve them to the correct IP addresses.

Usage
Clone or download this role into your Ansible roles directory.

Create an inventory file as described above.

Create a playbook that includes this role:

YAML
```
---
- hosts: all
  roles:
    - { role: kubernetes-ha-cluster }
```

Run the playbook:
Bash
```
ansible-playbook your_playbook.yml -i hosts
```

Configuration
This role uses templates for service configuration files (kubelet.service.j2, kube-proxy.service.j2, and haproxy.cfg.j2).
You can customize these templates to adjust configurations as needed for your environment.
License
MIT License

Contributing
Pull requests and suggestions are welcome!