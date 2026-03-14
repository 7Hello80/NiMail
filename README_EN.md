# NiMail

<div align="center">

![Go Version](https://img.shields.io/badge/go-%3E%3D1.21-blue.svg)
[![Stars](https://img.shields.io/github/stars/7Hello80/NiMail?style=social)](https://github.com/7Hello80/NiMail/stargazers)
[![Forks](https://img.shields.io/github/forks/7Hello80/NiMail?style=social)](https://github.com/7Hello80/NiMail/network/members)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey.svg)
![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)
![Version](https://img.shields.io/badge/version-v1.0.0-blue.svg)

[[中文文档]](README.md)
[[English]](README_EN.md)

🚀 **Professional Email Management System**

Lightweight mail server with full SMTP/IMAP/POP3 protocol support, modern management interface, multi-domain and multi-user management, one-click deployment.

</div>

## Features

- **Full Protocol Support** - Complete SMTP/IMAP/POP3 implementation, compatible with mainstream clients like Outlook, Foxmail, Thunderbird
- **Modern Interface** - Responsive admin dashboard with clean and intuitive user experience
- **Multi-Domain Management** - Support for multiple domains with independent DKIM key configuration
- **Multi-User Collaboration** - Independent mailbox space, flexible quota control, permission management
- **External Email Aggregation** - Connect external mailboxes like QQ, 163, Gmail for unified sending and receiving
- **Enterprise-Grade Security** - TLS/SSL end-to-end encryption, SPF/DKIM/DMARC anti-spoofing verification
- **Rapid Deployment** - Single binary file, no complex dependencies

## Download

Download the executable for your platform from the [Releases](../../releases) page.

**Available Platforms:**
- Linux (amd64 / arm64)
- Windows (amd64 / arm64)
- macOS (amd64 / arm64)

## Deployment

### Direct Deployment

```bash
# 1. Extract the downloaded file
tar -xzf nimail-1.0.0-linux-amd64.tar.gz
cd nimail-1.0.0-linux-amd64

# 2. Run the program
./nimail-1.0.0-linux-amd64
```

On first run, a `config.yaml` configuration file and `data` directory will be automatically generated.

### Systemd Service Deployment (Recommended)

```bash
# 1. Extract to specified directory
tar -xzf nimail-1.0.0-linux-amd64.tar.gz -C /opt/
mv /opt/nimail-1.0.0-linux-amd64 /opt/nimail

# 2. Create systemd service file
cat > /etc/systemd/system/nimail.service << 'EOF'
[Unit]
Description=NiMail Mail Server
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/opt/nimail
ExecStart=/opt/nimail/nimail
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
EOF

# 3. Start the service
systemctl daemon-reload
systemctl enable nimail
systemctl start nimail

# 4. Check status
systemctl status nimail
```

## Quick Start

### Access Admin Dashboard

Open your browser and visit `http://localhost:8080`

Default admin credentials:
- Username: `admin`
- Password: `admin123`

> Please change the default password in production environments

## Port Reference

| Service | Port | Description |
|---------|------|-------------|
| Web | 8080 | Admin dashboard |
| SMTP | 25 | Mail reception |
| SMTP | 465 | SMTP over SSL |
| SMTP | 587 | Mail submission (STARTTLS) |
| IMAP | 143 | Standard port |
| IMAP | 993 | IMAP over SSL |
| POP3 | 110 | Standard port |
| POP3 | 995 | POP3 over SSL |

## Configuration

Main configuration options in `config.yaml`:

```yaml
server:
  domain: mail.example.com    # Server domain

web:
  port: 8080                  # Web admin port

smtp:
  enabled: true
  port: 25
  tls_port: 465
  submission_port: 587

imap:
  enabled: true
  port: 143
  tls_port: 993

pop3:
  enabled: true
  port: 110
  tls_port: 995

tls:
  enabled: true
  cert_file: ./certs/cert.pem
  key_file: ./certs/key.pem

dkim:
  enabled: true
  selector: default
```

## DNS Configuration

To ensure proper mail sending and receiving, you need to configure relevant DNS records with your DNS provider.

Log in to the admin dashboard and navigate to the **Domain Management** page to view DNS configuration information for each domain, including:

- MX record
- SPF record
- DKIM record (public key)
- DMARC record

Simply add the corresponding records at your DNS provider according to the information displayed in the dashboard.

Or give the project a ⭐ Star, your support is my motivation to continue development!

## Tech Stack

- **Backend**: Go
- **Frontend**: Vue 3 + TypeScript + Element Plus
- **Database**: SQLite

---
