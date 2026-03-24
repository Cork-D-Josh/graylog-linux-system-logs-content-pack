<div align="center">

# 🐧 Graylog — Linux System Logs Content Pack

**Open-source content pack for parsing, normalizing, and enriching Linux system logs in Graylog**

![Work In Progress](https://img.shields.io/badge/🚧%20Work%20In%20Progress%20🚧-orange?style=for-the-badge)
![Graylog](https://img.shields.io/badge/Graylog-7.x-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Linux](https://img.shields.io/badge/Ubuntu%20%7C%20Debian-supported-brightgreen?style=for-the-badge&logo=linux)

</div>

---

## 📋 Description

This content pack provides a set of **parsing**, **normalization**, and **enrichment** rules for Linux system logs in Graylog.
It includes **pre-built dashboards** for real-time visibility into Linux system activity.

It is an open-source alternative inspired by the [official Graylog Illuminate Linux System Logs Content Pack](https://go2docs.graylog.org/illuminate-current/content_packs/linux_system_content_pack.html).

---

## 🖥️ Supported Distributions

| Distribution | Tested Versions |
|---|---|
| Ubuntu | 20.04 LTS (Focal Fossa), 22.04 LTS (Jammy Jellyfish), 24.04 LTS (Noble Numbat) |
| Debian | 11 (Bullseye), 12 (Bookworm) |

> ⚠️ **Debian 13 (Trixie)** support is planned but not yet tested.

---

## 📦 What's Included

| Source | Covered Events |
|---|---|
| **SSH** | Authentications success / failure events (password, public key) |
| **Sudo** | Elevated commands, success / failure events |
| **PAM** | Sessions, authentications, PAM modules (pam_unix, pam_sss) |
| **Users & Groups** | Creation, modification, deletion of users and groups |

Parsing is handled via **Graylog Pipeline Rules** using Grok patterns, regex, and lookup tables.

---

## 📸 Dashboards

> 🚧 Screenshots coming soon 🚧

---

## ⚙️ Requirements

- **Graylog >= 7.0.3** (built and tested on `7.0.3+cf37d91`)
- **rsyslog** installed (required for `/var/log/auth.log` — may not be installed by default on Ubuntu / Debian)
- **Filebeat 8.x** installed on monitored Linux hosts ([see configuration](config/filebeat.md))
- **SSH server** configured with `KbdInteractiveAuthentication no` ([see configuration](config/sshd.md))

---

## 🚀 Installation

### 1. Import the Content Pack

1. Go to **System / Content Packs**
2. Click **Upload**
3. **Choose File** → `linux_system_logs_content_pack.json`
4. Click **Upload** 
5. Click **Install**

### 2. Log Collection Setup

---

## 📊 Extracted Fields (examples)

| Field | Example | Description |
|---|---|---|
| `application_name` | `sshd` / `sudo` | Application that generated the event |
| `source_ip` | `10.1.2.3` | Source IP of the connection |
| `user_name` | `josh` | Target user |
| `event_outcome` | `success` / `failure` | Event result |
| `vendor_pam_module` | `pam_unix` | Module used (PAM) |
| `vendor_credential_type` | `password` / `publickey` | Authentication method used (SSH) |
| `vendor_ssh_signature` | `ED25519 SHA256:kfMkbBg0bg...` | Key fingerprint used for authentication (SSH) |
| `process_command_line` | `/bin/bash` | Command executed with elevated privileges (Sudo) |
| `vendor_sudo_error` | `user NOT in sudoers` | Sudo failure reason (Sudo) |
| `vendor_event_description` | `User password changed` | Description of the action taken (Users & Groups) |

> 📖 For the full list of extracted fields and their descriptions ([see documentation](docs/fields.md))

---

## 🗺️ Roadmap

- [ ] Global Overview — parsing & dashboard *(widget PAM in progress)*
- [X] SSH — parsing & dashboard
- [X] Sudo — parsing & dashboard
- [ ] Users & Groups — parsing *(in progress)* & dashboard
- [ ] Graylog 6.x compatibility

---

## 🤝 Contributing

Contributions are welcome !

---

## 📜 License

Distributed under the **MIT License**. See [LICENSE](LICENSE) for more details.

---

<div align="center">
Made with ❤️ for the Graylog community — by <a href="https://github.com/Cork-D-Josh">Cork-D-Josh</a>
</div>
