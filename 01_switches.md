# CCNA Fast Track - 01: Ethernet Switches

> Goal: Understand how switches forward traffic inside a LAN and why they are the backbone of modern networks.

---

# What is a Switch?

A switch is a Layer 2 (Data Link Layer) device that connects devices within the same Local Area Network (LAN).

Unlike a hub, a switch sends frames **only to the intended destination**, making the network much faster and more secure.

Example:

Laptop A ----\
              \
Laptop B ------> Switch ------ Printer
              /
Laptop C ----/

Every device is connected to a different switch port.

---

# Why not use a Hub?

Hub:
- Sends data to every device.
- Causes collisions.
- Shares bandwidth.
- Easy to sniff traffic.

Switch:
- Sends data only to the destination device.
- No unnecessary traffic.
- Dedicated bandwidth per port.
- Better performance and security.

---

# MAC Address

Every Network Interface Card (NIC) has a unique 48-bit MAC address.

Example:

```
00:1A:2B:3C:4D:5E
```

MAC addresses operate at Layer 2.

Think of it as a permanent house number for a network card.

---

# MAC Address Table (CAM Table)

A switch learns which MAC address is connected to which port.

Example:

| MAC Address | Port |
|-------------|------|
| AA:AA:AA... | Fa0/1 |
| BB:BB:BB... | Fa0/2 |
| CC:CC:CC... | Fa0/3 |

The switch builds this table automatically.

Command:

```
show mac address-table
```

---

# How a Switch Learns

Suppose:

PC A → Port 1

PC B → Port 2

Step 1

PC A sends a frame.

Switch learns:

```
AA -> Port1
```

Step 2

Destination MAC is unknown.

Switch floods the frame to every port except Port1.

Step 3

PC B replies.

Switch learns:

```
BB -> Port2
```

Now communication becomes direct.

No more flooding.

---

# Unknown Unicast Flooding

If the destination MAC isn't in the MAC table:

Switch sends the frame to all ports except the incoming port.

This happens only until the destination replies.

---

# Broadcast Frames

Broadcast MAC:

```
FF:FF:FF:FF:FF:FF
```

Broadcasts are sent to every device in the VLAN.

Examples:
- ARP Request
- DHCP Discover

---

# Unicast

One sender → One receiver

Most traffic is unicast.

Example:
Opening YouTube.

---

# Multicast

One sender → Multiple interested receivers.

Examples:
- IPTV
- Video conferencing
- Routing protocols

---

# Collision Domain

Every switch port is its own collision domain.

Example:

PC1 ----|
         |
PC2 ---- Switch

PC1 and PC2 cannot collide because each has a dedicated port.

---

# Broadcast Domain

By default,

All switch ports belong to one broadcast domain.

VLANs divide broadcast domains.

(We'll study VLANs next.)

---

# Duplex Modes

Half Duplex
- One direction at a time.

Full Duplex
- Send and receive simultaneously.

Modern switches use Full Duplex.

Command:

```
show interfaces
```

---

# Switch Forwarding Process

Frame arrives

↓

Read Source MAC

↓

Learn Source MAC

↓

Check Destination MAC

↓

Known?

YES → Forward only to correct port.

NO → Flood.

---

# Cisco Commands

View MAC table

```
show mac address-table
```

View interfaces

```
show interfaces status
```

View running configuration

```
show running-config
```

Show interface information

```
show interface GigabitEthernet0/1
```

---

# Cybersecurity Relevance

Attackers often abuse switches.

Examples:

- MAC Flooding Attack
- CAM Table Overflow
- ARP Spoofing
- VLAN Hopping (later)
- Rogue Switches

Blue teams monitor switch logs.

Red teams often exploit Layer 2 weaknesses after initial access.

---

# Packet Tracer Lab

Create:

PC1
PC2
PC3

↓

Connect all to one switch.

Open Command Prompt.

PC1

```
ping PC2
```

On the switch:

```
show mac address-table
```

Observe how MAC addresses appear after communication.

Clear the table:

```
clear mac address-table dynamic
```

Ping again.

Watch the learning process repeat.

---

# Interview Questions

Q1. Difference between Hub and Switch?

Q2. What is a MAC address?

Q3. What is a CAM table?

Q4. Why does a switch flood unknown traffic?

Q5. What is a collision domain?

Q6. What is a broadcast domain?

Q7. Which layer does a switch operate on?

Q8. Why is full duplex better?

Q9. What is the broadcast MAC address?

Q10. How does a switch learn MAC addresses?

---

# Key Takeaways

✅ Switches work at Layer 2.

✅ Switches forward frames using MAC addresses.

✅ Switches automatically build a CAM table.

✅ Unknown destinations are flooded.

✅ Broadcasts reach every device in the VLAN.

✅ Each switch port is its own collision domain.

✅ VLANs create separate broadcast domains.
