# set up the default terminal
ENV["TERM"]="linux"

Vagrant.configure("2") do |config|
  
  # set the image for the vagrant box
  config.vm.box = "opensuse/Leap-15.2.x86_64"
  ## Set the image version
  # config.vm.box_version = "15.2.31.247"

  # st the static IP for the vagrant box
  config.vm.network "private_network", ip: "192.168.50.4"

  # Explicitly enable rsync between the guest and host
  config.vm.synced_folder ".", "/vagrant", type: "rsync", 
  rsync__args: ["--verbose", "--rsync-path='sudo rsync'", "--archive", "--delete", "-z"]
  
  # configure port forwarding
  config.vm.network "forwarded_port", guest: 7111, host: 7111

  # Configure docker service to run when the machine boots
  config.vm.provision "shell", inline: <<-SHELL
    sudo systemctl enable docker
    sudo systemctl start docker
  SHELL

  # consifure the parameters for VirtualBox provider
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "8196"
    vb.cpus = 4
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
  end
end
