# Exercise 3: Advanced Ansible - Role-based Development and Ansible Galaxy

In this exercise, you will dive deeper into Ansible by exploring advanced topics such as role-based development and utilizing Ansible Galaxy. By the end of this exercise, you will have a solid understanding of how to structure your Ansible projects using roles and leverage Ansible Galaxy to enhance your automation capabilities.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step 1: Understanding Role-based Development](#step-1-understanding-role-based-development)
- [Step 2: Exploring Ansible Galaxy](#step-2-exploring-ansible-galaxy)
- [Step 3: Creating and Using Roles in Your Ansible Project](#step-3-creating-and-using-roles-in-your-ansible-project)
- [Step 4: Testing and Executing Your Advanced Ansible Project](#step-4-testing-and-executing-your-advanced-ansible-project)

## Prerequisites

- Ansible installed on your Ubuntu machine
- Basic knowledge of Ansible concepts and playbook development

## Step 1: Understanding Role-based Development

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

## Step 2: Exploring Ansible Galaxy
1. Ansible Galaxy is a repository for Ansible roles that allows you to discover, share, and reuse pre-built Ansible roles developed by the community. It provides a centralized location for finding and contributing to the Ansible ecosystem.

2. Browse the Ansible Galaxy website (https://galaxy.ansible.com/) to explore the available roles and their functionalities. Identify roles that align with your project requirements.

3. To install an Ansible role from Ansible Galaxy, use the ansible-galaxy command. For example, to install the nginx role, run the following command:

```
ansible-galaxy install nginx
```
This command installs the nginx role, along with any role dependencies specified in the `meta/main.yml` file of the role.

## Step 3: Creating and Using Roles in Your Ansible Project
1. Structure your Ansible project using roles. Create the necessary directories and files for your roles based on the role-based development approach.

2. Move your existing tasks, variables, and templates into separate roles. Refactor your Ansible playbooks to use these roles.

3. Enhance your project by incorporating external roles from Ansible Galaxy. Update your playbooks to include the roles you installed from Ansible Galaxy.

## Step 4: Testing and Executing Your Advanced Ansible Project
1. Verify the correctness of your role-based Ansible project by running test playbooks against your target hosts.

2. Execute your advanced Ansible project and observe the changes and configuration applied to your target hosts.

Congratulations! You have learned advanced Ansible techniques such as role-based development and utilizing Ansible Galaxy. These skills will enable you to structure your Ansible projects effectively and leverage the power of community-contributed roles.
