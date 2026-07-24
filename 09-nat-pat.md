# CCNA Fast Track - 09: NAT & PAT (Network Address Translation)

> Goal: Understand how private devices access the Internet using public IP addresses.

---

# Why Do We Need NAT?

Private IP addresses cannot be routed on the public Internet.

Examples:

```
192.168.1.10

10.0.0.25

172.16.5.100
```

If your laptop sends packets directly to Google with one of these addresses, Internet routers will drop them.

A router or firewall must translate the private address into a public address.

This process is called **Network Address Translation (NAT).**

---

# Private vs Public IP

Private IP ranges:

```
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16
```

Public IP:

Assigned by your ISP.

Example:

```
49.205.88.101
```

Every website on the Internet sees your public IP, not your private IP.

---

# Basic NAT Example

Home network:

```
Laptop
192.168.1.10
      │
Phone
192.168.1.20
      │
Printer
192.168.1.30
      │
Home Router
Private: 192.168.1.1
Public : 49.205.88.101
      │
Internet
```

When the laptop opens `google.com`:

Before NAT:

```
Source:
192.168.1.10
```

After NAT:

```
Source:
49.205.88.101
```

Google replies to the public IP, and the router translates the packet back to the laptop.

---

# Types of NAT

## 1. Static NAT

One private IP maps permanently to one public IP.

Example:

```
192.168.1.10

↓

49.205.88.101
```

Used for:

- Public web servers
- Mail servers
- VPN gateways

---

## 2. Dynamic NAT

Private IPs are translated using a **pool of public IP addresses**.

Example:

Public IP Pool:

```
49.205.88.101

49.205.88.102

49.205.88.103
```

A device receives a public IP only while communicating.

Less common today.

---

## 3. PAT (Port Address Translation)

Also called:

- NAT Overload

Many private devices share **one public IP**.

Example:

```
Laptop
192.168.1.10

↓

49.205.88.101:45001

Phone
192.168.1.20

↓

49.205.88.101:45002

TV
192.168.1.30

↓

49.205.88.101:45003
```

The router keeps a translation table using port numbers.

This is how almost all home routers work.

---

# NAT Translation Table

The router maintains a table similar to:

| Inside Local | Inside Global |
|--------------|---------------|
|192.168.1.10:51524|49.205.88.101:45001|
|192.168.1.20:49321|49.205.88.101:45002|

The router uses this table to return packets to the correct device.

---

# Inside and Outside

Inside Local:

Private IP of your device.

Example:

```
192.168.1.10
```

Inside Global:

Public IP representing your device on the Internet.

Example:

```
49.205.88.101
```

Outside Global:

Public IP of the remote server.

Example:

Google's server IP.

---

# Packet Flow

Laptop:

```
192.168.1.10
```

↓

Router performs PAT

↓

```
49.205.88.101:45001
```

↓

Google

↓

Reply:

```
49.205.88.101:45001
```

↓

Router checks NAT table

↓

Forwards to:

```
192.168.1.10
```

---

# Cisco Configuration (PAT)

Mark interfaces:

```
interface g0/0
ip nat inside

interface g0/1
ip nat outside
```

Create ACL for inside network:

```
access-list 1 permit 192.168.1.0 0.0.0.255
```

Enable PAT:

```
ip nat inside source list 1 interface g0/1 overload
```

---

# Verification Commands

Show NAT translations:

```
show ip nat translations
```

Show NAT statistics:

```
show ip nat statistics
```

---

# Packet Tracer Lab

Topology:

```
PC1

PC2

Switch

Router

Internet Server
```

Configure:

- Private LAN
- Public interface
- PAT

Generate traffic:

```
ping

web browser
```

Run:

```
show ip nat translations
```

Observe new entries appear in the NAT table.

---

# Common Problems

❌ Wrong inside/outside interface.

❌ Missing ACL.

❌ No overload keyword.

❌ Missing default route.

❌ ISP link down.

---

# Advantages of NAT

✔ Conserves public IPv4 addresses.

✔ Hides internal IP addresses.

✔ Allows many devices to share one public IP.

✔ Easy Internet access for private networks.

---

# Disadvantages of NAT

✘ Breaks true end-to-end connectivity.

✘ Some applications require port forwarding.

✘ Adds processing overhead.

✘ Makes troubleshooting slightly harder.

---

# NAT vs PAT

| NAT | PAT |
|------|-----|
| One-to-one translation | Many-to-one translation |
| Uses multiple public IPs | Usually one public IP |
| Less common | Most common today |
| Server publishing | Home/Office Internet |

---

# Cybersecurity Relevance

NAT provides **address hiding**, but it is **not a firewall**.

A firewall inspects and filters traffic.

NAT only changes IP addresses (and ports in PAT).

Common concepts:

- Port Forwarding
- DMZ
- Home routers
- Corporate firewalls
- Cloud NAT

Understanding NAT is essential when troubleshooting VPNs, reverse shells, or remote access.

---

# Interview Questions

Q1. What problem does NAT solve?

Q2. Difference between NAT and PAT?

Q3. Why are private IPs not routable on the Internet?

Q4. What is NAT Overload?

Q5. What is Static NAT used for?

Q6. What command shows NAT translations?

Q7. Does NAT provide firewall protection?

Q8. What is the difference between Inside Local and Inside Global?

Q9. Why is PAT widely used?

Q10. Why was NAT introduced?

---

# Key Takeaways

✅ NAT translates private IP addresses into public IP addresses.

✅ PAT allows many devices to share one public IP using different port numbers.

✅ Home routers almost always use PAT (NAT Overload).

✅ NAT hides internal addressing but does not replace a firewall.

✅ The NAT translation table tracks active connections.
