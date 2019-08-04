# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.provider :libvirt do |libvirt|
        libvirt.driver = "kvm"
    end
    config.vm.synced_folder './shared', '/vagrant', type: '9p', disabled: false, accessmode: "mapped"
    config.vm.box = "generic/ubuntu1804"
    config.vm.box_version = "1.9.20"
    config.vm.network "forwarded_port", guest: 5432, host: 5432
    config.vm.provision:shell, inline: <<-SHELL
        echo "root:rootroot" | sudo chpasswd
        sudo timedatectl set-timezone Asia/Ho_Chi_Minh
        sudo wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
        sudo echo "deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main" >> /etc/apt/sources.list.d/pgdg.list
    SHELL
    config.vm.provision:shell, path: "bootstrap.sh"

    config.vm.define "node1" do |node1|
        node1.vm.hostname = "node1"
    end

    config.vm.define "node2" do |node2|
        node2.vm.hostname = "node2"
    end
end
