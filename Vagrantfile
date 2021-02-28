# -*- mode: ruby -*-
# # vi: set ft=ruby :

# Specify minimum Vagrant version and Vagrant API version
Vagrant.require_version ">= 1.6.0"
VAGRANTFILE_API_VERSION = "2"

# Require YAML module
require 'yaml'

# Read YAML file with box details
servers = YAML.load_file('servers.yaml')

# Create boxes
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Iterate through entries in YAML file 
  servers.each do |s|
    config.vm.define s["name"] do |srv|
      srv.vm.box = s["box"]
      srv.vm.box_version = s["box_version"]
      srv.vm.hostname = s["name"]
      srv.vm.network "forwarded_port", guest: 22, host: s["ssh_port"]
      s["networks"].each do |n|
        if n["type"] == "public_network"
          srv.vm.network "public_network", bridge: n["bridge"], ip: n["ip"], netmask: n["netmask"]
        else
          srv.vm.network "private_network", ip: n["ip"], netmask: n["netmask"]
        end
      end
      if s["synced"] == ""
        srv.vm.synced_folder ".", "/vagrant" , type: "rsync"
      else
        s["synced"].each do |f|
          srv.vm.synced_folder f["src"], f["dst"], type: f["type"]
        end
      end
      srv.vm.provider "virtualbox" do |vb|
        vb.memory = s["ram"]
        vb.cpus = s["cpu"]  
        vb.customize ["modifyvm", :id, "--cableconnected1", "on"]
      end
    end
  end
end
