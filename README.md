# Cybersecurity Lab Setup — Week 1

**Networkwalks Internship — Building an Isolated Virtual Environment for Hands-on Security Practice**

## About This Project

As part of Week 1 of my Networkwalks internship, I created a dedicated cybersecurity laboratory using **VirtualBox and Kali Linux**.

The purpose of this lab is to provide a safe and controlled environment where I can practice cybersecurity concepts, test security tools, perform network experiments, and work with virtual machines without directly affecting my host computer or real-world network.

This setup provides a reusable foundation for upcoming cybersecurity labs and practical exercises.

---

## What This Lab Provides

* A fully configured **VirtualBox hypervisor** capable of running multiple virtual machines.
* **Kali Linux 2026.2** configured as the primary security-testing operating system.
* A dedicated **NAT Network** using the `10.0.0.0/24` network.
* Static IP configuration for the Kali Linux VM.
* Verified internet and DNS connectivity.
* A working gateway configuration.
* A clean VirtualBox snapshot for recovery.
* A controlled environment for future cybersecurity testing.

---

## Why an Isolated Cybersecurity Lab Is Important

Cybersecurity tools can perform powerful operations such as network discovery, scanning, enumeration, and security testing. Running these activities directly against a personal or production network can create unnecessary risks.

For this reason, I created a separate virtual network using:

* **Network:** `10.0.0.0/24`
* **Kali IP:** `10.0.0.2/24`
* **Gateway:** `10.0.0.1`
* **DNS:** `8.8.8.8`

The isolated environment allows future virtual machines to communicate with each other while keeping practical security testing separated from my normal network.

> **Important:** This laboratory is intended strictly for educational purposes. Security testing should only be performed against systems that I own or have explicit authorization to test.

---

## Environment Details

| Component    | Configuration                                  |
| ------------ | ---------------------------------------------- |
| Host OS      | Windows 11                                     |
| Host RAM     | 16 GB                                           |
| Processor    | Intel Core i7-8665U                                    |
| Hypervisor   | VirtualBox 7.2.14 r174565 (Qt6.8.0 on Windows) |
| Guest OS     | Kali Linux 2026.2                              |
| Guest RAM    | 2048 MB                                        |
| Network Type | NAT Network (isolated)                         |
| Kali IP      | 10.0.0.2/24                                    |
| Gateway      | 10.0.0.1                                       |
| DNS          | 8.8.8.8                                        |

---

# Setup Walkthrough

## 1. Installed 7-Zip

The first step was installing **7-Zip**, which was required to extract the compressed Kali Linux virtual machine package.
After extraction, the Kali appliance files were available for importing into VirtualBox.

---

## 2. Installed VirtualBox

Next, I installed **VirtualBox** on the Windows 11 host machine.
VirtualBox acts as the virtualization platform for this lab. It provides the environment in which Kali Linux and future virtual machines can run independently from the host operating system.

The installed version used for this setup was:
```text
VirtualBox 7.2.14 r174565 (Qt6.8.0 on Windows)
```
---

## 3. Created a Dedicated NAT Network

Instead of using VirtualBox's standard NAT configuration, I created a separate **NAT Network** specifically for the cybersecurity laboratory.

The network was configured as:
```text
10.0.0.0/24
```
This approach is useful for a multi-machine cybersecurity lab because virtual machines connected to the same NAT Network can communicate with each other while still having access to the internet through the host.
https://github.com/Talha30844/Cybersecurity-Lab-setup_Week1/blob/main/Screenshot(1)%202026-09-11%20.png


---

## 4. Imported the Kali Linux Virtual Machine

After preparing the network, I imported the pre-configured **Kali Linux 2026.2** virtual machine into VirtualBox.

I used VirtualBox's **Import Appliance** functionality rather than installing Kali Linux manually from an ISO file.

This made the initial deployment faster and provided a ready-to-configure Kali environment.

**KEEP HERE PICTURE**

---

## 5. Connected Kali Linux to the NAT Network

After importing the appliance, I opened the Kali virtual machine's network settings and connected its network adapter to the custom NAT Network.

This ensured that the Kali VM would use the dedicated laboratory network rather than the default VirtualBox networking configuration.

**KEEP HERE PICTURE**

---

## 6. Configured a Static IP Address

Once the network adapter was connected, I configured a static network configuration inside Kali Linux.

The final network values were:

* **IP Address:** `10.0.0.2/24`
* **Gateway:** `10.0.0.1`
* **DNS:** `8.8.8.8`

Using a fixed IP address makes the lab easier to manage because Kali will have a predictable address every time the virtual machine starts.

**KEEP HERE PICTURE**

---

## 7. Verified the Kali Network Configuration

After applying the static configuration, I checked the network interface to confirm that Kali had received the expected IP address.

The expected configuration was:

```text
10.0.0.2/24
```

on the Kali network interface.

**KEEP HERE PICTURE**

---

## 8. Tested Network Connectivity

After configuring the IP address, gateway, and DNS, I performed several connectivity tests.

The following commands were used:

### Check IP Address

```bash
ip a
```

This was used to verify the assigned IP address.

### Check Gateway

```bash
ping 10.0.0.1
```

This checked whether the Kali VM could communicate with its gateway.

### Check Internet Connectivity

```bash
ping 8.8.8.8
```

This verified internet connectivity.

### Check DNS Resolution

```bash
nslookup google.com
```

This confirmed that DNS resolution was functioning correctly.

**KEEP HERE PICTURE**

---

# A Networking Issue I Encountered

During the configuration process, I faced a connectivity problem after changing Kali Linux from DHCP to a manually configured static IP.

When I attempted:

```bash
ping google.com
```

Kali returned:

```text
ping google.com: Temporary failure in name resolution
```

Initially, this appeared to be a DNS-related problem.

However, after checking the DNS configuration inside Kali Linux, I confirmed that:

```text
nameserver 8.8.8.8
```

was already configured in `/etc/resolv.conf`.

This indicated that the DNS entry itself was not necessarily the main problem.

---

# Identifying the Actual Cause

After further investigation, the problem was traced back to the **VirtualBox NAT Network configuration**.

The addressing configuration on the VirtualBox side was not correctly aligned with the IP configuration being used by the Kali VM.

I reviewed the NAT Network settings and corrected the network configuration so that it matched the intended laboratory setup.

After making the correction, network connectivity started working again, including DNS resolution.

**KEEP HERE PICTURE**

---

# Lesson From the Troubleshooting Process

One important lesson from this issue was that an error such as:

```text
Temporary failure in name resolution
```

does not always mean that the DNS server configuration is the actual cause.

In a virtualized environment, connectivity depends on several components working together:

1. Guest operating system configuration
2. IP address
3. Subnet
4. Default gateway
5. DNS configuration
6. VirtualBox network configuration
7. NAT Network settings

Therefore, when troubleshooting a virtual machine, it is important to check both the **guest operating system** and the **virtualization platform**.

---

# Final Network Configuration

After resolving the issue, the Kali Linux laboratory environment was configured as follows:

| Setting      | Value         |
| ------------ | ------------- |
| Network      | `10.0.0.0/24` |
| Kali IP      | `10.0.0.2/24` |
| Gateway      | `10.0.0.1`    |
| DNS          | `8.8.8.8`     |
| Network Type | NAT Network   |

**KEEP HERE PICTURE**

---

# Verification of the Complete Setup

To make sure the environment was stable, I performed an end-to-end verification after completing the configuration.

### IP Address Verification

```bash
ip a
```

Expected result:

```text
10.0.0.2/24
```

This confirmed that the Kali network interface was using the expected static IP.

### Gateway Verification

```bash
ping 10.0.0.1
```

Expected result:

Successful replies from the gateway without packet loss.

### Internet Connectivity Verification

```bash
ping 8.8.8.8
```

Expected result:

Successful replies from the Google DNS server.

### DNS Verification

```bash
nslookup google.com
```

Expected result:

`google.com` successfully resolves to a valid IP address.

**KEEP HERE PICTURE**

---

# Sample Network Configuration

The final configuration verified on the machine was:

```text
IP Address: 10.0.0.2/24
Gateway: 10.0.0.1
DNS: 8.8.8.8
```

These values provide the Kali machine with a predictable address, gateway access, internet connectivity, and DNS resolution.

---

# Creating a Clean Snapshot

Once all networking and connectivity tests were completed successfully, I created a **VirtualBox snapshot** of the working Kali environment.

The snapshot acts as a recovery point for future cybersecurity labs.

If a future experiment changes the configuration or causes the VM to stop working correctly, I can restore this clean state instead of rebuilding the entire environment.

**KEEP HERE PICTURE**

---

# Why the Snapshot Is Important

A cybersecurity lab will often involve changing configurations, installing tools, modifying network settings, and testing different techniques.

Some experiments may unintentionally break the environment.

Having a clean snapshot makes recovery much easier:

```text
Working Lab
     ↓
Experiment
     ↓
Configuration Breaks
     ↓
Restore Snapshot
     ↓
Working Lab
```

This makes the environment reusable for future practical exercises.

---

# Key Takeaways

## 1. NAT vs NAT Network

A standard VirtualBox NAT configuration primarily provides a virtual machine with outbound internet access.

A **NAT Network** is more suitable for a multi-machine laboratory because multiple virtual machines connected to the same network can communicate with one another while also accessing the internet.

---

## 2. Static IP Configuration

Configuring a static IP is not limited to assigning an address.

The following values must work together correctly:

* IP address
* Subnet
* Gateway
* DNS

Incorrect configuration of any of these can result in connectivity problems.

---

## 3. Virtualization Network Configuration Matters

When troubleshooting a virtual machine, the problem may not always be inside the guest operating system.

The hypervisor's virtual networking configuration can also affect:

* IP addressing
* Gateway communication
* Internet access
* DNS resolution
* Communication between virtual machines

---

## 4. Snapshots Make Labs Easier to Maintain

A clean snapshot provides a reliable recovery point.

Instead of rebuilding the complete Kali environment after every major configuration problem, the virtual machine can be restored to a known working state.

---

## 5. Documentation Is Part of the Learning Process

Documenting the setup, configuration, problems, troubleshooting process, and final results makes the laboratory easier to reproduce.

It also helps identify what caused a problem and how it was resolved.

---

# Tools Used

The following tools were used to build this Week 1 cybersecurity environment:

* **7-Zip**
* **VirtualBox**
* **Kali Linux**

---

# Final Result

At the end of Week 1, I successfully established a working and isolated cybersecurity laboratory.

The final environment consists of:

```text
Host OS       : Windows 11
Hypervisor    : VirtualBox 7.2.14 r174565
Guest OS      : Kali Linux 2026.2
Guest RAM     : 2048 MB
Network       : NAT Network
Network Range : 10.0.0.0/24
Kali IP       : 10.0.0.2/24
Gateway       : 10.0.0.1
DNS           : 8.8.8.8
```

The environment has been tested for:

* Correct IP assignment
* Gateway connectivity
* Internet connectivity
* DNS resolution
* Snapshot restoration

This provides a stable foundation for the upcoming cybersecurity labs and hands-on security exercises.

**KEEP HERE PICTURE**

---

# About Me

**Muhammad Sami Ullah**
Cybersecurity Professional B082
**Networkwalks Internship — Week 1**
**Lab Environment Setup**

[LinkedIn](#)

---

# Acknowledgment

I would like to thank **Networkwalks** for providing the opportunity to work on this practical cybersecurity setup.

Special thanks to my instructor **Waqas Karim (CCIE)** for the guidance and support throughout the setup process, especially in understanding the reasoning behind the virtualization and networking configuration rather than simply following the steps.

This Week 1 lab has provided a strong practical foundation for continuing with more advanced cybersecurity exercises.
