# Automated LAMP Stack Deployment and PHP Application Verification

In this project, we automated the deployment of a LAMP (Linux, Apache, MySQL, PHP) stack on a "master" node using a Bash script. Additionally, we used Ansible to execute the Bash script on a "slave" node and verified that a PHP application is accessible through the VM's IP addresses.

## Prerequisites

Before you begin, ensure that you have the following prerequisites in place:

- **Vagrant**: Installed on your system to manage and provision virtual machines.
- **VirtualBox**: As the virtualization platform for running virtual machines.
- **GitHub**: If your PHP application is hosted on a GitHub repository.

## Setup Overview

Our project comprises two key components:

1. **Bash Script for LAMP Stack Deployment (On Master Node)**
   - The Bash script automates the deployment of a LAMP stack on the "master" node.
   - It clones a PHP application from a GitHub repository.
   - The script installs the necessary packages and configures the Apache web server and MySQL.

2. **Ansible Playbook (On Slave Node)**
   - An Ansible playbook is used to execute the Bash script on the "slave" node.
   - It verifies that the PHP application is accessible through the VM's IP addresses.

## Detailed Steps

### 1. LAMP Stack Deployment (On Master Node)

- Create a Bash script (`webconfig.sh`) that contains the necessary commands for LAMP stack deployment.

- Customize the script as needed, including package installation and configuration steps.

- Ensure the script is reusable and readable. You can provide comments and organize it logically.

### 2. Virtual Machine Setup

- Define the VM configurations in a Vagrantfile, including memory, box name, and IP addresses.

- Initialize and start the virtual machines using the Vagrant `vagrant up` command.

- Verify that all VMs are running by checking their status.

<img width="1375" alt="IMAGE 1" src="https://github.com/SpaceEl/SECOND-SEMESTER-CLOUDENG-ALTSCHOOL-EXAM/assets/105453871/a41af4e1-97de-45ed-a7ab-07afe9f1650e">


- Copy the Master's public key to the Slave VM to enable SSH key-based authentication.

### 3. Execute the Bash Script on the Master Node

- Copy the `webconfig.sh` script to the Master VM using Vagrant SCP.

- Make the script executable on the Master VM.

- Execute the script using the `vagrant ssh` command.

### 4. Ansible Setup (On Slave Node)

- Create an Ansible playbook (`playbook.yaml`) that defines tasks for executing the Bash script on the Slave Node.

- Ensure that the Ansible playbook specifies the correct host and SSH key settings.

- Copy the Ansible setup files to the Master VM, including the playbook and any necessary configurations.

- Copy the Bash script for deploying Apache, PHP, and Laravel to the Slave VM.

- Run the Ansible playbook from the Ansible directory on the Master VM.

### 5. Verification

- Once the deployment is complete, verify that the PHP application is accessible through the VM's IP addresses.

- You can access the application via a web browser using the IP addresses of the Master and Slave VMs.

<img width="1785" alt="IMAGE 2" src="https://github.com/SpaceEl/SECOND-SEMESTER-CLOUDENG-ALTSCHOOL-EXAM/assets/105453871/5045299b-fa4d-4e2b-b205-b7e123d28296">

## Troubleshooting

If you encounter any issues during the setup or need assistance, please refer to the troubleshooting section in the shell script or seek help from the community.

## Conclusion

By following these steps, you have successfully automated the deployment of a LAMP stack and verified the accessibility of a PHP application using Vagrant, Ansible, and Bash scripting. This automation simplifies the setup process and ensures consistency across your VMs.

For more advanced usage, consider extending this automation to handle additional configurations, deploy other applications, and perform routine maintenance tasks.

**Happy automating!**

## Author

- Elohor Godwin
- elohorgodwin4298@gmail.com

## License

This project is open-source and available under the [MIT License](LICENSE). You are free to use, modify, and distribute it as needed.
