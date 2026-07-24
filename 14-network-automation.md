# CCNA Fast Track - 14: Network Automation

> Goal: Understand how modern networks are managed using APIs, Python, and automation instead of manual CLI configuration.

---

# Why Network Automation?

Imagine managing:

- 5 routers → Easy
- 50 routers → Difficult
- 5,000 routers → Impossible manually

Instead of logging into every device, automation configures all devices at once.

Example:

Without automation:

```
SSH → Router1
SSH → Router2
SSH → Router3
...
SSH → Router500
```

With automation:

```
Python/Ansible Script

↓

All Routers Updated Automatically
```

---

# Traditional Networking

Network Engineer:

```
SSH

↓

Router

↓

CLI Commands
```

Problems:

- Slow
- Human errors
- Difficult to repeat
- Hard to audit

---

# Modern Networking

Automation Server

↓

API

↓

Router

↓

Configuration Applied

Benefits:

- Faster
- Repeatable
- Consistent
- Easy to audit

---

# APIs

API = Application Programming Interface.

An API allows software to communicate with another application.

Instead of typing CLI commands, your program sends requests.

Example:

```
Python

↓

REST API

↓

Router
```

---

# REST API

REST is the most common API style.

Common HTTP methods:

```
GET
```

Retrieve information.

```
POST
```

Create.

```
PUT
```

Replace.

```
PATCH
```

Update.

```
DELETE
```

Remove.

---

# JSON

Most APIs exchange data in JSON.

Example:

```json
{
  "hostname": "R1",
  "ip": "192.168.1.1",
  "status": "up"
}
```

JSON is lightweight and easy for humans and programs to read.

---

# YAML

YAML is commonly used for configuration files.

Example:

```yaml
hostname: R1

ip: 192.168.1.1

interfaces:
  - Gig0/0
  - Gig0/1
```

Tools like Ansible use YAML.

---

# Python

Python is the most popular language for network automation.

Typical tasks:

- Collect device information
- Configure routers
- Backup configurations
- Generate reports
- Monitor network health

Popular libraries:

- Netmiko
- Paramiko
- NAPALM
- Requests

---

# Ansible

Ansible is an automation tool.

Advantages:

- Agentless (uses SSH)
- Simple YAML playbooks
- Easy to learn
- Widely used

Example workflow:

```
Playbook

↓

SSH

↓

100 Routers

↓

Configuration Applied
```

---

# Infrastructure as Code (IaC)

Instead of configuring devices manually, store configurations as code.

Benefits:

- Version control (Git)
- Easy rollback
- Code review
- Automation

Common tools:

- Terraform
- Ansible

---

# Software-Defined Networking (SDN)

Traditional networking:

Every switch makes decisions independently.

SDN:

A central controller manages all network devices.

Example:

```
Controller

↓

Switch 1

↓

Switch 2

↓

Switch 3
```

Changes are made once on the controller and pushed everywhere.

---

# Cisco DNA Center

Cisco's SDN platform.

Features:

- Device management
- Automation
- Network monitoring
- Configuration deployment
- Security policy management

---

# Git and Version Control

Network configurations should be stored in Git.

Benefits:

- Track changes
- Roll back mistakes
- Collaborate with teams
- Audit who changed what

---

# Automation Workflow

```
Git Repository

↓

Ansible Playbook

↓

Python Script

↓

REST API

↓

Network Devices
```

This is common in enterprise environments.

---

# Cybersecurity Relevance

Automation helps security teams:

- Push firewall rules
- Rotate passwords
- Collect logs
- Audit configurations
- Detect policy violations
- Respond to incidents quickly

Example:

Instead of manually blocking a malicious IP on 300 firewalls, an automation script updates all of them in minutes.

---

# Packet Tracer Lab

Packet Tracer has limited automation support.

Instead, practice:

1. Configure two routers manually.
2. Export their configurations.
3. Compare differences.
4. Imagine automating those changes with Ansible or Python.

Later, in GNS3 or EVE-NG, you can automate real network devices.

---

# Common Mistakes

❌ Hardcoding passwords in scripts.

❌ Making changes directly on production devices.

❌ Not testing automation.

❌ Not storing configurations in Git.

---

# Interview Questions

Q1. Why is network automation important?

Q2. What is an API?

Q3. What is REST?

Q4. Difference between JSON and YAML?

Q5. Why is Python popular for networking?

Q6. What is Ansible?

Q7. What is Infrastructure as Code?

Q8. What is SDN?

Q9. What is Cisco DNA Center?

Q10. Why store configurations in Git?

---

# Key Takeaways

✅ Automation reduces manual work and errors.

✅ APIs allow software to manage network devices.

✅ REST APIs commonly use JSON.

✅ YAML is widely used for automation configuration.

✅ Python is the leading language for network automation.

✅ Ansible automates configuration over SSH.

✅ Git provides version control for network configurations.

✅ SDN centralizes network management.
