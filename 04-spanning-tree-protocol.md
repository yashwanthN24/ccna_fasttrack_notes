# CCNA Fast Track - 04: Spanning Tree Protocol (STP)

> Goal: Understand why Layer 2 loops are dangerous and how STP prevents them.

---

# Why Do We Need STP?

Imagine two switches connected with two cables.

```
      +-----------+
      | Switch A  |
      +-----------+
       |         |
       |         |
      +-----------+
      | Switch B  |
      +-----------+
```

This creates **redundancy**.

Good:
- If one cable fails, the other still works.

Bad:
- Frames can loop forever.

---

# What is a Layer 2 Loop?

Unlike routers, Ethernet switches do **not** have a TTL (Time To Live) for frames.

If a frame enters a loop:

```
Switch A → Switch B → Switch A → Switch B → ...
```

It never stops.

---

# Problems Caused by Loops

## 1. Broadcast Storm

One broadcast frame keeps circulating forever.

Result:
- Network becomes slow
- CPU usage increases
- Users lose connectivity

---

## 2. MAC Address Table Instability

The same MAC address appears on different ports repeatedly.

Example:

```
AA:AA:AA -> Port1

(after a moment)

AA:AA:AA -> Port2

(after a moment)

AA:AA:AA -> Port1
```

The switch becomes confused.

---

## 3. Duplicate Frames

Devices receive multiple copies of the same frame.

Applications may fail or behave unpredictably.

---

# What is STP?

STP (Spanning Tree Protocol) prevents Layer 2 loops by **blocking redundant links**.

Important:

It does **not** remove cables.

It simply places one redundant port into a blocking state.

Example:

```
      Switch A
        |  X
        |
      Switch B
```

`X` = Blocked Port

If the active cable fails, STP automatically activates the blocked port.

---

# Root Bridge

STP elects one switch as the **Root Bridge**.

Think of it as the "boss" of the Layer 2 network.

All path calculations are based on the Root Bridge.

---

# Root Bridge Election

Every switch has a **Bridge ID**.

Bridge ID consists of:

```
Priority + MAC Address
```

The switch with the **lowest Bridge ID** becomes the Root Bridge.

---

# Port Roles

## Root Port (RP)

- One per non-root switch
- Best path toward the Root Bridge

---

## Designated Port (DP)

- One per network segment
- Forwards traffic

---

## Blocking Port

- Prevents loops
- Does not forward normal traffic

---

# Port States (Classic STP)

1. Blocking
2. Listening
3. Learning
4. Forwarding
5. Disabled

Most traffic flows only in the **Forwarding** state.

---

# Rapid STP (RSTP)

RSTP (802.1w) is a faster version of STP.

Benefits:

- Faster convergence
- Less downtime
- Preferred in modern networks

---

# BPDU

Switches exchange special messages called:

**Bridge Protocol Data Units (BPDUs)**

These messages help:

- Elect the Root Bridge
- Detect loops
- Update the spanning tree

End devices never generate BPDUs.

---

# Cisco Commands

View STP information:

```
show spanning-tree
```

View VLAN-specific STP:

```
show spanning-tree vlan 10
```

Set switch priority:

```
spanning-tree vlan 10 priority 4096
```

Lower priority = Higher chance of becoming Root Bridge.

---

# Packet Tracer Lab

Topology:

```
      Switch1
      /      \
     /        \
Switch2------Switch3
```

Connect all three switches.

Without STP:
- A Layer 2 loop exists.

With STP:
- One link is automatically blocked.

Run:

```
show spanning-tree
```

Observe:
- Root Bridge
- Root Port
- Designated Port
- Blocking Port

Disconnect the active cable.

Watch STP unblock the backup link.

---

# Cybersecurity Relevance

Attackers may exploit STP to disrupt networks.

Common attacks:

- Rogue switch becomes Root Bridge
- BPDU spoofing
- Network instability

Defenses:

- BPDU Guard
- Root Guard
- Loop Guard

---

# BPDU Guard

Protects access ports.

If a BPDU is received on an access port:

```
Port shuts down automatically.
```

Prevents unauthorized switches.

Cisco:

```
spanning-tree bpduguard enable
```

---

# Root Guard

Prevents another switch from becoming the Root Bridge.

Useful on ports where you expect only downstream switches.

---

# Loop Guard

Protects against STP failures that might create loops.

---

# Common Mistakes

❌ Disabling STP.

❌ Connecting unmanaged switches without planning.

❌ Using the default Root Bridge unintentionally.

❌ Ignoring blocked ports during troubleshooting.

---

# Interview Questions

Q1. Why is STP required?

Q2. What is a Layer 2 loop?

Q3. What is a Broadcast Storm?

Q4. What is a Root Bridge?

Q5. How is the Root Bridge elected?

Q6. Difference between Root Port and Designated Port?

Q7. What are BPDUs?

Q8. What is BPDU Guard?

Q9. Difference between STP and RSTP?

Q10. Why should STP never be disabled in production?

---

# Key Takeaways

✅ STP prevents Layer 2 loops.

✅ It blocks redundant paths instead of removing cables.

✅ One switch becomes the Root Bridge.

✅ Switches exchange BPDUs to build the spanning tree.

✅ RSTP converges much faster than classic STP.

✅ BPDU Guard, Root Guard, and Loop Guard improve security.
