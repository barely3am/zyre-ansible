#e -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
VAGRANTFILE_LOCAL = 'Vagrantfile.local'

$script = <<SCRIPT
echo 'installing the basics'
apt-get update && apt-get install -y build-essential python-dev python2.7 python-pip python-dev aptitude \
    python-pip libffi-dev libssl-dev software-properties-common

echo 'installing ansible...'
pip install 'cryptography>=1.5' 'ansible>=2.6,<2.7'

cd /vagrant
ansible-playbook -i "localhost," -c local test.yml -vv

# ansible-playbook -i 'localhost,' -c local test.yml -vv -e pyzyre_debug=1

SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.provision "shell", inline: $script

  config.vm.box = 'ubuntu/xenial64'

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--cpus", "2", "--ioapic", "on", "--memory", "512" ]
  end

  if File.file?(VAGRANTFILE_LOCAL)
    external = File.read VAGRANTFILE_LOCAL
    eval external
  end
end

