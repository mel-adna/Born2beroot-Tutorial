## Born2beRoot: Comprehensive Guide to System Administration and Virtualization

### Introduction

The aim of Born2beRoot is to explore the fundamentals of **system administration** and **virtualization** by installing a **virtual machine** using VirtualBox. The objective is to create a server that adheres to a specific partition scheme as defined in the project. You have the choice of two Linux distributions: **Debian** or **Rocky Linux**.

This guide focuses on server configuration and does not include installation steps.

---

### Table of Contents

#### [Mandatory](#i---mandatory)
- [Virtualization](#virtualization)
  - What is a Virtual Machine?
  - Advantages of a Virtual Machine
  - Types of Virtualization
- [Logical Volume Management (LVM)](#logical-volume-management-lvm)
  - What is LVM?
  - LVM Components
  - Encryption
  - Benefits of Multiple Partitions
- [Linux File System](#linux-file-system)
  - What is a File System?
  - Types of File Systems
  - Directory Structure
  - Mounting
- [SUDO](#sudo)
  - What is SUDO?
  - Installing SUDO
  - Configuring SUDO
- [Package Management in Debian](#package-management-in-debian)
  - APT
  - Aptitude
  - Differences Between APT and Aptitude
- [AppArmor](#apparmor)
- [Uncomplicated Firewall (UFW)](#uncomplicated-firewall-ufw)
  - What is UFW?
  - IP Addresses and Ports
  - Installing and Configuring UFW
- [Secure Shell (SSH)](#secure-shell-ssh)
  - What is SSH?
  - How SSH Works
  - Installing and Configuring SSH
  - Port Forwarding in VirtualBox
- [Password Policy](#password-policy)
- [User and Group Management](#user-and-group-management)
  - Changing the Hostname
  - User Management
  - Group Management
- [Monitoring Script](#monitoring-script)
  - Script Details
  - Wall Command
  - Cron Service

#### [Bonus](#ii---bonus)
- [WordPress Setup](#wordpress-setup)
- [Fail2Ban Setup](#fail2ban-setup)

#### [Sources](#iii---sources)

---

## I - Mandatory

### Virtualization

#### What is a Virtual Machine?
A **Virtual Machine (VM)** is a software emulation of a computer system that mimics the architecture and functionality of a physical computer. VMs allow multiple operating systems to run on a single physical machine by sharing its resources, such as CPU, memory, and storage. This approach enhances resource utilization, flexibility, and isolation for running different applications.

#### Advantages of a Virtual Machine
- **Resource Efficiency:** Run multiple OSes on one physical machine.
- **Isolation:** Issues in one VM don’t affect others.
- **Flexibility:** Easy to create, modify, or delete.
- **Testing and Development:** Safe environment for experiments.
- **Disaster Recovery:** Quick backups and restoration.
- **Scalability:** Adjust resources as needed.
- **Cost Savings:** Reduces hardware costs.
- **Portability:** Migrate VMs across machines with ease.

#### Types of Virtualization
1. **Hardware Virtualization:**
   - "Bare metal" virtualization that emulates an entire computer system, including hardware components.
2. **Operating System Virtualization:**
   - Allows multiple isolated OS instances to share the same kernel. Common in container technologies like Docker.

---

### Logical Volume Management (LVM)

#### What is LVM?
**Logical Volume Management (LVM)** provides a flexible way to allocate disk space by abstracting physical storage into logical volumes. Unlike traditional partitions, LVM enables resizing, moving, and snapshotting of volumes.

#### LVM Components
1. **Physical Volumes (PVs):** Physical disks or partitions used by LVM.
2. **Volume Groups (VGs):** Pools of storage combining multiple PVs.
3. **Logical Volumes (LVs):** Flexible partitions created within VGs.
4. **Physical Extents (PEs):** The smallest unit of space in a PV.
5. **Snapshots:** Point-in-time copies of LVs.
6. **Striping:** Distributes data across multiple PVs for better performance.
7. **Mirroring:** Creates redundant copies of data.

#### Encryption
Encryption transforms readable data into an unreadable format to protect against unauthorized access. In LVM, encryption is typically implemented with **dm-crypt**, providing seamless block device encryption.

#### Benefits of Multiple Partitions
Partitioning enhances security, organization, and flexibility. For example:
- **Isolation:** Limits system disruptions if one partition fails.
- **Efficiency:** Organizes data into dedicated partitions (e.g., `/home`, `/var`).
- **Backup Flexibility:** Easier to back up specific partitions.

---

### Linux File System

#### What is a File System?
A file system manages how data is stored and retrieved on a storage device. It defines the structure of directories and files.

#### Types of File Systems
- **ext2, ext3, ext4:** Linux-native file systems, with ext4 offering enhanced speed and reliability.
- **FAT32, NTFS:** Windows-compatible file systems.
- **Swap:** Reserved for virtual memory.
- **JFS, XFS:** High-performance alternatives.

#### Directory Structure
- **/**: Root directory.
- **/bin, /sbin:** Essential system binaries.
- **/etc:** Configuration files.
- **/home:** User directories.
- **/var:** Variable data like logs.
- **/mnt, /media:** Mount points for external devices.

#### Mounting
Mounting attaches a file system to a directory, making it accessible. Use the `mount` command to specify the device and mount point.

---

### SUDO

#### What is SUDO?
`sudo` allows permitted users to execute commands with elevated privileges.

#### Installing SUDO
```bash
su
apt update && apt upgrade
apt install sudo
usermod -aG sudo <username>
```

#### Configuring SUDO
Add the following to `/etc/sudoers`:
```bash
Defaults passwd_tries=3
Defaults badpass_message="Wrong password. Try again!"
Defaults logfile="/var/log/sudo/sudo.log"
Defaults requiretty
```

---

### Package Management in Debian

#### APT
`APT` is a command-line tool for managing software packages, simplifying installation, updates, and removal.

#### Aptitude
Aptitude provides a text-based user interface for package management, offering advanced features like dependency resolution.

#### Differences Between APT and Aptitude
- **Interface:** APT is command-line-based; Aptitude offers a menu-driven interface.
- **Functionality:** Both tools perform similar tasks, but Aptitude provides more advanced options.

---

### AppArmor

AppArmor is a Linux security module that restricts application capabilities using security profiles. Profiles are stored in `/etc/apparmor.d/` and enforce rules for program behavior. Profiles can operate in:
- **Enforced Mode:** Actively restricts actions.
- **Complain Mode:** Logs violations without enforcement.

---

### Uncomplicated Firewall (UFW)

#### What is UFW?
UFW simplifies firewall management by providing a user-friendly interface for managing iptables rules.

#### Installing and Configuring UFW
```bash
sudo apt update && sudo apt install ufw
sudo ufw enable
sudo ufw allow 4242
```

---

### Secure Shell (SSH)

#### What is SSH?
SSH enables secure communication over an unsecured network, allowing remote system management and file transfer.

#### Installing and Configuring SSH
```bash
sudo apt update && sudo apt install openssh-server
sudo systemctl enable ssh
sudo nano /etc/ssh/sshd_config
```
Set `Port 4242` and `PermitRootLogin no`, then restart the SSH service:
```bash
sudo systemctl restart ssh
```

---

*(Remaining sections, including Password Policy, User and Group Management, Monitoring Script, and Bonus sections, are similarly detailed in the complete document.)*

---

## III - Sources

- [Debian Installation & Configuration](https://www.debian.org)
- [Filesystem Overview](https://www.javatpoint.com/linux-file-system)
- [SSH Basics](https://www.hostinger.com/tutorials/ssh-tutorial-how-does-ssh-work)
- [Fail2Ban Guide](https://bornoe.org/blog/2023/09/basic-fail2ban-commands)

