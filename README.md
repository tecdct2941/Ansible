
# Ansible ACI

Using Ansible modules during TECDCN-2941

## Modules

In this particualar modules we are leveraging modules in order to create several objects in the ACI fabric. The particular objects that are being created are:

  *Tenant VRF
  *Tenant BD
  *Tenant BD Subnet
  *Tenant App Profile
  *Tenant App Profile EPG

Required

* Python 2.7+
* [setuptools package](https://pypi.python.org/pypi/setuptools)
