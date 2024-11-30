# Task Detail:
The Nautilus DevOps team is testing Ansible playbooks on various servers within their stack. They've placed some playbooks under /home/thor/playbook/ directory on the jump host and now intend to test them on app server 1 in Stratos DC. However, an inventory file needs creation for Ansible to connect to the respective app. Here are the requirements:

a. Create an ini type Ansible inventory file /home/thor/playbook/inventory on jump host.

b. Include App Server 1 in this inventory along with necessary variables for proper functionality.

c. Ensure the inventory hostname corresponds to the server name as per the wiki, for example stapp01 for app server 1 in Stratos DC.

# Solution:
Check correct server detail from Nautilus and update in inventory

```
<server_name> ansible_host=<server_ip> ansible_user=your_username ansible_ssh_pass=your_password
```

Next, Validate the Inventory and Playbook

To ensure everything is set up correctly, validate both the inventory file and the playbook:

Validate the Inventory File:

```
ansible-inventory -i /home/thor/ansible/inventory --list
```

Validate the Playbook:

```
ansible-playbook /home/thor/ansible/playbook.yml --syntax-check
```
