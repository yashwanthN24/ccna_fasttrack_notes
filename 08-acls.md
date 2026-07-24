# CCNA Fast Track - 08: Access Control Lists (ACLs)

> Goal: Learn how routers and Layer 3 switches filter network traffic.

---

# What is an ACL?

An Access Control List (ACL) is a set of rules that decides whether network traffic is allowed or blocked.

Think of an ACL as a security guard.

Every packet arriving at a router is checked against the ACL.

If it matches a "permit" rule → Allowed.

If it matches a "deny" rule → Dropped.

---

# Why Do We Need ACLs?

Imagine this network:

```
           Router
         /        \
    HR VLAN      Guest VLAN
```

Requirements:

- HR can access the file server.
- Guests can access the Internet.
- Guests cannot access HR.

ACLs enforce these rules.

---

# Types of ACLs

## 1. Standard ACL

Filters only by **Source IP Address**.

Example:

```
Permit:
192.168.10.0/24

Deny:
Everyone else
```

Use when you only care who is sending traffic.

---

## 2. Extended ACL

Filters by:

- Source IP
- Destination IP
- Protocol
- Port Number

Example:

Allow:

```
192.168.10.0 → Web Server TCP 443
```

Block:

```
192.168.20.0 → Database
```

Extended ACLs are much more powerful.

---

# ACL Processing

Rules are checked from top to bottom.

Example:

```
1 Permit HR

2 Deny Guest

3 Permit IT
```

As soon as one rule matches, processing stops.

Order matters.

---

# Implicit Deny

Every ACL ends with an invisible rule:

```
deny any
```

If no rule matches, the packet is dropped.

Always remember this.

---

# Wildcard Masks

Cisco ACLs use wildcard masks instead of subnet masks.

Rule:

```
0 = Must Match

1 = Ignore
```

Examples:

Subnet Mask:

```
255.255.255.0
```

Wildcard:

```
0.0.0.255
```

Examples:

One host:

```
192.168.10.5

Wildcard:

0.0.0.0
```

Entire /24 network:

```
192.168.10.0

Wildcard:

0.0.0.255
```

---

# Standard ACL Example

Allow only:

```
192.168.10.0/24
```

Configuration:

```
access-list 10 permit 192.168.10.0 0.0.0.255
```

Apply:

```
interface g0/0

ip access-group 10 in
```

---

# Extended ACL Example

Allow HTTPS only:

```
access-list 100 permit tcp any host 192.168.10.10 eq 443
```

Allow DNS:

```
access-list 100 permit udp any any eq 53
```

Deny Telnet:

```
access-list 100 deny tcp any any eq 23
```

Allow everything else:

```
access-list 100 permit ip any any
```

---

# Inbound vs Outbound

Inbound:

Packet checked **before** entering the router.

```
PC

↓

ACL

↓

Router
```

Outbound:

Packet checked **after** routing decision.

```
Router

↓

ACL

↓

Destination
```

---

# ACL Placement

Standard ACL:

Place close to the **Destination**.

Why?

Because it only knows the source.

Extended ACL:

Place close to the **Source**.

Why?

Block unwanted traffic before it crosses the network.

---

# Common Protocol Numbers

HTTP

```
80
```

HTTPS

```
443
```

SSH

```
22
```

Telnet

```
23
```

DNS

```
53
```

SMTP

```
25
```

FTP

```
21
```

ICMP

Ping

---

# Packet Flow

```
Packet arrives

↓

ACL Rule 1?

↓

No

↓

Rule 2?

↓

No

↓

Rule 3?

↓

Permit

↓

Forward Packet
```

If no rule matches:

```
Implicit Deny

↓

Drop Packet
```

---

# Verification Commands

Show ACLs:

```
show access-lists
```

Show interface:

```
show ip interface
```

Running config:

```
show running-config
```

---

# Packet Tracer Lab

Network:

```
HR

Guest

Server

Router
```

Create ACL:

Allow:

HR → Server

Deny:

Guest → Server

Allow:

Everyone → Internet

Test:

```
ping

web browser

ssh
```

Observe which packets succeed and which are blocked.

---

# Common Mistakes

❌ Forgetting:

```
permit ip any any
```

Everything gets blocked.

---

❌ Wrong wildcard mask.

---

❌ Applying ACL on the wrong interface.

---

❌ Wrong direction:

"in"

vs

"out"

---

❌ Rules in the wrong order.

Remember:

First match wins.

---

# Cybersecurity Relevance

ACLs are used everywhere:

- Firewalls
- Routers
- Layer 3 Switches
- Cloud Security Groups
- AWS NACLs
- Azure NSGs

Knowing ACLs helps understand enterprise network security.

---

# Interview Questions

Q1. What is an ACL?

Q2. Difference between Standard and Extended ACL?

Q3. What is an implicit deny?

Q4. Why does rule order matter?

Q5. Difference between inbound and outbound ACLs?

Q6. What is a wildcard mask?

Q7. Which ACL should be placed near the source?

Q8. Which protocol uses TCP port 443?

Q9. Which command displays ACLs?

Q10. Why are ACLs important for cybersecurity?

---

# Key Takeaways

✅ ACLs filter network traffic.

✅ Standard ACLs filter only Source IP.

✅ Extended ACLs filter Source, Destination, Protocol and Ports.

✅ Rules are processed top to bottom.

✅ First match wins.

✅ Every ACL ends with an implicit "deny any".

✅ Standard ACLs go near the destination.

✅ Extended ACLs go near the source.
