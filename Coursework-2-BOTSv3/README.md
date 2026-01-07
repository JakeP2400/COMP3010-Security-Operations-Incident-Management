# Digital Forensic Analysis Report: BOTSv3 Dataset
**Context:** Splunk-managed Security Operations Centre (SOC)
**Subject:** S3 Bucket Public Exposure & Endpoint Compliance Analysis

---

## Executive Summary
This report is a digital forensic analysis of the BOTSv3 dataset within a Splunk-managed Security Operations Centre (SOC) context. My investigation surrounds a critical security failure involved an S3 bucket becoming publicly accessible. The expose remained active for a period, potentially allowing a threat actor to interact with the storage and contents of the bucket. This document will provide the technical investigation and evidence for the findings and a roadmap for the remediations following.
---

## Introduction and Scope
The modern threat landscape demonstrates that a proactive approach is required for logging and monitoring. This investigation uses **Splunk Search Processing Language (SPL)** to query the **Boss of the SOC (BOTSv3)** dataset, which simulates a real-world breach at "Frothly," a fictitious company.

### Data Sources in Scope:
* **AWS CloudTrail:** Auditing API calls and account activity.
* **S3 Access Logs:** Tracking access requests to S3 buckets.
* **WinHostMon:** Monitoring Windows host system information.

The objectives of this report and investigation follow the S3 breach, and will include who caused the breach, what caused the breach, when did the breach occur and how did the breach occur and future recommendations for Frothly. This will establish the current security of Frothly through both its hardware and its software.
---

## SOC Roles and Incident Handling


* **SOC Analyst (Tier 1):** First responders. Perform basic alert triage to determine if a detection is harmful and report through proper channels.
* **SOC Analyst (Tier 2):** Perform deeper investigations, correlating data from multiple sources for detailed analysis.
* **SOC Analyst (Tier 3):** Experienced professionals who hunt for threats and lead incident response activities (containment, eradication, and recovery).

> **Note:** This report reflects analysis from all tiers, primarily **Tier 2** (technical investigation) and **Tier 3** (lessons learned and recommendations).

---

## Installation and Data Preparation
The Splunk instance was deployed on **Ubuntu 24.04.3 LTS** as a **single-instance deployment**. This emulates an enterprise environment where one instance manages all three primary functions:

1. **Data Input Tier**
2. **Indexer Tier**
3. **Search Management Tier**


### Preparation Steps:
1. **Download:** Acquired `botsv3_data_set.tgz` from the BOTSv3 GitHub.
2. **Extraction:** Extracted and copied the dataset into the Splunk apps folder using root permissions.
3. **Verification:** Validated data availability using the SPL command:
   `index=botsv3 earliest=0`

---

## Technical Analysis (Guided Questions)

### 1. Cloud Identity Auditing
**Question:** List the IAM users that accessed an AWS service?
**Analysis:** Using the `aws:cloudtrail` sourcetype, I analyzed the `userIdentity.userName` field.
* **SPL:** `index=botsv3 sourcetype="aws:cloudtrail" | stats count by userIdentity.userName`
* **Result:** The four IAM users are `bstoll`, `btun`, `splunk_access`, and `web_admin`.

### 2. Multi-factor Authentication (MFA) Compliance
**Question:** What field identifies AWS API activity without MFA?
**Analysis:** By filtering `eventType` against MFA-related fields, I identified the field responsible for tracking API authentication status.
* **Field:** `userIdentity.sessionContext.attributed.mfaAuthenticated`
* **Observation:** When this value is `false`, API activity occurred without MFA.

### 3. Asset Identification and Inventory
**Question:** What is the processor number used on the web servers?
**Analysis:** Investigating the `winhostmon` sourcetype for hardware events.
* **Value Found:** `CPU_TYP` = `Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz`.
* **Processor Number:** `E5-2676`.

---

## Cloud Data Breach (S3 Bucket Breach)

### 4. Event ID of the Public Access API Call
**Question:** What is the eventID of the API call that enabled public access?
**Analysis:** S3 uses Access Control Lists (ACLs). I searched for the `PutBucketAcl` eventName.
* **EventID:** `ab45689d-69cd-41e7-8705-5350402cf7ac`.

### 5. Responsible User
**Question:** What is Bud's username?
**Analysis:** The `userName` field within the `PutBucketAcl` event reveals the culprit.
* **User:** `bstoll`.

### 6. Compromised Bucket Name
**Question:** What is the name of the S3 bucket made public?
**Analysis:** Found in the `requestParameters.bucketName` field.
* **Bucket Name:** `frothlywebcode`.

### 7. Malicious File Upload
**Question:** What text file was uploaded while the bucket was public?
**Analysis:** Queried `aws:s3:accesslogs` for "txt" files with a `PUT` operation.
* **File Name:** `OPEN_BUCKET_PLEASE_FIX.txt`.
* **Significance:** This confirms a threat actor identified the vulnerability and successfully interacted with the storage.

---

## Endpoint Investigation and Compliance

### 8. Shadow IT & FQDN
**Question:** What is the FQDN of the endpoint running a non-compliant Windows edition?
**Analysis:** Used `winhostmon` to compare Operating Systems across hosts.
* **Anomaly:** Host `BSTOLL-L` was running *Microsoft Windows 10 Enterprise*, while others were on different standard versions.
* **FQDN Search:** `index="botsv3" host="BSTOLL-L" | search domain AND BSTOLL-L`
* **Result:** `BSTOLL-L.froth.ly`.

---

## Risk and Damage Assessment
* **Confidentiality:** The `frothlywebcode` bucket content was exposed; potential for code cloning and vulnerability analysis.
* **Integrity:** The successful `PUT` request of `OPEN_BUCKET_PLEASE_FIX.txt` proves that public write access was enabled.
* **Threat Actor Detection:** The rapid upload suggests Frothly’s infrastructure is under active observation by external parties.

---

## Security Recommendations

1. **Credential Rotation:** Immediately reset credentials for `bstoll`.
2. **Standardization:** Re-image `BSTOLL-L` to the corporate standard Windows edition to eliminate **Shadow IT**.
3. **Proactive Alerting:** Implement Splunk alerts for all `PutBucketAcl` events to provide the SOC with real-time visibility into permission changes.
4. **AWS Config:** Enable **AWS Config Managed Rules** to automatically remediate buckets that are set to public.
5. **Enforce MFA:** Mandate MFA for all IAM users for both Console and API access.



---

## Conclusion
The Frothly S3 bucket incident was caused by a configuration error by user `bstoll`. The investigation revealed a lack of MFA and the presence of a non-compliant "Shadow IT" device. By implementing the recommended technical controls and monitoring, Frothly can significantly reduce the risk of a repeat occurrence.

---

## References
1. [Splunk Search Overview](https://help.splunk.com/en/splunk-enterprise/search/search-manual/10.0/search-overview/about-the-search-language)
2. [Splunk Deployment Types](https://help.splunk.com/en/splunk-enterprise/get-started/overview/9.4/about-splunk-enterprise/about-splunk-enterprise-deployments)
3. [AWS IAM Introduction](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
4. [AWS CloudTrail Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)
5. [F5 Glossary: FQDN](https://www.f5.com/glossary/fully-qualified-domain-name-fqdn)
6. [NCSC Guidance: Shadow IT](https://www.ncsc.gov.uk/guidance/shadow-it)
7. [AWS Config Managed Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_use-managed-rules.html)