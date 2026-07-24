# CCNA Fast Track - 10: DHCP (Dynamic Host Configuration Protocol)

> Goal: Learn how devices automatically receive IP configuration when they join a network.

---

# What is DHCP?

DHCP (Dynamic Host Configuration Protocol) automatically provides network settings to clients.

Instead of manually configuring every device, a DHCP server assigns:

- IP Address
- Subnet Mask
- Default Gateway
- DNS Server
- Lease Time

Without DHCP, network administration becomes difficult in medium and large networks.

---

# Why Do We Need DHCP?

Without DHCP:

Imagine a company with 500 laptops.

Each laptop requires:

- IP Address
- Subnet Mask
- Gateway
- DNS Server

Configuring each device manually is slow and error-prone.

With DHCP:

The device connects to the network and receives its configuration automatically.

---

# DHCP Components

## DHCP Client

A device requesting network configuration.

Examples:

- Laptop
- Phone
- Desktop
- Smart TV

---

## DHCP Server

The device assigning IP addresses.

Examples:

- Windows Server
- Linux Server
- Home Router
- Cisco Router

---

# DHCP Lease

A DHCP address is usually **leased**, not permanently assigned.

Example:

Lease Time:

```
24 Hours
```

When the lease is close to expiring, the client requests a renewal.

If renewed, it usually keeps the same IP address.

---

# DORA Process

The DHCP process consists of four steps.

### 1. Discover

The client does not have an IP address.

It sends a **broadcast** asking:

> "Is there a DHCP server?"

```
DHCP Discover
```

---

### 2. Offer

The DHCP server replies:

> "I can give you this IP."

Example:

```
192.168.1.100
```

```
DHCP Offer
```

---

### 3. Request

The client replies:

> "I want that IP."

```
DHCP Request
```

---

### 4. Acknowledge

The server confirms.

```
DHCP ACK
```

Now the client can communicate.

---

# DORA Summary

```
Client

↓

Discover

↓

Server

↓

Offer

↓

Client

↓

Request

↓

Server

↓

ACK
```

Remember:

**DORA**

Discover

Offer

Request

Acknowledge

---

# DHCP Scope

A scope is the pool of IP addresses the server can assign.

Example:

```
192.168.1.100

↓

192.168.1.200
```

Devices receive addresses only from this range.

---

# Excluded Addresses

Some addresses should never be assigned dynamically.

Example:

```
192.168.1.1

Router

192.168.1.2

Server

192.168.1.3

Printer
```

These are excluded from the DHCP pool.

---

# DHCP Reservation

A reservation always gives the same IP address to a specific device.

Based on:

MAC Address

Example:

Printer

↓

Always receives:

```
192.168.1.10
```

Useful for:

- Printers
- Servers
- Cameras
- VoIP Phones

---

# DHCP Relay

DHCP broadcasts do not cross routers.

Suppose:

```
Client

↓

Router

↓

DHCP Server
```

The broadcast stops at the router.

Solution:

DHCP Relay

Cisco:

```
ip helper-address 192.168.20.10
```

The router forwards DHCP requests to the remote DHCP server.

---

# Cisco Router as DHCP Server

Exclude addresses:

```
ip dhcp excluded-address 192.168.1.1 192.168.1.20
```

Create a pool:

```
ip dhcp pool OFFICE
```

Network:

```
network 192.168.1.0 255.255.255.0
```

Gateway:

```
default-router 192.168.1.1
```

DNS:

```
dns-server 8.8.8.8
```

---

# Verification Commands

Show DHCP bindings:

```
show ip dhcp binding
```

Show DHCP pool:

```
show ip dhcp pool
```

---

# Packet Flow

```
Laptop

↓

DHCP Discover (Broadcast)

↓

Router/Home Router

↓

DHCP Offer

↓

Laptop

↓

DHCP Request

↓

Server

↓

DHCP ACK

↓

Laptop receives IP
```

---

# Packet Tracer Lab

Topology:

```
PC1

PC2

Switch

Router (DHCP Server)
```

Configure:

- DHCP Pool
- Gateway
- DNS
- Excluded Addresses

On each PC:

Choose:

```
DHCP
```

Verify:

```
ipconfig
```

Both PCs should automatically receive IP addresses.

---

# Common Problems

❌ DHCP pool exhausted.

❌ Wrong subnet mask.

❌ Missing default gateway.

❌ Missing relay agent.

❌ DHCP service disabled.

---

# Cybersecurity Relevance

Common attacks:

### Rogue DHCP Server

An attacker connects a fake DHCP server.

Clients receive:

- Wrong Gateway
- Wrong DNS
- Wrong IP

Traffic can then be intercepted.

---

### DHCP Starvation

The attacker repeatedly requests new IP addresses until the DHCP pool is exhausted.

Legitimate users can no longer obtain an IP address.

---

# DHCP Snooping

Cisco switches can protect against rogue DHCP servers.

Features:

- Trusted Ports
- Untrusted Ports
- Drops fake DHCP responses

Very common in enterprise networks.

---

# Interview Questions

Q1. What is DHCP?

Q2. What information does DHCP provide?

Q3. Explain the DORA process.

Q4. What is a DHCP lease?

Q5. What is a DHCP reservation?

Q6. Why is DHCP Relay needed?

Q7. What command configures a relay agent?

Q8. What is DHCP Snooping?

Q9. What is a Rogue DHCP Server?

Q10. What command shows DHCP bindings?

---

# Key Takeaways

✅ DHCP automatically assigns IP configuration.

✅ The DORA process is Discover → Offer → Request → ACK.

✅ IP addresses are leased, not permanently assigned.

✅ Reservations assign the same IP to specific devices.

✅ DHCP Relay allows clients to use a DHCP server on another network.

✅ DHCP Snooping protects against rogue DHCP servers.
