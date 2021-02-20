# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/amazonlinux-2"
  config.vm.synced_folder "./src", "/home/vagrant/src"

  # config.vm.provider "virtualbox" do |vb|
  #   vb.memory = "8192"
  # end

  config.vm.provision :vagrant_user, type: "shell", privileged: false, inline: <<-SHELL
    sudo yum install -y git gcc openssl-devel readline-devel zlib-devel
    git clone https://github.com/rbenv/rbenv.git ~/.rbenv
    cd ~/.rbenv && src/configure && make -C src
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
    echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
    source ~/.bash_profile
    mkdir -p "$(rbenv root)"/plugins
    git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build
    rbenv install 2.7.2
    rbenv global 2.7.2
  SHELL
end
