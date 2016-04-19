Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/wily64"

  config.vm.network "forwarded_port", guest: 8080, host: 18080

  # config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.synced_folder "ansible", "/tmp/ansible/"

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y ansible
    sudo ansible-playbook -i "localhost," -c local -vvvv /tmp/ansible/jenkins-playbook.yml

    echo ""
    echo " *** Jenkins installed, server is listening at"
    echo " ***    http://localhost:18080"
    echo " ***"
    echo " *** AdminPassword is:"
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  SHELL
end
