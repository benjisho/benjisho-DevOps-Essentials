# Exercise 3: Advanced Ansible - Role-based Development and Ansible Galaxy

In this exercise, you will dive deeper into Ansible by exploring advanced topics such as role-based development and utilizing Ansible Galaxy. By the end of this exercise, you will have a solid understanding of how to structure your Ansible projects using roles and leverage Ansible Galaxy to enhance your automation capabilities.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step 1: Installing Ansible on Ubuntu](#step-1-installing-ansible-on-ubuntu)
- [Step 2: Understanding Role-based Development](#step-2-understanding-role-based-development)
- [Step 3: Exploring Ansible Galaxy](#step-3-exploring-ansible-galaxy)
- [Step 4: Creating and Using Roles in Your Ansible Project](#step-4-creating-and-using-roles-in-your-ansible-project)
- [Step 5: Testing and Executing Your Advanced Ansible Project](#step-5-testing-and-executing-your-advanced-ansible-project)

## Prerequisites

- Ansible installed on your Ubuntu machine
- Basic knowledge of Ansible concepts and playbook development

## Step 1: Installing Ansible on Ubuntu
To install Ansible on Ubuntu, you can use the following steps:

1. Open a terminal.

2. Update the package lists using the following command:
   ```
   sudo apt update
   ```
3. Install the software-properties-common package, which provides the add-apt-repository command:
   ```
   sudo apt install software-properties-common
   ```
4. Add the Ansible PPA repository to your system:
   ```
   sudo add-apt-repository --yes --update ppa:ansible/ansible
   ```
   - This command configures the PPA on your system and ensures that it is up to date.

6. Install Ansible:
   ```
   sudo apt install ansible
   ```
7. The installation process will download and install Ansible along with its dependencies.

### Note:
On older Ubuntu distributions, the software-properties-common package is called python-software-properties. You may need to use apt-get instead of apt in older versions.
If you encounter an error related to the -u or --update flag, it means that your Ubuntu version does not support it. In that case, you can omit the --update flag from the add-apt-repository command.
Once the installation is complete, you can verify that Ansible is installed by running the following command:
```
ansible --version
```
- This command will display the Ansible version information if the installation was successful.

## Step 2: Understanding Role-based Development

1. Roles provide a way to organize and structure your Ansible code by grouping related tasks, variables, and templates into reusable units. They promote code reusability and modularity in your Ansible projects.

2. Ansible roles follow a specific directory structure. Here's an example directory structure for an Ansible role named `webserver`:

   ```
   webserver/
   ├── tasks/
   │   └── main.yml
   ├── templates/
   │   └── index.html.j2
   ├── vars/
   │   └── main.yml
   ├── meta/
   │   └── main.yml
   ├── group_vars/
   │   └── all.yml
   ├── host_vars/
   │   └── server1.yml
   ├── requirements.yml
   └── README.md
   ```
   - The tasks directory contains the main tasks file (main.yml) that defines the actions to be performed.
   - The templates directory stores the template files used by the role.
   - The vars directory contains variable files (main.yml) that define role-specific variables.
   - The meta directory stores metadata about the role, such as dependencies.
   - The group_vars and host_vars directories store variable files specific to groups or hosts.
   - The requirements.yml file specifies any external role dependencies.
   - The README.md file provides documentation about the role.

3. Each file in the directory structure serves a specific purpose. Here's an example code snippet for each file:

tasks/main.yml:

```
---
- name: Install and configure web server
  apt:
    name: apache2
    state: latest
  notify: Restart Apache
```
templates/index.html.j2:
```
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to my website</title>
</head>
<body>
    <h1>Welcome!</h1>
</body>
</html>
```

vars/main.yml:

```
---
webserver_port: 80
```
meta/main.yml:

```
---
dependencies:
  - role: common
```
group_vars/all.yml:

```
---
webserver_domain: example.com
```
host_vars/server1.yml:

```
---
webserver_ip: 192.168.1.100
```

## Step 3: Exploring Ansible Galaxy
1. Ansible Galaxy is a repository for Ansible roles that allows you to discover, share, and reuse pre-built Ansible roles developed by the community. It provides a centralized location for finding and contributing to the Ansible ecosystem.

2. Browse the Ansible Galaxy website (https://galaxy.ansible.com/) to explore the available roles and their functionalities. Identify roles that align with your project requirements.

3. To install an Ansible role from Ansible Galaxy, use the ansible-galaxy command. For example, to install the nginx role, run the following command:

```
ansible-galaxy install nginx
```
This command installs the nginx role, along with any role dependencies specified in the `meta/main.yml` file of the role.

## Step 4: Creating and Using Roles in Your Ansible Project
1. Structure your Ansible project using roles. Create the necessary directories and files for your roles based on the role-based development approach.

2. Move your existing tasks, variables, and templates into separate roles. Refactor your Ansible playbooks to use these roles.

3. Enhance your project by incorporating external roles from Ansible Galaxy. Update your playbooks to include the roles you installed from Ansible Galaxy.

## Step 5: Testing and Executing Your Advanced Ansible Project
1. Verify the correctness of your role-based Ansible project by running test playbooks against your target hosts.

2. Execute your advanced Ansible project and observe the changes and configuration applied to your target hosts.

Congratulations! You have learned advanced Ansible techniques such as role-based development and utilizing Ansible Galaxy. These skills will enable you to structure your Ansible projects effectively and leverage the power of community-contributed roles.
