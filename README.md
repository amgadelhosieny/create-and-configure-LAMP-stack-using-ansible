# LAMP Stack Setup with Ansible

This repository contains an Ansible project to automatically configure and deploy a LAMP (Linux, Apache, MySQL, PHP) stack on a remote server. The setup includes the installation and configuration of Apache and MySQL with PHP support.

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Roles Overview](#roles-overview)
  - [Webserver Role](#webserver-role)
  - [Database Role](#database-role)
- [How to Use](#how-to-use)
  - [Step 1: Clone the Repository](#step-1-clone-the-repository)
  - [Step 2: Edit the Hosts File](#step-2-edit-the-hosts-file)
  - [Step 3: Edit Variables (Optional)](#step-3-edit-variables-optional)
  - [Step 4: Run the Playbook](#step-4-run-the-playbook)
- [Additional Notes](#additional-notes)

## Overview

This Ansible project provides two main roles:

1. **Webserver Role**: Installs and configures Apache and PHP on your server.
2. **Database Role**: Installs and configures MySQL, and sets up a MySQL database with a specific root password.

### AWS Deployment

Two separate EC2 instances are created for this project:

- **Web Server Instance**: Dedicated to running Apache and PHP.
- **Database Server Instance**: Dedicated to running MySQL.

This separation of roles ensures better performance, security, and scalability.

## Prerequisites

Before running the playbook, ensure you have the following:

- **Ansible installed** on your local machine:
  ```bash
  pip install ansible
  ```

- **Two remote servers** (e.g., EC2 instances) with SSH access:
  - One for the web server (Apache + PHP).
  - One for the database server (MySQL).

- The servers should have **Python installed**, as Ansible uses it for executing commands.
- A GitHub repository to push your code (if you're working on a versioned project).

## Roles Overview

### Webserver Role

This role installs and configures Apache and PHP. It also deploys a custom `phpinfo.php` file to test PHP installation.

**Key steps involved:**

- Install Apache and PHP packages.
- Configure the Apache web server using custom templates.
- Deploy `phpinfo.php` to confirm PHP installation.
- Ensure Apache is started and enabled to run on boot.

**Variables for this role:**

- `apache_document_root`: Defines the document root for Apache (default is `/var/www/html`).
- `apache_server_name`: Configures the server name (e.g., `mywebsite.local`).

### Database Role

This role installs and configures MySQL, sets the root password, and deploys a basic `.my.cnf` configuration file to store MySQL root credentials.

**Key steps involved:**

- Install MySQL Server.
- Set the MySQL root password.
- Create a `.my.cnf` configuration file for MySQL root user authentication.

**Variables for this role:**

- `mysql_root_password`: The root password for MySQL.
- `db_name`: The name of the MySQL database to create.
- `db_user`: The MySQL user to create.
- `db_password`: The password for the new MySQL user.

## How to Use

### Step 1: Clone the Repository

```bash
git clone https://github.com/<your-username>/create-and-configure-LAMP-stack-using-ansible.git
cd create-and-configure-LAMP-stack-using-ansible
```

### Step 2: Edit the Hosts File

Update the `hosts` file with your target servers' IP addresses or hostnames. For example:

```ini
[web]
web_server_ip_or_hostname

[db]
db_server_ip_or_hostname
```

### Step 3: Edit Variables (Optional)

If you'd like to change the default values, edit the `defaults/main.yml` files inside the `webserver` and `dbserver` roles. Here you can specify the document root, server name, MySQL root password, and more.

### Step 4: Run the Playbook

To execute the playbook and set up the LAMP stack on your servers:

```bash
ansible-playbook -i hosts playbook.yml
```

This will:

1. Install and configure Apache and PHP on the web server instance.
2. Install and configure MySQL on the database server instance.


## Additional Notes

- If you're using AWS EC2, ensure your security groups allow incoming traffic on ports:
  - **80 (HTTP)** for the web server.
  - **3306 (MySQL)** for the database server.
- You may need to adjust your firewall settings for both Apache and MySQL.
- Ensure your servers have adequate resources for running a LAMP stack.

