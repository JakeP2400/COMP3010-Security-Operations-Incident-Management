# 🛡️ Project 1: PCAP Forensic Analysis (Cobalt Strike C2)

This project involved a detailed forensic analysis of a provided PCAP file to investigate a security incident. The full, detailed report is available below, along with a brief video walkthrough demonstrating the key investigative steps.

### 🎥 Video Walkthrough

*(This is where you would link your 10-minute video walkthrough)*
`[https://youtu.be/O7TAI9Pr7TI]`

---

### Summary of Findings

As detailed in the full report, the investigation successfully answered the three key questions:

1.  **Which system was compromised?**
    * The compromised system was the host at internal IP **`10.9.23.102`** (MAC: `00:08:02:1c:47:ae`). This host was the source of all malicious downloads and C2 communications.

2.  **What was the infection method?**
    * The infection was a multi-stage attack initiated at `16:44:38 UTC` when the host downloaded **`documents.zip`** from the malicious domain **`attirenepal.com`**. This zip contained a malicious Excel macro file (`chart-1530076591.xls`), which then executed to download further payloads.

3.  **What was the attack type?**
    * The attack was identified as an **advanced Cobalt Strike C2 (Command and Control) campaign**. This was confirmed by identifying C2 beaconing, the use of "domain fronting" (`ocsp.verisign.com`) to hide traffic, and post-infection activity including reconnaissance (`api.ipify.org`) and a final spam campaign (via SMTP).

### 🛠️ Methodology & Tools

* **Wireshark:** Used for all packet-level inspection, filtering (HTTP, DNS, SMTP), and TCP stream reconstruction.
* **VirusTotal:** Used to cross-reference suspicious IPs (`185.106.96.158`, `185.125.204.174`) and domains (`survmeter.live`, `securitybusinpuff.com`) to confirm their malicious reputation.
* **Base64 Decoder:** Used to decode the password (`13691369`) for the SMTP spam campaign.

---

### 📜 Full Incident Report

*(This is where you would add your final PDF. Make sure to upload it to this directory.)*

[**Download the Full PDF Report: `CW1_Report.pdf`**](./CW1_Report.pdf)