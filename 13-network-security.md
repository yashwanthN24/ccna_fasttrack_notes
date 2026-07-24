# CCNA Fast Track - 13: Network Security

> Goal: Learn the core security mechanisms used to protect enterprise networks.

---

# What is Network Security?

Network security is the practice of protecting:

- Devices
- Users
- Data
- Network services

from unauthorized access, attacks, and misuse.

Security follows the **CIA Triad**:

- Confidentiality → Only authorized users can access data.
- Integrity → Data cannot be modified without permission.
- Availability → Systems remain accessible.

---

# Network Security Layers

```
Internet
     │
Firewall
     │
Router
     │
Switch
     │
Access Point
     │
Endpoints
```

Security should exist at every layer.

---

# Port Security

Normally, any device can connect to a switch port.

Port Security limits which MAC addresses are allowed.

Example:

```
Fa0/1

Allowed MAC:
AA:BB:CC:DD:EE:FF
```

If another device connects:

```
Violation
```

Possible actions:

- Protect
- Restrict
- Shutdown (most common)

Cisco:

```
interface fa0/1

switchport mode access

switchport port-security

switchport port-security maximum 1

switchport port-security violation shutdown

switchport port-security mac-address sticky
```

Sticky learns the first MAC automatically and saves it.

---

# SSH vs Telnet

## Telnet

- Port 23
- Plain text
- Password visible
- Never use in production

---

## SSH

- Port 22
- Encrypted
- Secure remote management

Always prefer SSH.

Cisco:

```
ip domain-name lab.local

crypto key generate rsa

username admin secret StrongPassword

line vty 0 4

transport input ssh

login local
```

---

# AAA

AAA stands for:

Authentication

Authorization

Accounting

Authentication:

Who are you?

Authorization:

What can you do?

Accounting:

What did you do?

Large organizations often use:

- RADIUS
- TACACS+

---

# VPN

VPN = Virtual Private Network

Creates an encrypted tunnel over the Internet.

Example:

```
Laptop

↓

Encrypted Tunnel

↓

Company Firewall

↓

Internal Network
```

Common VPNs:

- IPsec
- SSL VPN
- WireGuard
- OpenVPN

---

# Firewalls

A firewall filters traffic between networks.

Example:

```
Internet

↓

Firewall

↓

Internal LAN
```

Rules:

Allow:

```
HTTPS
```

Block:

```
Telnet
```

Firewalls inspect traffic before allowing it through.

---

# IDS vs IPS

## IDS

Intrusion Detection System

- Detects attacks
- Generates alerts
- Does not block traffic

---

## IPS

Intrusion Prevention System

- Detects attacks
- Blocks malicious traffic automatically

---

# Network Segmentation

Instead of placing every device in one network:

Create separate VLANs.

Example:

```
HR

Finance

Servers

Guests
```

Advantages:

- Limits attack spread
- Improves performance
- Easier access control

---

# Secure Device Management

Always:

✔ Change default passwords.

✔ Disable unused ports.

✔ Disable unused services.

✔ Use SSH instead of Telnet.

✔ Keep firmware updated.

✔ Back up configurations.

---

# Common Layer 2 Attacks

## MAC Flooding

Attacker floods fake MAC addresses.

Result:

CAM table overflow.

Switch behaves like a hub.

Defense:

Port Security.

---

## ARP Spoofing

Attacker sends fake ARP replies.

Traffic is redirected through the attacker.

Defense:

Dynamic ARP Inspection (DAI)

DHCP Snooping

Static ARP (limited use)

---

## DHCP Starvation

Attacker consumes all DHCP addresses.

Defense:

DHCP Snooping

Port Security

---

## Rogue DHCP Server

Fake DHCP server gives clients:

- Wrong Gateway
- Wrong DNS

Defense:

DHCP Snooping

---

## VLAN Hopping

Attacker gains access to another VLAN.

Defense:

- Disable DTP
- Change Native VLAN
- Configure access ports correctly

---

# Physical Security

Always protect:

- Switches
- Routers
- Server racks
- Network closets

Physical access often means complete compromise.

---

# Security Best Practices

✔ Principle of Least Privilege

✔ Strong passwords

✔ Multi-Factor Authentication (MFA)

✔ Regular updates

✔ Log monitoring

✔ Network segmentation

✔ Secure backups

✔ Disable unused services

✔ Monitor network traffic

---

# Verification Commands

Show Port Security:

```
show port-security
```

Show SSH:

```
show ip ssh
```

Show Active Sessions:

```
show users
```

Show Interface Status:

```
show interfaces status
```

---

# Packet Tracer Lab

Configure:

- Port Security
- SSH
- VLANs
- ACLs

Test:

- Connect another laptop to a secured port.
- Verify the port shuts down.
- Log in using SSH.
- Confirm Telnet is disabled.

---

# Common Mistakes

❌ Leaving default passwords.

❌ Using Telnet.

❌ No VLAN segmentation.

❌ Unsecured management interfaces.

❌ Ignoring firmware updates.

---

# Interview Questions

Q1. What is Port Security?

Q2. What is Sticky MAC?

Q3. SSH vs Telnet?

Q4. Explain AAA.

Q5. IDS vs IPS?

Q6. What is a VPN?

Q7. How does ARP Spoofing work?

Q8. What is DHCP Snooping?

Q9. What is VLAN Hopping?

Q10. Why is network segmentation important?

---

# Key Takeaways

✅ Use SSH instead of Telnet.

✅ Port Security prevents unauthorized devices.

✅ AAA controls authentication, authorization, and accounting.

✅ Firewalls filter traffic.

✅ IDS detects attacks; IPS detects and blocks them.

✅ VLANs improve both security and performance.

✅ Layer 2 attacks can be mitigated using features like DHCP Snooping, DAI, and Port Security.
