# Task Details
There is some data on all app servers in Stratos DC. The Nautilus development team shared some requirement with the DevOps team to alter some of the data as per recent changes they made. The DevOps team is working to prepare an Ansible playbook to accomplish the same. Below you can find more details about the task.

Write a playbook.yml under /home/thor/ansible on jump host, an inventory is already present under /home/thor/ansible directory on Jump host itself. Perform below given tasks using this playbook:

We have a file /opt/security/blog.txt on app server 1. Using Ansible replace module replace string xFusionCorp to Nautilus in that file.

We have a file /opt/security/story.txt on app server 2. Using Ansiblereplace module replace the string Nautilus to KodeKloud in that file.

We have a file /opt/security/media.txt on app server 3. Using Ansible replace module replace string KodeKloud to xFusionCorp Industries in that file.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.

# Solution

```
---
- name: Using Ansible replace module, replace string in file
  become: yes
  hosts: all
  tasks:
    - name: Replace string in mentioned file
      replace:
        path: "{{ item.file }}"
        regexp: "{{ item.exp }}"
        replace: "{{ item.replace }}"
      loop:
        - { hostname: 'stapp01', file: '/opt/devops/blog.txt', exp: 'xFusionCorp', replace: 'Nautilus' }
        - { hostname: 'stapp02', file: '/opt/devops/story.txt', exp: 'Nautilus', replace: 'KodeKloud' }
        - { hostname: 'stapp03', file: '/opt/devops/media.txt', exp: 'KodeKloud', replace: 'xFusionCorp Industries' }
      when: inventory_hostname == item.hostname
```

Reference:

https://docs.ansible.com/ansible/latest/collections/ansible/builtin/lineinfile_module.html
