
# Ansible ACI

Using Ansible modules during TECDCN-2941

## Modules

In this particualar modules we are leveraging modules in order to create several objects in the ACI fabric. The particular objects that are being created during this demo are:

* Tenant VRF
* Tenant BD
* Tenant BD Subnet
* Tenant App Profile
* Tenant App Profile EPG

## Installation

In the machine you are going to be performing the Ansble playbook do the following steps:

  sudo pip install ansible==2.4.0

* Python 2.7+
* [setuptools package](https://pypi.python.org/pypi/setuptools)
