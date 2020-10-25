# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :webserver => {
        :box_name => "centos/7",
        :ip_addr => '192.168.11.101'
  },
  :rsyslog => {
        :box_name => "centos/7",
        :ip_addr => '192.168.11.102'
  }
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

      config.vm.define boxname do |box|

          box.vm.box = boxconfig[:box_name]
          box.vm.host_name = boxname.to_s

          #box.vm.network "forwarded_port", guest: 3260, host: 3260+offset

          box.vm.network "private_network", ip: boxconfig[:ip_addr]

          box.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "512"]
          end
          
          box.vm.provision "shell", inline: <<-SHELL
            mkdir -p ~root/.ssh; cp ~vagrant/.ssh/auth* ~root/.ssh
            yum install vim -y
          SHELL
      end
          config.vm.define "webserver" do |webserver|
                webserver.vm.provision "shell", inline: <<-SHELL
                mkdir -p ~root/.ssh; cp ~vagrant/.ssh/auth* ~root/.ssh
                echo "toor" | sudo passwd root --stdin
                # здесь для server
                SHELL
          end
          config.vm.define "rsyslog" do |rsyslog|
                rsyslog.vm.provision "shell", inline: <<-SHELL
                mkdir -p ~root/.ssh; cp ~vagrant/.ssh/auth* ~root/.ssh
                echo "toor" | sudo passwd root --stdin
                SHELL
          end
          config.vm.provision "ansible" do |ansible|
            ansible.playbook = "playbook.yml"
          end
  end
end
