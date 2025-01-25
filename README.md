# create-and-configure-LAMP-stack-using-ansible

LAMP Stack Setup with Ansible

This repository contains an Ansible project to automatically configure and deploy a LAMP (Linux, Apache, MySQL, PHP) stack on a remote server. The setup includes the installation and configuration of Apache and MySQL with PHP support.
Table of Contents


This structure includes:

- **`ansible.cfg`**: The Ansible configuration file.
- **`hosts`**: The inventory file specifying the target servers.
- **`playbook.yml`**: The main playbook that includes both `webserver` and `dbserver` roles.
- **`roles/`**: Contains roles for configuring the database server (`dbserver`) and the web server (`webserver`).
  - **`defaults/main.yml`**: Default variables for each role.
  - **`handlers/main.yml`**: Handlers for actions like restarting services.
  - **`tasks/main.yml`**: The tasks to be executed for each role.
  - **`templates/`**: Templates like MySQL and Apache config files.
  - **`tests/`**: Contains basic tests for the roles.
  - **`vars/main.yml`**: Additional variables for each role.


    Overview
    Prerequisites
    Roles Overview
        Webserver Role
        Database Role
    How to Use
    License

Overview

This Ansible project provides two main roles:

    Webserver Role: Installs and configures Apache and PHP on your server.
    Database Role: Installs and configures MySQL, and sets up a MySQL database with a specific root password.

Prerequisites

Before running the playbook, ensure you have the following:

    Ansible installed on your local machine.
        You can install Ansible via pip:

        pip install ansible

    A remote server (EC2 instance, for example) with SSH access.

    The server should have Python installed, as Ansible uses it for executing commands.

    A GitHub repository to push your code (if you're working on a project versioned with Git).

Roles Overview
Webserver Role

This role installs and configures Apache and PHP. It also deploys a custom phpinfo.php file to test PHP installation. Key steps involved:

    Install Apache and PHP packages.
    Configure the Apache web server using custom templates.
    Deploy phpinfo.php to confirm PHP installation.
    Ensure Apache is started and enabled to run on boot.

The variables for this role include:

    apache_document_root: Defines the document root for Apache (default is /var/www/html).
    apache_server_name: Configures the server name (e.g., mywebsite.local).

Database Role

This role installs and configures MySQL, sets the root password, and deploys a basic .my.cnf configuration file to store MySQL root credentials.

The steps involved include:

    Install MySQL Server.
    Set the MySQL root password.
    Create a .my.cnf configuration file for MySQL root user authentication.

The variables for this role include:

    mysql_root_password: The root password for MySQL.
    db_name: The name of the MySQL database to create.
    db_user: The MySQL user to create.
    db_password: The password for the new MySQL user.

How to Use
Step 1: Clone the Repository

git clone https://github.com/<username>/create-and-configure-LAMP-stack-using-ansible.git
cd create-and-configure-LAMP-stack-using-ansible

Step 2: Edit the Hosts File

Update the hosts file with your target server's IP address or hostname. For example:

[web]
your_server_ip_or_hostname

[db]
your_server_ip_or_hostname

Step 3: Edit Variables (Optional)

If you'd like to change the default values, edit the defaults/main.yml files inside the webserver and dbserver roles. Here you can specify the document root, server name, MySQL root password, and more.
Step 4: Run the Playbook

To execute the playbook and set up the LAMP stack on your server:

ansible-playbook -i hosts playbook.yml

This will install and configure Apache, PHP, and MySQL on your remote server.
License

This project is licensed under the MIT License - see the LICENSE file for details.
Additional Notes:

    If you're using AWS EC2, ensure your security group allows incoming traffic on ports 80 (HTTP) and 3306 (MySQL).
    You may need to adjust your firewall settings for both Apache and MySQL.
