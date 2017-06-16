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
    set -e

    sudo apt-get -q -y update
    sudo apt-get -q -y upgrade
    sudo apt-get -q -y install build-essential gnupg2 libgmp-dev

    curl -sSL https://rvm.io/mpapis.asc | gpg2 --import -
    curl -sSL https://get.rvm.io | bash -s stable --ruby=2.4.0 --gems=bundler --quiet-curl
    source /home/vagrant/.rvm/scripts/rvm

    cd #{project_root}
    rm Gemfile.lock || true
    bundle install

    for s in 'cd #{project_root}'; do
      grep -q -F "$s" $HOME/.bashrc || echo "$s" >> $HOME/.bashrc
    done
  SHELL

end
