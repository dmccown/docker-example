VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/trusty64"
  config.ssh.insert_key = false

  config.vm.define 'host1' do |machine|
    machine.vm.hostname = 'host1'
    machine.vm.network 'private_network', ip: '10.11.0.101'
  end

  config.vm.define 'host2' do |machine|
    machine.vm.hostname = 'host2'
    machine.vm.network 'private_network', ip: '10.11.0.102'
  end

  config.vm.define 'host3' do |machine|
    machine.vm.hostname = 'host3'
    machine.vm.network 'private_network', ip: '10.11.0.100'

    machine.vm.provision :ansible do |ansible|
      ansible.playbook = "site.yml"
      ansible.groups = {
        "primary" => ["host1"],
        "secondary" => ["host2", "host3"],
      }

      # Disable default limit (required with Vagrant 1.5+)
      ansible.limit = 'all'
    end
  end

  config.vm.provider 'virtualbox' do |vb|
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ['modifyvm', :id, '--memory', '1024']
  end
end
