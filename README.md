# ansible-infra-bootstrap


## ✅ `README.md` — Ansible EC2 Bootstrap

````markdown
# Ansible Infra Bootstrap

This project uses **Ansible** to automate the setup of an AWS **EC2** instance with the following services:

- MySQL
- PostgreSQL
- Nginx

It is useful for quickly provisioning a development or testing environment on a fresh Ubuntu-based EC2 instance.

---

## 🚀 Features

- Provision EC2 instance with:
  - ✅ MySQL Server
  - ✅ PostgreSQL Server
  - ✅ Nginx Web Server
- Easy configuration via `inventory.ini` and `setup.yml`
- SSH-based provisioning using Ansible

---

## 🧾 Files

| File Name      | Description                                      |
|----------------|--------------------------------------------------|
| `inventory.ini`| Contains EC2 host IP and SSH details             |
| `setup.yml`    | Ansible playbook to install and configure services|

---

## 🛠️ Prerequisites

- An EC2 instance running Ubuntu 
- SSH access via a `.pem` key
- Ansible installed on your control machine (the machine from which you run Ansible)

Install Ansible :

```bash
sudo apt update && sudo apt install ansible -y
````

---

## 🧩 Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/shashibabu123/ansible-infra-bootstrap.git
cd ansible-infra-bootstrap
```

### 2. Update `inventory.ini`

```ini
[web]
<EC2_PUBLIC_IP> ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/your-key.pem
```

Replace:

* `<EC2_PUBLIC_IP>` with your instance's public IP
* `your-key.pem` with your actual key filename

> Ensure the key has correct permissions:
> `chmod 400 ~/.ssh/your-key.pem`

---

### 3. Run the Playbook

```bash
ansible-playbook -i inventory.ini setup.yml
```

This will:

* Install and start MySQL
* Install and start PostgreSQL
* Install and start Nginx

---

## 🧪 Verify Installation

SSH into the EC2 instance:

```bash
ssh -i ~/.ssh/your-key.pem ubuntu@<EC2_PUBLIC_IP>
```

Then run:

```bash
mysql --version
psql --version
systemctl status nginx
```

---

## 📂 Project Structure

```
ansible-ec2-setup/
├── README.md
├── inventory.ini
├── setup.yml
├── roles/
│   ├── mysql/
│   │   └── main.yml
│   ├── postgres/
│   │   └── main.yml
│   └── nginx/
│       └── main.yml

```

---

## 🙌 Author

**Shashibabu**
GitHub: [shashibabu123](https://github.com/shashibabu123)

---




# OUTPUT OF MY TASK
# STEP: 4
root@ip-172-31-27-254:~/ansible-ec2-setup# ansible-playbook -i inventory.ini setup.yml

PLAY [Setup EC2 with MySQL, PostgreSQL, and Nginx] *****************************

TASK [Gathering Facts] *********************************************************
ok: [3.89.33.41]

TASK [Update apt packages] *****************************************************
changed: [3.89.33.41]

TASK [Install MySQL] ***********************************************************
changed: [3.89.33.41]

TASK [Enable and start MySQL] **************************************************
ok: [3.89.33.41]

TASK [Install PostgreSQL] ******************************************************
changed: [3.89.33.41] => (item=postgresql)
changed: [3.89.33.41] => (item=postgresql-contrib)

TASK [Enable and start PostgreSQL] *********************************************
ok: [3.89.33.41]

TASK [Install Nginx] ***********************************************************
changed: [3.89.33.41]

TASK [Enable and start Nginx] **************************************************
ok: [3.89.33.41]

PLAY RECAP *********************************************************************
3.89.33.41                 : ok=8    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

# STEP:-5
root@ip-172-31-27-254:~/ansible-ec2-setup# mysql --version && psql --version && curl localhost     

mysql  Ver 8.0.41-0ubuntu0.24.04.1 for Linux on x86_64 ((Ubuntu))
psql (PostgreSQL) 16.8 (Ubuntu 16.8-0ubuntu0.24.04.1)
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
root@ip-172-31-27-254:~/ansible-ec2-setup# ls
inventory.ini  setup.yml
root@ip-172-31-27-254:~/ansible-ec2-setup# Read from remote host ec2-3-89-33-41.compute-1.amazonaws.com: Connection reset by peer
Connection to ec2-3-89-33-41.compute-1.amazonaws.com closed.
client_loop: send disconnect: Connection reset by peer

Here is an updated `README.md` documentation tailored for your project, assuming it includes Ansible roles for setting up infrastructure with Grafana, Promtail, and possibly Loki:

---

```markdown
# Ansible Infra Bootstrap with Grafana Integration

This repository contains an Ansible-based infrastructure bootstrap setup that includes monitoring with Grafana and Promtail. It is designed to be used on Ubuntu-based EC2 instances or virtual machines.

## 🔧 Project Structure

```

ansible-infra-bootstrap/
├── inventory.ini/
│                # Inventory file with target EC2 IPs
├── roles/
│   ├── logging/
│   │   ├── tasks/             # Tasks to install and configure Promtail
│   │   └── templates/         # promtail-config.yml, etc.
│   └── grafana/
│       ├── tasks/             # Install and configure Grafana
│       └── templates/         # Optional Grafana config files
├── playbook.yml               # Main Ansible playbook
└── README.md                  # This documentation

````

## 🚀 Features

- Installs and configures:
  - Docker and Docker Compose
  - Promtail for log shipping
  - Grafana for log and metrics visualization
- Auto-detects Docker containers and reads their logs from `/var/lib/docker/containers/*/*.log`
- Uses Promtail to ship logs to a Loki server or another Grafana-compatible backend

## 📦 Requirements

- Ansible installed on your control machine (`pip install ansible`)
- Ubuntu-based EC2 instance(s) or VM(s)
- SSH access to the instances

## 🛠️ Usage

### 1. Update Inventory

Edit `inventory/hosts.ini` and add your server IP:
```ini
[logging]
your-server-ip ansible_user=ubuntu
````

### 2. Run the Playbook

```bash
ansible-playbook -i inventory/hosts.ini playbook.yml
```

### 3. Access Grafana

Once setup is complete, Grafana will be running on:

```
http://your-server-ip:3000
```

* Default credentials:

  * **Username:** `admin`
  * **Password:** `admin` (change on first login)

### 4. Add Loki as a Data Source (if using remote Loki)

If you're using an external Loki instance:

* Go to **Grafana > Configuration > Data Sources**
* Choose **Loki** and configure the URL (e.g., `http://localhost:3100` or remote endpoint)

## 📁 Promtail Configuration Template

Located at `roles/logging/templates/promtail-config.yml.j2`. It is set to collect logs from:

```yaml
/var/lib/docker/containers/*/*.log
```

With labels:

```yaml
job: dockerlogs
```

## 🧪 Testing Logs

You can test log ingestion by running a container:

```bash
docker run --rm -d nginx
```

Then check Grafana Explore tab with query:

```
{job="dockerlogs"}
```

