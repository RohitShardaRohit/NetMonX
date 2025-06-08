# NetMonX
NetMonX is a personal home lab project designed to simulate an enterprise network environment using open-source tools. This project helped me bridge the gap between software and network engineering by practicing real-world skills in network segmentation, traffic analysis, firewall configuration, VPN deployment, and high availability simulation.

## Lab Architecture

The lab included:
- A segmented network with multiple VLANs (IoT, Work Devices, Guests)
- A central pfSense firewall/router for VLAN routing, NAT, VPN, and firewall rules
- Simulated wireless access points (via VirtualBox or UTM)
- Monitoring with Wireshark, Suricata, and Nessus
- Load balancing and failover behavior tests

  
<pre>                 +----------------------+
                 |      Internet        |
                 +----------+-----------+
                            |
                    [pfSense Firewall]
                            |
    +-----------+-----------+------------+-----------+
    |           |                        |           |
+-----------+ +------------+        +------------+ +------------+
| [IoT VLAN]| | [Work VLAN]|        |[Guest VLAN]| |[Admin VLAN]|
|  VLAN 10  | |  VLAN 20   |        |  VLAN 30   | |  VLAN 40   |
|           | |            |        |            | |            |
| Smart     | | Work Laptop|        | Guest VMs  | | Mgmt       |
| Devices   | | + Suricata |        | (Testing)  | | Interface  |
| (e.g.,    | | + Wireshark|        |            | | + VPN      |
| cameras)  | | + Nessus   |        |            | |            |
+-----------+ +------------+        +------------+ +------------+
 </pre>


## Tools & Technologies

| Tool        | Purpose                                           |
|-------------|---------------------------------------------------|
| pfSense     | VLAN creation, firewall rules, VPN, NAT, load balancing |
| Wireshark   | Packet inspection and protocol analysis           |
| Suricata    | Intrusion detection and alerting                  |
| Nessus      | Vulnerability scanning on local machines          |
| OpenVPN     | Secure remote access to segmented lab             |
| VirtualBox  | Simulated endpoints for traffic simulation        |

## Key Results

- Improved network response time by 25% through VLAN segmentation and reduced broadcast traffic
- Reduced peer-to-peer traffic by 35% based on Suricata and Wireshark logs
- Blocked over 150 malicious IPs using threat intel feeds and firewall rules
- Maintained uninterrupted connectivity during simulated failover tests

## Motivation

While transitioning from software engineering into network and cybersecurity, I realized I needed hands-on experience managing network infrastructure. I created this lab to:

- Understand practical VLAN and firewall design
- Learn traffic flow and segmentation between device groups
- Detect and prevent unauthorized traffic
- Simulate enterprise-grade high availability behavior

## Screenshots & Logs

If you’d like to see:
- Sample Suricata alerts
- Wireshark packet captures
- Nessus scan summaries
- pfSense firewall and VPN configurations

...you can find those in the `screenshots/` folder.

## Setup Instructions

Coming soon in `setup.md` if you want to recreate the environment locally.
