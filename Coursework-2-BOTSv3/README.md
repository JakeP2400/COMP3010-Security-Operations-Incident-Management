# 🛡️ Project 2: Splunk Incident Analysis (BOTSv3 Dataset)

This project has involved using Splunk to aanalyse the BOTSv3 dataset (Boss of the SOC). The full report will be available once completed with a video walkthrough.

### Summary of My Findings

As detailed in the full report, the investigation successfully answered the three key questions:

1.  **List out the IAM users that accessed an AWS service (successfully or unsuccessfully) in Frothly's AWS environment?**
    * Using the command **index="botsv3" earliest=0 sourcetype="aws:cloudtrail"**, it revealed that the users who aaccessed an AWS service were **bstroll,btun,splunk_access,web_admin**. This is evidenced in (./Screenshots/Q1).
