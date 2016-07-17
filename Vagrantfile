Vagrant.require_version ">= 1.8.1"
Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 4000, host: 4000

  project_root = "/home/web/data"

  config.vm.network "private_network", type: "dhcp"
  config.vm.synced_folder ".", project_root, type: "nfs"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 512
  end

  config.vm.provision "shell", keep_color: true, privileged: false, inline: <<-SHELL
    sudo apt-get -q -y update
    sudo apt-get -q -y upgrade
    gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
    curl -sSL https://get.rvm.io | bash -s stable --ruby=2.1.7 --gems=bundler --quiet-curl
    source /home/vagrant/.rvm/scripts/rvm
    cd #{project_root}
    bundle install

    echo "cd #{project_root}" >> ~/.bashrc
  SHELL

end
