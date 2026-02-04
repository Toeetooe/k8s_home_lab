Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end

  # ===== MASTER =====
  config.vm.define "k8s-master" do |m|
    m.vm.hostname = "k8s-master"
    m.vm.network "private_network", ip: "192.168.56.10"
    m.vm.provision "shell", path: "scripts/common.sh"
    m.vm.provision "shell", path: "scripts/master.sh"
  end

  # ===== WORKER 1 =====
  config.vm.define "k8s-worker1" do |w|
    w.vm.hostname = "k8s-worker1"
    w.vm.network "private_network", ip: "192.168.56.11"
    w.vm.provision "shell", path: "scripts/common.sh"
    w.vm.provision "shell", path: "scripts/worker.sh"
  end

end
