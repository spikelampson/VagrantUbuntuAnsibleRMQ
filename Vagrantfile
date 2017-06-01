# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

	# Need to update the hosts files across the cluster...
	# config.hostmanager.include_offline = true

Vagrant.configure("2") do |config|
	config.hostmanager.enabled = true
	config.hostmanager.manage_guest = true
	config.hostmanager.include_offline = true
	N = 3
	(1..N).each do |rabbit_id|
		#config.vm.provision :hostmanager
		config.vm.define "rabbit#{rabbit_id}" do |rabbit|
			rabbit.vm.box = "bento/ubuntu-16.04" 
			rabbit.vm.hostname = "rabbit#{rabbit_id}"
			rabbit.vm.network "private_network", ip: "192.168.77.#{20+rabbit_id}"

			# Only execute once the Ansible provisioner,
			#	 # when all the machines are up and ready.
			if rabbit_id == N
				rabbit.vm.provision :ansible do |ansible|
				# Disable default limit to connect to all the machines
					ansible.limit = "all"
					ansible.playbook = "rmqPlaybook.yml"
				end
			end
		end
		# config.vm.provision :hostmanager
	end
end

