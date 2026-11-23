# Lab Environment and Baseline Reconnaissance

Security Assessment of Brew & Bean Cafe Web Portal, Task 1 (Ezitech Cyber Security internship).
Only my own local virtual machines were tested. Reconnaissance only, no exploitation.

## Network setup (host-only)
- Hypervisor: Oracle VirtualBox on Windows
- Target VM: "OWASP Juice Shop" (Ubuntu 21.10), IP **192.168.56.108**
- Attacker VM: Kali Linux, IP **192.168.56.102**
- Both VMs sit on the same private **host-only** network (192.168.56.0/24). The intentionally vulnerable app can be reached only from my own machine, not from the internet or my home network.
- Proof: screenshots 01 and 02 (both VMs on 192.168.56.x, ping works), 03 (both VMs running), 04 (Juice Shop open at http://192.168.56.108:3000).

## What I did
1. Checked the Kali IP and pinged the target (screenshots 01, 02)
2. Opened the web app in the browser (screenshots 03, 04)
3. Ping sweep: `nmap -sn 192.168.56.0/24` (screenshot 05)
4. Full scan: `nmap -sV -sC -p- -oN nmap_full.txt 192.168.56.108` (screenshots 06 to 09)
5. OS detection: `nmap -O -oN nmap_os.txt 192.168.56.108` (screenshot 10)
6. HTTP headers: `curl -I http://192.168.56.108:3000` (screenshot 11)
7. Marked the login form and search bar as entry points (screenshots 12, 13)

## Results in short
| Port | Service | Version |
|------|---------|---------|
| 22/tcp | ssh | OpenSSH 8.4p1 Ubuntu |
| 80/tcp | http | Apache httpd 2.4.48 |
| 3000/tcp | http | Node.js app, OWASP Juice Shop |

## Files
- `findings.txt`: open ports, technologies and potential entry points
- `scans/nmap_scan_report.txt`: Nmap scan report summary
- `screenshots/`: evidence of each step
