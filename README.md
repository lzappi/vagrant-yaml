# vagrant-yaml

This Vagrantfile works with an external data file (a YAML file, named servers.yaml) to create multiple Vagrant boxes easily. 

The servers.yaml file contains all the specifics and can be easily edited to change the number and type of boxes to create. 

The Vagrantfile remains unchanged. 
It supports multiple private and public networks with Virtualbox as provider.
In *server.yaml' you need to specify at least:

 * name (hostname)
 * box (image)
 * ram
 * cpu
 * networks (can be private or public. If public you need to specify the bridge adapter)
 
You can copy *server.yaml.example* into server.yaml and editing as for your requirements.

Below is an example of a two node environment: node1 has is ubuntu 16.04, 2048 MB RAM, 2 CPUs, two public networks and one private network; node2 is a ubuntu 14.04, 1024 GB RAM, 1 cpu and one public network.

'''
- name: node1
  box: bento/ubuntu-16.04
  ram: "2048"
  cpu: "2"
  networks:
    - network: "cloud-in-mgmt"
      type: public_network
      bridge: eno1
      ip: "172.22.141.101"
      netmask: "255.255.255.0"
    - network: "public-net"
      type: public_network
      bridge: eno2
      ip: "172.22.140.101"
      netmask: "255.255.255.0"
    - network: "cloud-mgmt"
      type: private_network
      ip: "10.20.0.101"
      netmask: "255.255.255.0"

- name: node2
  box: bento/ubuntu-14.04
  ram: "1024"
  cpu: "1"
  networks:
    - network: "cloud-in-mgmt"
      type: public_network
      bridge: eno1
      ip: "172.22.141.102"
      netmask: "255.255.255.0"
'''
 
Enjoy and good vagrant
 
Lorenzo  
