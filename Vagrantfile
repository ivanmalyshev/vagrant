# -*- mode: ruby -*-
# vi: set ft=ruby :

# VM array
# Массив виртмашин
virt_machines=[
  {
    :hostname => "rmq1",
    :ip => "192.168.88.238"
  },
  {
    :hostname => "rmq2",
    :ip => "192.168.88.239"
  }
]

# Show VM GUI
# Показывать гуй виртмашины
HOST_SHOW_GUI = false 

# VM RAM
# Оперативная память ВМ
HOST_MEMMORY = "512" 

# VM vCPU
# Количество ядер ВМ
HOST_CPUS = 2

# Network adapter to bridge
# В какой сетевой адаптер делать бридж
#HOST_BRIDGE = "Intel(R) Ethernet Connection (2) I219-V" 
HOST_BRIDGE = "enp0s31f6"

# Which box to use
# Из какого бокса выкатываемся
HOST_VM_BOX = "generic/ubuntu2004" 

################################################
# Parameters passed to provision script
# Параметры передаваемые в скрипт инициализации
################################################

# Script to use while provisioning
# Скрипт который будет запущен в процессе настройки
HOST_CONFIIG_SCRIPT = "settings.sh" 

# Additional user
# Дополнительный пользователь
HOST_USER = 'mid'

# Additional user pass. Root pass will be same
# Пароль дополнительного пользователя. Пароль рута будет таким же
HOST_USER_PASS = 'midx11011' 

# Run apt dist-upgrade
# Выполнить apt dist-upgrade
HOST_UPGRADE = 'false' 



#VAGRANT_LOG=info vagrant up

Vagrant.configure("2") do |config|
	virt_machines.each do |machine|
		config.vm.box = HOST_VM_BOX
		config.vm.define machine[:hostname] do |node|
			node.vm.hostname = machine[:hostname]
			node.vm.network :public_network, bridge: HOST_BRIDGE, ip: machine[:ip]
			node.vm.provider "virtualbox" do |current_vm, override|
				current_vm.name = machine[:hostname]
				current_vm.gui = HOST_SHOW_GUI
				current_vm.memory = HOST_MEMMORY
				current_vm.cpus = HOST_CPUS
				override.vm.provision "shell", path: 'settings.sh', args: [	'mid', 	'midx11011',	'false', 	machine[:hostname], 	machine[:ip] ], run: "once"
			end
		end
	end
end
