baseBox = "bento/ubuntu-22.04"
Vagrant.configure("2") do |config|
  config.vm.synced_folder "ansible", "/home/vagrant/ansible"
  config.vm.synced_folder "ssh", "/home/vagrant/.ssh"
  config.ssh.insert_key = false
  config.ssh.private_key_path = "ssh/id_rsa"
  config.vm.define "test_ansible", primary: true do |subconfig|
    subconfig.vm.box = baseBox
    subconfig.vm.network "private_network", ip: "192.168.58.100"
    subconfig.vm.provision "shell", priviledged: false, inline: <<-SHELL
      # pip install ansible
      sudo apt-get update
      sudo apt-get install -y python3-pip python3-virtualenv
      source /home/vagrant/ansible/venv/bin/activate
      pip3 install ansible

      # run ansible playbook
      # ansible-playbook /home/vagrant/ansible/playbook.yml
    SHELL
  end
  config.vm.define "test_server" do |subconfig|
    subconfig.vm.box = baseBox
    subconfig.vm.network "private_network", ip: "192.168.58.101"
  end
  config.vm.define "test_client" do |subconfig|
    subconfig.vm.box = baseBox
    subconfig.vm.network "private_network", ip: "192.168.58.102"
  end
end