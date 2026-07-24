# CCNA Fast Track - 05: Inter-VLAN Routing

> Goal: Learn how devices in different VLANs communicate using a Router or Layer 3 Switch.

---

# Why Can't Different VLANs Communicate?

Remember:

Each VLAN is a separate Layer 2 network.

Example:

VLAN10

PC1 → 192.168.10.10

PC2 → 192.168.10.20

These can communicate.

---

VLAN20

PC3 → 192.168.20.10

PC4 → 192.168.20.20

These can communicate.

---

But:

PC1 → PC3 ❌

Why?

Because a Layer 2 switch does **not** route packets between different IP networks.

---

# The Solution

Use a Layer 3 device.

Either:

- Router
- Layer 3 Switch

These devices make routing decisions using IP addresses.

---

# Default Gateway

Every PC needs a default gateway.

Think of it like this:

"If I don't know where the destination is, send the packet to the gateway."

Example:

PC

IP: 192.168.10.10

Mask: 255.255.255.0

Gateway:

192.168.10.1

---

# Packet Flow

PC1 wants to reach:

192.168.20.10

Step 1

PC1 checks:

Is destination in my subnet?

No.

Step 2

Send packet to:

Default Gateway

192.168.10.1

Step 3

Router receives packet.

Step 4

Router looks at routing table.

Step 5

Router forwards packet into VLAN20.

PC3 receives packet.

---

# Router-on-a-Stick (ROAS)

Instead of using one router interface per VLAN,

we use:

ONE physical interface

↓

Many logical subinterfaces.

Example:

```
Switch ===== Trunk ===== Router

                 |
     G0/0.10  VLAN10
     G0/0.20  VLAN20
     G0/0.30  VLAN30
```

The link between switch and router **must be a trunk** because it carries multiple VLANs.

---

# Router Configuration

Enable interface:

```
interface g0/0

no shutdown
```

Create VLAN10 subinterface:

```
interface g0/0.10

encapsulation dot1Q 10

ip address 192.168.10.1 255.255.255.0
```

Create VLAN20:

```
interface g0/0.20

encapsulation dot1Q 20

ip address 192.168.20.1 255.255.255.0
```

Now the router can route between VLAN10 and VLAN20.

---

# Switch Configuration

Trunk toward router:

```
interface g0/1

switchport mode trunk
```

That's all.

---

# Layer 3 Switch

Enterprise networks usually use Layer 3 switches.

Instead of using subinterfaces,

the switch creates:

SVIs

(Switched Virtual Interfaces)

Example:

```
interface vlan 10

ip address 192.168.10.1 255.255.255.0

no shutdown
```

Enable routing:

```
ip routing
```

Done.

The switch now routes between VLANs itself.

---

# Router vs Layer 3 Switch

Router

✔ WAN support

✔ Internet connectivity

✔ Better for branch offices

Slower for LAN routing

---

Layer 3 Switch

✔ Very fast

✔ Hardware routing

✔ Used in enterprises

✔ Better for campus LANs

---

# Packet Tracer Lab

Topology:

PC1

↓

Switch

↓

Router

↓

Switch

↓

PC2

Create:

VLAN10

VLAN20

Assign:

PC1

192.168.10.10

Gateway

192.168.10.1

PC2

192.168.20.10

Gateway

192.168.20.1

Configure:

Switch trunk

Router subinterfaces

Ping:

PC1 → PC2

Should work.

---

# Verification Commands

Router:

```
show ip interface brief

show running-config

show ip route
```

Switch:

```
show vlan brief

show interfaces trunk
```

PC:

```
ipconfig

ping

arp -a
```

---

# Common Problems

❌ Wrong default gateway

❌ Router interface shutdown

❌ Missing dot1Q encapsulation

❌ Trunk not configured

❌ Wrong VLAN assignment

❌ Wrong subnet mask

---

# Cybersecurity Relevance

Inter-VLAN routing is where security policies are enforced.

Examples:

Finance

↓

Can access Database

Guest Wi-Fi

↓

Internet Only

Blocked from Servers

ACLs (next lesson) control this traffic.

---

# Interview Questions

Q1. Why can't different VLANs communicate?

Q2. What is a default gateway?

Q3. What is Router-on-a-Stick?

Q4. Why is a trunk required?

Q5. What is a subinterface?

Q6. What does `encapsulation dot1Q` do?

Q7. Difference between Router and Layer 3 Switch?

Q8. What is an SVI?

Q9. Why enable `ip routing`?

Q10. Where are security policies usually applied?

---

# Key Takeaways

✅ VLANs are separate IP networks.

✅ Different VLANs require Layer 3 routing.

✅ Every PC needs a default gateway.

✅ Router-on-a-Stick uses one trunk and multiple subinterfaces.

✅ Layer 3 switches route much faster than routers inside a LAN.

✅ ACLs are commonly used to control traffic between VLANs.
