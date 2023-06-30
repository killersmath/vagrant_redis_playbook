# This guide is optimized for Vagrant 1.8 and above.
# Older versions of Vagrant put less info in the inventory they generate.
Vagrant.require_version ">= 1.8.0"

Vagrant.configure(2) do |config|
  config.vm.box = "generic/rhel8"


  config.vm.define "v5" do |v5|
    v5.vm.hostname = "v5"
    v5.vm.network "private_network", ip: "192.168.33.40"
  
    v5.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.name = "v5"
      vb.memory = "2048"
      vb.cpus = "2"
    end

    # v5.vm.provision "file", source: "keys/.ssh/vagrant_rsa.pub", destination: "~/.ssh/authorized_keys"

    v5.vm.provision "shell" do |s|
      ssh_pvt_key = File.read("/developer/vagrant/.ssh/chave_ssh")
      s.inline = <<-SHELL
        echo "#{ssh_pvt_key}" > /home/vagrant/.ssh/id_rsa
      SHELL
    end
  end

  config.vm.define "v2" do |v2|
    v2.vm.hostname = "v2"
    v2.vm.network "private_network", ip: "192.168.33.50"
  
    v2.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.name = "v2"
      vb.memory = "2048"
      vb.cpus = "2"
    end

    v2.vm.provision "shell" do |s|
      ssh_pub_key = File.readlines("/developer/vagrant/.ssh/chave_ssh.pub").first.strip
      s.inline = <<-SHELL
        echo "#{ssh_pub_key}" >> /home/vagrant/.ssh/authorized_keys
        # echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
      SHELL
    end
  end

end