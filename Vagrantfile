# vi: set ft=ruby

VAGRANTFILE_API_VERSION = "2"

require 'yaml'

if File.file?('vagrantvms.yml')
  vagrantvmsfile = YAML.load_file('vagrantvms.yml')
else
  raise "Configuration file 'vagrantvms.yml' does not exist."
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false

  vagrantvmsfile.each do |vagrantvms|
    config.vm.define vagrantvms["name"] do |srv|
      srv.vm.hostname = vagrantvms["name"]
      srv.vm.box = vagrantvms["box"]

      srv.vm.provider :virtualbox do |vb|
        vb.name = vagrantvms["name"]
        vb.memory = vagrantvms["mem"]
        vb.cpus = vagrantvms["cpus"]
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--ioapic", "on"]
      end
    end
  end
end
