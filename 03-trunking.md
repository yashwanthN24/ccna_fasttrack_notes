# CCNA Fast Track - 03: Trunking (802.1Q)

> Goal: Learn how multiple VLANs travel between switches using a single cable.

---

# Why Do We Need Trunking?

Suppose you have two switches.

Without trunking:

        Switch A              Switch B

VLAN10 -------- Cable -------- VLAN10

VLAN20 -------- Cable -------- VLAN20

VLAN30 -------- Cable -------- VLAN30

You would need one cable for every VLAN.

This becomes impossible when you have dozens of VLANs.

---

# The Solution: Trunk Port

A trunk port carries traffic for multiple VLANs over a single physical cable.

Example:

           VLAN10
           VLAN20
           VLAN30
              │
          Trunk Link
              │
        +-------------+
        | Switch A    |
        +-------------+
              │
        +-------------+
        | Switch B    |
        +-------------+

One cable carries frames from many VLANs.

---

# Access Port vs Trunk Port

## Access Port

- Belongs to one VLAN
- Connects PCs, printers, IP phones
- Sends untagged frames

Example:

PC ---> Access Port ---> VLAN10

---

## Trunk Port

- Carries many VLANs
- Connects switches
- Connects Layer 3 switches
- Connects routers (Router-on-a-Stick)
- Sends tagged frames

Example:

Switch ---- Trunk ---- Switch

---

# How Does the Switch Know Which VLAN a Frame Belongs To?

The switch inserts a VLAN tag into the Ethernet frame.

This is called:

IEEE 802.1Q

Example:

Original Frame

Ethernet Header
↓

Data

After tagging

Ethernet Header

↓

VLAN Tag (VLAN 20)

↓

Data

The receiving switch reads the tag and forwards the frame to the correct VLAN.

---

# Native VLAN

One VLAN on a trunk is sent **without a VLAN tag**.

This is the Native VLAN.

Default:

VLAN 1

Best Practice:

Change it to an unused VLAN such as:

VLAN 999

Never use VLAN 1 as the Native VLAN in production.

---

# Allowed VLANs

A trunk does not have to carry every VLAN.

Example:

Allowed:

VLAN10

VLAN20

Blocked:

VLAN30

VLAN40

Cisco command:

switchport trunk allowed vlan 10,20

This improves security and reduces unnecessary traffic.

---

# Trunk Example

Switch A

PC1 VLAN10

PC2 VLAN20

↓

Trunk

↓

Switch B

PC3 VLAN10

PC4 VLAN20

Communication:

PC1 ↔ PC3 ✅

PC2 ↔ PC4 ✅

PC1 ↔ PC4 ❌

Different VLANs still cannot communicate without Layer 3 routing.

---

# DTP (Dynamic Trunking Protocol)

Cisco switches can automatically negotiate trunk links.

Modes:

dynamic auto

dynamic desirable

trunk

access

Best Practice:

Do not rely on DTP.

Configure trunks manually.

---

# Cisco Configuration

Configure trunk:

interface GigabitEthernet0/1

switchport mode trunk

Verify:

show interfaces trunk

Allow only VLANs 10 and 20:

switchport trunk allowed vlan 10,20

Change Native VLAN:

switchport trunk native vlan 999

---

# Packet Flow

PC1 (VLAN10)

↓

Access Port

↓

Switch adds VLAN10 tag

↓

Trunk Link

↓

Second Switch reads VLAN10 tag

↓

Access Port removes tag

↓

PC2

End devices never see VLAN tags.

---

# Packet Tracer Lab

Topology:

PC1 ---- Switch1 ---- Trunk ---- Switch2 ---- PC2

Create:

VLAN10

VLAN20

Assign:

PC1 -> VLAN10

PC2 -> VLAN10

Configure the link between switches as a trunk.

Ping:

PC1 → PC2

Should work.

Now remove VLAN10 from the allowed VLAN list.

Ping again.

It should fail.

This demonstrates the effect of allowed VLANs.

---

# Cybersecurity Relevance

Misconfigured trunks can expose multiple VLANs.

Common attacks:

- VLAN Hopping
- Double Tagging
- Switch Spoofing using DTP
- Native VLAN attacks

Defenses:

- Disable DTP
- Use manual trunk configuration
- Change Native VLAN
- Restrict allowed VLANs
- Disable unused switch ports

---

# Common Mistakes

❌ Forgetting to configure trunk mode.

❌ Native VLAN mismatch between switches.

❌ Forgetting to allow a VLAN on the trunk.

❌ Connecting a PC to a trunk port.

---

# Interview Questions

Q1. What is a trunk port?

Q2. Difference between access and trunk ports?

Q3. Why is IEEE 802.1Q used?

Q4. What is the Native VLAN?

Q5. Why should VLAN 1 not be used as the Native VLAN?

Q6. What is DTP?

Q7. How do switches identify VLANs over a trunk?

Q8. Can a trunk carry multiple VLANs?

Q9. Why restrict allowed VLANs?

Q10. Name two VLAN-related attacks.

---

# Key Takeaways

✅ Access ports carry one VLAN.

✅ Trunk ports carry multiple VLANs.

✅ IEEE 802.1Q adds VLAN tags.

✅ Native VLAN traffic is untagged.

✅ End devices never receive tagged frames.

✅ Manual trunk configuration is more secure than automatic negotiation.
