VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    vault_password_file = "~/.vault_demo.txt"
    config.vm.define "app1.local" do |vagrant1|
        vagrant1.vm.box = "ubuntu/trusty64"
        vagrant1.vm.hostname = "app1.local"
        vagrant1.vm.network "forwarded_port", guest: 80, host: 8901
        vagrant1.vm.network "private_network", ip: "10.10.10.11"
        vagrant1.vm.provision "ansible" do |ansible|
            ansible.vault_password_file = vault_password_file
            ansible.playbook = "site.yml"
            ansible.inventory_path = 'vagrant-inventory'
        end
    end
    config.vm.define "mysql.local" do |vagrant3|
        vagrant3.vm.box = "ubuntu/trusty64"
        vagrant3.vm.hostname = "mysql.local"
        vagrant3.vm.network "forwarded_port", guest: 3306, host: 8902
        vagrant3.vm.network "private_network", ip: "10.10.10.21"
        vagrant3.vm.provision "ansible" do |ansible|
            ansible.vault_password_file = vault_password_file
            ansible.playbook = "site.yml"
            ansible.inventory_path = 'vagrant-inventory'
        end
    end
end
