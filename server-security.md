# 🛡️ Advanced Server Security Guide

> A practical and comprehensive guide to hardening your Linux-based servers for production environments.

---

## 📖 Table of Contents

1. [Why Server Security Matters](#why-server-security-matters)
2. [Core Security Principles](#core-security-principles)
3. [Access Control & Authentication](#access-control--authentication)
4. [Network Security](#network-security)
5. [File System & Process Hardening](#file-system--process-hardening)
6. [Logging, Auditing & Monitoring](#logging-auditing--monitoring)
7. [Backup & Disaster Recovery](#backup--disaster-recovery)
8. [Security Tools Overview](#security-tools-overview)
9. [Automation & Compliance](#automation--compliance)
10. [Further Reading & Resources](#further-reading--resources)

---

## 🔍 Why Server Security Matters

Servers are prime targets for cyberattacks due to the critical data and services they host. A single misconfigured setting or outdated package can result in data breaches, downtime, and reputational loss. Proper server hardening mitigates these risks significantly.

---

## 🔐 Core Security Principles

1. **Principle of Least Privilege (PoLP)**
   - Only grant users and services the minimal level of access required.
   - Use role-based access control (RBAC) wherever applicable.

2. **Defense in Depth**
   - Apply multiple layers of security: network firewall, application security, host-based monitoring, etc.

3. **Attack Surface Minimization**
   - Remove unnecessary services, packages, and open ports.

4. **Secure by Default**
   - Default configurations are rarely secure. Always audit and reconfigure.

---

## 🔑 Access Control & Authentication

- **SSH Security**
  - Disable root login: `PermitRootLogin no`
  - Use strong SSH keys (2048+ bits RSA or preferably ED25519)
  - Restrict login via `AllowUsers` or `AllowGroups`

- **Multi-Factor Authentication (MFA)**
  - Use tools like `Google PAM`, `Duo`, or `Authy` for SSH MFA.

- **Account Auditing**
  - Regularly check `/etc/passwd`, `/etc/group`, and `sudoers`
  - Disable or delete unused accounts

---

## 🌐 Network Security

- **Firewall Configuration**
  - Use `ufw`, `firewalld`, or raw `iptables` to block unauthorized traffic
  - Use `default deny` policies

- **Port Scanning & Exposure**
  - Use `nmap` or `netstat` to review open ports
  - Run services on non-standard ports when possible

- **SSH Port Knocking (Optional)**
  - Adds stealth layer by requiring a hidden “knock” to expose ports

- **Rate Limiting & Throttling**
  - Use `fail2ban` and/or `iptables` rate-limiting rules to prevent brute-force attacks

---

## 🗂️ File System & Process Hardening

- **Disable Unused Filesystems**
  - Disable `cramfs`, `squashfs`, `udf`, etc. in `/etc/modprobe.d/`

- **Mount Options**
  - Use `noexec`, `nodev`, and `nosuid` on non-essential mounts (e.g., `/tmp`, `/home`)

- **Setuid & Setgid Monitoring**
  - Use `find / -perm /6000` to monitor binaries with special permissions

- **AppArmor / SELinux**
  - Implement MAC (Mandatory Access Control) to contain process behavior

---

## 📊 Logging, Auditing & Monitoring

- **Enable & Secure Logs**
  - Use `rsyslog` or `journald`, store logs in separate partition if possible
  - Monitor `/var/log/auth.log`, `/var/log/syslog`, etc.

- **Audit Framework**
  - Use `auditd` to track file access, privilege escalation, etc.

- **File Integrity Monitoring**
  - Use `AIDE`, `Tripwire`, or `OSSEC` to detect unauthorized file changes

- **Centralized Logging**
  - For fleets of servers, aggregate logs using tools like ELK Stack, Graylog, or Fluentd

---

## 💾 Backup & Disaster Recovery

- **Automated Backups**
  - Use tools like `rsnapshot`, `borg`, or `rclone`

- **Offsite & Encrypted Backups**
  - Store in a secure cloud or offsite location
  - Encrypt with `gpg` or `openssl`

- **Test Your Restores**
  - Backups are worthless if they can’t be restored; test regularly!

---

## 🧰 Security Tools Overview

| Tool        | Purpose                                 |
|-------------|------------------------------------------|
| `fail2ban`  | Blocks IPs after failed login attempts   |
| `ufw`       | Simple firewall management               |
| `rkhunter`  | Scans for rootkits                       |
| `lynis`     | Full security audit tool                 |
| `clamAV`    | Antivirus scanner                        |
| `auditd`    | Logs access and system-level events      |
| `aide`      | File integrity checker                   |
| `AppArmor`  | Process-level access control             |
| `chkrootkit`| Detects common rootkits                  |

---

## 🧪 Automation & Compliance

- **Security Baselines**
  - Use CIS Benchmarks to audit system configurations
  - Tools like `OpenSCAP`, `Lynis`, or `CIS-CAT` help validate compliance

- **Configuration Management**
  - Use Ansible, Chef, or Puppet to automate secure configurations across environments

- **Continuous Monitoring**
  - Integrate tools with CI/CD to scan during deployment (e.g., `Trivy`, `Clair` for container scanning)

---

## 📚 Further Reading & Resources

- [Linux Security Checklist (Linux.com)](https://www.linux.com/training-tutorials/linux-security-basic-checklist/)
- [OWASP Server Security Guide](https://owasp.org/www-project-server-security/)
- [Initial Server Setup on DigitalOcean](https://www.digitalocean.com/community/tutorial_series/initial-server-setup)
- [The CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks)
- [NSA Hardening Guides](https://www.nsa.gov/Press-Room/News-Highlights/Article/Article/2700950/nsa-releases-guidance-on-securing-network-infrastructure-devices/)

---

## 🤝 Contribute

We welcome contributions! If you have new tools, practices, or checklists to suggest, feel free to fork the repo, make changes, and submit a pull request.

