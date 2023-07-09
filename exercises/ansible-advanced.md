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

- Basic knowledge of Ansible concepts and playbook development
- Basic knowledge of Ubuntu command-line interface (CLI) and package management (apt).
- Ansible installed on your Ubuntu machine (refer to Step 1 for installation instructions).
- Internet access on the Ubuntu machine for downloading the updates, packeges and roles from Ansible Galaxy.
- A target environment and access to it (virtual machines or containers, or remote servers) where you can test your Ansible playbooks and roles.

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
   ├── ansible.cfg
   ├── tasks/
   │   └── main.yml
   ├── inventory/
   │   ├── ALL
   │   ├── webservers
   │   └── database_servers
   ├── group_vars/
   │   └── all.yml
   ├── host_vars/
   │   ├── webserver1.yml
   │   ├── webserver2.yml
   │   └── webserver3.yml
   ├── templates/
   │   └── index.html.j2
   ├── vars/
   │   └── main.yml
   ├── meta/
   │   └── main.yml
   ├── handlers/
   │   └── main.yml
   ├── files/
   │   └── myfile.conf
   ├── defaults/
   │   └── main.yml
   ├── library/
   │   └── mymodule.py
   ├── lookup_plugins/
   │   └── mylookup.py
   ├── filter_plugins/
   │   └── myfilter.py
   ├── requirements.yml
   └── README.md
   ```

- The `ansible.cfg` file specifies the configuration for your Ansible project. Place it in the root directory of your project.
- The `tasks` directory contains the main tasks file (main.yml) that defines the actions to be performed.
- The `inventory` directory contains inventory files that define your hosts and host groups.
- The `group_vars` directory stores variable files specific to groups.
- The `host_vars` directory stores variable files specific to individual hosts.
- The `templates` directory stores the template files used by the role.
- The `vars` directory contains variable files (main.yml) that define role-specific variables.
- The `meta` directory stores metadata about the role, such as dependencies.
- The `handlers` directory contains handler files that define actions triggered by events.
- The `files` directory stores static files that need to be copied to remote hosts.
- The `defaults` directory contains default variable files that provide default values.
- The `library` directory contains custom modules.
- The `lookup_plugins` directory stores custom lookup plugins.
- The `filter_plugins` directory stores custom filter plugins.
- The `requirements.yml` file specifies any external role dependencies.
- The `README.md` file provides documentation about the role.

3. Each file in the directory structure serves a specific purpose. Here's an example code snippet for each file:
### ansible.cfg
This file specifies the configuration for your Ansible project. It is placed in the root directory of your project. In the given example, it contains the following configuration:
```
[defaults]
inventory = inventory/
roles_path = roles/
```
### tasks/main.yml:
The tasks/main.yml file contains the main tasks to be performed by the role. In a production environment, it might look like this:

```
---
- name: Install and configure web server
  apt:
    name: apache2
    state: latest
  notify: Restart Apache
  become: yes
  become_user: root
  tags:
    - webserver
    - install

- name: Copy configuration file
  copy:
    src: myfile.conf
    dest: /etc/myapp/
    mode: 0644
    owner: root
    group: root
  notify: Reload Configuration
```
### inventory files
inventory/ALL
```
[all:children]
webservers
database_servers
```
inventory/webservers
```
[webservers_group]
webserver1 ansible_host=192.168.1.101

# Alternatively, you can define additional hosts like this:
# webserver2 ansible_host=192.168.1.102
# webserver3 ansible_host=192.168.1.103
# Alternatively to the groupvars you may write it this way:
# webserver1 ansible_host=192.168.1.101 ansible_connection=ssh ansible_ssh_user=my_server_username ansible_ssh_pass=my_server_ssh_password
# webserver2 ansible_host=192.168.1.102 ansible_connection=ssh ansible_ssh_user=my_server_username ansible_ssh_pass=my_server_ssh_password
# webserver3 ansible_host=192.168.1.103 ansible_connection=ssh ansible_ssh_user=my_server_username ansible_ssh_pass=my_server_ssh_password
```
inventory/database_servers:
```
[database_servers_group]
dbserver1 ansible_host=192.168.1.201

# Alternatively, you can define additional hosts like this:
# dbserver2 ansible_host=192.168.1.202
# dbserver3 ansible_host=192.168.1.203
# Alternatively to the groupvars you may write it this way:
# dbserver1 ansible_host=192.168.1.201 ansible_connection=ssh ansible_ssh_user=my_server_username ansible_ssh_pass=my_server_ssh_password
# dbserver2 ansible_host=192.168.1.202 ansible_connection=ssh ansible_ssh_user=my_server_username ansible_ssh_pass=my_server_ssh_password
# dbserver3 ansible_host=192.168.1.203 ansible_connection=ssh ansible_ssh_user=my_server_username ansible_ssh_pass=my_server_ssh_password
```
### group_vars/all.yml
The group_vars/all.yml file contains variable files specific to all hosts in a particular group. In a production environment, it might look like this:
```
---
webserver_domain: example.com
webserver_ssl_certificate: /etc/ssl/certs/example.com.crt
webserver_ssl_key: /etc/ssl/private/example.com.key

# webserver_ssh_username: my_server_username
# webserver_ssh_password: my_server_ssh_password

database_server: dbserver1
```
### host_vars/webserver1.yml
The host_vars/webserver.yml file contains variable files specific to a particular host. In a production environment, it might look like this:
```
---
webserver_ip: 192.168.1.101
ansible_connection: ssh
ansible_ssh_user: my_webserver1_username
ansible_ssh_pass: my_webserver1_ssh_password
webserver_port: 8080

# Alternatively to the groupvars you may write it this way:
# webserver_ip: 
#   - hostname: 192.168.1.101
#     ansible_connection: ssh
#     ansible_ssh_user: my_server1_username
#     ansible_ssh_pass: my_server1_ssh_password
```
### host_vars/webserver2.yml
```
---
webserver_ip: 192.168.1.102
ansible_connection: ssh
ansible_ssh_user: my_webserver2_username
ansible_ssh_pass: my_webserver2_ssh_password
webserver_port: 8080
```
### host_vars/webserver3.yml
```
---
webserver_ip: 192.168.1.103
ansible_connection: ssh
ansible_ssh_user: my_webserver3_username
ansible_ssh_pass: my_webserver3_ssh_password
webserver_port: 8080
```
### templates/index.html.j2:
The templates/index.html.j2 file contains the Jinja2 template for the web server's index page. In a production environment, it might look like this:
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
### vars/main.yml
The vars/main.yml file contains role-specific variables. In a production environment, it might look like this:
```
---
webserver_port: 80
webserver_document_root: "/var/www/html"
```
### meta/main.yml
The meta/main.yml file contains metadata about the role, such as dependencies. In a production environment, it might look like this:
```
---
dependencies:
  - role: common
  - role: database
```
### handlers/main.yml
The handlers/main.yml file contains handler tasks that define actions triggered by events. In a production environment, it might look like this:
```
---
- name: Restart Apache
  service:
    name: apache2
    state: restarted

- name: Reload Configuration
  service:
    name: apache2
    state: reloaded
```
### files/myfile.conf
The files/myfile.conf file contains static files that need to be copied to remote hosts. In a production environment, it might contain the configuration for the application:
```
# Configuration for MyApp
key = value
```
### defaults/main.yml
The defaults/main.yml file contains default variable files that provide default values. In a production environment, it might look like this:
```
---
myapp_version: "1.0"
myapp_timeout: 30
```
### library/mymodule.py
The library/mymodule.py filecontains custom Ansible modules written in **Python**. In a production environment, it might look like this:
```
import os

from ansible.module_utils.basic import AnsibleModule

def main():
    module = AnsibleModule(argument_spec=dict(
        path=dict(required=True, type='path'),
        content=dict(required=True, type='str')
    ))

    path = module.params['path']
    content = module.params['content']

    if os.path.exists(path):
        module.exit_json(changed=False, msg="File already exists.")

    with open(path, 'w') as f:
        f.write(content)

    module.exit_json(changed=True, msg="File created.")

if __name__ == '__main__':
    main()
```
### lookup_plugins/mylookup.py
The lookup_plugins/mylookup.py file contains custom lookup plugins written in **Python**. In a production environment, it might look like this:
```
from ansible.errors import AnsibleError, AnsibleParserError
from ansible.plugins.lookup import LookupBase

class MyLookup(LookupBase):
    def run(self, terms, variables=None, **kwargs):
        results = []
        for term in terms:
            if term == 'myterm':
                results.append('myvalue')
            else:
                raise AnsibleError(f"Invalid term: {term}")
        return results
```
### filter_plugins/myfilter.py
The filter_plugins/myfilter.py file contains custom filter plugins written in **Python**. In a production environment, it might look like this:
```
def myfilter(value):
    # Custom filter logic
    return value.upper()

class FilterModule(object):
    def filters(self):
        return {
            'myfilter': myfilter
        }
```
### requirements.yml
The requirements.yml file specifies any external role dependencies. In a production environment, it might look like this:
```
---
- src: https://github.com/example/role1.git
  version: master

- src: https://github.com/example/role2.git
  version: 2.0.0
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
