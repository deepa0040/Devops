# Task Detail
The Nautilus DevOps team needs to copy data from the jump host to all application servers in Stratos DC using Ansible. Execute the task with the following details:

a. Create an inventory file /home/thor/ansible/inventory on jump_host and add all application servers as managed nodes.

b. Create a playbook /home/thor/ansible/playbook.yml on the jump host to copy the /usr/src/security/index.html file to all application servers, placing it at /opt/security.

# Solution

Step1:
Create inventory that include all your application server detail

```
<server_name> ansible_host=<server_ip> ansible_user=your_username ansible_ssh_pass=your_password
<server_name> ansible_host=<server_ip> ansible_user=your_username ansible_ssh_pass=your_password
<server_name> ansible_host=<server_ip> ansible_user=your_username ansible_ssh_pass=your_password
```

Step2:
Create playbook.

```
---
- name: Copy file from remote to application sever
  hosts: all
  become: yes
  tasks:
  - name: Copy
    copy: 
      src: /usr/src/security/index.html
      dest: /opt/security
      
```

Note:

**hosts**: specifies the target machines on which tasks will be executed

**become**: allows you to ‘become’ another user, different from the user that logged into the machine (remote user).

Reference:

https://docs.ansible.com/ansible/2.8/user_guide/become.html#id1
https://docs.ansible.com/ansible/2.8/user_guide/intro_inventory.html#inventory-basics-hosts-and-groups
https://docs.ansible.com/ansible/2.8/modules/copy_module.html#copy-module
