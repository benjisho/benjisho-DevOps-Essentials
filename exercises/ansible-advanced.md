# Exercise 3: Infrastructure Provisioning and Configuration with Ansible and Terraform

In this exercise, you will learn how to provision and configure infrastructure using Ansible and Terraform. By the end of this exercise, you will have automated the provisioning of a virtual machine using Terraform and configured it using Ansible.

## Table of Contents

- [Step 1: Install Ansible and Terraform on your Ubuntu machine](#step-1-install-ansible-and-terraform-on-your-ubuntu-machine)
- [Step 2: Provision a virtual machine using Terraform](#step-2-provision-a-virtual-machine-using-terraform)
- [Step 3: Write an Ansible playbook for infrastructure configuration](#step-3-write-an-ansible-playbook-for-infrastructure-configuration)
- [Step 4: Execute the Ansible playbook](#step-4-execute-the-ansible-playbook)

## Step 1: Install Ansible and Terraform on your Ubuntu machine

1. Open a terminal.

2. Install Ansible:
   - Run the following commands to add the Ansible repository and install Ansible:
     ```bash
     sudo apt update
     sudo apt install software-properties-common
     sudo apt-add-repository --yes --update ppa:ansible/ansible
     sudo apt install ansible
     ```
   - Verify the installation by running `ansible --version`.

3. Install Terraform:
   - Run the following commands to install Terraform:
     ```bash
     sudo apt update
     sudo apt install wget unzip
     wget https://releases.hashicorp.com/terraform/1.0.8/terraform_1.0.8_linux_amd64.zip
     unzip terraform_1.0.8_linux_amd64.zip
     sudo mv terraform /usr/local/bin/
     ```
   - Verify the installation by running `terraform version`.

## Step 2: Provision a virtual machine using Terraform

1. Create a new directory for your Terraform project:
   ```bash
   mkdir terraform-project
   cd terraform-project
   ```
2. Create a Terraform configuration file named main.tf and open it in a text editor:
   ```
   touch main.tf
   nano main.tf
   ```
3. Add the following code to the main.tf file to define the Vultr provider and specify the desired infrastructure resources (e.g., virtual machine):
   ```
   provider "vultr" {
     api_key = "<your-vultr-api-key>"
   }

   resource "vultr_server" "example" {
     plan      = "vc2-1c-1gb"
     region    = "ams"
     hostname  = "my-vm"
     label     = "my-vm"
     os_id     = 387
   }
   ```
4. Save and close the main.tf file.
5. Initialize the Terraform working directory:
   ```
   terraform init
   ```

7. Preview the changes that Terraform will make:
   ```
   terraform plan
   ```
8. Apply the Terraform configuration to create the infrastructure resources:
   ```
   terraform apply
   ```
9. When prompted, type yes to confirm and proceed with the resource creation.

## Step 3: Write an Ansible playbook for infrastructure configuration
1. Create a new directory for your Ansible project:
   ```
   mkdir ansible-project
   cd ansible-project
   ```
2. Create an Ansible playbook named playbook.yml and open it in a text editor:
   ```
touch playbook.yml
nano playbook.yml
   ```
3. Add the following code to the playbook.yml file to configure the provisioned virtual machine:
   ```
   ---
   - name: Configure web server
   hosts: my-vm
   become: true

   tasks:
      - name: Install Nginx
         apt:
         name: nginx
         state: present
         tags: nginx
   ```

4. Save and close the playbook.yml file.

Step 4: Execute the Ansible playbook
1. Run the Ansible playbook using the following command, specifying the inventory file and playbook file:

   ```
   ansible-playbook -i <path-to-inventory-file> playbook.yml
   ```
2. Replace <path-to-inventory-file> with the path to your inventory file or specify the target host directly.

Example:
   ```
   ansible-playbook -i inventory.ini playbook.yml
   ```
3. Ansible will connect to the target host and execute the defined tasks, ensuring the desired infrastructure configuration.

Congratulations! You have automated the provisioning and configuration of infrastructure using Ansible and Terraform.
