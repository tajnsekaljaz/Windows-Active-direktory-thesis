# Attacks and Tools Used

## Attacks

### User Enumeration Attack

A user enumeration attack is the process of obtaining or discovering user names in a user database. For the attack to be successful, a vulnerability in the system is required, meaning that the system exposes some data in the state of a specific user. This attack is a brute force attack, meaning that through guessing, we obtain information that would otherwise be hidden. In the worst case, an attacker may gain full access to the user's device. The user enumeration attack targets three protocols: **NetBIOS**, **LDAP**, **SNMP enumeration**.

### Kerberos Attack

A Kerberos attack is executed after information gathering and reconnaissance. The attack exploits the Kerberos authentication protocol by stealing tickets and converting them from hashed password values (angl. hash) into plaintext passwords. Kerberos attacks can be prevented by using multi-factor authentication.

### Password Spraying Attack

Password spraying is a type of brute-force attack where the attacker tries to check whether common or frequently used passwords are associated with different user names. Instead of attempting all possible password combinations for a single user (typical of brute-force attacks), password spraying uses a limited number of common passwords on a wide range of user accounts \cite{mokhtar2022active}.

## Tools Used

All attacks will be carried out in a virtual environment, which allows safe testing and attack simulation. For this, we will need a virtual Windows server as the target system and a virtual device for performing the attacks. Kali Linux is the ideal operating system for the attacker as it includes many useful tools for analysis, information gathering, and executing attacks.

Kali Linux is the most powerful and popular penetration testing platform in the world, used by security professionals across various fields, including penetration testing, forensics, reverse engineering, and vulnerability assessment \cite{linux2020kali}. Kali Linux contains many tools such as Metasploit, Nmap, Wireshark, Burp Suite, and others, which enable attacks such as vulnerability scanning, application security testing, exploiting system vulnerabilities, and network traffic analysis. Additionally, Kali Linux also allows executing attacks such as DNS spoofing, phishing, brute force attacks, and others, making it the perfect platform for security experts who want to test the protection of their systems and networks.

It is essential to ensure that both virtual devices are in the same internal network (e.g., through the "Host-Only Network" or "Internal Network" setting in the virtualization environment, such as VirtualBox or VMware). This enables communication between the devices and the execution of attacks on the target infrastructure.

## Attacked Protocols

The attacker will look for vulnerabilities in the protocols used by the system. These protocols include SMB, LDAP, Kerberos, DNS, NetBios, and RPC.

### Address Resolution Protocol (ARP)

Address Resolution Protocol (ARP) is a key protocol on the second layer of the OSI model (Layer 2) that maps logical IP addresses to physical MAC addresses. It works by sending ARP requests in the form of broadcast messages within the local network. The device that detects a match with the requested address responds with its MAC address, enabling direct communication at the physical level.

### Server Message Block (SMB)

Server Message Block (SMB) is a higher-level protocol designed for file, printer, and resource sharing in computer networks. SMB allows clients to access remote resources and perform operations such as reading, writing, and managing files. This protocol typically uses TCP port 445.

### Lightweight Directory Access Protocol (LDAP)

Lightweight Directory Access Protocol (LDAP) is a protocol for accessing directories where organized information about users, devices, and network resources is stored. LDAP allows searching, reading, and editing data in directories based on the X.500 standard. It is commonly used in identity verification systems, such as Microsoft Active Directory, and supports encryption via TLS/SSL for secure communication.

### Remote Procedure Call (RPC)

Remote Procedure Call (RPC) is a technology that enables functions to be executed in distributed systems. A client sends a request to execute a specific function on a remote server, with network communication being transparent to developers. RPC typically uses dynamically assigned network ports coordinated by a mapper on network port 135 and plays a crucial role in multi-layered applications.

### Domain Name System (DNS)

Domain Name System (DNS) is a hierarchical system for converting domain names to IP addresses, enabling efficient routing of traffic on the internet. DNS servers are responsible for storing and resolving names through recursive or iterative queries. The protocol uses port 53 for communication over UDP (for queries) or TCP (for large responses and zone transfers) \cite{meyers2018comptia}.

### Kerberos

Kerberos is an authentication protocol that enables secure identity verification of users and services on a network. The main components of the Kerberos system are the Key Distribution Center (KDC), which contains two main services: the Authentication Service (AS) and the Ticket Granting Service (TGS). The authentication process in Kerberos occurs in several steps. First, the user enters their username and password. The client sends an authentication request to the KDC. The KDC verifies the user's password, which is never transmitted over the network in an unencrypted form. If authentication is successful, the KDC returns a Ticket Granting Ticket (TGT), which is encrypted with the KDC's secret key \cite{meyers2018comptia}. The user then uses this ticket to log into the desired service. In all these steps, encrypted session keys are used to protect communication, ensuring identity verification and service access without the risk of identity spoofing or captured passwords.

## Table: Commands and Their Usage

| **Command** | **Usage** |
|-------------|-----------|
| `arp-scan` | Scans the local network for devices using ARP requests. |
| `nmap` | Scans networks, open ports, services, and OS information. |
| `smbmap` | Investigates SMB shared folders and access rights. |
| `Enum4linux-ng` | Gathers information from SMB and LDAP, such as users and shared folders. |
| `rpcclient` | Connects to Microsoft RPC to gather information about users and groups. |
| `crackmapexec` | Checks credentials, searches for vulnerabilities, and allows executing commands via SMB, RDP, and WinRM. |
| `smbclient` | Allows browsing and transferring files from SMB shared folders. |
| `ldapsearch` | Retrieves information from directories, such as Active Directory, via LDAP. |
| `impacket-GetNPUsers` | Performs Kerberoasting to obtain credentials. |
| `john` | Cracks passwords from hashes obtained from systems. |
| `evil-winrm` | Allows remote command execution via WinRM using credentials. |
| `hydra` | Performs brute force password attacks on services such as SMB, SSH, and RDP. |


