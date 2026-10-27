# Cybersecurity Lab Setup — VirtualBox & Kali Linux

A documented beginner cybersecurity lab using **Oracle VirtualBox** on Windows and **Kali Linux** as a virtual machine. This repository contains screenshots of the setup and connectivity tests for Week 1, Project Module 1.

## Project objectives

- Install 7-Zip and Oracle VirtualBox.
- Run Kali Linux as a virtual machine.
- Configure a **NAT Network** with subnet `10.0.0.0/24`.
- Assign Kali the static IPv4 address **`10.0.0.2/24`** with gateway **`10.0.0.1`**.
- Confirm network and internet connectivity.
- Enable bidirectional clipboard and drag-and-drop.
- Share the Windows Downloads folder with Kali.
- Create a clean VM snapshot.

## Environment

| Component | Configuration |
|---|---|
| Host operating system | Windows |
| Hypervisor | Oracle VirtualBox 7.2.22 |
| Guest operating system | Kali Linux (VM: `Fayrouz`) |
| Virtual network mode | NAT Network (`NatNetwork`) |
| Subnet | `10.0.0.0/24` |
| Kali IPv4 | `10.0.0.2/24` |
| Default gateway | `10.0.0.1` |
| Shared folder | Windows Downloads → `/media/sf_Downloads` |

## Setup and evidence

### 1. Install prerequisites

Installed 7-Zip and VirtualBox, then prepared the Kali Linux virtual machine.

![7-Zip installation](screenshots/01-7zip-installed.png)

![VirtualBox version](screenshots/02-virtualbox-version.png)

### 2. Configure and start Kali Linux

The guest VM is configured as a 64-bit Debian-family Linux system and boots to the Kali desktop.

![VM settings](screenshots/03-kali-vm-configuration.png)

![Kali desktop](screenshots/04-kali-desktop.png)

### 3. Configure the NAT Network

Created/selected a VirtualBox **NAT Network** named `NatNetwork` using `10.0.0.0/24` with DHCP enabled. The VM's first network adapter is attached to this NAT Network.

![NAT Network settings](screenshots/05-nat-network-settings.png)

![VM adapter](screenshots/06-vm-network-adapter.png)

### 4. Configure Kali's IP address

Set the Kali interface `eth0` to the static address `10.0.0.2/24` with gateway `10.0.0.1`. Verified the address and routing table using:

```bash
ip a
ip route
```

![IP and route](screenshots/07-static-ip-and-route.png)

### 5. Verify connectivity

Tested access to the NAT gateway, a public IP address, and a hostname:

```bash
ping -c 3 10.0.0.1
ping -c 3 8.8.8.8
ping -c 3 google.com
```

The screenshots show successful replies and **0% packet loss** in the displayed tests. The hostname test also confirms DNS resolution worked at the time of testing.

![Gateway test](screenshots/08-gateway-connectivity.png)

![Internet tests](screenshots/09-internet-connectivity.png)

![Final IP and internet test](screenshots/10-final-ip-and-google-ping.png)

### 6. Enable integration features

Configured **Shared Clipboard** and **Drag-and-Drop** to **Bidirectional** in VirtualBox settings. Clipboard examples demonstrate text transferred between Windows and Kali.

![Integration settings](screenshots/11-clipboard-dragdrop-settings.png)

![Clipboard example 1](screenshots/14-clipboard-test-kali-to-windows.png)

![Clipboard example 2](screenshots/15-clipboard-test-windows-to-kali.png)

### 7. Configure a shared folder

Shared the Windows Downloads folder with Kali using the VirtualBox shared-folder feature. **Auto-mount** and **Make Machine-permanent** are enabled. The Linux shared-folder mount is available at `/media/sf_Downloads`.

![Shared folder](screenshots/12-shared-folder-config.png)

![Shared folder options](screenshots/13-shared-folder-options.png)

The screenshots below demonstrate access to the mounted shared folder from Kali. The final filtered listing confirms that files from the Windows Downloads directory are visible inside the guest:

![Windows and Kali](screenshots/16-windows-kali-file-transfer.png)

![Filtered shared-folder verification](screenshots/18-shared-folder-filtered-verification.png)

### 8. Save a clean snapshot

Created a snapshot named **Clean lab setup** to preserve the VM state for future lab exercises.

![Snapshot](screenshots/17-clean-lab-snapshot.png)

## Results

| Requirement | Evidence |
|---|---|
| VirtualBox and Kali setup | Screenshots 02–04 |
| NAT Network `10.0.0.0/24` | Screenshots 05–06 |
| Static Kali IP `10.0.0.2/24` | Screenshots 07 and 10 |
| Gateway connectivity | Screenshot 08 |
| Internet and DNS connectivity | Screenshots 09–10 |
| Bidirectional clipboard configured/tested | Screenshots 11, 14–15 |
| Drag-and-drop enabled | Screenshot 11 (configuration) |
| Shared Downloads folder configured and accessible | Screenshots 12–13, 16 and 18 |
| Clean snapshot | Screenshot 17 |

**Note:** The screenshots establish that drag-and-drop was enabled; they do not independently prove a drag-and-drop operation succeeded. The shared-folder screenshots show configuration and successful directory access from Kali. This verifies that the host files are visible inside the guest; it does not independently demonstrate drag-and-drop file transfer.

## Repository layout

```text
Kali-VirtualBox-Cybersecurity-Lab/
├── README.md
└── screenshots/
    ├── 01-7zip-installed.png
    ├── 02-virtualbox-version.png
    └── ... 18 numbered screenshots
```

## Safety and scope

This is a local virtual-machine lab for learning and authorized security testing. No external targets are involved in this setup documentation.
