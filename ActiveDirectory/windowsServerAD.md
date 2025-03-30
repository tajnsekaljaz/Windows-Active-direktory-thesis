# Overview of Windows Server and Active Directory

## 1. Windows Server & Security Features
Windows Server is a modern server operating system that offers numerous security features to protect enterprises from cyber threats. Key security functionalities include:
- **Windows Defender Advanced Threat Protection**
- **Shielded Virtual Machines**
- **Windows Admin Center**
- **Integration with Azure Active Directory**

Windows Server is ideal for businesses with high-security requirements, such as financial institutions, healthcare organizations, and the public sector. The integration with Microsoft Azure facilitates:
- **Data backups**
- **Application management**
- **Workflow optimization**

### Hardware & Performance
Windows Server supports the latest hardware, including **NVMe SSDs** and advanced **Hyper-V virtualization**, ensuring better management and faster system operations.

---

## 2. Hyper-V Virtualization
Hyper-V plays a crucial role in Windows Server by enabling the creation and management of virtual machines (VMs). Key benefits include:
- **Live Migration**: Move VMs between servers without downtime.
- **Containerization**: Enhances resource efficiency.
- **Shielded VMs**: Encrypts data and restricts unauthorized access.

---

## 3. Active Directory (AD) – Centralized Network Management
Active Directory is a core technology for centralized network management in large enterprises. 

### Features of Active Directory:
- **Active Directory Domain Controller (AD DC)**: Stores network object data.
- **Authentication & Authorization**: Uses credentials to verify user access.
- **Group Policies & Security**: Manages access rights and permissions.

### Logical & Physical Structure
- **Logical Structure**:
  - **Objects**: Users, groups, devices, policies.
  - **Forests & Trees**: Hierarchical grouping of domains.
  - **Domains**: Fundamental units for security and management.
- **Physical Structure**:
  - **Domain Controllers**: Validate user logins and enforce policies.
  - **Global Catalog Servers**: Store a partial copy of directory objects.
  - **Sites**: Represent network topology for better traffic management.

---

## 4. Trusts & Security Policies in AD
Windows Active Directory supports different types of **trust relationships** between domains:
- **One-Way Trust**: A domain trusts another but not vice versa.
- **Two-Way Trust**: Mutual trust between domains.
- **Transitive Trust**: Extends trust relationships across multiple domains.
- **Non-Transitive Trust**: Restricted to specified domains.

---

## 5. Domain Controllers & AD Infrastructure
### Domain Controller (DC)
A Domain Controller is a server that provides authentication and authorization services. It verifies:
- **User credentials** (username and password)
- **Access rights** based on policies and roles

### Global Catalog Server
- Stores copies of all objects in the domain.
- Facilitates **fast searches across the directory**.
- Ensures **partial data availability** when a domain is unreachable.

### Active Directory Sites
- Represent **physical network topology**.
- Improve **network efficiency** by reducing replication traffic.
