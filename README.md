# Elastic SIEM Home Lab

## Overview
This project demonstrates the setup of an Elastic Stack Security Information and Event Management (SIEM) system using a Kali Linux VM. It covers log collection, event generation, querying, visualization, and alert creation to simulate real-world security monitoring.

## Prerequisites
- **Virtualization Software**: VirtualBox or VMware
- **Basic Knowledge**: Linux and virtualization

## Setup Steps

### 1. Elastic Cloud Account Creation
I created an account in Elastic Cloud with a free trial and deployed an Elasticsearch instance.

**[Insert Image Here]**

### 2. Kali Linux VM Setup
The Kali Linux VM was downloaded and imported into VirtualBox/VMware. After starting the VM, the default credentials (`kali/kali`) were used to log in.

**[Insert Image Here]**

### 3. Elastic Agent Installation and Configuration
In the Elastic SIEM interface, the **Integrations** section was used to install **Elastic Defend**. The installation command was executed in the Kali terminal, and the installation was verified using:

```bash
sudo systemctl status elastic-agent.service
```

**[Insert Image Here]**

### 4. Security Event Generation (Nmap Scan)
Nmap was used to generate security events. The following commands were executed:

```bash
sudo nmap <vm-ip>
sudo nmap -sS <ip-address>
sudo nmap -sT <ip-address>
sudo nmap -p- <ip-address>
```

**[Insert Image Here]**

### 5. Querying Security Events in Elastic SIEM
Inside the Elastic SIEM interface, security events were queried using:

```bash
event.action:"nmap_scan" OR process.args:"sudo"
```

**[Insert Image Here]**

### 6. Dashboard Creation
A visualization dashboard was built in **Analytics > Dashboards** with the following configurations:
- **Metrics**: `Count`
- **X-axis**: `Timestamp`

**[Insert Image Here]**

### 7. Alert Configuration
A custom query rule was created in **Security > Alerts** to detect Nmap scans:

```bash
event.action:"nmap_scan"
```

Severity and notification settings were configured, and the rule was enabled.

**[Insert Image Here]**

## Conclusion
This lab provides hands-on experience with Elastic SIEM, focusing on:
- Log collection and security event generation.
- Querying and analyzing security events.
- Creating dashboards and alerts for incident response.

## Next Steps
- Experiment with different attack simulations and event queries.
- Explore additional integrations with cloud providers and log sources.
- Improve alerting strategies for real-world security monitoring.

### Additional Resources
- [Elastic Documentation](https://www.elastic.co/guide/index.html)
- [Elastic YouTube Channel](https://www.youtube.com/c/elastic)

---

This project is a valuable addition to a security portfolio, demonstrating practical knowledge of SIEM operations, log analysis, and security monitoring workflows.
