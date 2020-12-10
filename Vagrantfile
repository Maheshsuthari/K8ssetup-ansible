# -*- mode: ruby -*-
# # vi: set ft=ruby :

Vagrant.configure(2) do |config|

  (1..3).each do |i|
    config.vm.define "k8s#{i}" do |s|
      s.ssh.forward_agent = true
      s.vm.box = "ubuntu/xenial64"
      s.vm.hostname = "k8s#{i}"
      s.vm.network "public_network", ip: "192.168.46.#{i}"
      s.vm.provision :shell, path: "scripts/bootstrap_ansible.sh"
      if i == 1
        s.vm.provision :shell, inline: "PYTHONUNBUFFERED=1 ansible-playbook /vagrant/ansible/k8s-master.yml -c local"
      else
        s.vm.provision :shell, inline: "PYTHONUNBUFFERED=1 ansible-playbook /vagrant/ansible/k8s-worker.yml -c local"
      end
      #s.vm.network "public_network", ip: "172.42.42.#{i}",
       # auto_config: true
        #virtualbox__intnet: "k8s-net"
      s.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", "2048"]
        v.customize ["modifyvm", :id, "--cpus", "2"]
 
      #  v.name = "k8s#{i}"
      #  v.memory = 4096
      #  v.cpus = 3
      #  v.gui = false
      end
    end
  end

end
