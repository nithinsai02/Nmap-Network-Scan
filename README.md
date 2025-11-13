#  Nmap Network Scan — Local Network Reconnaissance

##  Objective
To perform a local network scan using Nmap to identify:
- Active hosts
- Open ports
- Running services
- OS fingerprints
- Basic network exposure & security insights

This task helps understand how reconnaissance works in cybersecurity.

---

## Tools Used
- Nmap
- Kali Linux VM (VirtualBox NAT network)

---

## Step 1 — Identifying Local IP Range
I ran the following command:

```
ifconfig
```

###  Results:
- Interface: `eth0`
- IP Address: `10.0.2.15`
- Subnet Mask: `255.255.255.0`
- Network Range: `10.0.2.0/24`

---

## Step 2 — Running Nmap SYN Scan

### Basic Network Scan
Command:
```
nmap -sS 10.0.2.15/24
```

###  Results:
Nmap discovered **3 active hosts**:
- `10.0.2.2` → 2 open ports  
- `10.0.2.3` → Host up (all ports filtered)  
- `10.0.2.15` → Host up (all ports closed)

###  Open ports found:
| Host | Port | State | Service |
|------|------|--------|----------|
| 10.0.2.2 | 135/tcp | open | msrpc |
| 10.0.2.2 | 445/tcp | open | microsoft-ds |

---

## Step 3 — Detailed Nmap Scan With OS & Version Detection

Command:
```
nmap -sS -sV -O -oN scan_results.txt 10.0.2.15/24
```

###  Key Findings:

### Host: 10.0.2.2
- Open Ports
  - `135/tcp` → Microsoft Windows RPC  
  - `445/tcp` → SMB (microsoft-ds)
- MAC Address: 52:55:0A:00:02:02
- Device Type: VirtualBox gateway / NAT bridge  
- OS Guess: QEMU / Oracle VirtualBox / AT&T embedded

---

### Host: 10.0.2.3
- No open ports found  
- All ports filtered (likely firewall)

---

### Host: 10.0.2.15
- No open ports  
- All ports closed (reset)  
- This is your own Kali machine  

---

## Security Analysis

###  Risks Identified:
- Port 135 (msrpc)  
  - Used by Windows RPC  
  - Historically associated with worm attacks(Blaster, Sasser)

- Port 445 (SMB)  
  - File sharing service  
  - Known for EternalBlue exploit (WannaCry)  
  - Should NOT be exposed unless required

###  Your own machine (`10.0.2.15`) is safe  
All ports are closed → good security posture.

---

##  How to Reduce Security Risks
- Disable unused Windows services such as SMB
- Block external access to ports 135 & 445
- Use host-based firewall rules
- Keep Windows updated (SMB vulnerabilities are serious)

---

## Screenshots
Place your screenshots inside the **/screenshots** folder:
- ifconfig.png  
- nmap_basic_scan.png  
- nmap_detailed_scan.png  

---

##  Files Included
- `README.md` — Full documentation  
- `scan_results.txt` — Saved Nmap output  
- `/screenshots/` — Screenshot folder  

---

##  Key Learnings
- How to identify network ranges  
- How TCP SYN scan works  
- Using Nmap for service detection  
- Understanding filtered vs. closed ports  
- Basic network attack surfaces  
- Recognizing risky Windows ports  

---

## ✔ Task Completed Successfully
All steps from the assignment were followed:
- Local network scanned  
- Ports discovered  
- Services analyzed  
- Risks identified  
- Results documented  

```
