# my-home-lab-journey
A technical guide and configuration log for building a home-scale data center using Proxmox VE. Focuses on Linux systems administration, networking, and hypervisor management.
# 🚀 Enterprise Home Lab: Proxmox Virtualization Project
A professional-grade virtualization environment built on a **Dell OptiPlex 7080**, designed for hosting high-availability services, Windows/Linux VMs, and containerized workloads.

---

## 🛠 Hardware Configuration
* **Host:** Dell OptiPlex 7080 
* * **Hypervisor:** Proxmox VE 8.x (Kernel: Latest stable)
* **Networking:** TP-Link Deco X20 Mesh System 
* **Storage:** Integrated NVMe SSD (Local & LVM-Thin)

## 🌐 Network Architecture
I have architected this lab to run "headless" (managed via Web GUI/SSH) with a dedicated static IP to ensure persistent access.
* **Server Static IP:** `192.168.68.50`
* **Gateway:** `192.168.68.1` (Deco X20 Router)
* **Primary DNS:** `1.1.1.1` (Cloudflare) for high-reliability resolution.

---

## 🔧 Engineering Log & Troubleshooting (The "Experience")

### 1. Networking Alignment & Connectivity
* **Challenge:** Initial "Connection Refused" error when accessing the Web UI.
* **Diagnosis:** Discovered an IP mismatch where the Proxmox default installation was on a `192.168.0.x` subnet while the local network (Deco X20) operated on `192.168.68.x`.
* **Resolution:** Accessed the physical console and manually reconfigured `/etc/network/interfaces` to align the `vmbr0` bridge with the router's subnet.

### 2. DNS & Package Management
* **Challenge:** The server could not reach external mirrors for updates.
* **Resolution:** Manually configured `/etc/resolv.conf` to use Cloudflare DNS.
* **Optimization:** Successfully migrated the system from the "Enterprise" repository to the "No-Subscription" repository to allow for full `dist-upgrade` and system hardening.

### 3. Current Project Status
* **Status:** Hypervisor is stable and fully updated.
* **In-Progress:** Provisioning a Windows 11 Pro Virtual Machine with VirtIO drivers and TPM 2.0 emulation for workstation tasks.
