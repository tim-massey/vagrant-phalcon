VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.forward_port 80, 8081

  # TODO: fix this hack that ensures 'apt-get update' runs before mysql
  # is provisioned with puppet
  config.vm.provision :shell, :inline => "apt-get update --fix-missing"

  # provision our sdev server with the necessary packages and services
  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "provision/puppet/manifests"
    puppet.module_path = "provision/puppet/modules"
    puppet.manifest_file  = "base.pp"
    puppet.options = ['--verbose']
  end

  # installer/updater for cphalcon
  # installer for phalcon-devtools
  config.vm.provision :shell do |sh|
    sh.path = "provision/shell/install_phalcon.sh"
  end
end
