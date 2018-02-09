# encoding: utf-8
# vim: ft=ruby expandtab shiftwidth=2 tabstop=2

require 'yaml'

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.ssh.forward_agent = true

  _conf = YAML.load(
    File.open(
      File.join(File.dirname(__FILE__), 'ansible/default.yaml'),
      File::RDONLY
    ).read
  )

  if File.exists?(File.join(File.dirname(__FILE__), 'ansible/local.yaml'))
    _site = YAML.load(
      File.open(File.join(File.dirname(__FILE__), 'ansible/local.yaml'),File::RDONLY).read
    )
    _conf.merge!(_site) if _site.is_a?(Hash)
  end

  # forcing config variables
  _conf["vagrant_dir"] = "/vagrant"

  config.vm.define _conf['hostname'] do |v|
  config.vm.network :private_network, ip: _conf['ip']
  end

  config.vm.box_check_update = true

  config.vm.hostname = _conf['hostname']
  #config.vm.network :private_network, ip: _conf['ip']

  #  config.vm.synced_folder _conf['synced_folder'],
  #      _conf['document_root'], :create => "true", :mount_options => ['dmode=755', 'fmode=644']

  config.vm.provider :virtualbox do |vb|
    vb.name = _conf['hostname']
    vb.memory = 2048
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.extra_vars = {
      config: _conf
    }
    ansible.playbook = "ansible/main.yaml"
  end
end
