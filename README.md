Kioptrix Level 1 - Penetration Test Report

1. Executive Summary
This project details the exploitation of the vulnerable machine "Kioptrix Level 1." The objective was to identify security flaws and escalate privileges to the root user. The attack vector focused on a buffer overflow vulnerability in the Apache web server.

2. Reconnaissance
I began with an Nmap scan to identify open ports and service versions.

Command:`nmap -sS -sC -T4 -A -p- 192.168.136.131 -o kioptrix_nmpapscan.txt`

Findings:
Port 22/tcp:OpenSSH 2.9p2 (Protocol 1.99)
Port 80/tcp:Apache httpd 1.3.20 (Unix) (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
Port 139/tcp:Samba smbd (Workgroup: MYGROUP)

3. Vulnerability Analysis
Based on the Nmap service detection, I identified two primary high-severity vulnerabilities:

1.Samba (Port 139):The service is running a version compatible with the `Trans2Open` overflow (CVE-2003-0201). This allows for remote command execution on the target.
2.Apache mod_ssl (Port 80/443):The version `mod_ssl/2.8.4` is vulnerable to a buffer overflow (CVE-2002-0082).

Selected Vector:
I chose to exploit the Samba service (Port 139) first, as it allows for a stable remote shell via Metasploit framework.
