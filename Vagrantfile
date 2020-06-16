# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANT_API_VERSION = "2"

windows_IP = "192.168.35.50"
git_user   = "Mike Scott"
git_email  = "mike.scott@hiscox.com" 

Vagrant.configure(VAGRANT_API_VERSION) do |config|

  config.vm.define "windows" do |this|
    this.vm.box = "gusztavvargadr/windows-10"
    this.vm.hostname = 'windows'
    this.vm.network :private_network, ip: windows_IP

    this.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2048]
    end

    this.vm.provision "shell", path: "install_chocolatey.ps1"

    this.vm.provision "shell", inline: <<-SCRIPT
      choco install git --yes
      git config --global user.name "#{git_user}"
      git config --global user.email "#{git_email}"
    SCRIPT

    this.vm.provision "shell", path: "install_devtools.ps1"

  end
end
