Configuring NVMe Namespaces on a Samsung U.2 PMA9A3 with the MINISFORUM MS-A2
This repository contains step-by-step notes, commands, and examples from my Hancock’s VMware Half Hour episode on configuring NVMe namespaces using a Samsung U.2 PMA9A3 enterprise SSD connected to a MINISFORUM MS-A2.

The aim is to provide homelab enthusiasts, virtualization admins, and storage engineers with a clear reference for creating, deleting, formatting, and attaching NVMe namespaces in a Linux environment.

📹 Video Walkthrough
Watch the full guide here: YouTube Link

🛠 Hardware Used
MINISFORUM MS-A2 Mini PC

Samsung U.2 PMA9A3 Enterprise SSD

U.2 to NVMe Adapter

📋 Overview of Steps Covered
Understanding U.2 NVMe SSDs

What they are

Enterprise benefits

Why namespaces matter

Namespace Use Cases

ESXi OS install

NVMe memory tiering

VMware vSAN

Linux Tools Required

nvme-cli package

nvme list for device discovery

nvme id-ctrl for controller information

Capacity Checks

tnvmcap – total capacity

unvmcap – unallocated capacity

Namespace Management Commands

Create namespaces of specific sizes (800GB, 1TB, 2TB)

Remove existing namespaces

Check number of namespaces supported

Attach/detach namespaces from the controller

Format namespaces with desired block size (e.g., 512 bytes)

Tips & Warnings

Block alignment considerations

Detecting fake or counterfeit NVMe drives

💻 Example Commands
bash
Copy
Edit
# List all NVMe devices
nvme list

# Show NVMe controller details
nvme id-ctrl /dev/nvme0

# Check total capacity
nvme id-ctrl /dev/nvme0 | grep tnvmcap

# Create a new namespace (example: 1TB)
nvme create-ns /dev/nvme0 -s 1953125000 -c 1953125000 -f 0

# Attach namespace to controller ID 0
nvme attach-ns /dev/nvme0 -n 1 -c 0

# Format namespace with 512B block size
nvme format /dev/nvme0n1 -b 512
⚠ Disclaimer
This process will erase all data on the NVMe device. Use in a lab environment unless you fully understand the implications.

🔗 Further Reading
NVMe Specifications

nvme-cli GitHub Repository


