# Ansible Web-Server

This project demonstrates the configuration and deployment of a web server on two virtual machines (VM1 and VM2) using Ansible.

## Prerequisites
- Oracle VirtualBox installed
- Two Virtual Machines (VM1 and VM2) with Ubuntu installed
- Ansible installed on the local machine (WSL Ubuntu)
- SSH access configured between the local machine and VMs

## VM Configuration
1. **Create two VMs** (VM1 and VM2) in Oracle VirtualBox.
2. **Set Network Adapter**: In each VM, set `Adapter 1` to `Bridged Adapter` to allow Ansible to connect.
3. **Install Ubuntu**: Attach the Ubuntu ISO file and install the OS on both VMs.

## Install Ansible on Local Machine
Run the following commands in the local Ubuntu terminal (WSL):
```sh
sudo apt update
sudo apt install ansible -y
```

## Configure SSH Access to VMs
1. **Install OpenSSH** (if not already installed):
    ```sh
    sudo apt install openssh-server -y
    ```
2. **Generate SSH key**:
    ```sh
    ssh-keygen -t rsa -b 4096
    ```
3. **Copy the SSH key to each VM**:
    ```sh
    ssh-copy-id vboxuser@<vm_ip_address>
    ```

## Set Up Ansible Inventory File
1. **Install Nginx on VMs** (before using Ansible):
    ```sh
    sudo apt install nginx -y
    ```
2. **Create an inventory file** (`inventory.ini`):
    ```sh
    nano inventory.ini
    ```
    Add the following content:
    ```ini
    [webservers]
    vm1 ansible_host=<vm1_ip> ansible_user=vboxuser
    vm2 ansible_host=<vm2_ip> ansible_user=vboxuser
    ```

## Create and Run Ansible Playbook
1. **Create a playbook file to deploy** (`webserver_deploy.yml`):
    ```sh
    nano webserver_deploy.yml
    ```
    Add the required Ansible tasks.
2. **Run the playbook to deploy**:
    ```sh
    ansible-playbook -i inventory.ini webserver_deploy.yml
    ```
3. **Create a playbook file to undeploy** (`webserver_undeploy.yml`):
    ```sh
    nano webserver_undeploy.yml
    ```
    Add the required Ansible tasks.
4. **To undeploy the web server**, run:
    ```sh
    ansible-playbook -i inventory.ini webserver_undeploy.yml
    ```

## Verify the Deployment
Open a web browser and go to:
```
http://<vm1_ip>:8080
http://<vm2_ip>:8080
```
## Repository Structure
```
/ansible-webserver
├── inventory.ini              # Ansible inventory file
├── webserver_deploy.yml       # Ansible playbook to deploy
├── webserver_undeploy.yml     # Ansible playbook to undeploy
├── README.md                  # Documentation

```
--By Sanjushree Golla
