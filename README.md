
# Ansible ACI

Example on how to levarege Ansible modules that were used during TECDCN-2941

## Modules

In this particualar modules we are leveraging modules in order to create several objects in the ACI fabric. The particular objects that are being created during this demo are:

* Tenant 
* Tenant VRF
* Tenant BD
* Tenant BD Subnet
* Tenant App Profile
* Tenant App Profile EPG

## Installation

In the machine you are going to be performing the Ansble playbook do the following steps:

    sudo pip install ansible==2.4.0
    
Verify Ansible was installed correctly by checking the version of code

    anisble --version
 
 The output should look like 
 
     ansible 2.4.0.0
        config file = None
        configured module search path = [u'/home/local/ECATSRTPDMZ/cobedien/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
        ansible python module location = /usr/lib/python2.7/site-packages/ansible
        executable location = /usr/bin/ansible
        python version = 2.7.5 (default, May  3 2017, 07:55:04) [GCC 4.8.5 20150623 (Red Hat 4.8.5-14)]
 
  
If you have git installed, clone the repository

    git clone https://github.com/tecdct2941/Ansible.git
  
## Executing the playbook

Once you succesfully clone the file. The last step is to execute the plyabook by running the following command. Make sure you are in the right directory /Playbook/Anisble-ACI

    ansible-playbook -i hosts site.yml

