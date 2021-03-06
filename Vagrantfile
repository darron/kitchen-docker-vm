# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.omnibus.chef_version = :latest
  config.berkshelf.enabled = true

  config.vm.box = "opscode-ubuntu-12.04"
  config.vm.box_url = "https://opscode-vm-bento.s3.amazonaws.com/vagrant/opscode_ubuntu-12.04_provisionerless.box"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--name", "docker-kitchen"]
    vb.customize ["modifyvm", :id, "--memory", "1280"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
  end

  config.vm.network "private_network", :ip => "192.168.101.101"

  config.vm.provision :chef_solo do |chef|
    chef.run_list = ['recipe[docker]']
    chef.json = {
      'docker' => {
        'install_type' => 'binary',
        'binary' => { 'version' => '0.6.6' },
        'bind_socket' => 'unix:///var/run/docker.sock',
        'bind_uri' => 'tcp://192.168.101.101:4242'
      }
    }
  end
end
