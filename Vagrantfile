# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.define "kali" do |kali|
    kali.vm.box = "kalilinux/rolling"
    kali.vm.hostname = "kali"
    kali.ssh.insert_key = false
    kali.vm.boot_timeout = 800
    kali.ssh.private_key_path = ["keys/.ssh/vagrant_rsa", "insecure_private_key"]
    kali.vm.provision "file", source: "keys/.ssh/vagrant_rsa.pub", destination: "~/.ssh/authorized_key"
	  kali.vm.provider :virtualbox do |vb|
	    vb.name = "Kali"
	  end
  end
  
  config.vm.define "vyos" do |vyos|
    vyos.vm.box = "rjet/vyos"
    vyos.vm.hostname = "att-rtr"
    vyos.ssh.insert_key = false
    vyos.vm.boot_timeout = 800
    vyos.ssh.private_key_path = ["keys/.ssh/vagrant_rsa", "insecure_private_key"]
    vyos.vm.provision "file", source: "keys/.ssh/vagrant_rsa.pub", destination: "~/.ssh/authorized_key"
    vyos.vm.synced_folder ".", "/vagrant", disabled: true
	  vyos.vm.provider :virtualbox do |vb|
	    vb.name = "VyOS"
	  end
  end

  config.vm.define "pf" do |pfsense|
    pfsense.vm.box = "kennyl/pfsense"
    pfsense.vm.hostname = "pfsense"
    pfsense.ssh.insert_key = false
    pfsense.vm.boot_timeout = 800
    pfsense.ssh.private_key_path = ["keys/.ssh/vagrant_rsa", "insecure_private_key"]
    pfsense.vm.synced_folder '/cygdrive/e/Vagrant/', '/vagrant', disabled: true
    pfsense.vm.provision "file", source: "keys/.ssh/vagrant_rsa.pub", destination: "~/.ssh/authorized_key"
	  pfsense.vm.provider :virtualbox do |vb|
	    vb.name = "Firewall"
	  end
  end

  config.vm.define "Splunk" do |splunk|
    splunk.vm.box = "petrichorFTK/W2k19_Splunk"
    splunk.vm.hostname = "Splunk"
    splunk.ssh.insert_key = false
    splunk.vm.boot_timeout = 800
    splunk.vm.graceful_halt_timeout = 180
    splunk.vm.communicator = "winrm"
    splunk.winrm.timeout = 120
	  splunk.vm.provider :virtualbox do |vb|
	    vb.name = "SIEM"
	  end
  end

  config.vm.define "bwa" do |bwa|
    bwa.vm.box = "petrichorFTK/owaspBWA"
    bwa.vm.hostname = "owaspBWA"
    bwa.ssh.insert_key = false
    bwa.vm.boot_timeout = 800
    bwa.vm.graceful_halt_timeout = 180
    bwa.ssh.insert_key = false
    bwa.ssh.private_key_path = ["keys/.ssh/vagrant_rsa", "insecure_private_key"]
    bwa.vm.synced_folder '/cygdrive/e/Vagrant/', '/vagrant', disabled: true
    bwa.vm.provision "file", source: "keys/.ssh/vagrant_rsa.pub", destination: "~/.ssh/authorized_key"
	  bwa.vm.provider :virtualbox do |vb|
	    vb.name = "owaspBWA"
	  end
  end
end
