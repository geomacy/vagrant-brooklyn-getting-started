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
  servers.each do |servers|
    config.vm.define servers["name"] do |srv|
      srv.vm.box = servers["box"]
      # srv.vm.network "private_network", ip: servers["ip"]
      # srv.vm.network "public_network", ip: servers["ip"], bridge: [
      #   "Intel(R) Ethernet Connection (2) I218-V"
      # ]

      if servers.has_key?("forwarded_ports")
        servers["forwarded_ports"].each do |ports|
          config.vm.network "forwarded_port", guest: ports["guest"], host: ports["host"], guest_ip: ports["guest_ip"]
        end
      end

      srv.vm.hostname = servers["name"]
      srv.vm.provider :virtualbox do |vb|
        vb.name = servers["name"]
        vb.memory = servers["ram"]
        vb.cpus = servers["cpus"]
      end
      if servers.has_key?("shell")
        servers["shell"].each do |cmd|
          config.vm.provision "shell", privileged: false, inline: cmd
        end
       end
    end
  end
end