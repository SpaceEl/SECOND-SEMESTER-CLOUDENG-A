# Automated LAMP Stack Deployment with Vagrant and Ansible

This project showcases an automation workflow for deploying a LAMP (Linux, Apache, MySQL, PHP) stack and a PHP application on two Ubuntu-based servers, "master" and "slave." The setup is achieved using Vagrant for virtual machine management and Ansible for configuration and orchestration.

## Overview

- Two virtual machines are created: "master" and "slave."
- On the "master" node, a bash script automates the deployment of the LAMP stack and a PHP application.
- The "slave" node is configured using an Ansible playbook to execute the bash script and verify the accessibility of the PHP application through the VM's IP addresses.

## Prerequisites

Before starting, ensure you have the following prerequisites installed on your host machine:

- [Vagrant](https://www.vagrantup.com/): For managing virtual machines.
- [VirtualBox](https://www.virtualbox.org/): As the virtualization provider.
- [Ansible](https://www.ansible.com/): For configuration management.

## Project Structure

- **Vagrantfile**: Defines VM configurations for "master" and "slave."
- **webconfig.sh**: The bash script for deploying the LAMP stack and PHP application on the "master" node.
- **playbook.yaml**: Ansible playbook for configuring the "slave" node and executing the bash script.

## Step-by-Step Guide

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/lamp-stack-automation.git
cd lamp-stack-automation

2. Install Vagrant SCP Plugin
To facilitate file transfer with Vagrant, install the Vagrant SCP plugin:
vagrant plugin install vagrant-scp

3. Customize VM Configurations
Edit the Vagrantfile to customize the VM configurations, including IP addresses, memory, and names for "master" and "slave."

4. Initialize and Start VMs
Initialize and start the virtual machines:
vagrant up

5. Copy Master's Public Key to Slave
Copy the public key from the "master" VM to the "slave" VM for SSH key-based authentication:

echo "Copying Master's public key to Slave"
master_public_key=$(vagrant ssh master -c "sudo su - vagrant -c 'cat ~/.ssh/ansible_id_rsa.pub'")
vagrant ssh slave -c "echo '$master_public_key' | sudo su - vagrant -c 'tee -a ~/.ssh/authorized_keys'"

6. Deploy LAMP Stack on Master
Copy and execute the script for deploying the LAMP stack and the PHP application on the "master" VM:
vagrant scp ./webconfig.sh master:~/webconfig.sh
vagrant ssh master -c "chmod +x ~/webconfig.sh && ~/webconfig.sh"

7. Copy Ansible Setup Files to Master
Copy the Ansible setup files to the "master" VM:
echo "Copying Ansible directory to master"
vagrant ssh master -c "rm -rf ~/apache_laravel_setup"
vagrant scp ./apache_laravel_setup master:~/

8. Copy Script to Deploy on Slave
Copy the script for deploying the LAMP stack and PHP application to the "slave" VM:
vagrant scp ./webconfig.sh master:~/apache_laravel_setup/webconfig.sh

9. Run Ansible Playbook
Run the Ansible playbook from the Ansible directory on the "master" VM to configure the "slave" VM:
vagrant ssh master -c "cd ~/apache_laravel_setup && ansible-playbook ./playbook.yaml"

10. Access Your Laravel Application
Visit the following URLs to test the Laravel deployment:

Master VM: http://192.168.56.7/
Slave VM: http://192.168.56.8/

Troubleshooting
If you encounter any issues during the setup or have questions, please feel free to reach out for assistance.

Author
Your Name
Your Email
License
This project is open-source and available under the MIT License. You are free to use, modify, and distribute it as needed.

