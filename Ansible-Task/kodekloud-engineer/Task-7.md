# Task Details
The Nautilus Application development team wanted to test some applications on app servers in Stratos Datacenter. They shared some pre-requisites with the DevOps team, and packages need to be installed on app servers. Since we are already using Ansible for automating such tasks, please perform this task using Ansible as per details mentioned below:

Create an inventory file /home/thor/playbook/inventory on jump host and add all app servers in it.

Create an Ansible playbook /home/thor/playbook/playbook.yml to install vim-enhanced package on all  app servers using Ansible yum module.

Make sure user thor should be able to run the playbook on jump host.

Note: Validation will try to run playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way, without passing any extra arguments

# Solution

**Step 1:** Create Inventory file

```
<server_name> ansible_host=<server_ip> ansible_user=your_username ansible_ssh_pass=your_password
<server_name> ansible_host=<server_ip> ansible_user=your_username ansible_ssh_pass=your_password
<server_name> ansible_host=<server_ip> ansible_user=your_username ansible_ssh_pass=your_password
```


**Step 2:** Create Playbook

```
---
- name: Install package using yum module
  become: yes
  hosts: all
  tasks: 
  - name: install package
    yum:
      name: vim-enhanced
      state: present
```
**Step 3:** Create Thor user by instuction mention in Task-6 

PATH=> Ansible-Task/kodekloud-engineer/Task-6.md
