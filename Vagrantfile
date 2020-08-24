Vagrant.configure('2') do |config|
    dev_dir = ENV['DEV_DIR']
    box = ENV['BOX'] || 'bento/ubuntu-20.04'
    cpus = ENV['CPUS'] || '4'
    mem = ENV['MEMORY'] || '4096'
    skip_gui = ENV['SKIP_GUI']
    skip_gui = ['true', 'yes', 'y', '1'].include? skip_gui

    config.vm.box = box
    config.vm.provider "vmware_desktop" do |v|
        v.vmx['memsize'] = mem
        v.vmx['numvcpus'] = cpus
        v.gui = !skip_gui
    end

    config.ssh.forward_agent = true
    config.vm.synced_folder dev_dir '/workspace' if dev_dir

    config.vm.provision 'ansible' do |ansible|
        ansible.playbook = './workstation.yml'
    end
end