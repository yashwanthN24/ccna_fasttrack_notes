# CCNA Fast Track - 06: Static Routing

> Goal: Learn how routers communicate with other networks using static routes.

---

# What is Routing?

Routing is the process of forwarding packets from one network to another.

Unlike switches, routers make decisions using **IP addresses**, not MAC addresses.

Example:

```
PC1 ---- Router ---- Router ---- PC2
```

PC1 and PC2 are on different networks.

The routers decide the best path.

---

# Routing Table

Every router has a routing table.

Think of it like Google Maps.

It answers one question:

> "Which interface should I use to reach the destination network?"

View it:

```
show ip route
```

Example:

```
192.168.10.0/24 -> Gig0/0
192.168.20.0/24 -> Gig0/1
0.0.0.0/0       -> 10.0.0.2
```

---

# Directly Connected Networks

When you configure an IP address on a router interface, the router automatically learns that network.

Example:

```
interface g0/0
ip address 192.168.10.1 255.255.255.0
```

The router automatically adds:

```
192.168.10.0/24 is directly connected
```

No static route is needed.

---

# Why Do We Need Static Routes?

Suppose:

```
LAN A ---- R1 ---- R2 ---- LAN B
```

R1 knows only LAN A.

R2 knows only LAN B.

How does R1 reach LAN B?

You manually tell it.

That's a **Static Route**.

---

# Static Route Syntax

```
ip route <destination-network> <subnet-mask> <next-hop-IP>
```

Example:

```
ip route 192.168.20.0 255.255.255.0 10.0.0.2
```

Meaning:

"To reach 192.168.20.0/24, send packets to router 10.0.0.2."

---

# Example Network

```
LAN1

192.168.10.0/24

      |

R1

10.0.0.1

========

10.0.0.2

R2

      |

LAN2

192.168.20.0/24
```

R1:

```
ip route 192.168.20.0 255.255.255.0 10.0.0.2
```

R2:

```
ip route 192.168.10.0 255.255.255.0 10.0.0.1
```

Now both LANs can communicate.

---

# Default Route

Instead of adding many routes, create one "catch-all" route.

```
0.0.0.0/0
```

This is the **Default Route**.

Cisco:

```
ip route 0.0.0.0 0.0.0.0 10.0.0.2
```

Meaning:

"If I don't know the destination, send it to 10.0.0.2."

Home routers usually have a default route pointing to the ISP.

---

# Next Hop vs Exit Interface

### Next Hop

```
ip route 192.168.20.0 255.255.255.0 10.0.0.2
```

Router forwards to another router's IP.

---

### Exit Interface

```
ip route 192.168.20.0 255.255.255.0 g0/1
```

Router sends packets directly out that interface.

Next-hop routes are generally preferred on Ethernet networks.

---

# Longest Prefix Match

A router always chooses the **most specific** route.

Example:

```
192.168.0.0/16

192.168.10.0/24
```

Packet:

```
192.168.10.50
```

The router chooses:

```
192.168.10.0/24
```

because `/24` is more specific than `/16`.

This is called **Longest Prefix Match**.

---

# Packet Flow

PC1 wants to reach:

```
192.168.20.10
```

Flow:

```
PC1

↓

Default Gateway

↓

R1

↓

Routing Table

↓

Static Route

↓

R2

↓

Destination LAN

↓

PC2
```

Every router repeats this process until the destination is reached.

---

# Packet Tracer Lab

Topology:

```
PC1 --- R1 --- R2 --- PC2
```

Networks:

```
192.168.10.0/24

10.0.0.0/30

192.168.20.0/24
```

Configure:

- Router IP addresses
- Static routes
- Default gateways on PCs

Test:

```
ping
```

Then verify:

```
show ip route
```

---

# Verification Commands

Show routing table:

```
show ip route
```

Show interfaces:

```
show ip interface brief
```

Ping another router:

```
ping 10.0.0.2
```

Trace packet path:

```
traceroute 192.168.20.10
```

---

# Common Problems

❌ Wrong next-hop IP

❌ Interface shutdown

❌ Missing return route

❌ Wrong subnet mask

❌ Wrong default gateway on PC

Remember:

Communication is **two-way**.

If only one router has a route, replies cannot return.

---

# Cybersecurity Relevance

Static routing is common in:

- Firewalls
- DMZ networks
- VPN tunnels
- Small office routers
- Lab environments

Knowing routing helps when:

- Pivoting during penetration tests
- Troubleshooting VPNs
- Analyzing packet captures
- Reading firewall rules

---

# Interview Questions

Q1. What is routing?

Q2. Difference between a switch and a router?

Q3. What is a routing table?

Q4. What is a static route?

Q5. What is a default route?

Q6. What is the next hop?

Q7. Why is a return route required?

Q8. What is Longest Prefix Match?

Q9. Which command displays the routing table?

Q10. When should static routing be used?

---

# Key Takeaways

✅ Routers forward packets using IP addresses.

✅ Routing decisions come from the routing table.

✅ Directly connected networks are learned automatically.

✅ Static routes are manually configured.

✅ Default routes handle unknown destinations.

✅ Routers always choose the most specific (longest prefix) matching route.
