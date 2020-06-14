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


  config.vm.define "w2k16" do |w2k16|
    w2k16.vm.box = "petrichorFTK/w2k16"
    w2k16.vm.hostname = "dc01"
    w2k16.ssh.insert_key = false
    w2k16.vm.boot_timeout = 800
	w2k16.vm.network "private_network", ip: "10.10.98.10",
	  virtualbox__intnet: true
	w2k16.vm.network "forwarded_port", guest: 3389, host: 33389, protocol: "tcp",
	  auto_correct: true
    w2k16.vm.graceful_halt_timeout = 180
    w2k16.vm.communicator = "winrm"
    w2k16.winrm.timeout = 120
    w2k16.vm.provision "shell", privileged: "true", inline: "Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))"
    w2k16.vm.provision "shell", privileged: "true", inline: "choco install -y notepadplusplus Firefox 7zip putty bitvise-ssh-client git winlogbeat -v"
	w2k16.vm.provision "shell", privileged: "true", inline: "git clone https://github.com/DefensiveOrigins/DomainBuildScripts"
	w2k16.vm.provision "shell", privileged: "true", inline: "git clone https://github.com/davidprowe/BadBlood"
	w2k16.vm.provision "shell", privileged: "true", inline: "git clone https://github.com/olafhartong/sysmon-modular"
	w2k16.vm.provision "file", source: "uploads/pfSense-pkg-zeek-0.1.1.txz", destination: "C:/Users/vagrant/pfSense-pkg-zeek-0.1.1.txz"
	w2k16.vm.provision "file", source: "uploads/config-pfSense_v2.xml", destination: "C:/Users/vagrant/config.xml"
	w2k16.vm.provision "shell", privileged: "true", inline: "Set-NetIPAddress -InterfaceIndex 2 -IPAddress 10.10.98.10 -PrefixLength 24"
    w2k16.vm.provision "shell", privileged: "true", inline: "Set-DnsClientServerAddress -InterfaceIndex 2 -ServerAddress ('127.0.0.1','1.1.1.1')"
	  w2k16.vm.provider :virtualbox do |vb|
	    vb.name = "dc01"
		vb.cpus  = "2"
		vb.memory = "4096"
	  end
  end



  config.vm.define "w10" do |w10|
    w10.vm.box = "detectionlab/win10"
    w10.vm.hostname = "w10"
    w10.ssh.insert_key = false
	w10.vm.graceful_halt_timeout = 180
	w10.vm.network "private_network", type: "dhcp",
	  virtualbox__intnet: true
    w10.vm.communicator = "winrm"
    w10.winrm.timeout = 240
    w10.vm.boot_timeout = 900
	  w10.vm.provider :virtualbox do |vb|
	    vb.name = "wkstn"
		vb.memory = "4096"
		vb.cpus = "1"
	  end
  end

  config.vm.define "ub18" do |ub18|
    ub18.vm.box = "ubuntu/bionic64"
    ub18.vm.hostname = "siem"
    ub18.ssh.insert_key = false
    ub18.vm.boot_timeout = 800
	ub18.vm.network "private_network", ip: "10.10.98.20",
	  virtualbox__intnet: true
	ub18.vm.provision "shell", privileged: "true", inline: "git clone https://github.com/cyb3rward0g/HELK.git"
    ub18.vm.provision "shell", privileged: "true", inline: "curl -fsSl https://get.docker.com -o get-docker.sh"
    ub18.vm.provision "shell", privileged: "true", inline: "chmod +x get-docker.sh"
	ub18.vm.provision "shell", privileged: "true", inline: "./get-docker.sh"
    ub18.vm.provision "shell", privileged: "true", inline: "systemctl enable docker.service"
    ub18.vm.provision "shell", privileged: "true", inline: "systemctl start docker.service"
	  ub18.vm.provider :virtualbox do |vb|
	    vb.name = "SIEM"
		vb.cpus  = "2"
		vb.memory = "8192"
	  end
  end

  config.vm.define "pfsense" do |pf|
    pf.vm.box = "ksklareski/pfsense-ce"
    pf.ssh.insert_key = false
    pf.vm.boot_timeout = 800
	pf.vm.network "private_network", ip: "10.10.98.1"
	pf.ssh.shell = 'sh'
	pf.vm.provision "shell", privileged: "true", inline: "sed -i.bak s/no/yes/g /usr/local/etc/pkg/repos/FreeBSD.conf"
    pf.vm.provision "shell", privileged: "true", inline: "sed -i.bak s/no/yes/g /usr/local/share/pfSense/pkg/repos/pfSense-repo.conf"
#   pf.vm.provision "shell", privileged: "true", inline: "pkg update -fq && pkg install -y zeek"
#	pf.vm.provision "file", source: "uploads/pfSense-pkg-zeek-0.1.1.txz", destination: "/tmp/pfSense-pkg-zeek-0.1.1.txz"
#	pf.vm.provision "shell", inline: "pkg add /tmp/pfSense-pkg-zeek-0.1.1.txz"
#	pf.vm.provision "file", source: "uploads/config-pfSense_v2.xml", destination: "/tmp/config.xml"
#	pf.vm.provision "shell", inline: "mv /tmp/config.xml /cf/conf/config.xml; chown root:wheel /cf/conf/config.xml"
	  pf.vm.provider :virtualbox do |vb|
	    vb.name = "FW"
		vb.cpus  = "1"
		vb.memory = "1024"
	  end
  end	
=end


  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
