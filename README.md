# Mini Network with Router and Firewall

This project demonstrates how to build a small virtual network using **Ubuntu 18.04** virtual machines in VMware.  
The goal was to create a simple router with a firewall and two client machines connected to it.  

---

## Network Topology

The overall lab structure is shown below:  

<img width="1132" height="441" alt="schema" src="https://github.com/user-attachments/assets/a3cf141a-1c54-4ac9-b990-88eeb2e784d1" />

*Figure 1: Mini network with router, two clients, and firewall*

---

## Setup Overview

- **3 Virtual Machines** were created:
  - **Router** (Ubuntu 18.04)
  - **Client 1** (Ubuntu 18.04)
  - **Client 2** (Ubuntu 18.04)

- **Network configuration**:
  - The router had **two network adapters**:
    - **NAT** – for internet access
    - **Host-Only** – to connect local clients
  - Each client had a **Host-Only** adapter and was assigned a static IP address through netplan configuration.

---

## Configuration Steps

1. **Assign IP addresses**  
   - Router (Host-Only): `192.168.56.131`  
   - Client 1: `192.168.56.132`  
   - Client 2: `192.168.56.133`  

   Clients used the router (`192.168.56.131`) as their default gateway.

   <img width="832" height="338" alt="router_ip_show" src="https://github.com/user-attachments/assets/c4f9fccd-fc86-443e-bec3-92e66d2ab42a" />


2. **Enable IP forwarding** on the router:  
   ```bash
   sudo sysctl -w net.ipv4.ip_forward=1
3. **Configure NAT and Firewall on the router**
   
  NAT was enabled with iptables so that clients could access the internet through the router.
  Basic firewall rules were added to experiment with network traffic control, for example:
  - Allowing only HTTP/HTTPS connections
  - Restricting internet access for specific clients
