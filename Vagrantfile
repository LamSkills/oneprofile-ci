VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'centos/7'

  # Tweak VirtualBox configuration for GUI applications
  config.vm.provider :virtualbox do |v|
    v.name = 'centos'
    v.memory = 2048
    v.cpus = 2
    #v.gui = true
  end

  config.vm.synced_folder ".", "/vagrant"
  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.provision "prepare-installation", privileged: true, type: "shell", inline: <<-SHELL
    sudo yum -y install python2-dnf libselinux-python yum
    sudo yum -y install ansible
  SHELL
  config.vm.provision "run", type: "shell", inline: <<-SHELL
    cd /vagrant/ansible
    su -c "ansible-playbook -u vagrant playbook.yml" vagrant
  SHELL

end