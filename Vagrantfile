Vagrant.configure("2") do |config|
  servers=[
    {
      :hostname => "ansible-control",
      :box => "takesako/alpine-virt-v3.18",
      :ip => "192.168.56.100",
      :ssh_port => '2214'
    },
    {
      :hostname => "db01",
      :box => "takesako/alpine-virt-v3.18",
      :ip => "192.168.56.101",
      :ssh_port => '2210'
    },
    {
      :hostname => "web01",
      :box => "takesako/alpine-virt-v3.18",
      :ip => "192.168.56.102",
      :ssh_port => '2211'
    },
    {
      :hostname => "web02",
      :box => "takesako/alpine-virt-v3.18",
      :ip => "192.168.56.103",
      :ssh_port => '2212'
    },
    {
      :hostname => "loadbalancer",
      :box => "takesako/alpine-virt-v3.18",
      :ip => "192.168.56.104",
      :ssh_port => '2213'
    }
  ]
config.vm.provision "shell", inline:"apk add --no-cache python3 py3-pip"
  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]
      config.vm.provision "shell", inline:"apk add --no-cache python3 py3-pip",run: "always"      
      node.vm.network :private_network, ip: machine[:ip]
      node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
      node.vm.provider :virtualbox do |v|
      	v.gui = true
      end
    end
  end

end
