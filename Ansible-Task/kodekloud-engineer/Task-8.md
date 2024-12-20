# Task detail
The Nautilus DevOps team has some data on each app server in Stratos DC that they want to copy to a different location. However, they want to create an archive of the data first, then they want to copy the same to a different location on the respective app server. Additionally, there are some specific requirements for each server. Perform the task using Ansible playbook as per requirements mentioned below:

Create a playbook named playbook.yml under /home/thor/ansible directory on jump host, an inventory file is already placed under /home/thor/ansible/ directory on Jump Server itself.

Create an archive ecommerce.tar.gz (make sure archive format is tar.gz) of /usr/src/itadmin/ directory ( present on each app server ) and copy it to /opt/itadmin/ directory on all app servers. The user and group owner of archive ecommerce.tar.gz should be tony for App Server 1, steve for App Server 2 and banner for App Server 3.

Note: Validation will try to run playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way, without passing any extra arguments.

# Solution

**Step 1:** Create a playbook

```
---
- name: Archive directory /usr/src/sysops/
  become: yes
  hosts: all
  tasks: 
  - name: Archive directory /usr/src/sysops/
    archive:
      path: /usr/src/sysops/
      dest: /opt/sysops/beta.tar.gz
      format: gz

  - name: Update archive ownership
    file:
     path: /opt/sysops/beta.tar.gz
     owner: "{{ item.owner }}"
     group: "{{ item.group }}"
    loop:
    - { hostname: 'stapp01', owner: 'tony', group: 'tony'}
    - { hostname: 'stapp02', owner: 'steve', group: 'steve'}
    - { hostname: 'stapp03', owner: 'banner', group: 'banner'}
    when:
      inventory_hostname == item.hostname
```

Step 2: Run playbook using below command

```
ansible-playbook -i inventory playbook.yml
```

Reference:

https://docs.ansible.com/ansible/latest/collections/community/general/archive_module.html
https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_loops.html
