# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Name the box for Vagrant
  config.vm.define :swiftup

  config.vm.provider "virtualbox" do |swiftup|
     swiftup.name = "swiftup"
  end

  config.vm.hostname = "swiftup"

  config.omnibus.chef_version = "11.4.0"

  # Default to using Ubuntu, unless specified otherwise
  case ENV['VMBOX']
  when 'centos64'
    config.vm.box = "CentOS-6.4-x86_64-minimal"
    config.vm.box_url = "http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-x86_64-v20130427.box"
  else
    config.vm.box = "opscode-ubuntu-12.04"
    config.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/opscode_ubuntu-12.04_chef-11.2.0.box"
  end

  config.ssh.max_tries = 40
  config.ssh.timeout   = 120

  # Enabling the Berkshelf plugin. To enable this globally, add this configuration
  # option to your ~/.vagrant.d/Vagrantfile file
  config.berkshelf.enabled = true

  config.vm.provision :chef_solo do |chef|
    chef.roles_path = "roles"
    chef.add_role("swift-all-in-one")

    chef.json = {
    }

    chef.run_list = [
        "recipe[apt]",
        "recipe[yum]",
        "recipe[swift::object-server]",
        "recipe[swift::container-server]",
        "recipe[swift::account-server]"
    ]
  end
end
