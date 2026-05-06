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
