#
# Vagrantfile, with Chef-solo provisioning
# vi: set ft=ruby : 

Vagrant.configure("1") do |config|
    config.vm.box = "openplatform-base"
    #config.vm.box_url = "/Volumes/ERIC_DATA/vagrant/templates/precise64.box"

    config.vm.define :opfw do |opfw_config|
        opfw_config.vm.network :hostonly, "192.168.100.10"
        opfw_config.vm.host_name = "opfw.local"
        # Port 8000 on the host will go to port 80 on the Vagrant box
        #opfw_config.vm.network :forwarded_port, guest: 80, host: 8000, auto_correct: true

        # Here's a folder for passing stuff back and forth
        #opfw_config.vm.synced_folder "./shared", "/home/vagrant/host_shared"
        config.vm.provision :chef_solo do |opfw_chef|
            opfw_chef.json = {
              :mysql => {
                :server_root_password => "qrwe1423",
                :server_repl_password => "qrwe1423",
                :server_debian_password => "qrwe1423"
              }
            }
            opfw_chef.cookbooks_path = "cookbooks"
            opfw_chef.add_recipe "apt"
            opfw_chef.add_recipe "ohai"
            opfw_chef.add_recipe "build-essential"
            # opfw_chef.add_recipe "mysql::server"
            # opfw_chef.add_recipe "database"
        end
    end
end

Vagrant.configure("2") do |config|
    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "512"]
    end
end
