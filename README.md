# Ansible

Here are the files used during the Ansible demo in TECDCN-2941 in order to create multiple objects in ACI. The objects that would be created are:
  a) Tenant VRF
  b) Tenant BD
  c) Tenant BD Subnet
  d) Tenant App Profile
  e) Tenant App Profile EPG
  
  
***************************************************************************************************************
*Here is the file for the group variables that are going to be used.                                          *
*You will find here the username/password for the APIC                                                        *
***************************************************************************************************************
/home/user/Playbooks/Ansible-ACI/group_vars/all
  
---

ansible_connection: local

user: admin
pass: cisco.123
  
  
***************************************************************************************************************
*Here is the file for the common device variables used.                                                       *
*You will find here several variables                                                                         *
***************************************************************************************************************

/home/user/Playbooks/Ansible-ACI/roles/aci/vars/main.yml
  
  ---
# vars file for aci
tenant_name: TECDCN-2941
vrf_name: TECDCN-2941-vrf
bd_name: TECDCN-2941-bd
gateway_ip: 10.1.1.1
subnet_mask: 24
app_profile_name: TECDCN-2941-ap
epg_name: TECDCN-2941-epg


***************************************************************************************************************
*Here is the file for the task that we would like to perform.                                                 *
*Keep in mind this is a small example. It is always recommended to check the documentation for the latest     *
*information                                                                                                  *
***************************************************************************************************************

/home/user/Playbooks/Ansible-ACI/roles/aci/tasks/main.yml
 
---
# tasks file for aci
- name: CREATE ACI TENANT VRF
  aci_vrf:
    action: post
    vrf: "{{ vrf_name }}"
    tenant: "{{ tenant_name }}"
    hostname: "{{ inventory_hostname }}"
    username: "{{ user }}"
    password: "{{ pass }}"
    use_ssl: no

- name: CREATE ACI TENANT BD
  aci_bd:
    action: post
    tenant: "{{ tenant_name }}"
    bd: "{{ bd_name }}"
    vrf: "{{ vrf_name }}"
    host: "{{ inventory_hostname }}"
    username: "{{ user }}"
    password: "{{ pass }}"
    use_ssl: no

- name: CREATE ACI TENANT BD SUBNET
  aci_bd_subnet:
    action: post
    bd: "{{ bd_name }}"
    gateway: "{{ gateway_ip }}"
    mask: "{{ subnet_mask }}"
    tenant: "{{ tenant_name }}"
    host: "{{ inventory_hostname }}"
    username: "{{ user }}"
    password: "{{ pass }}"
    use_ssl: no

- name: CREATE ACI TENANT APP PROFILE
  aci_ap:
    action: post
    ap: "{{ app_profile_name }}"
    tenant: "{{ tenant_name }}"
    hostname: "{{ inventory_hostname }}"
    username: "{{ user }}"
    password: "{{ pass }}"
    use_ssl: no

- name: CREATE ACI TENANT APP PROFILE EPG
  aci_epg:
    action: post
    epg: "{{ epg_name }}"
    ap: "{{ app_profile_name }}"
    tenant: "{{ tenant_name }}"
    bd: "{{ bd_name }}"
    hostname: "{{ inventory_hostname }}"
    username: "{{ user }}"
    password: "{{ pass }}"
    use_ssl: no
    
    
***************************************************************************************************************
*Here is the file for the inventory. The inventory refers to the device(s) that we will be performing the     *
*task(s)                                                                                                      *
***************************************************************************************************************

/home/user/Playbooks/Ansible-ACI/hosts
        
# hosts file for Ansible playbook

[apic]
10.0.243.20

***************************************************************************************************************
*Here is the file for the playbook that we will be leveraging                                                 *
***************************************************************************************************************

/home/user/Playbooks/Ansible-ACI/site.yml


# main playbook

- hosts: apic
  roles:
    - role: aci
    

***************************************************************************************************************
*Ansible Playbook Execution                                                                                   *
***************************************************************************************************************

/home/local/ECATSRTPDMZ/cobedien/Playbooks/Ansible-ACI/
ansible-playbook -i hosts site.yml
