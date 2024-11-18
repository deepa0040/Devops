# Task
Task-1

Ansible utilizes SSH connections to communicate with remote hosts. The Nautilus DevOps team intends to employ a unified Ansible manager for overseeing several remote hosts. To streamline operations, they seek to use a common remote user to connect with all remote hosts.

Update the Ansible configuration file located at /home/thor/ansible-t5q5/ansible-t5q5.cfg on the jump host to set a default remote user as deploy. Please refrain from creating a new configuration file.

Note: This is a sample Ansible configuration. If you intend to test an Ansible playbook using this configuration, you may need to explicitly set the ANSIBLE_CONFIG variable.

Task-2:

The Nautilus DevOps team will be managing multiple hosts using Ansible. Each host possesses unique properties such as hostnames, login credentials, etc. Therefore, a custom inventory file is necessary to manage these hosts efficiently. The team has delineated the following requirements to address this situation.

Ensure that the default inventory path is appropriately modified to point to /home/thor/ansible-t5q6/inventory-t5q6 in the Ansible configuration file located at /home/thor/ansible-t5q6/ansible-t5q6.cfg. Please refrain from creating a new configuration file.

Note: This is a sample Ansible configuration. If you intend to test an Ansible playbook using this configuration, you may need to explicitly set the ANSIBLE_CONFIG variable.

Task-3:

a.. On jump host create a playbook /home/thor/ansible/playbook-t2q3.yml to copy /usr/src/finance-t2q3/linux-t2q3.txt file on same host at location /opt/finance-t2q3.

Note: Validation will try to run the playbook using command ansible-playbook -i localhost playbook-t2q3.yml so please make sure the playbook works this way without passing any extra arguments.

Task-4:
a. On jump host we already have an inventory file /home/thor/ansible/inventory-t2q2.

b. On jump host create a playbook /home/thor/ansible/playbook-t2q2.yml to copy /usr/src/finance-t2q2/system-t2q2.txt file to all application servers at location /opt/finance-t2q2 with permissions 0600.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory-t2q2 playbook-t2q2.yml so please make sure the playbook works this way without passing any extra arguments.

Task-5

The Nautilus DevOps team is working to create some data on different app servers in using Ansible. They want to create some files/directories and have some specific requirements related to this task. Find below more details about the same:

Create a playbook called playbook-t4q6.yml under /home/thor/playbook/ directory and configure it to create a file called /opt/file-t4q6.txt on all App Servers. The contents of the file must be This file is created by Ansible!. Inventory is already placed under /home/thor/playbook/inventory-t4q6.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory-t4q6 playbook-t4q6.yml, so please make sure the playbook works this way without passing any extra arguments.

Task-6

The Nautilus DevOps team is was doing some cleanup work on all app servers in Stratos DC. Instead of doing this manually they want to utilise Ansible for the same. Below are the requirements team has received.

a. Utilise the inventory file /home/thor/playbook/inventory-t4q4, present on the jump host.

b. Create a playbook name /home/thor/playbook/playbook-t4q4.yml to delete a file named /opt/fruits-t4q4.txt from all App Servers.

Note: Validation will attempt to execute the playbook using the command ansible-playbook -i inventory-t4q4 playbook-t4q4.yml. Please ensure the playbook functions correctly with this command alone, without requiring any additional arguments.

Task-7

The Nautilus DevOps team aims to test their Ansible playbooks, stored in the /home/thor/playbook/ directory on the jump host, specifically on app server 1 in the Stratos DC. To facilitate this, the team requires the creation of an inventory file to enable Ansible's connection to the specified app server. Below are the outlined requirements:

a. Create an ini type Ansible inventory file /home/thor/playbook/inventory-t3q1 on jump host.

b. Add App Server 1 in this inventory.

c. The inventory hostname of the host should be the server name as per the wiki, for example stapp01 for app server 1.

d. The playbook should seamlessly execute using the command ansible-playbook -i inventory-t3q1 playbook-t3q1.yml --list-hosts

Task-8

The Nautilus Application development team wanted to test some applications on app servers in Stratos Datacenter. They shared some pre-requisites with the DevOps team, and packages need to be installed on app servers. Since they already created some playbooks, now they wanted to make some changes in inventories.


There is an inventory file /home/thor/playbooks/inventory-t3q3 on jump host. It has some aliases named web1, web2 and web3 for three hosts respectively. Update this inventory file to add an alias called db1 for server4.company.com host.

Task-9

We plan to utilize various Ansible modules moving forward. To enhance our familiarity, the team intends to practice commonly used modules by creating playbooks for specific tasks.

Create a playbook named /home/thor/ansible/playbook-t1q4.yml on the jump host. Configure the playbook to generate a file named /tmp/file.txt on the jump host itself. Utilize the copy module and ensure the file contains the content: Welcome to the KKE Tests!

Task-10

A playbook on the jump host previously functioned correctly. However, a team member recently made modifications that resulted in misconfiguration. Subsequently, when we attempted to execute it, an error occurred. We require someone to review the playbook, identify the issue, and rectify it.


The playbook name is /home/thor/ansible/playbook-t1q6.yml, make sure it executes without any error.
