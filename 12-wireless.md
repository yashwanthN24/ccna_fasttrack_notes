# CCNA Fast Track - 12: Wireless Networking (Wi-Fi)

> Goal: Understand how Wi-Fi works, how devices connect securely, and the basics of enterprise wireless networks.

---

# What is Wi-Fi?

Wi-Fi is a wireless LAN (WLAN) technology based on IEEE 802.11 standards.

Instead of Ethernet cables, devices communicate using radio waves.

Example:

```
Laptop
      \
Phone ---> Access Point ---> Router ---> Internet
      /
Tablet
```

---

# Basic Components

## Client

A device that connects to Wi-Fi.

Examples:

- Laptop
- Smartphone
- Tablet

---

## Access Point (AP)

A device that provides wireless connectivity.

It bridges wireless clients to the wired LAN.

---

## Wireless Router

A home router usually combines:

- Router
- Switch
- Access Point
- DHCP Server
- NAT

into one device.

---

# Frequency Bands

## 2.4 GHz

Advantages:

- Longer range
- Better wall penetration

Disadvantages:

- Lower speed
- More interference

Used by:

- IoT devices
- Older devices

---

## 5 GHz

Advantages:

- Faster
- Less interference

Disadvantages:

- Shorter range

Best for:

- Gaming
- Video streaming
- Office laptops

---

## 6 GHz (Wi-Fi 6E / Wi-Fi 7)

Advantages:

- Highest speeds
- Lowest interference

Requires compatible hardware.

---

# Wi-Fi Standards

| Standard | Band | Notes |
|----------|------|------|
| 802.11n (Wi-Fi 4) | 2.4/5 GHz | Good range |
| 802.11ac (Wi-Fi 5) | 5 GHz | Faster |
| 802.11ax (Wi-Fi 6) | 2.4/5 GHz | Better efficiency |
| Wi-Fi 6E | 6 GHz | Extra spectrum |
| Wi-Fi 7 | 2.4/5/6 GHz | Latest generation |

For CCNA, know the progression rather than every speed.

---

# SSID

SSID = **Service Set Identifier**

This is simply the Wi-Fi network name.

Example:

```
Office-WiFi
```

Clients choose an SSID when connecting.

---

# BSSID

Every Access Point has a unique MAC address.

This MAC address is called the **BSSID**.

One SSID may have multiple BSSIDs if several APs provide the same network.

---

# Authentication vs Encryption

Authentication:

"Who are you?"

Encryption:

"Protect the data being transmitted."

Both are necessary for secure Wi-Fi.

---

# Wi-Fi Security

## Open Network

No password.

Anyone can join.

Not secure.

---

## WEP

Very old.

Broken.

Never use.

---

## WPA

Improved over WEP.

Also outdated.

---

## WPA2

Uses AES encryption.

Still widely used.

Suitable for most environments.

---

## WPA3

Latest standard.

Provides stronger encryption and better protection against password attacks.

Recommended whenever available.

---

# Enterprise Wi-Fi

Home:

One shared password.

Enterprise:

Uses:

```
802.1X

RADIUS Server
```

Each user logs in with unique credentials.

Benefits:

- Central authentication
- Individual user accounts
- Better auditing

---

# Roaming

Large buildings have many Access Points.

Example:

```
AP1 ---- AP2 ---- AP3
```

A laptop automatically connects to the strongest AP while moving.

This process is called **Roaming**.

---

# Channels

Wi-Fi channels prevent interference.

Nearby APs should use different channels.

For 2.4 GHz:

Channels **1, 6, and 11** are commonly used because they do not overlap.

---

# Cisco Verification Commands

View wireless interfaces:

```
show wireless
```

(Exact commands depend on Cisco platform.)

---

# Packet Flow

```
Laptop

↓

Authentication

↓

Encryption Established

↓

Access Point

↓

Switch

↓

Router

↓

Internet
```

---

# Packet Tracer Lab

Create:

- Wireless Router
- Laptop
- Smartphone

Configure:

SSID:

```
OfficeWiFi
```

Security:

```
WPA2-PSK
```

Password:

```
StrongPassword123
```

Connect clients and verify Internet connectivity.

---

# Common Problems

❌ Wrong Wi-Fi password.

❌ Weak signal.

❌ Incorrect channel selection.

❌ DHCP failure.

❌ MAC filtering blocking the device.

---

# Cybersecurity Relevance

Common wireless attacks:

- Evil Twin Access Point
- Rogue Access Point
- Deauthentication Attack
- Weak Password Cracking
- WPS Attacks

Defenses:

- WPA3 or WPA2-AES
- Strong passwords
- Disable WPS
- Monitor for rogue APs
- Use enterprise authentication (802.1X)

---

# Interview Questions

Q1. What is an SSID?

Q2. Difference between SSID and BSSID?

Q3. Difference between authentication and encryption?

Q4. Why is WEP insecure?

Q5. WPA2 vs WPA3?

Q6. What is an Access Point?

Q7. What is roaming?

Q8. Which channels are commonly used in 2.4 GHz?

Q9. What is 802.1X?

Q10. Name two common Wi-Fi attacks.

---

# Key Takeaways

✅ Wi-Fi uses IEEE 802.11 standards.

✅ An Access Point connects wireless devices to the wired LAN.

✅ 2.4 GHz offers better range, while 5 GHz and 6 GHz offer higher speeds.

✅ SSID is the network name; BSSID is the AP's MAC address.

✅ WPA2 and WPA3 are the preferred security protocols.

✅ Enterprise Wi-Fi commonly uses 802.1X with a RADIUS server.
