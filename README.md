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
- [License](#license)
- [Additional Notes](#additional-notes)

## Overview

This Ansible project provides two main roles:

1. **Webserver Role**: Installs and configures Apache and PHP on your server.
2. **Database Role**: Installs and configures MySQL, and sets up a MySQL database with a specific root password.

## Prerequisites

Before running the playbook, ensure you have the following:

- **Ansible installed** on your local machine:
  ```bash
  pip install ansible
  ```

- **A remote server** (e.g., an EC2 instance) with SSH access.
- The server should have **Python installed**, as Ansible uses it for executing commands.
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

Update the `hosts` file with your target server's IP address or hostname. For example:

```ini
[web]
your_server_ip_or_hostname

[db]
your_server_ip_or_hostname
```

### Step 3: Edit Variables (Optional)

If you'd like to change the default values, edit the `defaults/main.yml` files inside the `webserver` and `dbserver` roles. Here you can specify the document root, server name, MySQL root password, and more.

### Step 4: Run the Playbook

To execute the playbook and set up the LAMP stack on your server:

```bash
ansible-playbook -i hosts playbook.yml
```

This will install and configure Apache, PHP, and MySQL on your remote server.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Additional Notes

- If you're using AWS EC2, ensure your security group allows incoming traffic on ports **80 (HTTP)** and **3306 (MySQL)**.
- You may need to adjust your firewall settings for both Apache and MySQL.
- Ensure your server has adequate resources for running a LAMP stack.

