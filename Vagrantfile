# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.box_check_update = false

  config.vm.hostname = "osm-varnish-tile-cache"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 443, host: 8443

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--memory",              1024]
    vb.customize ["modifyvm", :id, "--cpus",                4]
    vb.customize ["modifyvm", :id, "--chipset",             "ich9"]
    vb.customize ["modifyvm", :id, "--nictype1",            "virtio"]
    vb.customize ["modifyvm", :id, "--nictype2",            "virtio"]
    vb.customize ["modifyvm", :id, "--vram",                "10"]
    vb.customize ["modifyvm", :id, "--hpet",                "on"]
    vb.customize ["modifyvm", :id, "--pae",                 "on"]
    vb.customize ["modifyvm", :id, "--ioapic",              "on"]
    vb.customize ["modifyvm", :id, "--usb",                 "off"] # Force No USB1
    vb.customize ["modifyvm", :id, "--usbehci",             "off"] # Force No USB2
  end

  config.vm.provider "lxc" do |lxc, override|
    override.vm.box = "fgrehm/trusty64-lxc"
    lxc.customize 'cgroup.memory.limit_in_bytes', "1024M"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "site.yml"
  end
end
