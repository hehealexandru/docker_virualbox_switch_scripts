<div align="center">

# 🔀 Docker Desktop ↔ VirtualBox Hypervisor Switch (Linux)

![Linux](https://img.shields.io/badge/OS-Linux-orange)
![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04-E95420)
![Docker](https://img.shields.io/badge/Docker%20Desktop-Supported-2496ED)
![VirtualBox](https://img.shields.io/badge/VirtualBox-Supported-blue)
![KVM](https://img.shields.io/badge/KVM-Switchable-green)
![Shell](https://img.shields.io/badge/Shell-Bash-black)

</div>

---

## 📌 Overview

This project provides two simple **Bash scripts** that allow you to safely switch between:

- **Docker Desktop for Linux** (which requires **KVM**)
- **VirtualBox** (which requires **direct VT-x access**)

On Linux, these two **cannot run at the same time** because they both need exclusive control of the hardware virtualization engine.

This solution allows both tools to coexist on the same system using a **clean switch + reboot** approach.

---

## 🧠 Technical Background

- Docker Desktop for Linux runs inside a lightweight VM using **QEMU + KVM**
- VirtualBox requires **direct access to Intel VT-x / AMD-V**
- Only **one hypervisor** can control hardware virtualization at a time

Attempting to run both simultaneously results in errors such as:
- `VT-x is being used by another hypervisor`
- `/dev/kvm not found`

---

## 🔀 Switching Concept

| Mode | KVM | VirtualBox | Docker Desktop |
|----|----|-----------|----------------|
| Docker Mode | Enabled | ❌ | ✅ |
| VirtualBox Mode | Disabled | ✅ | ❌ |

A **reboot is required** after each switch to ensure stability.

---

## ⚙️ Installation Tutorial:

Clone the repository:
```sh
git clone https://github.com/hehealexandru/docker_virualbox_switch_scripts.git
cd docker_virualbox_switch_script
```

Move the Scripts to System Path
```sh
sudo mv use-docker use-virtualbox /usr/local/bin/
```

Make the Scripts Executable
```sh
sudo chmod +x /usr/local/bin/use-docker
sudo chmod +x /usr/local/bin/use-virtualbox
```

Verify Installation
```sh
which use-docker
which use-virtualbox
```

Run which Program You want to Use
```sh
use-docker
sudo reboot

use-virtualbox
sudo reboot
```
## 🚧 Future Work

This project is currently tested on **Ubuntu 22.04 / 24.04**.

Future improvements will focus on extending compatibility to other Linux distributions, including:

- Fedora
- Arch Linux
- Independent OS

Distribution-specific differences (package names, systemd behavior, kernel module handling) will be addressed as part of this effort.
