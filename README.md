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
ansible-infra-bootstrap/
├── inventory.ini
└── setup.yml
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
root@ip-172-31-27-254:~/ansible-ec2-setup# mysql --version && psql --version && curl localhost   && sudo ss -tulnp | grep 3306 &&   sudo ss -tulnp | grep 5432 

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
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
tcp   LISTEN 0      151               0.0.0.0:3306       0.0.0.0:*    users:(("mysqld",pid=7158,fd=23))
tcp   LISTEN 0      70              127.0.0.1:33060      0.0.0.0:*    users:(("mysqld",pid=7158,fd=21))
tcp   LISTEN 0      200               0.0.0.0:5432       0.0.0.0:*    users:(("postgres",pid=7247,fd=6))
tcp   LISTEN 0      200                  [::]:5432          [::]:*    users:(("postgres",pid=7247,fd=7))

