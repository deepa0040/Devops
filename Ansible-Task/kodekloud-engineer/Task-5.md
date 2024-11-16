# Task Details
The Nautilus DevOps team is testing various Ansible modules on servers in Stratos DC. They're currently focusing on file creation on remote hosts using Ansible. Here are the details:

a. Create an inventory file ~/playbook/inventory on jump host and include all app servers.

b. Create a playbook ~/playbook/playbook.yml to create a blank file /home/opt.txt on all app servers.

c. Set the permissions of the /home/opt.txt file to 0777.

d. Ensure the user/group owner of the /home/opt.txt file is tony on app server 1, steve on app server 2 and banner on app server 3.

# Solution

Step1: Create inventory that include all your application server detail

```
<server_name> ansible_host=<server_ip> ansible_user=your_username ansible_ssh_pass=your_password
<server_name> ansible_host=<server_ip> ansible_user=your_username ansible_ssh_pass=your_password
<server_name> ansible_host=<server_ip> ansible_user=your_username ansible_ssh_pass=your_password
```

Step2: Create playbook.
```
---
- name: Create Blank file in all application server
  hosts: all
  become: yes
  tasks: 
  - name: Create blank file
    file:
      path: /home/opt.txt
      state: touch
      mode: '0777'
      owner: "{{item.owner}}"
      group: "{{item.group}}"
    loop:
    - { hostname: 'stapp01', owner: 'tony', group: 'tony' }
    - { hostname: 'stapp02', owner: 'steve', group: 'steve' }
    - { hostname: 'stapp03', owner: 'banner', group: 'banner' }
    when: inventory_hostname == item.hostname
```
Step3: Verify the playbook and inventory using below command

```
ansible-inventory -i inventory --list
ansible-playbook -i inventory playbook.yml
```

Reference:

https://docs.ansible.com/ansible/2.8/modules/file_module.html#file-module
https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_loops.html
