require 'pathname'

HN = Pathname.new(Dir.pwd).basename.to_s.gsub('_','-');

VAGRANTFILE_API_VERSION = "2"
VM_COUNT = 2

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  (1..VM_COUNT).each do |i|
    config.vm.define "vm#{i}" do |subconfig|
      subconfig.vm.box = ENV['VAGRANT_CONFIG_VM_BOX'] || 'parallels/debian-8.7'
      subconfig.vm.hostname = HN + i.to_s
      subconfig.vm.provider "parallels" do |prl|
        prl.memory = 2048
        prl.cpus = 2
      end

      subconfig.vm.provision :ansible do |ansible|
        ansible.extra_vars = "host_vars/vm#{i}/keepalived.yml"
        ansible.groups = {
          "vm1" => "[vm#{i}]"
        }
        ansible.playbook = "test.yml"
        ansible.sudo = true
      end
    end
  end
end
