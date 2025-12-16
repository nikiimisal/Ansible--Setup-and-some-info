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

---

##🔹 Why do we use Ansible?

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

































