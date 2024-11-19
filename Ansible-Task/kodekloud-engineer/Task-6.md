# Task Detail

The Nautilus DevOps team is planning to test several Ansible playbooks on different app servers in Stratos DC. Before that, some pre-requisites must be met. Essentially, the team needs to set up a password-less SSH connection between Ansible controller and Ansible managed nodes. One of the tickets is assigned to you; please complete the task as per details mentioned below:

a. Jump host is our Ansible controller, and we are going to run Ansible playbooks through thor user from jump host.

b. There is an inventory file /home/thor/ansible/inventory on jump host. Using that inventory file test Ansible ping from jump host to App Server 1, make sure ping works.

# Solution:

**Step 1:** Create thor user in the existing inventory server and Enable no passwd authentication.

Create a User

```
sudo useradd thor
sudo passwd thor
```

**Configure Sudo Privileges:**

Ensure the thor user has the necessary sudo privileges on all managed nodes.

```
sudo visudo
```

Add the following line:

```
thor ALL=(ALL) NOPASSWD: ALL
```

**Step 2:** Generate SSH Key Pair on Controller:

```
ssh-keygen -t rsa -b 2048
```

Press Enter to accept the default file location and leave the passphrase empty.

**Step 3:** Copy SSH Key to Managed Nodes:

Use ssh-copy-id to copy the public key to each managed node.

```
ssh-copy-id ansible@<managed_node_ip>
```

Repeat this for all managed nodes.

**Step 4:** To ping all server in inventory, run below command

```
ansible -i inventory all -m ping
```
