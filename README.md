## What is Ansible?

Ansible is an automation tool used to automate IT tasks such as server configuration, software installation, application deployment, and infrastructure management.

👉 In simple terms:<br>
Ansible lets you manage multiple servers with a single command.

**Ansible** is an **IT automation, configuration management, and provisioning tool**.

- It is used to **deploy, manage, build, test, and configure** systems
- It can manage **anything** from full server environments to websites and applications
- Ansible uses **Playbooks**
- Playbooks are written in **YAML**
- YAML files are **human-readable**

 <p align="center">
  <img src="https://github.com/nikiimisal/Ansible--Setup-and-some-info/blob/main/img/ansi.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>


---

## 🔹 Why do we use Ansible?

- To apply the same configuration on multiple servers
- To install and update software
- To deploy applications
- To manage Dev / QA / Prod environments
- To reduce manual work and human errors

---

## How Ansible Works

### 1️⃣ Modules
- **Modules are small programs** that perform a specific task  
  (example: install a package, start a service, copy a file)
- Modules are executed using **YAML-based playbooks**
- Examples: `apt`, `yum`, `service`, `copy`

👉 *Modules = “what action to perform”*

---

### 2️⃣ Inventory
- **Inventory contains details of multiple servers**
- It defines **where the task should be executed**
- Can include:
  - IP addresses
  - Hostnames
  - Server groups (web, db, app)

👉 *Inventory = “on which servers to run the task”*

---

### 3️⃣ Playbook
- A **Playbook is a YAML file**
- It defines **which modules to run** and **on which target servers**
- Example use case:
  - Install a web server on a **remote (target) server**

👉 *Playbook = “how and in what order tasks are executed”*


yaml
```
---

- name: Install nginx
  hosts: webservers
  tasks:
    - name: Install nginx package
      apt:
        name: nginx
        state: present
```

## Simple Flow

```
Inventory → Playbook → Modules → Target Servers
```

- Inventory → server details
- Playbook → instructions (YAML)
- Modules → actual work
- Target server → where work happens

---

## 🔹 Key components of Ansible

| Component     | Description                                          |
| ------------- | ---------------------------------------------------- |
| **Inventory** | List of servers (IP or hostnames)                    |
| **Playbook**  | YAML file containing automation steps                |
| **Module**    | Pre-built units like `apt`, `yum`, `copy`, `service` |
| **Task**      | A single action                                      |
| **Role**      | Reusable structure for playbooks                     |
| **Facts**     | System information (OS, IP, RAM, etc.)               |

---

## 🔹 Ansible vs Shell Script (quick comparison)

| Ansible                                 | Shell Script                 |
| --------------------------------------- | ---------------------------- |
| Idempotent (safe to run multiple times) | May cause errors if repeated |
| Manages multiple servers easily         | Usually single server        |
| Human-readable YAML                     | Complex Bash                 |
| Agentless                               | Requires manual handling     |

---

## 🔹 Real-world example


Without Ansible (Manual):

- Login to each server
- Install software
- Update configuration
- Restart services


With Ansible:

- Write one playbook
- Run one command
- Task completed on all servers 🚀

---


<h1>📘 Ansible Setup Guide</h1>

🚀 Step 1: Launch EC2 Instance  
<br>
Launch an EC2 instance from the AWS Console and give it the name **ansible**.  
This name helps in easy identification later.

 <p align="center">
  <img src="https://github.com/nikiimisal/Ansible--Setup-and-some-info/blob/main/img/Screenshot%202025-12-16%20234829.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>

---

🔐 Step 2: Connect Using SSH  

Login to the instance using SSH from your terminal:
```
ssh -i Downloads/server1.pem ec2-user@<public-ip>
```
This provides secure access to the EC2 server.

---

🖥️ Step 3: Change Hostname  

After login, change the hostname of the instance. 

```
 sudo hostnamectl hostname Aansible
```
This helps you understand that this server is used for Ansible when working with multiple machines.


 <p align="center">
  <img src="https://github.com/nikiimisal/Ansible--Setup-and-some-info/blob/main/img/Screenshot%202025-12-16%20181320.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>


---

🌐 Step 4: Allow Required Ports  
In the Security Group, allow:
- Port 22 → SSH access  
- Port 80 → Web/Application access  

⚠️ Ansible does not require a specific port, but these ports are commonly needed.

---

🔄 Step 5: Update the System 

Run system update to install all available updates:
```
sudo yum update -y  
```

 <p align="center">
  <img src="https://github.com/nikiimisal/Ansible--Setup-and-some-info/blob/main/img/Screenshot%202025-12-16%20181738.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>


---

📦 Step 6: Install Ansible  

Install Ansible using:
```
sudo yum install ansible -y  
```
 <p align="center">
  <img src="https://github.com/nikiimisal/Ansible--Setup-and-some-info/blob/main/img/Screenshot%202025-12-16%20182032.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>

---

📁 Step 7: Ansible Directory Structure  

After installation, Ansible creates a folder at:
```
 /etc/ansible/

 cd /etc/ansible/  
```

 <p align="center">
  <img src="https://github.com/nikiimisal/Ansible--Setup-and-some-info/blob/main/img/Screenshot%202025-12-17%20000015.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>


---

🗂️ Step 8: Create Playbooks Folder 

Create a folder to store all Ansible playbooks:
```
sudo mkdir playbooks
cd playbooks  
```
✅ Ansible setup is now complete and ready for playbook creation 🎉


---





















