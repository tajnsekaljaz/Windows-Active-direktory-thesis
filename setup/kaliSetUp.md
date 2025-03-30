# Kali Linux Setup Guide

## 1) Download Kali ISO File
Download the Kali Linux ISO from the official website:
[Get Kali Linux](https://www.kali.org/get-kali/)

## 2) Setup Kali in VirtualBox
### Configure Network Adapters:
- **Adapter 1: NAT** 
  - The NAT adapter allows a virtual machine to access external networks by sharing the host system's network connection.
- **Adapter 2: Host-Only** 
  - The Host-Only adapter creates a network that is only accessible between the virtual machine and the host system.

## 3) Setup DNS

Run the following command to edit network interfaces:
```bash
sudo nano /etc/network/interfaces
```

Add the following lines:
```plaintext
auto eth1
iface eth1 inet dhcp
```

Restart the networking service:
```bash
sudo systemctl restart networking
```

## 4) Ping Devices to Verify Connectivity

### Test External Connectivity
Ping Google DNS to check for internet access:
```bash
ping 8.8.8.8
```

### Check Local Network Connectivity
On Windows, use:
```cmd
ipconfig
```
On Linux, use:
```bash
ifconfig
```

Find the IP address from the second network adapter (e.g., `192.168.x.x`, `10.0.0.x`, or `172.16.x.x`) and test connectivity by pinging it:
```bash
ping <IP_ADDRESS>

