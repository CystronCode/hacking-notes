# notes.md

## Core Commands Reference
*   `ls`: Lists files.
*   `pwd`: Prints the current working directory.
*   `cd ~`: Changes to the current user's home directory.
*   `mkdir`: Creates a new directory.
*   `cd "directory_name"`: Navigates to the specified directory.
*   `touch filename.ext`: Creates an empty file.
*   `nano`: Opens a terminal-based text editor.

---

## OverTheWire: Bandit Walkthrough Notes

### Bandit 1
*   **Command:** `cat filename`
*   **Action:** Reads the file and outputs text to the terminal.

### Bandit 2
*   **Command:** `cat ./-filename` or `cat "./--file name--"`
*   **Action:** Reads files with special characters (`-`, `+`, `_`) or spaces. 
*   **Note:** Prefixing with `./` prevents Linux from interpreting `-filename` as a command flag. Quotes handle spaces.

### Bandit 3
*   **Command:** `cd inhere`, `ls -a`, `cat ./.hiddenfile`
*   **Action:** `ls -a` reveals hidden files (files starting with a dot). `.` denotes the current directory, `..` denotes the parent directory.

### Bandit 4
*   **Command:** `file ./*`
*   **Action:** Determines the exact file type (e.g., ASCII text vs. binary data) for all files in the current directory, since `cat` cannot efficiently parse binary files.

### Bandit 5
*   **Command:** `find . -type f -size 1033c ! -executable`
*   **Action:** Locates files matching strict criteria.
    *   `.`: Current directory.
    *   `-type f`: Files only (ignores directories).
    *   `-size 1033c`: Exact size in bytes (`c`).
    *   `! -executable`: Non-executable files only (`!` negates the condition).

### Bandit 6
*   **Command:** `find / -size 33c -user bandit7 -group bandit6`
*   **Action:** Searches the entire server (`/`) for a file with specific size, owner, and group parameters.

### Bandit 7
*   **Command:** `grep "millionth" data.txt`
*   **Action:** Searches for and outputs the specific line containing the target string.

### Bandit 8
*   **Command:** `sort data.txt | uniq -u`
*   **Action:** `sort` groups duplicates together, enabling `uniq -u` to extract only the lines that do not repeat. (Use `-c` for counts, `-d` for duplicates).

### Bandit 9
*   **Command:** `strings data.txt`
*   **Action:** Extracts and outputs human-readable strings embedded within a binary or data file.

### Bandit 10
*   **Command:** `base64 -d data.txt`
*   **Action:** Decodes a Base64 encoded file.

### Bandit 11
*   **Command:** `tr "A-Za-z" "N-ZA-Mn-za-m"`
*   **Action:** Translates (rotates) characters to reverse a ROT13 cipher.

### Bandit 12
*   **Commands:** `xxd -r`, `mv`, `gzip -d`, `bzip2 -d`, `tar -xf`
*   **Action:** Reverses a hex dump (`xxd -r`) back into a binary file, then repeatedly renames extensions (`mv`) and extracts nested compression layers (`gzip`, `bzip2`, `tar`).

### Bandit 13
*   **Command:** `ssh -i bandit.key user@host`
*   **Action:** Connects to a server using a specific private key file instead of a password.
*   **Security:** `chmod 600 bandit.key` must be applied to restrict read/write access to the owner only; SSH will reject exposed keys.

### Bandit 14
*   **Command:** `nc localhost 30000`
*   **Action:** Uses Netcat to open an interactive network pipe to a specific port, waiting for raw text input to be sent.

### Bandit 15
*   **Command:** `openssl s_client -connect localhost:30001 -quiet`
*   **Action:** Establishes an encrypted SSL/TLS tunnel to prevent interception. `-quiet` prevents the tool from misinterpreting the password as an internal command.

### Bandit 16
*   **Command:** `nmap -sV -p 31000-32000 localhost`
*   **Action:** Scans a specified port range to identify open ports and determine the services/versions running on them.

### Bandit 17
*   **Command:** `diff file1 file2`
*   **Action:** Compares two files and outputs the differences.

### Bandit 18
*   **Command:** `ssh user@host -p port "cat readme"`
*   **Action:** Executes a command directly over SSH, bypassing local configurations (like `.bashrc`) that immediately force a logout upon standard connection.

### Bandit 19
*   **Command:** `./bandit20-do cat /etc/bandit_pass/bandit20`
*   **Action:** Exploits a SUID executable to run commands with the elevated privileges of the file's owner.

### Bandit 20
*   **Command:** `nc -l -p <port>`
*   **Action:** Starts a local listening server to catch a connection triggered by running a target binary (`./suconnect`).

### Bandit 21
*   **Concept:** `/etc/cron.d/`
*   **Action:** Inspecting cron configurations reveals the exact schedules and locations of automated system scripts.
> **Analogy:** Checking a company’s automated shift schedule to see exactly what time a security guard walks past a specific door.

### Bandit 22
*   **Command:** `echo "string" | md5sum`
*   **Action:** Calculates the unique MD5 hash of a string, often used to predict dynamically generated filenames.
> **Analogy:** A meat grinder; put a phrase in, and it churns out a fixed-length string of characters that acts as a secret vault number.

### Bandit 23
*   **Commands:** `chmod +x script.sh`, `cp script.sh /target_directory`
*   **Action:** Makes a malicious script executable and moves it into a cron spool directory for automatic execution by root.
> **Analogy:** Sliding a written command into a manager's inbox, knowing their secretary blindly executes whatever is in that tray.

### Bandit 24
*   **Commands:** `for`, `echo`, `nc`
*   **Action:** Pipes a generated loop of all 10,000 possible PIN combinations directly into a listening network service via Netcat.
> **Analogy:** Buying 10,000 lottery tickets and feeding them into a scanner until the machine registers a win.

### Bandit 25
*   **Commands:** `v` (in `more`), `:set shell=/bin/bash`
*   **Action:** Forces the `more` pager to pause by shrinking the terminal, launching `vi` to bypass a restricted shell environment by spawning a new, unrestricted shell.
> **Analogy:** Forcing a guided museum tour to stop by narrowing the hallway, giving you a brief window to slip through a side door.

### Bandit 26
*   **Concept:** SUID binary
*   **Action:** Utilizing a privilege wrapper to temporarily gain file owner rights to read restricted files.
> **Analogy:** Borrowing a manager’s master keycard that is chained to a clipboard; you can open doors, but only while holding the clipboard.

### Bandit 27
*   **Command:** `git clone`
*   **Action:** Downloads a full remote Git repository, including history and hidden directories.
> **Analogy:** Making a complete photocopy of corporate archives to analyze locally.

### Bandit 28
*   **Commands:** `git log`, `git show`
*   **Action:** Reviews commit timelines and reveals exact data additions/removals in past versions.
> **Analogy:** Rolling back security footage to see a password written on a whiteboard before it was erased.

### Bandit 29
*   **Commands:** `git branch -a`, `git checkout`
*   **Action:** Lists parallel branches and switches the working directory to a hidden track.
> **Analogy:** Stepping out of the main timeline into an alternate universe where the secret was never redacted.

### Bandit 30
*   **Commands:** `git tag`, `git show`
*   **Action:** Locates custom markers attached to historical points and extracts metadata.
> **Analogy:** Finding a sticky note hidden on the back of an archived photograph.

### Bandit 31
*   **Commands:** `git add`, `git commit`, `git push`
*   **Action:** Stages, saves, and forces changes to a remote server to trigger a password release.
> **Analogy:** Writing your own rule into the company handbook and dropping it on the boss's desk for mandatory approval.

### Bandit 32
*   **Command:** `$0`
*   **Action:** References the shell variable for the current process, executing it to bypass filters converting input to uppercase.
> **Analogy:** A bouncer demands you speak in uppercase letters; instead, you hand him your ID card (`$0`) to grant access without triggering his rule.

### Permission Basics

r = read = 4  
w = write = 2  
x = execute = 1  

Add them:

7 = rwx  
6 = rw-  
5 = r-x  
4 = r--  


## Permission Structure

-rwxr-xr--

Breakdown:

-   rwx   r-x   r--
|    |     |     |
type owner group others



## File Type

- = normal file  
d = directory  
l = symbolic link  



## Symbol Meaning

u = user(owner)  
g = group  
o = others  
a = all  

+ = add permission  
- = remove permission  
= = set exact permission  



## Directory Permissions

r = see filenames  
w = create/delete  
x = enter/access  



## setuid Visual

-rwsr-xr-x

s = setuid enabled



## setuid Commands

chmod u+s file  
chmod 4755 file  

Leading 4 = setuid


## Sticky Bit

t = sticky bit

Example:

drwxrwxrwt

Meaning:

users cannot delete others' files

Common in:

/tmp
## Network Fundamentals & Attack Vectors

### TCP/IP Architecture & Encapsulation
- The network operates on four layers: Application (Data), Transport (Segments), Internet (Packets), and Network Access (Frames).
- Data is encapsulated as it moves down the stack (adding headers) and decapsulated as it moves up (stripping headers).
- Vulnerabilities are layer-specific; you exploit the distinct rules of one layer, not the network as a whole.

### TCP vs. UDP
- TCP is connection-oriented, requiring a 3-way handshake (SYN, SYN-ACK, ACK) to guarantee reliable, ordered delivery.
- UDP is connectionless, prioritizing maximum speed over reliability by firing packets without establishing a session.
- TCP is weaponized via state exhaustion (tying up connections); UDP is weaponized via spoofed amplification (reflecting massive traffic).

### SYN Flood DDoS
- Exploits the TCP handshake by sending thousands of SYN requests and intentionally ignoring the SYN-ACK responses.
- The target server allocates RAM for each half-open connection until it runs out of memory and crashes.
- Defense requires SYN cookies, strict rate limiting, or load balancing to handle the artificial state overhead.

### IP Routing & Spoofing (Layer 3)
- IP addresses dictate global routing and remain constant from the true source to the final destination.
- IP Spoofing involves forging the source IP in the packet header to hide origin or orchestrate reflection attacks.
- IP Spoofing cannot be used for two-way interception, because the target's replies will route to the forged IP, not the attacker.

### MAC & ARP Spoofing (Layer 2)
- MAC addresses are physical hardware identifiers that change at every single router hop to navigate the immediate physical segment.
- Address Resolution Protocol (ARP) maps logical IPs to physical MACs on local networks but lacks any authentication.
- ARP Spoofing poisons the caches of both the router and the target device to route local traffic through the attacker (Man-in-the-Middle).

### Subnetting & CIDR
- Subnetting uses bitwise masks (e.g., /24) to mathematically divide a flat network into logically isolated zones.
- Proper segmentation restricts lateral movement, ensuring a compromised low-privilege machine cannot directly route to critical infrastructure.
- Mapping a target's CIDR blocks is the mandatory first step of internal network reconnaissance.

### TCP Windowing & Flags
- TCP headers use control flags (SYN, ACK, RST, FIN, PSH, URG) to dictate the exact state and behavior of a connection.
- Attackers use "Half-Open" stealth scans by sending a SYN, receiving a SYN-ACK, and abruptly terminating with an RST.
- This confirms a port is open without completing the handshake, bypassing application-level logging.

### BGP (Border Gateway Protocol)
- BGP is the routing protocol of the internet backbone, allowing massive Autonomous Systems (ISPs) to advertise optimal traffic paths.
- It was built on implicit trust, meaning global routers inherently believe the routing advertisements of their peers.
- BGP Hijacking involves a malicious entity falsely advertising the best route to a target, allowing them to intercept or blackhole global traffic.

### VLAN Hopping
- Virtual LANs logically isolate traffic on a shared physical switch using assigned 802.1Q tags.
- Attackers execute Double-Tagging by wrapping a restricted internal VLAN tag inside an external native VLAN tag.
- The first switch strips the outer tag and blindly forwards the traffic, injecting the attacker into the restricted segment.

### ICMP (Internet Control Message Protocol)
- ICMP is a connectionless diagnostic protocol used by routers and hosts to communicate errors or test reachability (Ping).
- Because it is necessary for troubleshooting, perimeter firewalls frequently allow ICMP traffic while blocking unknown TCP/UDP ports.
- Attackers exploit this leniency by packing stolen data or command-and-control instructions into the arbitrary payload section of an ICMP Echo Request.


## The OSI Model

### L7 - Application (Data)
- **Function:** Interfaces directly with software and users via HTTP, DNS, FTP.
- **Vulnerabilities:** Software flaws such as Cross-Site Scripting (XSS), SQL Injection (SQLi), and Phishing.
- **Defense:** Web Application Firewalls (WAF) and secure coding practices.

### L6 - Presentation (Data)
- **Function:** Handles encryption, decryption, and data formatting (JPEG, ASCII, TLS/SSL).
- **Vulnerabilities:** Cryptographic failures or downgrading secure connections.
- **Defense:** Enforcing strong cipher suites and certificate pinning.

### L5 - Session (Data)
- **Function:** Opens, manages, and tears down communication dialogues between hosts.
- **Vulnerabilities:** Targeting authentication tokens (Session Hijacking) to impersonate users.
- **Defense:** Short session timeouts and secure, randomized cookies.

### L4 - Transport (Segments)
- **Function:** Manages host-to-host reliability using TCP (guaranteed) or UDP (fast).
- **Vulnerabilities:** State-exhaustion attacks (SYN Floods) and stealth port scanning.
- **Defense:** Rate-limiting, SYN cookies, and Stateful Firewalls.

### L3 - Network (Packets)
- **Function:** Handles logical addressing (IPv4/IPv6) and inter-network routing (Routers, BGP).
- **Vulnerabilities:** IP spoofing, routing loop attacks, and fragmentation bypasses.
- **Defense:** Access Control Lists (ACLs) and strict route filtering.

### L2 - Data Link (Frames)
- **Function:** Handles physical addressing (MAC) and local network switching (Switches, VLANs).
- **Vulnerabilities:** Local Man-in-the-Middle (ARP Spoofing) and broadcast storms.
- **Defense:** Port Security, Dynamic ARP Inspection, and proper VLAN segmentation.

### L1 - Physical (Bits)
- **Function:** The raw transmission of signals over cables, fiber optics, or radio frequencies.
- **Vulnerabilities:** Physical destruction, radio jamming, or hardware keystroke loggers.
- **Defense:** Locked doors, security cameras, and shielded cables.
