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
 
Enjoy and good vagrant
 
Lorenzo
