# -*- mode: ruby -*-
# vi: ft=ruby :

# file     : Vagrantfile
# purpose  : build vagrant rhcsa-rhce-lab-environment
#
# author   : harald van der laan
# date     : 2017/03/16
# version  : v1.0.1
#
# changelog:
# - v1.0.1    fixed non working System eth1
# - v1.0.0    initial version

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

	# disable vagrant-vbguest auto update
	if defined? VagrantVbguest
		config.vbguest.auto_update = false
	end

	# setting lanhuage locale environment variable
	ENV["LC_ALL"] = "en_US.UTF-8"
	ENV["LANG"] = "en_US.UTF-8"

	# configure labipa server
	config.vm.define "labipa" do |node|
		node.vm.box = "centos/7"
		node.vm.hostname = "labipa.example.com"
		node.vm.network "private_network", ip: "172.16.20.2", auto_config: false

		# provider settings for labipa
		node.vm.provider "virtualbox" do |vbox|
			vbox.customize [
				"modifyvm", :id,
				"--memory", 1024,
				"--cpus", 1,
				"--name", "labipa",
			]
		end

		# provisioning for labipa
		node.vm.provision "ansible" do |ansible|
			ansible.playbook = "provision/labipa.yml"
            ansible.host_vars = { "labipa" => { "private_ipv4_address" => "172.16.20.2", "private_ipv6_address" => "fd00:cafe::2" }}
		end
	end

	# condigure system1 and system2 srvers
	(1..2).each do |i|
		config.vm.define "system#{i}" do |node|
			node.vm.box = "centos/7"
			node.vm.hostname = "system#{i}.example.com"
			node.vm.network "private_network", ip: "172.16.20.#{i}0", auto_config: false
			node.vm.network "private_network", ip: "172.16.20.1#{i}0", auto_config: false
			node.vm.network "private_network", ip: "172.16.20.2#{i}0", auto_config: false

			# provider settings for system1 and system2
			node.vm.provider "virtualbox" do |vbox|
				vbox.customize [
					"modifyvm", :id,
					"--memory", 512,
					"--cpus", 1,
					"--name", "system#{i}"
				]

				line = `VBoxManage list systemproperties | grep "Default machine folder"`
				vb_machine_folder = line.split(':')[1].strip()
				disk_name = "disk2.vmdk"
				disk = File.join(vb_machine_folder, "system#{i}", disk_name)

				unless File.exist?(disk)
					vbox.customize [
						"createhd",
						"--filename", disk,
						"--variant", "Fixed",
						"--format", "vmdk",
						"--size", 1 * 1024,
					]
					vbox.customize [
						"storagectl", :id,
						"--name", "SATA Controller",
						"--add", "sata",
					]
				end

				vbox.customize [
					"storageattach", :id,
					"--storagectl", "SATA Controller",
					"--port", 2,
					"--device", 0,
					"--type", "hdd",
					"--medium", disk,
				]
			end

			# provision for system1 and system2
			node.vm.provision "ansible" do |ansible|
				ansible.playbook = "provision/system.yml"
				ansible.host_vars = { "system#{i}" => { "private_ipv4_address" => "172.16.20.#{i}0", "private_ipv6_address" => "fd00:cafe::#{i}0" }}
			end
		end
	end
end
