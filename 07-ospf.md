# CCNA Fast Track - 07: OSPF (Open Shortest Path First)

> Goal: Learn how routers automatically exchange routes without manually creating static routes.

---

# Why Not Use Static Routes?

Imagine this network:

```
PC --- R1 --- R2 --- R3 --- R4 --- Server
```

With static routing:

- R1 needs routes to R2, R3, R4
- R2 needs routes to R1, R3, R4
- R3 needs routes to R1, R2, R4
- R4 needs routes to R1, R2, R3

As the network grows, static routes become difficult to manage.

Dynamic routing protocols solve this problem.

---

# What is OSPF?

OSPF (Open Shortest Path First) is a **dynamic routing protocol**.

Instead of manually configuring routes, routers automatically:

- Discover neighbors
- Exchange routing information
- Build routing tables
- Update routes when the network changes

---

# OSPF Process

```
Router starts

↓

Sends Hello packets

↓

Finds neighboring routers

↓

Forms OSPF adjacency

↓

Exchanges routing information

↓

Calculates shortest paths

↓

Installs routes in routing table
```

---

# Hello Packets

Routers periodically send **Hello packets**.

Purpose:

- Discover neighbors
- Verify they are still alive
- Form OSPF relationships

If Hello packets stop arriving, the neighbor is considered down.

---

# Neighbor Relationship

Example:

```
R1 -------- R2
```

Both routers:

- Exchange Hello packets
- Become neighbors
- Share routes

Now each router knows networks behind the other.

---

# Link-State Database (LSDB)

Each OSPF router builds a map of the entire network.

This map is called the:

**Link-State Database (LSDB)**

Every router has the same topology map.

---

# Shortest Path First (SPF)

OSPF runs Dijkstra's Shortest Path First algorithm.

It calculates:

> "What is the best path to every network?"

The path with the **lowest cost** is chosen.

---

# OSPF Cost

OSPF doesn't count hops.

It uses **Cost**.

Generally:

- Higher bandwidth = Lower cost
- Lower bandwidth = Higher cost

Example:

```
1 Gbps → Cost 1

100 Mbps → Cost 10

10 Mbps → Cost 100
```

The router chooses the path with the lowest total cost.

---

# Router ID

Every OSPF router has a unique Router ID.

Example:

```
1.1.1.1

2.2.2.2

3.3.3.3
```

It identifies the router within the OSPF domain.

---

# OSPF Areas

Large networks are divided into **Areas**.

```
Area 0
```

is the **Backbone Area**.

Every other area connects to Area 0.

Example:

```
Area1

   |

Area0

   |

Area2
```

For CCNA, focus mainly on **single-area OSPF (Area 0).**

---

# DR and BDR

On Ethernet networks, OSPF elects:

- Designated Router (DR)
- Backup Designated Router (BDR)

Purpose:

Reduce unnecessary routing updates.

Without DR:

Every router talks to every other router.

With DR:

All routers send updates to the DR.

The DR distributes them efficiently.

---

# Basic Cisco Configuration

Enable OSPF:

```
router ospf 1
```

Advertise a network:

```
network 192.168.10.0 0.0.0.255 area 0
```

Advertise another:

```
network 10.0.0.0 0.0.0.3 area 0
```

---

# Verification Commands

Neighbors:

```
show ip ospf neighbor
```

Routes:

```
show ip route
```

OSPF Interfaces:

```
show ip ospf interface
```

OSPF Database:

```
show ip ospf database
```

---

# Packet Flow

```
PC

↓

R1

↓

OSPF Routing Table

↓

Best Path

↓

R2

↓

R3

↓

Destination
```

If a link fails:

```
R1

↓

OSPF detects failure

↓

Calculates new path

↓

Traffic continues
```

No manual changes are required.

---

# Packet Tracer Lab

Topology:

```
PC --- R1 --- R2 --- R3 --- PC
```

Assign IP addresses.

Enable OSPF on all routers.

Advertise connected networks.

Verify:

```
show ip ospf neighbor

show ip route
```

Disconnect one link.

Observe how OSPF finds an alternate path automatically.

---

# Common Problems

❌ Wrong Area number

❌ Network command missing

❌ Interfaces shut down

❌ Router IDs duplicated

❌ Hello/Dead timer mismatch

---

# Cybersecurity Relevance

OSPF is common in:

- Enterprise LANs
- Data centers
- Campus networks

Attackers may try to:

- Inject fake routes
- Form unauthorized OSPF neighbors
- Redirect traffic

Defenses:

- OSPF authentication
- Interface restrictions
- Monitoring neighbor changes

---

# Interview Questions

Q1. What is OSPF?

Q2. Why use OSPF instead of static routes?

Q3. What are Hello packets?

Q4. What is a Router ID?

Q5. What is the LSDB?

Q6. What algorithm does OSPF use?

Q7. What metric does OSPF use?

Q8. What is Area 0?

Q9. What are DR and BDR?

Q10. Which command shows OSPF neighbors?

---

# Key Takeaways

✅ OSPF is a dynamic routing protocol.

✅ Routers automatically discover neighbors using Hello packets.

✅ OSPF builds a Link-State Database (LSDB).

✅ It uses Dijkstra's SPF algorithm.

✅ Lowest-cost path is preferred.

✅ Area 0 is the OSPF backbone.

✅ OSPF automatically adapts to network changes.
