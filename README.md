# Week2-Networkwalks-intership-footprint-and-Network-scanning-

# 🔍 Network Reconnaissance with Nmap & Zenmap

![Nmap](https://img.shields.io/badge/Tool-Nmap-blue)
![Zenmap](https://img.shields.io/badge/GUI-Zenmap-lightgrey)
![Platform](https://img.shields.io/badge/Platform-Windows-0078D6)
![Internship](https://img.shields.io/badge/NetworkWalk-Week%202-success)

> **NetworkWalk Internship, Week 2.** A hands-on network discovery exercise: identify my machine's network configuration with `ipconfig`, run a host discovery scan with **Nmap** through **Zenmap**, visualize the network topology, and export the results for documentation.

---

## 📌 Objectives

- Identify local network configuration from the command line
- Run a host discovery (ping) scan with Nmap
- Read and interpret the scan output
- Visualize the discovered topology
- Save the results as a file for documentation

## 🛠️ Tools

| Tool | Purpose |
|------|---------|
| [Command Prompt](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig) (`ipconfig`) | Inspect network adapters, IP addresses, gateway |
| [Nmap](https://nmap.org/) | Network discovery and security auditing |
| [Zenmap](https://nmap.org/zenmap/) | Official graphical front end for Nmap |

---

## 🧪 Walkthrough

### Step 1: Inspect the network configuration

```bash
ipconfig
```

![ipconfig output](screenshots/01-ipconfig.jpg)

The `Ethernet 2` adapter reports the following configuration:

```text
IPv4 Address. . . . . . . . . . . : 192.168.88.33
Subnet Mask . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . : 192.168.88.1
```

**What this tells us:**

```text
Subnet mask 255.255.255.0  ->  /24 network  ->  254 usable host addresses
Gateway     192.168.88.1   ->  the router that connects this LAN to the outside
IPv6        present        ->  the adapter is dual-stack (IPv4 + IPv6)
```

Other adapters (Wi-Fi, local-area connections) show `Media disconnected`, which confirms that **Ethernet 2** is the active interface.

---

### Step 2: Run a host discovery scan with Zenmap

Zenmap setup:

```text
Target  : 192.168.56.1
Profile : Ping scan
Command : nmap -sn 192.168.56.1
```

![Zenmap ping scan](screenshots/02-zenmap-ping-scan.jpg)

Scan output:

```text
Starting Nmap 7.91 ( https://nmap.org ) at 2026-11-09 14:49 +0100
Nmap scan report for 192.168.56.1
Host is up.
Nmap done: 1 IP address (1 host up) scanned in 8.90 seconds
```

**Reading the result:**

| Element | Meaning |
|---------|---------|
| `-sn` | Ping scan: discovers live hosts **without** scanning ports |
| `Host is up.` | The target replied to discovery probes |
| `1 IP address (1 host up)` | One address scanned, one responsive host |

This is the quietest form of reconnaissance: it answers the question *"is anything alive here?"* before going deeper.

---

### Step 3: Visualize the topology

Zenmap's **Topology** tab renders the scan as a graph:

![Zenmap topology](screenshots/03-zenmap-topology.jpg)

```text
[ localhost ] ------- [ 192.168.56.1 ]
   (scanner)             (discovered host, shown in green)
```

A green node means the host is **up**. As more hosts are scanned, the graph grows into a map of the network.

---

### Step 4: Save the results

Zenmap lets you export results and the topology view. The save dialog offers several formats:

![Save dialog](screenshots/04-save-dialog.jpg)

```text
Available export formats:
  PDF  |  PNG  |  PostScript  |  SVG
```

The same output can be saved straight from the command line:

```bash
nmap -sn 192.168.56.1 -oN scan_results.txt   # human-readable text
nmap -sn 192.168.56.1 -oX scan_results.xml   # XML, for tools and reports
```

---

## 🧠 Key Takeaways

```text
1. Reconnaissance comes first, for attackers and defenders alike.
2. Host discovery (-sn) maps what is alive before any port scan.
3. Visual topology makes network structure easy to understand.
4. Documenting scan results is a core professional habit.
5. Only scan networks you own or are authorized to test.
```

## 🚀 Next Steps

```bash
nmap -sV 192.168.56.1        # detect service versions on open ports
nmap -A -T4 192.168.56.1     # OS detection, scripts, traceroute
nmap -sn 192.168.88.0/24     # discover every live host on the LAN
```

## ⚖️ Ethical Use

Only scan systems and networks that you **own** or have **explicit written permission** to test. Unauthorized scanning may be illegal.

## 🔗 Useful Links

- [Nmap official website](https://nmap.org/)
- [Nmap download page](https://nmap.org/download)
- [Zenmap GUI](https://nmap.org/zenmap/)
- [Nmap reference guide](https://nmap.org/book/man.html)
- [Microsoft `ipconfig` documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig)

## 👤 Author

**Your Name**YounoussaGassama 
[LinkedIn](https://www.linkedin.com/) | [GitHub](https://github.com/)

*NetworkWalk Internship, Week 2*# week-2-networkwalks-intership-