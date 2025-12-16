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
Launch an EC2 instance from the AWS Console and give it the name **ansible**.  
This name helps in easy identification later.

🔐 Step 2: Connect Using SSH  

Login to the instance using SSH from your terminal:
```
ssh -i Downloads/server1.pem ec2-user@<public-ip>
```
This provides secure access to the EC2 server.

🖥️ Step 3: Change Hostname  

After login, change the hostname of the instance. 

```
 sudo hostnamectl hostname Aansible
```
This helps you understand that this server is used for Ansible when working with multiple machines.

🌐 Step 4: Allow Required Ports  
In the Security Group, allow:
- Port 22 → SSH access  
- Port 80 → Web/Application access  

⚠️ Ansible does not require a specific port, but these ports are commonly needed.

🔄 Step 5: Update the System 

Run system update to install all available updates:
```
sudo yum update -y  
```

📦 Step 6: Install Ansible  

Install Ansible using:
```
sudo yum install ansible -y  
```

📁 Step 7: Ansible Directory Structure  

After installation, Ansible creates a folder at:
```
 /etc/ansible/  
```
Move into this directory:
```
cd /etc/ansible/  
```

🗂️ Step 8: Create Playbooks Folder 

Create a folder to store all Ansible playbooks:
```
sudo mkdir playbooks
cd playbooks  
```
✅ Ansible setup is now complete and ready for playbook creation 🎉


<h1>📘 Ansible Example  1 – Ping Playbook (Easy & Beginner Friendly) 🧠✨</h1>

🔍 What does the ping command do?  
The `ping` command is used to **check connectivity**.  
For example:
- `ping google.com` → checks internet connectivity 🌐  
- `ping localhost` → checks local machine connectivity 💻  

👉 Till now, we were checking connectivity **manually** using ping.  
Now we will do the **same thing using Ansible automation** ⚙️🤖.

---

🛠️ How will we do this in Ansible?  
We will write a **playbook (YAML file)** that performs the ping operation automatically.

---

🧑‍💻 Step 1: Create Local Workspace  
On your **local machine**, create a folder named **ansible**.  
This folder will act as your workspace.

📂 Open **Git Bash** inside this folder  
🧑‍🎨 Then open the folder in **VS Code**

---

📝 Step 2: Create Playbook File  
Inside VS Code, create a new file named:

`ping.yml`

Add the following content inside the file 👇
```
# ping command -> check connectivity
---

- name: Check the connectivity
  hosts: localhost
  tasks:
    - name: check the connectivity using ping command
      ansible.builtin.ping:
```

🧾 Step 3: Copy and Paste into Terminal

After creating the `ping.yml` file in VS Code,
save the file, then copy the file content
and paste it into the terminal where Ansible is installed.

This ensures that the playbook is available and ready to be executed from the terminal.

🧪 Step 4: Syntax Check (Like Terraform Plan)

In Terraform, before running `terraform apply`, we run `terraform plan`

to check whether:
- the syntax is correct
- everything is properly defined

Similarly, in Ansible, we use the following command to check for syntax errors before running the playbook:
```
ansible-playbook ping.yml --syntax-check
```

If no errors are displayed, it means the playbook syntax is correct and safe to run ✅

▶️ Step 5: Run the Playbook

After a successful syntax check, run the playbook using:
```
ansible-playbook ping.yml
```

If you have created a shortcut or alias, you can also run:
```
ap ping.yml
```

📊 Step 6: Verify Output

In Ansible, status codes are shown after a command or playbook is executed.<br>
After execution, if you see output like:
```
ok=2
```
✅ This means the task was executed successfully<br>
   and all defined tasks completed without any errors. 🎉



<h1>Ansible Example  2 –Create a folder using Ansible</h1>

```
---

- name: Create a file
  hosts: localhost
  tasks:
    - name: create ansible file
      ansible.builtin.file:
        path: /root/ansible.txt
        state: touch
```

<h1>⚡ Create a Shortcut (Alias) for Ansible Playbook  </h1>

If you do not want to type the full command every time,  
you can create a **shortcut (alias)** for it.

---

📝 Step 1: Open Profile File  
Open the system profile file using the command:

```
nano /etc/profile
```

---

➕ Step 2: Add Alias  
Scroll to the **bottom of the file** and add the following line:

```
alias ap='ansible-playbook'
```

This creates a shortcut where `ap` will work the same as `ansible-playbook`.

---

🔄 Step 3: Apply the Changes  
To apply the changes without restarting the system, run:

```
source /etc/profile
```

---

✅ Now you can run Ansible playbooks using the shortcut command:

```
ap ping.yml
```

This makes working with Ansible faster and easier 🚀😄

























