# AI Context Guide: Cyber Security Lab Setup (Ubuntu 24.04)

> [!IMPORTANT]
> **To any AI Chatbot reading this:** This file contains the complete system state, history, and future roadmap for a cyber security lab setup. Please read this entirely to understand the project context.

---

## 1. System & Hardware Context

- **Host System**: Ubuntu 24.04 LTS (Gnome Desktop).
- **CPU**: Intel Core i5 (7th Gen) - amd64 architecture.
- **RAM**: 12GB Total (Physical).
- **Storage**:
  - 120GB SSD (System Drive - `/`).
  - 1TB HDD (Storage Drive - `/dev/sdb1` mounted at `Software`).
- **Storage Strategy**: All Virtual Machines (VMs) are stored on the **1TB HDD** at `/media/Software/VirtualBox_VMs` to preserve SSD space.

---

## 2. Project Status & History

### Lab Component 1: Kali Linux (COMPLETED)

- **Deployment**: VirtualBox 7.x
- **VM Type**: Debian (64-bit).
- **Resources**: 4GB RAM, 2 CPUs, 100GB VDI Disk (Stored on HDD).
- **Environment**: XFCE Desktop.
- **Key Configurations**:
  - GRUB installed on `/dev/sda` (within the VM).
  - VirtualBox Guest Additions installed and verified.
  - **Shared Clipboard**: Enabled (Bidirectional).
  - **Auto-Resize**: Working successfully.
  - **Software Installed**: Google Chrome, OpenVPN.
- **Verified Shortcuts**:
  - `Left Ctrl` for internal OS work.
  - `Right Ctrl` (Host Key) for VirtualBox actions (Full screen, etc.).
  - `Ctrl + Shift + V` for pasting into the Kali terminal.

---

## 3. Technical Knowledge Base

- **amd64**: The architecture name for 64-bit systems (Intel/AMD).
- **Virtual Disk Mapping**: Inside the VM, the disk is mapped as `/dev/sda`. This is a virtual `.vdi` file stored on the physical host's HDD (`/dev/sdb1`). It is isolated from the host SSD.
- **GRUB**: The initial bootloader that manages the startup sequence of the guest OS.
- **VPN**: OpenVPN used for TryHackMe (tun0 interface active).

---

## 4. Future Roadmap (To-Do List)

### Immediate Next Steps:

1. **TryHackMe Connection (COMPLETED)**:
   - Access [THM](https://tryhackme.com) via Chrome/Firefox.
   - Download `.ovpn` configuration.
   - Run `sudo openvpn your_file.ovpn` (Verified working).
2. **Snapshot Management**: Create a "Backup" snapshot of the current state.

### Upcoming VM Installations:

- [ ] **Ubuntu Guest**: 2GB RAM, 40GB Disk on HDD.
- [ ] **Windows 11**: 4GB-6GB RAM, 80GB Disk on HDD (Requires TPM/Secure Boot config).

---

**End of Context Guide.**
