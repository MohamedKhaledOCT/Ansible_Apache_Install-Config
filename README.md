بالطبع! إليك نموذجًا لملف README لمشروعك. يمكنك تخصيصه حسب الحاجة:

---

# Ansible Apache Deployment with Whitelist

## Overview
This project automates the deployment and configuration of the Apache web server on a group of servers using Ansible. It includes a whitelist-based access control mechanism to restrict access to specific IPs, ensuring a secure setup.

---

## Features
- Install and configure the Apache web server automatically.
- Use a Jinja2 template (`apache.conf.j2`) for flexible and dynamic configuration.
- Allow access only to specific IP addresses using a whitelist.
- Automate enabling the Apache site and restarting the service when configuration changes.

---

## Prerequisites
- **Ansible** must be installed on the control machine.
- Target servers must:
  - Support SSH access.
  - Have the `ubuntu` user with `sudo` privileges.
- A valid inventory file (`inventory.ini` or `inventory.yml`).
- Define an SSH private key for access.

---

## Project Structure
```
.
├── ansible.cfg          # Ansible configuration file
├── Apache.yaml          # Main Ansible Playbook
├── apache.conf.j2       # Jinja2 template for Apache configuration
├── inventory.ini        # Inventory file for managing target servers
```

---

## How to Use

### 1. Clone the Repository
```bash
git clone https://github.com/MohamedKhaledOCT/Ansible_Apache_Install-Config.git
cd Ansible_Apache_Install-Config
```

### 2. Configure the Inventory File
Edit `inventory.ini` or `inventory.yml` to include your target servers and ensure correct settings for the `ubuntu` user.

### 3. Run the Playbook
Use the following command to deploy Apache:
```bash
ansible-playbook -i inventory.ini Apache.yaml
```

### 4. Verify Deployment
- Access the web server using the IP of one of the servers in the inventory.
- Confirm that only the whitelisted IPs can access the server.

---

## Files Explained

### `ansible.cfg`
Configures Ansible behavior, disabling host key checking for smoother SSH connections.

### `Apache.yaml`
Defines tasks to:
- Install Apache.
- Configure it using a Jinja2 template.
- Enable the Apache site configuration.
- Start and enable the Apache service.

### `apache.conf.j2`
A dynamic Apache configuration template that:
- Sets the `ServerName` and `DocumentRoot`.
- Implements IP-based access control via a whitelist.

### `inventory.ini`
Specifies the target servers and their connection details.

---

## Customization
- Modify `allowed_ips` in `Apache.yaml` to define the IPs allowed to access the server.
- Update `apache.conf.j2` to add or change configuration directives as needed.
- Adjust the `ansible_user` and `ansible_ssh_private_key_file` in the inventory file to match your environment.

---

## Example Configuration
Sample variables from `Apache.yaml`:
```yaml
vars:
  apache_document_root: /var/www/html
  apache_name: mywebsite.local
  allowed_ips:
    - 192.168.1.13
    - 192.168.1.15
    - 192.168.1.20
```

---

## Troubleshooting
- If Apache fails to start, check the syntax of the configuration file:
  ```bash
  sudo apachectl configtest
  ```
- Use `ansible-playbook` with verbose output for debugging:
  ```bash
  ansible-playbook -i inventory.ini Apache.yaml -vvv
  ```

---

## License
This project is open-source and available under the [MIT License](https://opensource.org/licenses/MIT).

---
