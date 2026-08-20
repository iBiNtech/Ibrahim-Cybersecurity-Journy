# 🔒 Cybersecurity Lab Environment Setup
Building an isolated virtual lab for penetration testing and ethical hacking practice
__________________________________
# 📌 Project Overview
This project is about creating a virtual cybersecurity and penetration-testing laboratory using VirtualBox and Kali Linux. The main objective of this lab
is to build a secure and controlled environment where different cybersecurity tools, network scanning techniques, reconnaissance processes, vulnerability assessments, and other security testing activities can be practiced safely and repeatedly.
The laboratory is set up on a private virtual network, allowing more virtual machines to be added in the future and used as target systems for authorized security testing and learning purposes.
__________________________________
# 🎯 Objectives
The main objectives of this project include:
- Installing and configuring VirtualBox for virtualization.
- Setting up Kali Linux as a virtual machine within VirtualBox.
- Creating a private NAT Network to support the cybersecurity laboratory environment.
- Configuring network settings to enable proper connectivity for the Kali Linux VM.
- Assigning a stable IP address to the Kali Linux virtual machine.
- Testing and confirming network communication and DNS functionality.
- Creating a clean virtual machine snapshot for backup and easy recovery.
- Recording and documenting the entire laboratory setup process.
- Preparing the lab environment for future cybersecurity learning and practical projects.
__________________________________
# 🛡️ Purpose of the Lab
This laboratory is designed to provide a secure, isolated, and controlled environment for cybersecurity education and authorized security testing.
It allows users to practice security techniques, explore cybersecurity tools, and perform testing activities without affecting real-world systems.
The lab can be used for tasks such as:
- Conducting network reconnaissance.
- Performing port scanning activities.
- Carrying out vulnerability assessments.
- Analyzing network packets.
- Testing web application security.
- Practicing exploitation techniques in a controlled environment.
- Experimenting with different cybersecurity tools and technologies.

_____________________________
> ⚠️ Important: This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.
_________________________
# 🏗️ Lab Architecture
Additional target machines can be added to the same virtual network in future projects.
_________________________
# ⚙️ Lab Configuration
|🧩 Component|	⚙️ Configuration|
|--|--|
|🖥️ Host OS|	Windows 10|
|🧠 Host RAM|	8 GB|
|⚡ Processor|	Intel Core i7|
|🧰 Hypervisor|	VirtualBox 7.2|
|🐉 Security OS|	Kali Linux 2026.2|
|🧠 Kali RAM	|2048 MB|
|🌐 Virtual Network|	NAT Network|
|📡 Network Address|	10.0.0.0/24|
|🐧 Kali IP Address|	10.0.0.2/24|
|🚪 Default Gateway|	10.0.0.1|
|🌍 DNS Server|	8.8.8.8|
|🔮 Future VM Range|	10.0.0.3–10.0.0.99|
_________________________

# 🪜 Lab Setup Procedure
_________________________
# Step 1. Install 7-Zip
7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a .7z archive.

**Tool:** 7-Zip
_________________________
# Step 2. Install VirtualBox
VirtualBox was installed as the hypervisor.
_________________________
# Step 3. Create the NAT Network
A dedicated NAT Network was created in VirtualBox.

Configuration: Network Name: NatNetwork IPv4 Prefix: 10.0.0.0/24 DHCP: Enabled IPv6: Disabled
! [](Natnetwork.png)

A **NAT Network** was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity.

This will allow future attacker and target VMs to communicate within the lab.
_________________________
# Step 4. Import Kali Linux
The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

The VM network adapter was configured as follows:

Adapter 1
```text
Attached to: NAT Network
Network:     NatNetwork
Adapter Type: Intel PRO/1000 MT Desktop
```

The VM was allocated:
```text
RAM: 2048 MB
```
! [](Homekali.png)
 A shared folder was also configured for transferring required files between the host operating system and the Kali VM.

# Step 5. Configure the Kali Linux Network
The Kali Linux network configuration was checked and configured with a consistent IPv4 address.

Example configuration:

```text
IP Address: 10.0.0.2
Subnet Mask: 255.255.255.0
Gateway: 10.0.0.1
DNS: 8.8.8.8
```
! [A consistent IP address makes it easier to document the lab and reference the Kali machine in future exercises.]
(Natnetconfig.png)

_________________________
# Step 6. Create a Clean VM Snapshot
After completing the initial configuration, a VirtualBox snapshot was created.

Example snapshot name:

```text
Clean Kali - Network Setup
```
The snapshot represents the clean baseline of the laboratory.

If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline.
_________________________
# 🔎 Lab Verification
|✅ Test|	🧾 Command|	🎯 Expected Result|
|--|--|--|
|🌐 Check IP address|	ip a	Correct Kali IP displayed|
|📡 Test gateway|	ping 10.0.0.1	|Successful replies|
|🌍 Test Internet connectivity|	ping 8.8.8.8|	Successful replies|
|🔎 Test DNS resolution|	nslookup networkwalks.com|	Domain resolves|
|🧰 Verify Nmap|	nmap --version|	Nmap version displayed|
|🔄 Verify snapshot|	Restore snapshot and run| ip a	Baseline configuration restored|

Example Results

```text
IP Address:
10.0.0.2/24

Gateway:
10.0.0.1

DNS:
8.8.8.8
```
_________________________
# 🐞 Problems Encountered & Solutions
Documenting problems is an important part of the project.

## Problem 1. Internet Connectivity After Static IP Configuration
After manually configuring the IPv4 settings, Internet connectivity may fail depending on the Kali/NetworkManager configuration.

One workaround used during this lab was:
```text
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```
The network connection was then restarted/rebooted and connectivity was tested again.

> Important: Network interface and connection names may differ between systems. Students should first identify their actual connection name before running an nmcli command.

## Problem 2. VirtualBox VT-x / Virtualization Error
The VM initially failed to start because hardware virtualization was disabled in the system firmware/BIOS.

The issue was resolved by:

Restarting the computer.
Entering BIOS/UEFI settings.
Enabling Intel VT-x / hardware virtualization.
Saving the configuration.
Restarting the computer.
Starting the Kali VM again.
After enabling virtualization, the VM started successfully.
_________________________
# 💡 What I Learned
Through this project, I learned how to create and configure a virtual environment for cybersecurity practice.

## The most important concepts I learned include:

**1. NAT vs NAT Network**
A standard NAT configuration and a NAT Network serve different purposes.

A NAT Network allows multiple VMs connected to the same virtual network to communicate with one another while providing network address translation for external connectivity.

This makes it useful for building a multi-machine cybersecurity laboratory.

**2. Virtual Machine Networking**
I learned how VirtualBox virtual network adapters connect virtual machines to different types of networks and how network configuration affects communication between machines.

**3. Static IP Configuration**
I learned how to configure and verify IPv4 addressing, subnet masks, gateways, and DNS settings in Kali Linux.

**4. VM Snapshots**
I learned that a clean snapshot should be created before performing risky or experimental activities.

This provides a known-good recovery point for future cybersecurity exercises.

**5. Documentation**
I learned that documenting commands, configuration, screenshots, problems, and solutions is an important part of a professional cybersecurity project.
_________________________
# 🔐 Security & Ethical Use
This laboratory is intended strictly for education purposes only.
_________________________
# 🔗 Tools & Resources
7-Zip: https://7-zip.org/download.html
VirtualBox: https://virtualbox.org/wiki/Downloads
Kali Linux: https://kali.org/get-kali
_________________________
# 👤 Author
**Ibrahim Mustapha**
Cybersecurity Professional B082

**LinkedIn:**
_________________________
## 📌 Project Information
Program Name: Cybersecurity at Networkwalks | Week: 01 | Project: Cybersecurity & Pentesting Lab Setup | Repository: GitHub
