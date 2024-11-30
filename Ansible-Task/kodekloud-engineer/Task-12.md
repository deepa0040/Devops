# Task Details
There are some files that need to be created on all app servers in Stratos DC. The Nautilus DevOps team want these files to be owned by user root only however, they also want that the app specific user to have a set of permissions on these files. All tasks must be done using Ansible only, so they need to create a playbook. Below you can find more information about the task.

Create a playbook named playbook.yml under /home/thor/ansible directory on jump host, an inventory file is already present under /home/thor/ansible directory on Jump Server itself.

Create an empty file blog.txt under /opt/sysops/ directory on app server 1. Set some acl properties for this file. Using acl provide read '(r)' permissions to group tony (i.e entity is tony and etype is group).

Create an empty file story.txt under /opt/sysops/ directory on app server 2. Set some acl properties for this file. Using acl provide read + write '(rw)' permissions to user steve (i.e entity is steve and etype is user).

Create an empty file media.txt under /opt/sysops/ on app server 3. Set some acl properties for this file. Using acl provide read + write '(rw)' permissions to group banner (i.e entity is banner and etype is group).

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way, without passing any extra arguments.

# Solution

```
---
- name:  Set some acl properties for created empty file in app server.
  become: yes
  hosts: all
  tasks:
  - name: Create empty file.
    file:
      path: "{{ item.file }}"
      state: touch
    loop:
    - { hostname: 'stapp01', file: '/opt/sysops/blog.txt' }
    - { hostname: 'stapp02', file: '/opt/sysops/story.txt' }
    - { hostname: 'stapp03', file: '/opt/sysops/media.txt' }
    when: inventory_hostname == item.hostname
  - name: Set some acl properties for created empty file 
    acl:
      path: "{{ item.file }}"
      etype: "{{ item.etype }}"
      entity: "{{ item.entity }}"
      permissions: "{{ item.permission }}"
      state: present
    loop:
    - { hostname: 'stapp01', file: '/opt/sysops/blog.txt', etype: 'group', entity: 'tony', permission: 'r' }
    - { hostname: 'stapp02', file: '/opt/sysops/story.txt', etype: 'user', entity: 'steve', permission: 'rw' }
    - { hostname: 'stapp03', file: '/opt/sysops/media.txt',etype: 'group', entity: 'banner', permission: 'rw' }
    when: inventory_hostname == item.hostname
```

Reference:

https://docs.ansible.com/ansible/latest/collections/ansible/posix/acl_module.html
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html
https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_loops.html
https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_conditionals.html
