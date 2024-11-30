# Task details
The Nautilus DevOps team wants to install and set up a simple httpd web server on all app servers in Stratos DC. Additionally, they want to deploy a sample web page for now using Ansible only. Therefore, write the required playbook to complete this task. Find more details about the task below.

We already have an inventory file under /home/thor/ansible directory on jump host. Create a playbook.yml under /home/thor/ansible directory on jump host itself.

Using the playbook, install httpd web server on all app servers. Additionally, make sure its service should up and running.

Using blockinfile Ansible module add some content in /var/www/html/index.html file. Below is the content:

Welcome to XfusionCorp!

This is  Nautilus sample file, created using Ansible!

Please do not modify this file manually!

The /var/www/html/index.html file's user and group owner should be apache on all app servers.

The /var/www/html/index.html file's permissions should be 0744 on all app servers.

Note:

i. Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.

ii. Do not use any custom or empty marker for blockinfile module.

# Solution

**Step-1** : Create a playbook.yml under /home/thor/ansible directory on jump host itself.

Requirement 1: Install httpd web server on all app servers. Additionally, make sure its service should up and running.

First check OS of app server using below command:

```
cat /etc/os-release
```
In my case It's Centos, so I'm using Yum package for httpd installation.
```
---	
- name: install httpd web server on all app servers
  become: yes
  hosts: all
  tasks: 
  - name: Install httpd web server
    yum:
      name: httpd
      state: present
      update_cache: yes
  - name: Start and enable the service
    service:
      name: httpd
      state: started
      enabled: yes
```

Check below command in app server to confirm if httpd service is installed and running.

```
systemctl status httpd
```

Requiremen-2: Using blockinfile Ansible module add some content in /var/www/html/index.html file.

```
---
- name: install httpd web server on all app servers
  become: yes
  hosts: all
  tasks:
  - name: Install httpd web server
    yum:
      name: httpd
      state: present
      update_cache: yes
  - name: Start and enable the service
    service:
      name: httpd
      state: started
      enabled: yes
  - name: Check if file Exist.
    stat:
      path: /var/www/html/index.html
    register: file_result
  - name: Create file if it does not exist
    file:
      path: /var/www/html/index.html
      state: touch
    when: not file_result.stat.exists
  - name: Add content in /var/www/html/index.html
    blockinfile:
      path: /var/www/html/index.html
      block: |
        Welcome to XfusionCorp!
        This is  Nautilus sample file, created using Ansible!
        Please do not modify this file manually!
```

Requirement-3: Update file Owner, group and permission  

```
---
- name: install httpd web server on all app servers
  become: yes
  hosts: all
  tasks:
  - name: Install httpd web server
    yum:
      name: httpd
      state: present
      update_cache: yes
  - name: Start and enable the service
    service:
      name: httpd
      state: started
      enabled: yes
  - name: Check if file Exist.
    stat:
      path: /var/www/html/index.html
    register: file_result
  - name: Create file if it does not exist
    file:
      path: /var/www/html/index.html
      state: touch
    when: not file_result.stat.exists
  - name: Add content in /var/www/html/index.html
    blockinfile:
      path: /var/www/html/index.html
      block: |
        Welcome to XfusionCorp!
        This is  Nautilus sample file, created using Ansible!
        Please do not modify this file manually!
  - name: Update file owner and group
    command:
      cmd: chown apache:apache /var/www/html/index.html
  - name: Update file permission
    command:
      cmd: chmod 0744 /var/www/html/index.html 
```

Reference:

https://docs.ansible.com/ansible/latest/collections/ansible/builtin/blockinfile_module.html
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/stat_module.html
https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_conditionals.html
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/debug_module.html
