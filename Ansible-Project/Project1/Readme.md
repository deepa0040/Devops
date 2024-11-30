# Monitoring tool setup in Manage Node Server

Step 1: Launch 2 server

![image](https://github.com/user-attachments/assets/620dfd55-92ed-4ae2-8bbb-5b97aeba1afc)

Step 2: Use below command to set the hostname to differentiate server

```
sudo hostnamectl set-hostname new-hostname
sudo nano /etc/hosts                            # add or update line 127.0.1.1    new-hostname
sudo reboot
```
![image](https://github.com/user-attachments/assets/4c549f56-6471-4a36-b041-5409b7e3f2a7)

Exit and Relogin your server.

![image](https://github.com/user-attachments/assets/366f84b5-2c81-42f5-8c2e-c4eadb65eb02)

Step 3: Enable the password authentication in Monitoring node.

```
Run in manage node below command
- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf` or `/etc/ssh/sshd_config`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`
```

![image](https://github.com/user-attachments/assets/c071316d-4a43-450e-bd96-351886872208)

Step:4 Installation in Central node server (i.e Main server where Ansible is installed)

Install python and Ansible and connect to MonitoringNode server.

```
#!/bin/bash

sudo apt update
sudo apt install python3
python3 --version
sudo apt install python3-pip
pip3 --version
pip install ansible
sudo apt install ansible-core
echo "connect to manage node from central node"
ssh-keygen
chmod 600 ansible.pem
ssh-copy-id -f "-o IdentityFile ansible.pem" ubuntu@35.87.132.179
echo "login using"
ssh -o ' IdentityFile ansible.pem' 'ubuntu@35.87.132.179'
#or
#ssh ubuntu@35.87.132.179
```

![image](https://github.com/user-attachments/assets/ab173356-7b63-4624-981b-ff454ed2b85d)

![image](https://github.com/user-attachments/assets/6bb57e4e-ded7-41bb-b1ec-6d167f343a74)

Step 5: Upload the code given in This Repo to Ansible Server and Run the Playbook with below command

```
ansible-playbook -i inventory playbook.yml
```

![image](https://github.com/user-attachments/assets/4579ebf7-a9ea-4676-bca0-9936757c8da8)

![image](https://github.com/user-attachments/assets/609616c9-3808-401c-bbe8-8bdcedca6d4a)
![image](https://github.com/user-attachments/assets/ab6c9a7c-5f33-41f1-81bd-d6d912a998d5)

Grafana

![image](https://github.com/user-attachments/assets/a7f5333a-b2bf-4f0e-86d5-19dd6a36ec87)

Alertmanager

![image](https://github.com/user-attachments/assets/6350711f-9db7-48cb-99d8-49cfba05616b)

Prometheous

![image](https://github.com/user-attachments/assets/2b9389e6-7a32-48a4-ab1d-09086398d8b4)

Node Exported
![image](https://github.com/user-attachments/assets/f3a5e8eb-5828-4233-bbdd-5c26f3987348)


