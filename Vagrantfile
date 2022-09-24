Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2204"                     # image box
  config.vm.box_check_update = true                        # auto Updates
  config.vm.network "private_network", ip: "192.168.33.10" # Assigning private network
  config.vm.synced_folder ".", "/home"                     # Sync folder
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"                                     # Memory Allocation 
    vb.name = "ubuntu22"                                   # Server name
  end
  config.vm.provision "shell", inline: <<-SHELL

  apt update &&  apt full-upgrade -y # Update the system
  apt purge -y apport                # purge the old application
  apt autoremove -y                  # remove the unnecessarry items
  apt install curl -y                # install curl
  apt install docker.io -y           # install docker
  # Docker-compose repo
  sudo curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
  chmod +x /usr/local/bin/docker-compose # installing docker-compose
  apt install git -y                     # install git optional
  apt install vim -y                     # install vim
  docker-compose --version               # checking the installation
  # MiniKube repo
  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
  sudo install minikube-linux-amd64 /usr/local/bin/minikube # installing minikube
  minikube version                                          # checking the installation
  #Kubectl repo
  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
  sudo install kubectl /usr/local/bin/kubectl # Installing kubectl
  kubectl version --client -o json            # checking the installation
  # install virtualbox
  apt install -y virtualbox virtualbox-ext-pack 

  echo "Installization is sucessful"
  
  SHELL

  
end
