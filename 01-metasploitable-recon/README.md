01 — Metasploitable 2 Reconnaissance Scan

**Goal:** Identify open ports and running services on a deliberately vulnerable host to find likely attack vectors.

**Setup:** Kali Linux (10.10.10.3) and Metasploitable 2 (10.10.10.4) on an isolated VirtualBox NAT Network (LabNet, 10.10.10.0/24), with no connection to the host network.

**Steps taken:**

```
nmap -sV -oN meta-scan.txt 10.10.10.4
```

**Result:** ~23 open ports. Top findings ranked by risk:

| Port | Service | Risk | Severity |
| --- | --- | --- | --- |
| 1524 | bindshell (Metasploitable root shell) | Root shell with no auth | Critical |
| 21 | vsftpd 2.3.4 | Known backdoor, CVE-2011-2523 | Critical |
| 6667 | UnrealIRCd | Known backdoor, CVE-2010-2075 | Critical |
| 445 | Samba 3.X-4.X | Possible usermap command injection, CVE-2007-2447 (version not confirmed) | High |
| 23 | Linux telnetd | Credentials sent in plaintext | High |

<img width="880" height="156" alt="image" src="https://github.com/user-attachments/assets/67c1bf59-ad8a-4439-9f3b-6b94dbec69ed" />



**What I learned:** Version banners point straight to known CVEs, which is most of the triage work in a real scan. A banner isn't proof on its own, which is why the next step was confirming one of these with an actual exploit.
