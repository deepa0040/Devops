# Task Details
One of the DevOps team members has created a zip archive on jump host in Stratos DC that needs to be extracted and copied over to all app servers in Stratos DC itself. Because this is a routine task, the Nautilus DevOps team has suggested automating it. We can use Ansible since we have been using it for other automation tasks. Below you can find more details about the task:

We have an inventory file under /home/thor/ansible directory on jump host, which should have all the app servers added already.

There is a zip archive /usr/src/data/datacenter.zip on jump host.

Create a playbook.yml under /home/thor/ansible/ directory on jump host itself to perform the below given tasks.

Unzip /usr/src/data/datacenter.zip archive in /opt/data/ location on all app servers.

Make sure the extracted data must has the respective sudo user as their user and group owner, i.e tony for app server 1, steve for app server 2, banner for app server 3.

The extracted data permissions must be 0777.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way, without passing any extra arguments.

# Solution

Step 1: Create a playbook

```
---
- name: Unzip /usr/src/sysops/datacenter.zip archive in /opt/sysops/ location on all app servers
  become: yes
  hosts: all
  tasks: 
  - name: Unzip /usr/src/sysops/datacenter.zip
    unarchive:
      src: /usr/src/sysops/datacenter.zip
      dest: /opt/sysops/
  - name: Update all file ownership inside folder
    command:
      cmd: chown -R "{{ item.owner}}":"{{ item.group}}" /opt/sysops
    loop:
    - { hostname: 'stapp01', owner: 'tony', group: 'tony'}
    - { hostname: 'stapp02', owner: 'steve', group: 'steve'}
    - { hostname: 'stapp03', owner: 'banner', group: 'banner'}
    when:
      inventory_hostname == item.hostname

  - name: Update permission inside folder
    command:
      cmd: chmod -R 0755 /opt/sysops
   
```
Note: We can also use shell and file module for same operation

Step 2: Run playbook using below command

```
ansible-playbook -i inventory playbook.yml
```

Reference:

https://docs.ansible.com/ansible/latest/collections/ansible/builtin/unarchive_module.html
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/command_module.html
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/shell_module.html
