# Example Vagrantfile for openstack
# To use it, you have to install the plugin by:
# 'vagrant plugin install vagrant-openstack-provider'
# If you do not have more providers, just type 'vagrant up',
# otherwise you have to specify vagrant up --provider=openstack'

# Download OpenStack API RC file
# Go to Project -> Compute -> Access & Security -> API Access
# Down RC file by hitting Download OpenStack RC File
# Put $USER-openrc.sh in here and type chmod a+x $USER-openrc.sh

require 'vagrant-openstack-provider'

# Load openstack variables if they are not loaded
variables = %w{OS_AUTH_URL OS_USERNAME OS_PASSWORD OS_TENANT_NAME}
missing = variables.find_all { |v| ENV[v] == nil }
unless missing.empty?
   Dir.glob('*-openrc.sh').each do |f|
      puts("Loading #{f}")
      system("./#{f}")
   end
end


Vagrant.configure('2') do |config|
  
  # Openstack parameters
  config.vm.provider :openstack do |os|
    os.openstack_auth_url = "#{ENV['OS_AUTH_URL']}/tokens"
    os.username           = "#{ENV['OS_USERNAME']}"
    os.password           = "#{ENV['OS_PASSWORD']}"
    os.tenant_name        = "#{ENV['OS_TENANT_NAME']}"
    os.flavor             = 'm1.small'
    os.image              = 'Ubuntu 14.04'
    os.floating_ip_pool   = 'net04_ext'
    os.security_groups    = ['default']
    os.floating_ip        = 'auto' 
  end

  config.vm.define :ubuntu do |config|
      # Name
      config.vm.box = "ubuntu"

      # Default user for ubuntu
      config.ssh.username = 'ubuntu'

      # Make sure the private key from the key pair is provided 
      # config.ssh.private_key_path = "~/.ssh/id_rsa"

      config.ssh.pty = true
      config.vm.provision :ansible do |ansible|
         ansible.playbook = "playbook.yml"
      end

      # Enable provisioning with shell
      #config.vm.provision :shell do |shell|
      #  shell.inline = $debscript
      #  # shell.args   = "#{ENV['DEBEMAIL']}, #{ENV['DEBFULLNAME']}"
      #end
      # or
      #config.vm.provision :shell, path: "bootstrap.sh"
  end

end

