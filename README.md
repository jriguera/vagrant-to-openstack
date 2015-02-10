# vagrant-to-openstack
How to spin up vms on openstack using vagrant

About
=====

Example Vagrantfile using openstack provider an provisioning using ansible.
More info about how to use it: https://github.com/ggiamarchi/vagrant-openstack-provider

Install
=======

To use it, you have to install the vagrant, ansible and the openstack-vagrant plugin by doing:
`# vagrant plugin install vagrant-openstack-provider`


If you do not have more providers, just type `vagrant up`, otherwise you have to specify 
`# vagrant up --provider=openstack`

You also have to download OpenStack API RC file for your project with your credentials, go to 
`Project -> Compute -> Access & Security -> API Access` and Download RC file by hitting `Download OpenStack RC File`.
Put `$PROJECT-openrc.sh` in the folder and type `chmod a+x $PROJECT-openrc.sh`. When you type `vagrant up` it will ask you for your OpenStack password.
