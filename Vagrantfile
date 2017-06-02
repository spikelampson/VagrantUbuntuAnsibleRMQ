# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
	# Requires vagrant-hostmanager plugin. This updates the /etc/hosts files on the created boxes.
	config.hostmanager.enabled = true
	config.hostmanager.manage_guest = true
	config.hostmanager.include_offline = true
	# Number of boxes to create
	N = 4
	(1..N).each do |rabbit_id|
		config.vm.define "rabbit#{rabbit_id}" do |rabbit|
			rabbit.vm.box = "bento/ubuntu-16.04" 
			rabbit.vm.hostname = "rabbit#{rabbit_id}"
			rabbit.vm.network "private_network", ip: "192.168.77.#{20+rabbit_id}"

			# Only execute once the Ansible provisioner,
			# when all the machines are up and ready.
			if rabbit_id == N
				rabbit.vm.provision :ansible do |ansible|
					# Disable default limit to connect to all the machines
					ansible.limit = "all"
					ansible.playbook = "rmqPlaybook.yml"
				end
			end
		end
	end
end

