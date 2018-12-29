Vagrant.configure("2") do |config|

config.vm.define "k8s_master" do |k8s_master|

    k8s_master.vm.box = "ubuntu/xenial64"

    k8s_master.vm.network "private_network", ip: "192.168.10.21", port: "6443"

    k8s_master.vm.hostname = "k8s-master"

    k8s_master.vm.provider :virtualbox do |vb|

      vb.customize ["modifyvm", :id, "--memory", "1026"]

      vb.customize ["modifyvm", :id, "--cpus", "2"]

      end

    k8s_master.vm.provision "shell", inline: <<-SHELL

      sudo echo "192.168.10.22 k8s-node-1" | sudo tee -a /etc/hosts

      sudo echo "192.168.10.23 k8s-node-2" | sudo tee -a /etc/hosts

      sudo apt-get -y update

      sudo apt-get -y install firewalld 

      sudo service firewalld start

      sudo firewall-cmd --permanent --zone=public --add-port=6443/tcp

      sudo firewall-cmd --reload     

    SHELL

  end


    config.vm.define "k8s_node_1" do |k8s_node1|

        k8s_node1.vm.box = "ubuntu/xenial64"

        k8s_node1.vm.network "private_network", ip: "192.168.10.22"

        k8s_node1.vm.hostname = "k8s-node-1"

        k8s_node1.vm.provision "shell", inline: <<-SHELL

           sudo echo "192.168.10.21 k8s-master" | sudo tee -a /etc/hosts

           sudo apt-get -y update

        SHELL

        end
 
    config.vm.define "k8s_node_2" do |k8s_node2|

      k8s_node2.vm.box = "ubuntu/xenial64"

      k8s_node2.vm.network "private_network", ip: "192.168.10.23"

      k8s_node2.vm.hostname = "k8s-node-2"

      k8s_node2.vm.provision "shell", inline: <<-SHELL

       sudo echo "192.168.10.21 k8s-master" | sudo tee -a /etc/hosts

       sudo apt-get -y update

    SHELL

  end

end
