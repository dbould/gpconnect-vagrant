# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 3306, host: 6081

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.20.81"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "./html", "/var/www/html"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true

    # Customize the amount of memory on the VM:
    vb.memory = "8192"
    vb.cpus = "8"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    add-apt-repository ppa:openjdk-r/ppa -y
    apt-get update
    echo "\n----- Installing Apache and Java 8 ------\n"
    apt-get -y install apache2 openjdk-8-jdk
    update-alternatives --config java
    echo "\n----- Installing Tomcat ------\n"
    groupadd tomcat
    useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat
    wget -q http://mirrors.gigenet.com/apache/tomcat/tomcat-8/v8.0.30/bin/apache-tomcat-8.0.30.tar.gz
    mkdir /opt/tomcat
    tar xvf apache-tomcat-8*tar.gz -C /opt/tomcat --strip-components=1
    chgrp -R tomcat /opt/tomcat/conf
    chmod g+rwx /opt/tomcat/conf
    chmod g+r /opt/tomcat/conf/*
    chown -R tomcat /opt/tomcat/work/ /opt/tomcat/temp/ /opt/tomcat/logs/
    wget -q https://gist.githubusercontent.com/adeubank/1a8db1958578146120a2/raw/c796a8881d95dd2cbe47d1ffee8246463ec2c7a1/tomcat.conf
    sudo mv tomcat.conf /etc/init/
    sed -i "s#</tomcat-users>#  <user username=\\"admin\\" password=\\"secret\\" roles=\\"manager-gui,admin-gui\\"/>\\n</tomcat-users>#" /opt/tomcat/conf/tomcat-users.xml
    initctl reload-configuration
    initctl start tomcat
    curl -sL https://deb.nodesource.com/setup_7.x | bash -
    apt-get install -y nodejs
    apt-get install -y maven
    apt-add-repository ppa:brightbox/ruby-ng
    apt-get update
    apt-get install -y ruby2.3 ruby2.3-dev
    curl -sL https://rubygems.org/rubygems/rubygems-2.6.11.tgz >> rubygems2.6.10.tgz
    tar xzvf rubygems2.6.10.tgz
    sudo ruby setup.rb
    debconf-set-selections <<< "mysql-server mysql-server/root_password password vagrant"
    debconf-set-selections <<< "mysql-server mysql-server/root_password_again password vagrant"
    apt-get install -y mysql-server-5.6
    apt-get install -y mysql-client-5.6
    apt-get install -y mysql-client-core-5.6
    apt-get install -y libmysql-java
    mysql -uroot -pvagrant -e "CREATE USER 'answer'@'localhost' IDENTIFIED BY 'answer99q';"
    mysql -uroot -pvagrant -e "GRANT ALL PRIVILEGES ON *.* TO 'answer'@'localhost' WITH GRANT OPTION;"
    mysql -uroot -pvagrant -e "GRANT ALL PRIVILEGES ON *.* TO 'answer'@'%' WITH GRANT OPTION;"
    echo 'CLASSPATH=$CLASSPATH:/usr/share/java/mysql.jar' >> /home/vagrant/.bashrc
    echo 'export CLASHPATH' >> /home/vagrant/.bashrc
    echo 'JAVA_HOME="/usr/bin/java"' >> /home/vagrant/.bashrc
    echo 'M3_HOME="/usr/share/maven"' >> /home/vagrant/.bashrc
    echo 'RUBY_HOME="/usr/bin/ruby2.3"' >> /home/vagrant/.bashrc
    echo 'RUBYGEMS_HOME="/usr/lib/ruby/2.3.0/rubygems"' >> /home/vagrant/.bashrc
    echo 'PATH="$JAVA_HOME:$M2_HOME:$RUBY_HOME:$RUBYHOME:$PATH"' >> /home/vagrant/.bashrc
    apt-get install -y ant
    SHELL
end
