# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  ################## ROUTER ##################

  config.vm.define "router" do |router|

    router.vm.box = "ubuntu/xenial64"
    router.vm.hostname = "router"
    router.vm.synced_folder "shared_router", "/shared"

    router.vm.network "private_network", ip: "10.10.1.1"
    router.vm.network "private_network", ip: "10.10.2.1"

    router.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 2048
    end

    router.vm.provision "ansible" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "playbook-router.yml"
    end

  end

  ################## CLIENT ##################

  config.vm.define "client" do |client|

    client.vm.box = "ubuntu/trusty64"
    client.vm.hostname = "client"
    client.vm.synced_folder "shared_client", "/shared"

    client.vm.network "private_network", ip: "10.10.1.2"

    client.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get upgrade
      apt-get install iperf
      apt-get install sip-tester
    SHELL

  end

  ################## SERVER ##################

  config.vm.define "server" do |server|

    server.vm.box = "ubuntu/trusty64"
    server.vm.hostname = "server"
    server.vm.synced_folder "shared_server", "/shared"

    server.vm.network "private_network", ip: "10.10.2.2"

    server.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get upgrade
      apt-get install iperf
      apt-get install sip-tester
    SHELL

  end

end
