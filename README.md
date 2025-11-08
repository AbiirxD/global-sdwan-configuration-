# 🌐 Global SD-WAN Configuration Project

## 🧩 Overview
This project showcases a **Cisco Viptela SD-WAN deployment** designed for a global enterprise network.  
It demonstrates my understanding of **WAN design**, **BGP/OMP routing**, **VRFs**, **TLOCs**, **app-aware routing**, and **automation using Python and vManage API**.

The lab environment simulates a multi-region WAN with centralized policies, monitoring, and automated configuration templates.

---

## 🏗️ Topology
The following components are included:
- **vManage** – Centralized management and policy orchestration  
- **vBond** – Control plane authentication and orchestration  
- **vSmart** – Centralized control plane  
- **vEdge routers** – Data plane devices deployed across different regions  

📊 Diagram:  
![SD-WAN Topology](topology/sdwan-topology.png)

---

## ⚙️ Technologies Used
- **Cisco Viptela SD-WAN (vManage, vBond, vSmart, vEdge)**
- **BGP**, **OMP**, **VRFs**, **TLOCs**
- **App-aware routing**, **Centralized control policies**
- **Python**, **REST API**, **CSV templates**
- **GNS3 / VMware for lab simulation**

---

## 🧠 Objectives
- Deploy and configure a multi-region SD-WAN fabric  
- Implement site-specific and centralized control/data policies  
- Automate template deployment via Python + CSV + vManage API  
- Validate BGP and OMP route propagation  
- Optimize performance using application-aware routing policies  

---

## 🧰 Repository Contents

| Folder | Description |
|---------|--------------|
| `topology/` | Diagrams and network topology files |
| `configs/` | Device configuration templates and CSV variables |
| `automation/` | Python scripts using vManage API for template deployment |
| `docs/` | Documentation, lessons learned, and troubleshooting steps |

---

## 🤖 Automation Example
Example snippet from `push_templates.py`:

```python
import requests, json, csv

vmanage_host = "192.168.1.10"
auth = ("admin", "admin")

with open('vManage-template.csv') as f:
    csv_data = csv.DictReader(f)
    for row in csv_data:
        payload = {
            "deviceIP": row["Device_IP"],
            "templateName": row["Template_Name"]
        }
        requests.post(f"https://{vmanage_host}/dataservice/template/device/config/attachfeature",
                      auth=auth, json=payload, verify=False)
