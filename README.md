# Cybersecurity Lab Setup — Week 1

**Networkwalks Internship — Building an Isolated Virtual Environment for Hands-on Security Practice**

## About This Project

As part of Week 1 of my Networkwalks internship, I created a dedicated cybersecurity laboratory using **VirtualBox and Kali Linux**.

The purpose of this lab is to provide a safe and controlled environment where I can practice cybersecurity concepts, test security tools, perform network experiments, and work with virtual machines without directly affecting my host computer or real-world network.

This setup provides a reusable foundation for upcoming cybersecurity labs and practical exercises.

## What This Lab Provides

* A fully configured **VirtualBox hypervisor** capable of running multiple virtual machines.
* **Kali Linux 2026.2** configured as the primary security-testing operating system.
* A dedicated **NAT Network** using the `10.0.0.0/24` network.
* Static IP configuration for the Kali Linux VM.
* Verified internet and DNS connectivity.
* A working gateway configuration.
* A clean VirtualBox snapshot for recovery.
* A controlled environment for future cybersecurity testing.

## Why an Isolated Cybersecurity Lab Is Important

Cybersecurity tools can perform powerful operations such as network discovery, scanning, enumeration, and security testing. Running these activities directly against a personal or production network can create unnecessary risks.

For this reason, I created a separate virtual network using:

* **Network:** `10.0.0.0/24`
* **Kali IP:** `10.0.0.2/24`
* **Gateway:** `10.0.0.1`
* **DNS:** `8.8.8.8`

The isolated environment allows future virtual machines to communicate with each other while keeping practical security testing separated from my normal network.

> **Important:** This laboratory is intended strictly for educational purposes. Security testing should only be performed against systems that I own or have explicit authorization to test.


## Environment Details

| Component    | Configuration                                  |
| ------------ | ---------------------------------------------- |
| Host OS      | Windows 11                                     |
| Host RAM     | 16 GB                                           |
| Processor    | Intel Core i7-8665U                             |
| Hypervisor   | VirtualBox 7.2.14 r174565                      |
| Guest OS     | Kali Linux 2026.2                              |
| Guest RAM    | 2048 MB                                        |
| Network Type | NAT Network (isolated)                         |
| Kali IP      | 10.0.0.2/24                                    |
| Gateway      | 10.0.0.1                                       |
| DNS          | 8.8.8.8                                        |

# Setup Walkthrough

## 1. Installed 7-Zip

The first step was installing **7-Zip**, which was required to extract the compressed Kali Linux virtual machine package.
After extraction, the Kali appliance files were available for importing into VirtualBox.


## 2. Installed VirtualBox

Next, I installed **VirtualBox** on the Windows 11 host machine.
VirtualBox acts as the virtualization platform for this lab. It provides the environment in which Kali Linux and future virtual machines can run independently from the host operating system.

The installed version used for this setup was:
```text
VirtualBox 7.2.14 r174565 (Qt6.8.0 on Windows)
```

## 3. Created a Dedicated NAT Network

Instead of using VirtualBox's standard NAT configuration, I created a separate **NAT Network** specifically for the cybersecurity laboratory.

The network was configured as:
```text
10.0.0.0/24
```
This approach is useful for a multi-machine cybersecurity lab because virtual machines connected to the same NAT Network can communicate with each other while still having access to the internet through the host.

<img width="960" height="504" alt="Screenshot(1) 2026-09-11 " src="https://github.com/user-attachments/assets/e57d9dbe-4848-4f09-aace-10f6f42e8965" />
<img width="960" height="504" alt="Screenshot2 2026-09-11 " src="https://github.com/user-attachments/assets/048c3c94-c0f0-4c75-8e3e-8d88db8c0be1" />


## 4. Imported the Kali Linux Virtual Machine

After preparing the network, I imported the pre-configured **Kali Linux 2026.2** virtual machine into VirtualBox.

I used VirtualBox's **Import Appliance** functionality rather than installing Kali Linux manually from an ISO file.

This made the initial deployment faster and provided a ready-to-configure Kali environment.
<img width="951" height="500" alt="Screenshot(3) 2026-09-11 " src="https://github.com/user-attachments/assets/2b7206c6-f29f-4a12-88bb-30021afc6131" />


## 5. Connected Kali Linux to the NAT Network

After importing the appliance, I opened the Kali virtual machine's network settings and connected its network adapter to the custom NAT Network.

This ensured that the Kali VM would use the dedicated laboratory network rather than the default VirtualBox networking configuration.
<img width="960" height="504" alt="Screenshot(4) 2026-09-11 " src="https://github.com/user-attachments/assets/31d0d285-7869-4262-9396-eb617786c0cb" />
<img width="642" height="464" alt="Screenshot(6) 2026-09-11 " src="https://github.com/user-attachments/assets/af7bfb6c-1df0-47c2-a8a1-335991bc644c" />

## 6. Configured a Static IP Address

Once the network adapter was connected, I configured a static network configuration inside Kali Linux.

The final network values were:

* **IP Address:** `10.0.0.2/24`
* **Gateway:** `10.0.0.1`
* **DNS:** `8.8.8.8`

Using a fixed IP address makes the lab easier to manage because Kali will have a predictable address every time the virtual machine starts.
<img width="642" height="464" alt="Screenshot(7) 2026-09-11 " src="https://github.com/user-attachments/assets/f9b647e6-ab14-4734-95bd-ee59ee6bb014" />


## 7. Verified the Kali Network Configuration

After applying the static configuration, I checked the network interface to confirm that Kali had received the expected IP address.

The expected configuration was:
```text
10.0.0.2/24
```
on the Kali network interface.

<img width="642" height="464" alt="Screenshot(8) 2026-09-11 " src="https://github.com/user-attachments/assets/a0d009b2-9a9d-44a1-adfe-cf657fc11861" />


## 8. Tested Network Connectivity

After configuring the IP address, gateway, and DNS, I performed several connectivity tests.

The following commands were used:

### Check IP Address

```bash
ip a
```
This was used to verify the assigned IP address.

<img width="642" height="464" alt="Screenshot(9) 2026-09-11 " src="https://github.com/user-attachments/assets/9e981dbe-d898-4bd5-bd8d-269e4fb04849" />\
<img width="642" height="464" alt="Screenshot(10) 2026-09-11 " src="https://github.com/user-attachments/assets/ecff386a-6699-4f3c-88e1-13d4f8241cf5" />
<img width="641" height="463" alt="screenshot (11)" src="https://github.com/user-attachments/assets/ae677fc3-c3bb-43a5-b67b-61f730f5382e" />
<img width="641" height="463" alt="Screenshot 2026-09-11 103743" src="https://github.com/user-attachments/assets/327fba96-c5b3-4e6a-9a25-a5a439348cd1" />

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
<img width="960" height="504" alt="Screenshot 2026-09-11 104803" src="https://github.com/user-attachments/assets/6eb871b8-1e75-4498-bd1b-e0599bc34c53" />



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



# Key Takeaways

## 1. NAT vs NAT Network

A standard VirtualBox NAT configuration primarily provides a virtual machine with outbound internet access.

A **NAT Network** is more suitable for a multi-machine laboratory because multiple virtual machines connected to the same network can communicate with one another while also accessing the internet.



## 2. Static IP Configuration

Configuring a static IP is not limited to assigning an address.

The following values must work together correctly:

* IP address
* Subnet
* Gateway
* DNS

Incorrect configuration of any of these can result in connectivity problems.



## 3. Virtualization Network Configuration Matters

When troubleshooting a virtual machine, the problem may not always be inside the guest operating system.

The hypervisor's virtual networking configuration can also affect:

* IP addressing
* Gateway communication
* Internet access
* DNS resolution
* Communication between virtual machines



## 4. Snapshots Make Labs Easier to Maintain

A clean snapshot provides a reliable recovery point.

Instead of rebuilding the complete Kali environment after every major configuration problem, the virtual machine can be restored to a known working state.



## 5. Documentation Is Part of the Learning Process

Documenting the setup, configuration, problems, troubleshooting process, and final results makes the laboratory easier to reproduce.

It also helps identify what caused a problem and how it was resolved.



# Tools Used

The following tools were used to build this Week 1 cybersecurity environment:

* **7-Zip**
* **VirtualBox**
* **Kali Linux**



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



# About Me

**Muhammad Talha**

Cybersecurity Professional B083

**Networkwalks Internship — Week 1**

**Lab Environment Setup**

[LinkedIn](https://lnkd.in/p/dEeuEJUb)


# Acknowledgment

I would like to thank **Networkwalks** for providing the opportunity to work on this practical cybersecurity setup.
Special thanks to my instructor **Waqas Karim (CCIE)** for the guidance and support throughout the setup process, especially in understanding the reasoning behind the virtualization and networking configuration rather than simply following the steps.
This Week 1 lab has provided a strong practical foundation for continuing with more advanced cybersecurity exercises.
