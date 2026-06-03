# SOC-Homelab

## 📌 Project Overview
This repository documents the architecture, deployment, and ongoing operations of my Security Operations Center (SOC) and network infrastructure homelab. The goal of this project is to simulate a production environment to practice infrastructure management, defensive security operations, log aggregation, and engineering custom detection alerts.

### 🚀 Core Capabilities
* **Layered Network Security:** Segregated VLANs managed via an OPNsense firewall with strict inter-VLAN routing rules, enforcing network segmentation and least privilege network access
* **Centralized Log Aggregation:** Centralized log collection (Firewall, Network Switches, NAS, and Endpoints) routing through Elastic Agents to SIEM.
* **SIEM & EDR Integration:** Threat detection utilizing Security Onion (ELK Stack) and Wazuh EDR through alerting and log investigation. 
* **Attack Simulation:** An Active Directy on-prem domain with endpoints domained joined, used to mimic enterprise infrastructure and create attack scenearios. 


## 🛠️ The Tech Stack
* **Hypervisor:** Proxmox VE
* **Firewall/Routing:** OPNsense & Wireguard VPN
* **Switching:** Ubiquiti UniFi
* **SIEM:** Security Onion (ELK Stack)
* **EDR/XDR:** Wazuh
* **Log Ingest:** Elastic Agent (`elastic01`)
* **Identity:** Windows Server 2022 (`helmcove.com` Domain Controller)
* **DMZ Zone:** Web Server (`websvr01`) & Minecraft Server (`gensvr0101`)
* **Storage:** Synology NAS (NFS)


## Network Segmentation (VLANs)
The environment is hosted on a Proxmox VE hypervisor and segmented into isolated security zones via **OPNsense** to enforce the principle of least privilege:

| Zone / VLAN | Description | Key Assets |
| :--- | :--- | :--- |
| **Management** | Core infrastructure management interfaces | Proxmox VE, OPNsense WebUI, Unifi Switch (Only Secure VPN can access) |
| **Server** | Identity and centralized storage | `DC01` (Active Directory), Synology NAS |
| **Security/SOC** | SIEM, monitoring, and analysis tools | Security Onion (ELK), Wazuh Manager |
| **DMZ Zone**| Outwards facing Servers | Webserver & Minecraft Server) |
| **Prod**| User simulation and endpoint testing | Windows/Linux Workstations with Wazuh Agents |



## 🚨 Custom Detections & Alert Engineering
A major focus of this lab is creating custom detection rules within ELK stack to detect and monitor any malicious activity.

Current detection engineering use cases implemented:
* **New User or Group Created:** Alerts for any new users or groups added onto my Linux or Windows Server/Endpoints.



## 🔮 Future Roadmap
- [ ] **Threat Intelligence Integration:** Deploy OpenCTI and MISP to feed malicious indicators into the SIEM pipeline.
- [ ] **Deception Technology:** Deploy honeypots to generate external alerts. 
