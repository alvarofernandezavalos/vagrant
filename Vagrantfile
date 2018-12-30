Vagrant.configure("2") do |config|
  config.vm.boot_timeout = 60
  config.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant", :mount_options => ["dmode=777", "fmode=600"]
   
  config.vm.define "pulpo" do |pulpo|
    pulpo.vm.provision :shell, :inline => "apt-get install software-properties-common -y"
	pulpo.vm.provision :shell, :inline => "apt-add-repository ppa:ansible/ansible"
	pulpo.vm.provision :shell, :inline => "apt-get update"
	pulpo.vm.provision :shell, :inline => "apt-get install ansible -y --no-install-recommends"
    pulpo.vm.boot_timeout = 600
	pulpo.vm.host_name = "pulpo"
    pulpo.vm.box = "ubuntu/xenial64"
    pulpo.vm.provider "virtualbox" do |vb|
      vb.memory = 512
      vb.cpus = 1
	  vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
    end
    #pulpo.vm.network "forwarded_port", host: 8080, guest: 80, auto_correct: true
    pulpo.vm.network "private_network", ip: "192.168.68.10", virtualbox__intnet: true, auto_config: true
  end

  config.vm.define "calamar" do |calamar|
    calamar.vm.provision :shell, :inline => "apt-get update && apt-get install python -y --no-install-recommends"
	calamar.vm.boot_timeout = 600
	calamar.vm.host_name = "calamar"
    calamar.vm.box = "ubuntu/xenial64"
    calamar.vm.provider "virtualbox" do |vb|
      vb.memory = 512
      vb.cpus = 1
	  vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
    end
    calamar.vm.network "forwarded_port", host: 8082, guest: 80, auto_correct: true
    calamar.vm.network "private_network", ip: "192.168.68.11", virtualbox__intnet: true, auto_config: true
	
	#config.vm.provision "ansible" do |ansible|
	#	ansible.playbook = "ansible/request.yml"
	#end
	
  end
end