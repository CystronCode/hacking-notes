# Jairaj S - Cybersecurity Portfolio & Research Notes

*"Dharma lies in the pursuit of knowledge and the defense of systems."*

## 🛡️ Objective
This repository is a live documentation of my solo cybersecurity progression[cite: 1]. The objective is clear: build a public proof of work, prioritize manual exploitation over automated tools, and prepare for the eJPT certification[cite: 1].

## ⚙️ Core Methodology
*   **Manual First:** Tools amplify understanding; they do not replace it[cite: 1]. No `SQLmap` before manual database extraction; no `LinPEAS` before manual SUID enumeration[cite: 1].
*   **Visible Proof:** A clean commit history and detailed writeups outweigh private study[cite: 1].
*   **Foundations:** Network traffic analysis and file system fluency form the core of every exploit[cite: 1].

## 🗺️ Progression Roadmap

### Phase 0: Linux CLI Foundations (Complete)
*   Mastered file system operations, encoding formats (Base64, hex), and execution permissions via OverTheWire Bandit (Levels 0–33)[cite: 1].

### Phase 1: Networking & Reconnaissance (Current)
*   **Focus:** OSI model, TCP/IP, DNS routing, and subnet calculation[cite: 1].
*   **Practical:** Packet analysis via Wireshark and building custom Python-based TCP port scanners[cite: 1].

### Phase 2: Web Application Security
*   **Focus:** OWASP Top 10, SQL Injection, XSS (Reflected/Stored/DOM), and IDOR[cite: 1].
*   **Practical:** Manual vulnerability exploitation using Burp Suite against DVWA[cite: 1].

### Phase 3: File Analysis & Digital Forensics
*   **Focus:** Magic bytes, steganography, memory dumps, and PCAP analysis[cite: 1].
*   **Practical:** Extracting hidden data using `binwalk` and `steghide`, solving PicoCTF challenges, and building custom Python file parsers[cite: 1].

### Phase 4: Infrastructure & Privilege Escalation
*   **Focus:** SUID abuse, cron jobs, Active Directory mechanics (Kerberos, Pass-the-Hash)[cite: 1].
*   **Practical:** Metasploitable2 exploitation, developing manual PrivEsc cheat sheets, and executing local privilege escalation on Linux and Windows targets[cite: 1].

### Phase 5: Real-World Targets
*   **Focus:** Black-box testing and automated custom tooling[cite: 1].
*   **Practical:** Rooting Hack The Box (HTB) machines (e.g., Lame) using independent methodology and finalizing Python security scripts[cite: 1].

## 🛠️ Custom Tooling (In Development)
This repository houses scripts built from scratch to automate specific phases of the kill chain[cite: 1]:
*   `port-scanner.py`: A socket-based TCP port scanner without third-party libraries[cite: 1].
*   `file-inspector.py`: A forensics tool designed to extract magic bytes and printable strings[cite: 1].
*   `recon-script.py`: An automated Nmap parser that generates structured markdown reports[cite: 1].
*   `web-fuzzer.py`: A custom directory brute-forcing tool[cite: 1].

## 📄 Writeups & Reports
*   *DVWA Vulnerability Audit* (Upcoming)[cite: 1]
*   *PicoCTF Forensics Methodology* (Upcoming)[cite: 1]
*   *Attacktive Directory Kill Chain* (Upcoming)[cite: 1]
*   *HTB Lame: Penetration Test Report* (Upcoming)[cite: 1]

---
**Legal Boundary:** All testing is strictly restricted to owned environments (TryHackMe, HTB, DVWA, Metasploitable2, PicoCTF) or explicitly authorized targets[cite: 1]. Unauthorized access is a criminal offense under the IT Act 2000 (Section 66)[cite: 1].
