# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "win12r2"
  config.vm.network "forwarded_port", guest: 3389, host: 3389
  config.vm.network "forwarded_port", guest: 8111, host: 8111
  config.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"
#  config.vm.provision "shell", path: "bootstrap.ps1"
  config.omnibus.chef_version = :latest
  config.vm.provider "virtualbox" do |v|
     v.gui = false
  end
  config.vm.synced_folder "./cookbooks", 'c:\tmp\cookbooks'
  config.vm.provision "chef_solo" do |chef|
    chef.cookbooks_path = ["cookbooks"]
    chef.run_list = [
      "recipe[teamcity]",
      "recipe[teamcity::install_jdk]",
      "recipe[teamcity::install_teamcity]",
      "recipe[teamcity::install_dotnet]",
      "recipe[teamcity::install_winfeatures]"
    ]
#    chef.add_recipe "visualstudio"
  end
end
