# Task details
The Nautilus DevOps team is practicing some of the Ansible modules and creating and testing different Ansible playbooks to accomplish tasks. Recently they started testing an Ansible file module to create soft links on all app servers. Below you can find more details about it.

Write a playbook.yml under /home/thor/ansible directory on jump host, an inventory file is already present under /home/thor/ansible directory on jump host itself. Using this playbook accomplish below given tasks:

Create an empty file /opt/dba/blog.txt on app server 1; its user owner and group owner should be tony. Create a symbolic link of source path /opt/dba to destination /var/www/html.

Create an empty file /opt/dba/story.txt on app server 2; its user owner and group owner should be steve. Create a symbolic link of source path /opt/dba to destination /var/www/html.

Create an empty file /opt/dba/media.txt on app server 3; its user owner and group owner should be banner. Create a symbolic link of source path /opt/dba to destination /var/www/html.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way without passing any extra arguments.

# Solution 

```
---
- name: Create soft links on all app servers
  become: yes
  hosts: all
  tasks:
  - name: Create an empty file on all app server.
    file:
      path: "{{ item.file }}"
      state: touch
      owner: "{{ item.owner }}"
      group: "{{ item.group }}"
    loop:
    - { file: '/opt/dba/blog.txt', owner: 'tony', group: 'tony', hostname: 'stapp01' }
    - { file: '/opt/dba/story.txt', owner: 'steve', group: 'steve', hostname: 'stapp02' }
    - { file: '/opt/dba/media.txt', owner: 'banner', group: 'banner', hostname: 'stapp03' }
    when: inventory_hostname == item.hostname
  - name: Create a symbolic link.
    file:
      src: /opt/dba
      dest: /var/www/html
      state: link
```

Reference:

https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html
https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_loops.html
https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_conditionals.html
