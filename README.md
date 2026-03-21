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

🚀 **专业的邮箱管理系统**

轻量级邮件服务器，支持 SMTP/IMAP/POP3 全协议，现代化管理界面，多域名多用户管理，一键部署。

</div>

## 功能特性

- **全协议支持** - SMTP/IMAP/POP3 完整实现，兼容 Outlook、Foxmail、Thunderbird 等主流客户端
- **现代化界面** - 响应式管理后台，清晰直观的操作体验
- **多域名管理** - 支持绑定多个域名，独立 DKIM 密钥配置
- **多用户协作** - 独立邮箱空间、灵活配额控制、权限管理
- **外部邮箱聚合** - 可接入 QQ、163、Gmail 等外部邮箱，统一收发管理
- **企业级安全** - TLS/SSL 全链路加密，SPF/DKIM/DMARC 反伪造验证
- **极速部署** - 单二进制文件，无需复杂依赖

## 待支持的功能列表

| 名称 | 是否完成 |
| ------ | ------ |
| webhook推送 | 已支持 |

欢迎建言

## 下载

从 [Releases](../../releases) 页面下载对应平台的可执行文件。

**可用平台：**
- Linux (amd64 / arm64)
- Windows (amd64 / arm64)
- macOS (amd64 / arm64)

## 部署

### 直接部署

```bash
# 1. 解压下载的文件
tar -xzf nimail-1.0.0-linux-amd64.tar.gz
cd nimail-1.0.0-linux-amd64

# 2. 运行程序
./nimail-1.0.0-linux-amd64
```

首次运行会自动生成 `config.yaml` 配置文件和 `data` 数据目录。

### 宝塔面板部署（推荐）

在宝塔面板的网站的Go项目部署

### Systemd 服务部署

```bash
# 1. 解压到指定目录
tar -xzf nimail-1.0.0-linux-amd64.tar.gz -C /opt/
mv /opt/nimail-1.0.0-linux-amd64 /opt/nimail

# 2. 创建 systemd 服务文件
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

# 3. 启动服务
systemctl daemon-reload
systemctl enable nimail
systemctl start nimail

# 4. 查看状态
systemctl status nimail
```

## 快速开始

### 访问管理后台

打开浏览器访问 `http://localhost:8080`

默认管理员账号：
- 用户名：`admin`
- 密码：`admin123`

> 请在生产环境中及时修改默认密码

## 端口说明

| 服务 | 端口 | 说明 |
|------|------|------|
| Web | 8080 | 管理后台 |
| SMTP | 25 | 邮件接收 |
| SMTP | 465 | SMTP over SSL |
| SMTP | 587 | 邮件提交 (STARTTLS) |
| IMAP | 143 | 标准端口 |
| IMAP | 993 | IMAP over SSL |
| POP3 | 110 | 标准端口 |
| POP3 | 995 | POP3 over SSL |

## 配置说明

配置文件 `config.yaml` 主要配置项：

```yaml
server:
  domain: mail.example.com    # 服务器域名

web:
  port: 8080                  # Web管理端口

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

## DNS 配置

为确保邮件正常收发，需要在 DNS 服务商处配置相关记录。

登录管理后台，在 **域名管理** 页面可以查看每个域名对应的 DNS 配置信息，包括：

- MX 记录
- SPF 记录
- DKIM 记录（公钥）
- DMARC 记录

按照后台显示的信息在 DNS 服务商处添加相应记录即可。

## 💖 支持项目

如果这个对你有帮助，请考虑支持一下：

<div align="center">

### 请我喝杯咖啡 ☕

| 微信支付 | 支付宝 |
|:--------:|:------:|
| <img src="./image/vx.png" alt="微信" width="240" height="315"> | <img src="./image/alipay.jpg" alt="支付宝" width="240" height="315"> |

</div>

或者给项目点个 ⭐ Star，你的支持是我继续开发的动力！

## 技术栈

- **后端**: Go
- **前端**: Vue 3 + TypeScript + Element Plus
- **数据库**: SQLite
