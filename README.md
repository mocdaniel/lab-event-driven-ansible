# Event-Driven Ansible Lab

This is a lab designed to demonstrate Ansible and how Event-Driven Ansible (**EDA**) builds on top of its capabilities.

The setup is done with Ansible, too. It will install **Ansible, EDA, Prometheus**, and **Alertmanager** on a VM to demonstrate some of the capabilities of EDA.

## Prerequisites

To follow along with this lab in its entirety, you will need four VMs:

> [!NOTE]
> If you want to skip Ansible basics and go straight to EDA, you'll need just the `eda-controller.example.com` VM and can skip the others.

| VM name            | OS          |
|--------------------|-------------|
| eda-controller.example.com | CentOS/Rocky 8.9 |
| company.example.com        | CentOS/Rocky 8.9 |
| internal.example.com       | Ubuntu 22.04     |
| webshop.example.com        | OpenSUSE 15.5    |

**You'll need to be able to SSH to each of these VMs as root using SSH keys.**

## Lab Setup

### Clone the repository and create a Python virtual environment

```bash
git clone https://github.com/mocdaniel/lab-event-driven-ansible.git
cd lab-event-driven-ansible
python3 -m venv .venv
source .venv/bin/activate
```

### Install Ansible and other dependencies

```bash
pip install -r requirements.txt
```

### Create the inventory file

```yaml
---
# hosts.yml
webservers:
  hosts:
    webshop.example.com:
      ansible_host: <ip-address>
      webserver: nginx
    company.example.com:
      ansible_host: <ip-address>
      webserver: httpd
    internal.example.com:
      ansible_host: <ip-address>
      webserver: apache2
eda_controller:
  hosts:
    eda-controller.example.com:
      ansible_host: <ip-address>
```

### Install Needed Roles and Collections
    
```bash
ansible-galaxy install -r requirements.yml
```

### Run the Setup Playbook

After you created the inventory file and filled in the IP addresses, you can run the setup playbook:

```bash
ansible-playbook playbooks/setup.yml
```
