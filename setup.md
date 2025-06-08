# NetMonX – Lab Setup Guide

This guide walks through the setup of the NetMonX project

---

## Requirements

- Virtualization software: VirtualBox, VMware, or UTM
- pfSense ISO: [https://www.pfsense.org/download/](https://www.pfsense.org/download/)
- At least 8 GB RAM and 2 CPU cores
- Internet access
- Optional: Additional VMs for traffic generation or simulated users

---

---

### 1. Install pfSense in VirtualBox

- Create a new VM (BSD 64-bit), allocate 2 GB RAM and 2 CPUs
- Attach the pfSense ISO as the boot disk
- Add two network adapters:
  - Adapter 1 (WAN): set to NAT or Bridged Adapter
  - Adapter 2 (LAN): set to Host-only Adapter or Internal Network
- Boot and install pfSense with default settings

### 2. Access pfSense Web GUI

- From the LAN side, access the GUI at `https://192.168.1.1`
- Login with `admin` / `pfsense`, then change password
- Navigate to Interfaces > Assignments > VLANs

### 3. Create VLANs

- Create the following VLANs:
  - VLAN 10: IoT
  - VLAN 20: Work
  - VLAN 30: Guest
  - VLAN 40: Admin
- Assign each VLAN to a unique interface (e.g., `em1.10`, `em1.20`, etc.)
- Enable each interface and set static IPs (e.g., `192.168.10.1`, `192.168.20.1`)

### 4. Configure DHCP and Firewall Rules

- Enable DHCP on each VLAN with appropriate address range
- Set firewall rules:
  - Allow Internet for all VLANs
  - Block VLAN-to-VLAN traffic except Admin → others
  - Block all inbound unsolicited traffic

### 5. Set Up VPN Access

- Navigate to VPN > OpenVPN Wizard
- Create a new CA, server certificate, and OpenVPN server
- Configure client export and connect from an external device

### 6. Deploy Security Tools in Work VLAN

- Create a Linux VM connected to VLAN 20
- Install:
  - Wireshark: `sudo apt install wireshark`
  - Suricata: `sudo apt install suricata`
  - Nessus: [https://www.tenable.com/products/nessus](https://www.tenable.com/products/nessus)
- Configure Suricata to monitor the interface (e.g., `eth0`)
- Use Nessus to scan devices in other VLANs (e.g., IoT)

### 7. Simulate Traffic

- Connect additional VMs or physical devices to each VLAN
- Generate traffic:
  - Web browsing
  - Port scanning (e.g., `nmap`)
  - Malware test samples (e.g., EICAR string)
- Observe alerts in Suricata and analyze packets in Wireshark

### 8. Optional: Load Balancing and Failover

- Add a second WAN interface (e.g., USB adapter or virtual NIC)
- Configure Gateway Groups under System > Routing
- Assign weight/priority and simulate WAN failure by disabling one
- Monitor uptime and connection stability

---

## Data Collection and Metrics

- Use Suricata logs to track alerts and signatures triggered
- Use Wireshark to measure response times and broadcast traffic
- Analyze pfSense firewall logs for blocked/allowed traffic
- Export Nessus scan reports to identify vulnerabilities

---

## Notes

- Be sure to disable unused rules and accounts after testing
- Keep pfSense and all tools up to date
- All test traffic should remain in an isolated environment

---

## License

This lab configuration is for educational and personal learning use only.


