# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
    :inetRouter => {
        :box_name => "centos/7",
        :memory => 512,
        :net => [
                   {ip: '192.168.255.1', adapter: 2, netmask: "255.255.255.248", virtualbox__intnet: "net-route"},
                ]
  },
    :centralRouter => {
        :box_name => "centos/7",
        :memory => 512,
        :net => [
                   {ip: '192.168.255.2', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "net-route"},
                   {ip: '192.168.100.1', adapter: 3, netmask: "255.255.255.252", virtualbox__intnet: "office1-net"},
                   {ip: '192.168.200.1', adapter: 4, netmask: "255.255.255.252", virtualbox__intnet: "office2-net"},
                   {ip: '192.168.0.1', adapter: 5, netmask: "255.255.255.240", virtualbox__intnet: "dir-net"},
                   {ip: '192.168.0.33', adapter: 6, netmask: "255.255.255.240", virtualbox__intnet: "hw-net"},
                   {ip: '192.168.0.65', adapter: 7, netmask: "255.255.255.192", virtualbox__intnet: "mgt-net"},
                ]
  },
  
    :centralServer => {
        :box_name => "centos/7",
        :memory => 512,
        :net => [
                   {ip: '192.168.0.2', adapter: 2, netmask: "255.255.255.240", virtualbox__intnet: "dir-net"},
                ]
  },
  
    :office1Router => {
        :box_name => "centos/7",
        :memory => 512,
        :net => [
               {ip: '192.168.100.2', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "office1-net"},
               {ip: '192.168.2.1', adapter: 3, netmask: "255.255.255.192", virtualbox__intnet: "office1_dev-net"},
               {ip: '192.168.2.65', adapter: 4, netmask: "255.255.255.192", virtualbox__intnet: "office1_test_srv-net"},
               {ip: '192.168.2.129', adapter: 5, netmask: "255.255.255.192", virtualbox__intnet: "office1_mngrs-net"},
               {ip: '192.168.2.193', adapter: 6, netmask: "255.255.255.192", virtualbox__intnet: "office1_hw-net"},
            ]
},
    :office1Server => {
        :box_name => "centos/7",
        :memory => 512,
        :net => [
               {ip: '192.168.2.194', adapter: 2, netmask: "255.255.255.192", virtualbox__intnet: "office1_hw-net"},
               {adapter: 3, auto_config: false, virtualbox__intnet: true},
               {adapter: 4, auto_config: false, virtualbox__intnet: true},
            ]
},
    :office2Router => {
        :box_name => "centos/7",
        :memory => 512,
        :net => [
               {ip: '192.168.200.2', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "office2-net"},
               {ip: '192.168.1.1', adapter: 3, netmask: "255.255.255.128", virtualbox__intnet: "office2_dev-net"},
               {ip: '192.168.1.129', adapter: 4, netmask: "255.255.255.192", virtualbox__intnet: "office2_mngrs-net"},
               {ip: '192.168.1.193', adapter: 5, netmask: "255.255.255.192", virtualbox__intnet: "office2_hw-net"},
            ]
},
    :office2Server => {
        :box_name => "centos/7",
        :memory => 512,
        :net => [
               {ip: '192.168.1.194', adapter: 2, netmask: "255.255.255.192", virtualbox__intnet: "office2_hw-net"},
               {adapter: 3, auto_config: false, virtualbox__intnet: true},
               {adapter: 4, auto_config: false, virtualbox__intnet: true},
            ]
}  


}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

    config.vm.define boxname do |box|

        box.vm.box = boxconfig[:box_name]
        box.vm.host_name = boxname.to_s

        box.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", boxconfig[:memory]]
        end

        boxconfig[:net].each do |ipconf|
          box.vm.network "private_network", ipconf
        end
              
        # config.vm.provision "ansible" do |ansible|    
        # # ansible.verbose = "v"
        # ansible.playbook = "ansible/playbook.yml" 
        # end

      end

  end
  
end