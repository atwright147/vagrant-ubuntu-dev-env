Vagrant.require_version ">= 1.7"

# Check to determine whether we're on a windows or linux/os-x host,
# later on we use this to launch ansible in the supported way
# source: https://stackoverflow.com/questions/2108727/which-in-ruby-checking-if-program-exists-in-path-from-ruby
def which(cmd)
    exts = ENV['PATHEXT'] ? ENV['PATHEXT'].split(';') : ['']
    ENV['PATH'].split(File::PATH_SEPARATOR).each do |path|
        exts.each { |ext|
            exe = File.join(path, "#{cmd}#{ext}")
            return exe if File.executable? exe
        }
    end
    return nil
end

PROJECT_NAME = "ubuntu-dev-env"

Vagrant.configure("2") do |config|
    config.vm.provider "virtualbox" do |v|
        v.name = PROJECT_NAME
        v.memory = 2048
        v.cpus = 2
    end

    config.vbguest.auto_update = true
    config.vm.box = "bento/ubuntu-18.04"
    config.vm.network :private_network, ip: "192.168.55.11"
    config.ssh.forward_agent = true

    # If ansible is in your path it will provision from your HOST machine
    # If ansible is not found in the path it will be instaled in the VM and provisioned from there
    if which('ansible-playbook')
        config.vm.provision "shell", inline: "sudo apt-get -y update -qq && sudo apt-get -y install -qq python", run: "once"
        config.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible/playbook.yml"
            ansible.inventory_path = "ansible/inventories/hosts"
            ansible.limit = 'all'
            ansible.compatibility_mode = '2.0'
            # ansible.verbose = "vvv"
        end
    else
        config.vm.provision :shell, path: "ansible/windows.sh", args: [PROJECT_NAME]
    end

    # config.vm.synced_folder "./", "/vagrant"
    config.vm.synced_folder '.', '/vagrant', disabled: true
end
