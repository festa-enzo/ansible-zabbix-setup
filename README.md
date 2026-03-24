 Ansible Zabbix Setup

Automation project using Ansible to install and configure Zabbix on Linux environments.
 
 Overview

This repository provides an automated way to deploy a complete monitoring stack using Ansible. It installs and configures:

* Zabbix Server
* Zabbix Agent
* Database (MySQL/MariaDB or PostgreSQL)
* Web interface

The goal is to provide a fast, consistent, and reproducible setup.

## Requirements

* Linux control node (Oracle Linux 9, RHEL, CentOS, etc.)
* Ansible installed
* SSH access to target hosts
* Sudo privileges on managed nodes

## Project Structure

```
.
├── playbook.yml
├── roles/
├── group_vars/
├── host_vars/
└── .gitignore
```

##  Inventory File (YAML format)

The inventory file is ignored via `.gitignore` for security reasons. You must create your own local version.

### ➤ Create the file

```bash
touch hosts.yml
```

### ➤ Example inventory in YAML

```yaml
all:
  children:
    zabbix_server:
      hosts:
        zabbix-server-1:
          ansible_host: 192.168.1.10
          ansible_user: oracle

    zabbix_agents:
      hosts:
        agent-1:
          ansible_host: 192.168.1.20
          ansible_user: oracle

        agent-2:
          ansible_host: 192.168.1.21
          ansible_user: oracle
```

### ➤ Using SSH key

```yaml
all:
  children:
    zabbix_server:
      hosts:
        zabbix-server-1:
          ansible_host: 192.168.1.10
          ansible_user: oracle
          ansible_ssh_private_key_file: ~/.ssh/id_rsa
```

---

##  Run with YAML inventory

```bash
ansible-playbook -i hosts.yml playbook.yml
```

##  Notes

* Make sure your SSH access is properly configured.
* You can test connectivity with:

```bash
ansible all -i hosts -m ping
```

* Adjust variables in `group_vars/` and `host_vars/` as needed.

---

## 📄 License

This project is open-source and available under the MIT License.
