Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
 # config.vm.boot_timeout = 600

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 4096
    vb.cpus = 2
  end

  # ===== MASTER =====
  config.vm.define "k8s-cp01" do |m|
    m.vm.hostname = "k8s-cp01"
    m.vm.provider "virtualbox" do |vb|
      vb.name = "k8s-cp01"
    end
    m.vm.network "private_network", ip: "192.168.56.10"
    # Fix default route (VERY IMPORTANT)
    m.vm.provision "shell", inline: <<-SHELL
      sudo ip route del default || true
      sudo ip route add default via 10.0.2.2 dev enp0s3
    SHELL
    m.vm.provision "shell", path: "scripts/common.sh"
    m.vm.provision "shell", path: "scripts/master.sh"
  end

  # ===== WORKER 1 =====
  config.vm.define "k8s-wk01" do |w|
    w.vm.hostname = "k8s-wk01"
    w.vm.provider "virtualbox" do |vb|
      vb.name = "k8s-wk01"
    end
    w.vm.network "private_network", ip: "192.168.56.11"
      # Fix default route
    w.vm.provision "shell", inline: <<-SHELL
      sudo ip route del default || true
      sudo ip route add default via 10.0.2.2 dev enp0s3
    SHELL
    w.vm.provision "shell", path: "scripts/common.sh"
    w.vm.provision "shell", path: "scripts/worker.sh"
  end

  # ===== WORKER 2 =====
  config.vm.define "k8s-wk02" do |w|
    w.vm.hostname = "k8s-wk02"
    w.vm.provider "virtualbox" do |vb|
      vb.name = "k8s-wk02"
    end
    w.vm.network "private_network", ip: "192.168.56.12"
      # Fix default route
    w.vm.provision "shell", inline: <<-SHELL
      sudo ip route del default || true
      sudo ip route add default via 10.0.2.2 dev enp0s3
    SHELL
    w.vm.provision "shell", path: "scripts/common.sh"
    w.vm.provision "shell", path: "scripts/worker.sh"
  end
end
