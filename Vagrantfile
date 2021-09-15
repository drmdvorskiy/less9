Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 1
  end

  config.vm.provision "file", source: "key/id_rsa.pub", destination: "/home/vagrant/.ssh/id_rsa.pub"
  config.vm.provision "shell", inline: <<-SHELL
    cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
  SHELL

  config.vm.define "haproxy" do |haproxy|
    haproxy.vm.box = "ubuntu/focal64"
    haproxy.vm.hostname = "haproxy"
    haproxy.vm.network "private_network", ip: "192.168.6.2", hostname: true
    haproxy.vm.synced_folder ".", "/vagrant", disabled: true
  end

  config.vm.define "etcd" do |etcd|
    etcd.vm.box = "ubuntu/focal64"
    etcd.vm.hostname = "f2"
    etcd.vm.network "private_network", ip: "192.168.6.3", hostname: true
    etcd.vm.synced_folder ".", "/vagrant", disabled: true
  end

  config.vm.define "postgresql1" do |postgresql1|
    postgresql1.vm.box = "ubuntu/focal64"
    postgresql1.vm.hostname = "postgresql1"
    postgresql1.vm.network "private_network", ip: "192.168.6.4", hostname: true
    postgresql1.vm.synced_folder ".", "/vagrant", disabled: true
  end

  config.vm.define "postgresql2" do |postgresql2|
    postgresql2.vm.box = "ubuntu/focal64"
    postgresql2.vm.hostname = "postgresql2"
    postgresql2.vm.network "private_network", ip: "192.168.6.5", hostname: true
    postgresql2.vm.synced_folder ".", "/vagrant", disabled: true
  end

end
