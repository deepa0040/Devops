### Task Detail:

An Ansible playbook needs completion on the jump host, where a team member left off. Below are the details:

The inventory file /home/thor/ansible/inventory requires adjustments. The playbook must run on App Server 3 in Stratos DC. Update the inventory accordingly.

Create a playbook /home/thor/ansible/playbook.yml. Include a task to create an empty file /tmp/file.txt on App Server 3.

**Solution**:

**Step1**: Correct inventory file:

Check correct server detail from Nautilus and update in inventory

```
<server_name> ansible_host=<server_ip> ansible_user=your_username ansible_ssh_pass=your_password
```

**Step2**: Create playbook

```
---
- name: Create an empty file on App Server 3
  hosts: Stratos_DC
  vars_files:
    - /home/thor/ansible/vault.yml
  tasks:
    - name: Create an empty file
      file:
        path: /tmp/file.txt
        state: touch

```

**Step** 3: Validate the Inventory and Playbook

To ensure everything is set up correctly, validate both the inventory file and the playbook:

Validate the Inventory File:

```
ansible-inventory -i /home/thor/ansible/inventory --list
```

Validate the Playbook:

```
ansible-playbook /home/thor/ansible/playbook.yml --syntax-check
```
