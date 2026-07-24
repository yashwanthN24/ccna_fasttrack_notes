# CCNA Fast Track - 02: VLANs (Virtual LANs)

> Goal: Understand why VLANs exist, how they reduce broadcast traffic, and how they improve security and network organization.

---

# What is a VLAN?

A VLAN (Virtual Local Area Network) is a logical separation of devices on the same physical switch.

Instead of buying multiple switches, you can divide one switch into multiple isolated networks.

Think of a VLAN as creating several "virtual switches" inside one physical switch.

Example:

                  Switch
        +----------------------+
        | VLAN 10 | VLAN 20    |
        | HR      | Finance    |
        +----------------------+

Although connected to the same switch, devices in different VLANs cannot communicate directly.

---

# Why Do We Need VLANs?

Imagine a company:

- HR Department
- Finance Department
- IT Department
- Guests

Without VLANs:

Everyone is in one network.

Problems:
- Too many broadcasts
- Poor performance
- No isolation
- Security risks

With VLANs:

HR  -> VLAN 10
Finance -> VLAN 20
IT -> VLAN 30
Guest -> VLAN 40

Each department becomes its own broadcast domain.

---

# Broadcast Domain

A broadcast domain is a group of devices that receive a broadcast frame.

Broadcast MAC:

```
FF:FF:FF:FF:FF:FF
```

Without VLANs:

```
PC1
PC2
PC3
PC4

   |
 Switch
```

If PC1 sends an ARP request, every PC receives it.

With VLANs:

```
VLAN10
PC1
PC2

VLAN20
PC3
PC4
```

Now:

ARP from PC1 reaches only PC2.

PC3 and PC4 never see it.

This reduces unnecessary traffic.

---

# VLAN IDs

Each VLAN has an ID.

Common examples:

```
1      Default VLAN
10     HR
20     Finance
30     IT
40     Guest
99     Management
999    Native/Unused (commonly used in labs)
```

Valid range:

```
1 - 4094
```

---

# Default VLAN

Every switch port belongs to VLAN 1 by default.

Example:

```
show vlan brief
```

Output:

Fa0/1 VLAN1

Fa0/2 VLAN1

Fa0/3 VLAN1

Until changed, every new device joins VLAN 1.

Best practice:
Avoid using VLAN 1 for user devices in production.

---

# Access Port

An access port belongs to exactly ONE VLAN.

Example:

PC

↓

Switch Port

↓

VLAN 10

Traffic leaving the port is **untagged** because end devices don't understand VLAN tags.

Cisco configuration:

```
interface fa0/1

switchport mode access

switchport access vlan 10
```

---

# VLAN Tagging (802.1Q)

Switches need a way to identify which VLAN a frame belongs to.

They insert a VLAN tag into Ethernet frames.

This is called:

```
IEEE 802.1Q
```

The tag contains the VLAN ID.

PCs never see these tags because access ports remove them before sending frames.

---

# Native VLAN

On a trunk link (covered next lesson), one VLAN is sent **without a tag**.

This is the Native VLAN.

Default:

```
VLAN 1
```

Best practice:

Change it to an unused VLAN (for example VLAN 999).

---

# Communication Rules

Same VLAN:

```
PC1 VLAN10

↓

Switch

↓

PC2 VLAN10

Works
```

Different VLANs:

```
PC1 VLAN10

↓

Switch

↓

PC2 VLAN20

Blocked
```

A Layer 3 device (router or Layer 3 switch) is required for communication between different VLANs.

This is called **Inter-VLAN Routing** (next topics).

---

# Why VLANs Improve Security

Without VLANs:

Everyone shares the same network.

An attacker can:

- Discover every device
- Broadcast attacks everywhere
- ARP spoof the whole LAN

With VLANs:

Attack surface is reduced.

Example:

Guest Wi-Fi cannot reach:

- Servers
- Employee laptops
- Printers

unless routing rules explicitly allow it.

---

# Cisco Commands

Show VLANs

```
show vlan brief
```

Create VLAN

```
configure terminal

vlan 10

name HR
```

Assign interface

```
interface fa0/1

switchport mode access

switchport access vlan 10
```

Delete VLAN

```
no vlan 10
```

---

# Packet Tracer Lab

Create:

- 1 Switch
- 4 PCs

Assign:

PC1 -> VLAN10

PC2 -> VLAN10

PC3 -> VLAN20

PC4 -> VLAN20

IP Addresses:

PC1 192.168.10.10/24

PC2 192.168.10.20/24

PC3 192.168.20.10/24

PC4 192.168.20.20/24

Test:

PC1 → PC2

Should work.

PC1 → PC3

Should fail.

Why?

Because switches do not route between VLANs.

---

# Cybersecurity Relevance

VLANs are everywhere:

- Office networks
- Data centers
- Universities
- Hospitals
- Banks

Common attacks:

- VLAN Hopping
- Double Tagging
- Switch Spoofing
- Native VLAN attacks

Defenses:

- Disable unused ports
- Change Native VLAN
- Disable DTP
- Use Port Security
- Separate management VLAN

We'll cover these in later lessons.

---

# Interview Questions

Q1. What is a VLAN?

Q2. Why do companies use VLANs?

Q3. What is a broadcast domain?

Q4. Can VLAN10 communicate with VLAN20?

Q5. What device enables communication between VLANs?

Q6. What is VLAN 1?

Q7. What is an access port?

Q8. What is IEEE 802.1Q?

Q9. What is the Native VLAN?

Q10. Why do VLANs improve security?

---

# Key Takeaways

✅ A VLAN creates a separate logical network.

✅ Each VLAN is its own broadcast domain.

✅ Devices in different VLANs cannot communicate without a Layer 3 device.

✅ Access ports belong to a single VLAN.

✅ VLAN tagging uses IEEE 802.1Q.

✅ VLANs improve performance, organization, and security.
