# Windows-Active-direktory-thesis

In this GitHub repository, I will guide you through the process of setting up a vulnerable Active Directory on a Windows Server 2019. I will also show you some of the common attacks that this AD environment is vulnerable to, and explain how to implement the appropriate protections to secure it.

[!IMPORTANT]  
The thesis is still a work in progress.

## Basic inormation about Windows active directory and attacks used

To get the basinc understanding of the techonlogy used folow the links.

- **[Information about Active Directory](ActiveDirectory/windowsServersAD.md)**: Some information about the services we are attacking.
- **[Inforamtion about the attacks used](ActiveDirectory/usedAttacks.md)**: Some information about the attacks that were used in the exercise. 
## Setting Up the Environment

To get started, please refer to the following setup instructions:

- **[Kali Linux Setup Guide](setup/kaliSetUp.md)**: Steps for setting up Kali Linux for penetration testing.
- **[Windows 2019 VM Setup Guide](setup/windows2019VMsetup.md)**: Instructions for configuring a Windows Server 2019 VM to run Active Directory.

These setup guides are located in the `setup` directory, which is essential for getting the vulnerable Active Directory environment up and running.

## Enumeration and first attacks

- **[Scanning Instructions](enumeration/Scanning_Instructions.md)**: Instructions on how to perform network scanning and enumeration.
- **[Impacket and Evil-WinRM Steps](Kerberoasting/attack/Impacket_Evil_WinRM_Steps.md)**: Detailed steps on using Impacket and Evil-WinRM for attacks and gaining remote access.
- **[User Creation and Password Spraying Attack](Password\ Spraying/attack/User_Creation_and_Spraying_Attacks.md)**: Instructions on creating user files and running password spraying attacks.

