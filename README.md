# Mini Network with Router and Firewall

This project demonstrates how to build a small virtual network using **Ubuntu 18.04** virtual machines in VMware.  
The goal was to create a simple router with a firewall and two client machines connected to it.

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

--

## Configuration Steps

1. **Assign IP addresses**  
   - Router (Host-Only): `192.168.56.131`  
   - Client 1: `192.168.56.132`  
   - Client 2: `192.168.56.133`  

   Clients used the router (`192.168.56.131`) as their default gateway.

2. **Enable IP forwarding** on the router:
   ```bash
   sudo sysctl -w net.ipv4.ip_forward=1
   
3. **Configure NAT and Firewall on the router**  
   NAT was enabled with iptables so that clients could access the internet through the router.  
   Basic firewall rules were added to experiment with network traffic control, for example:   
   - Allowing only HTTP/HTTPS connections  
   - Restricting internet access for specific clients  
