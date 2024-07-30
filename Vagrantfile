IMAGE_NAME = "generic/rhel9"    # Base image of VM which is vagrant box of RHEL 9 as default.
BOX_VERSION = "4.3.2"           # Base image version of above image as, 4.2.16
VM = "rhel9"                    # Name of VM
CPU_VM = 4                      # Specify the CPU of VM (Example: 1, 2)
MEMORY_VM = 4096                # Specify the RAM of VM in MB (Example: 2048, 4096)
HDD = '20GB'                    # HDD of Each VM (Examples: "15GB", "20GB", "30GB")

IP_VM = '192.168.56.56'         # Private IP of VM

Vagrant.configure("2") do |config|
  config.vagrant.plugins = ['vagrant-disksize', 'vagrant-hostmanager']
  config.ssh.insert_key = false
  config.vm.box_check_update = false
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true  # false to disable update '/etc/hosts' of host with guest VMs dns.
  config.hostmanager.manage_guest = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true
  config.vm.hostname = VM                   # Set the hostname
  config.disksize.size = HDD                # Configure the disk size

  # Configure the synced folder
  config.vm.synced_folder ".", "/vagrant", disabled: false
  config.vm.define VM
  # Configure the provider
  config.vm.provider "virtualbox" do |vmm|
    vmm.name = VM                           # Virtualbox GUI VM Name
    vmm.memory = MEMORY_VM
    vmm.cpus = CPU_VM
    vmm.gui = false
    vmm.linked_clone = false
  end

  # Configure the VM box and version
  config.vm.box = IMAGE_NAME
  config.vm.box_version = BOX_VERSION

  # Configure the network
  config.vm.network "private_network", ip: IP_VM

  # Provision the VM
  config.vm.provision "shell", inline: <<-SHELL
    sh /vagrant/ShellScripts/update_ssh_config.sh   # Enable Password based login (username: vagrant,password: vagrant)
    #sh /vagrant/ShellScripts/register_system_redhat.sh
    #sh /vagrant/ShellScripts/download-packages.sh
    #sh /vagrant/ShellScripts/unregister_system_redhat.sh
  SHELL
end
