# COMP3010: Security Operations & Incident Management Portfolio

Welcome to my portfolio for the COMP3010 module. This repository contains my practical coursework, demonstrating hands-on skills in network forensics, incident response (IR), and Security Information and Event Management (SIEM).

### Quick Summary for Employers

| Skill Domain | Tools & Technologies |
| :--- | :--- |
| **Network Forensics** | Wireshark, TCP/IP Analysis, Packet-level Inspection |
| **Incident Response** | Malware Triage, Attack Chain (Kill Chain) Analysis, Reporting |
| **Threat Intelligence** | VirusTotal, Base64 Decoding, Indicator of Compromise (IoC) Analysis |
| **SIEM & Log Analysis** | Splunk (BOTSv3 Dataset), Splunk Search Processing Language (SPL) |
| **Cloud Security** | AWS Log Analysis (CloudTrail, S3) |

---

## Projects Overview

### Project 1: 🛡️ PCAP Forensic Analysis (Cobalt Strike C2)

A deep-dive investigation of a network capture (PCAP) file to identify a multi-stage cyber attack. I successfully triaged the incident, identified the compromised host, and reverse-engineered the attack chain from the initial malicious download to the final C2 beaconing.

**Key Skills Demonstrated:**
* Network traffic analysis with **Wireshark**.
* Reconstructing malicious payloads from TCP streams.
* Identifying C2 infrastructure using "domain fronting" techniques.
* Decoding exfiltrated data (Base64).
* Authoring a professional incident report with actionable prevention steps.

[**➡️ View Project 1 Details**](./Coursework-1-PCAP/README.md)
---

### Project 2: 📈 SIEM Analysis of BOTSv3 (Splunk)

An investigation of the "Boss of the SOC" (BOTSv3) dataset using **Splunk**. This project involved setting up a Splunk instance, ingesting a large-scale security dataset, and using Splunk Search Processing Language (SPL) to answer guided questions about a simulated incident, with a focus on AWS cloud security.

**Key Skills Demonstrated:**
* **Splunk** instance setup and data ingestion.
* Querying large datasets with **Splunk SPL**.
* Analyzing **AWS CloudTrail** and S3 access logs.
* Correlating data from multiple sources to investigate an incident.
* Creating a professional report and video presentation within GitHub.

[**➡️ View Project 2 Details**](./Coursework-2-SIEM/README.md)