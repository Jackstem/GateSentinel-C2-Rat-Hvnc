# 🛡️ GateSentinel

A modern C2 (Command and Control) framework designed for security research and penetration testing.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Go Version](https://img.shields.io/badge/Go-1.19+-00ADD8.svg)](https://golang.org)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey.svg)](https://github.com/kyxiaxiang/GateSentinel)

## Overview

GateSentinel is a lightweight C2 framework featuring a Go-based server and C-based client, providing secure remote control capabilities with traffic disguise and encryption.

> **⚠️ Early Development Notice**
>
> This project is in early development with AI-assisted code. Architecture may change significantly. Please report issues via GitHub.

## Key Features

- **🔐 Traffic Disguise** - C2 traffic wrapped as HTML comments
- **🌐 HTTP/HTTPS Support** - Dual protocol with flexible switching
- **🔒 Custom Encoding** - Scrambled Base64 for data security
- **⚡ Hot Reload** - Configuration updates without restart
- **🎯 Stealth Endpoints** - Customizable API paths
- **📊 Web Interface** - Intuitive beacon management dashboard
- **🔧 Flexible Deployment** - EXE and DLL client modes

## Screenshots

### Main Console
![Main Console](screenshots/20250717095706.png)

### Beacon Management
![Beacon Management](screenshots/20250717095742.png)

### Task Execution
![Task Execution](screenshots/20250717095847.png)

### System Monitoring
![System Monitoring](screenshots/20250717100650.png)

## Quick Start

### Server Setup
```bash
cd server
go build -o gatesentinel
./gatesentinel

# Access: http://localhost:8080/websafe/admin
# Default credentials: admin / admin123
```

### Client Setup
```bash
cd beacon
gcc -o beacon.exe beacon.c http.c tasks.c utils.c -lwininet -ladvapi32
./beacon.exe
```

## Configuration

### Server Configuration (config.json)
```json
{
  "server": {
    "host": "0.0.0.0",
    "port": 8080,
    "enable_https": true,
    "https_port": 8443
  },
  "routes": {
    "beacon_endpoint": "/api.jsp",
    "admin_prefix": "/websafe/admin"
  },
  "traffic_disguise": {
    "enable": true,
    "prefix": "<!--",
    "suffix": "-->"
  }
}
```

### Client Configuration (config.h)
```c
#define SERVER_HOST L"127.0.0.1"
#define SERVER_PORT 8080
#define USE_HTTPS 1
#define API_ENDPOINT L"/api.jsp"
```

## Current Features

- ✅ HTTP/HTTPS communication
- ✅ Traffic disguise as web content
- ✅ Process management
- ✅ Remote command execution
- ✅ Web admin interface
- ✅ Hot reload configuration

## Roadmap

- 🔄 **Webhook Integration** - Slack, Discord, Teams notifications
- 💾 **File Management** - Upload/download with chunked transfer
- 🎯 **Advanced Payloads** - BOF, .NET assembly loading, PIC beacon
- 📸 **Screen Capture** - Real-time screenshots with multi-monitor support
- 📊 **Enhanced Monitoring** - Keylogging, network traffic analysis
- 🎨 **UX Improvements** - Cobalt Strike-like interactive experience

## Architecture

```
┌─────────────┐    HTTPS/HTTP    ┌─────────────┐
│   Beacon    │ ◄──────────────► │   Server    │
│  (C/C++)    │  Disguised       │    (Go)     │
└─────────────┘  Traffic         └──────┬──────┘
                                        │
                                   ┌────▼────┐
                                   │   Web   │
                                   │  Admin  │
                                   └─────────┘
```

## Security Features

- **Traffic Obfuscation** - HTML comment wrapping for C2 communication
- **TLS/SSL Encryption** - Secure transmission channel
- **Custom Base64** - Scrambled encoding tables for data protection
- **Certificate Bypass** - Client-side SSL error ignoring capability
- **Stealth Endpoints** - Hidden API paths to avoid detection

## SSL Certificate Setup

```bash
# Generate self-signed certificate
mkdir -p server/certs
openssl genrsa -out server/certs/server.key 2048
openssl req -new -x509 -key server/certs/server.key \
  -out server/certs/server.crt -days 365 -subj "/CN=localhost"
```

## Project Structure

```
GateSentinel/
├── server/          # Go server
│   ├── config/      # Configuration management
│   ├── handler/     # HTTP handlers
│   ├── models/      # Data models
│   ├── static/      # Static assets
│   └── main.go      # Entry point
├── beacon/          # C client
│   ├── beacon.c     # Main program
│   ├── http.c       # HTTP communication
│   ├── tasks.c      # Task handling
│   └── config.h     # Configuration
└── docs/            # Documentation
```

## Contributing

### Issue Reporting
- **Critical Bugs** - Report via GitHub Issues immediately
- **Feature Requests** - Submit through GitHub Issues
- **General Questions** - Use GitHub Discussions

### Code Contributions
- Fork the repository and submit Pull Requests
- Follow existing code style and conventions
- Add appropriate tests for new features
- Update documentation accordingly

### Development Guidelines
- Write clear commit messages
- Include comments for complex logic
- Ensure backward compatibility when possible
- Test on multiple platforms before submitting

## Legal Notice

**This tool is for authorized security testing and research purposes only.**

Users must:
- Obtain proper authorization before testing
- Comply with all applicable local and international laws
- Take full responsibility for their actions
- Respect data protection and privacy regulations

Unauthorized access to computer systems is illegal. The developers assume no liability for misuse of this tool.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Community & Support

- **GitHub Issues** - Bug reports and feature requests
- **GitHub Discussions** - Technical discussions and Q&A
- **Knowledge Planet** - Regular updates and community support

## Star History

If this project helps you, please give us a star!

[![Star History](https://api.star-history.com/svg?repos=kyxiaxiang/GateSentinel&type=Date)](https://star-history.com/#kyxiaxiang/GateSentinel&Date)

---

**Disclaimer**: This software is provided for educational and authorized testing purposes only. Users are solely responsible for ensuring legal compliance in their jurisdiction.