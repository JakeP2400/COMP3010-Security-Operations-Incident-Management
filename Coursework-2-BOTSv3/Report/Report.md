## 📝 Coursework 2: BOTSv3 Incident Analysis and Presentation

### Task 

BOTSv3, or Boss of the SOC (BOTS) Dataset Version 3, is a publicly available, pre-indexed sample security dataset and Capture The Flag (CTF) platform created by Splunk to train and test the skills of cybersecurity professionals, students, and enthusiasts. It simulates a realistic security incident within a fictitious brewing company named "Frothly," providing a massive collection of logs—including network, endpoint, email, and cloud service data from environments like Amazon AWS and Microsoft Azure—which participants must analyze using Splunk's Search Processing Language (SPL) to investigate the simulated attack and answer specific questions following the cyber kill chain methodology.

Your individual task is to investigate and report on security incidents using the Boss of the SOC v3 (BOTSv3) dataset within Splunk.

---

### Setup and Dataset Retrieval

1.  Go to `https://github.com/splunk/botsv3` to retrieve the dataset.
2.  Set up your own **Splunk on Ubuntu VM**.
3.  Follow the instructions on the botsv3 repo to ingest the dataset.

---

### Deliverables 

1.  A **public GitHub repository** containing a **`README.md` file** written as your professional report.
2.  A **YouTube video presentation (max 10 minutes)** embedded/linked in the GitHub repository.
3.  **Evidence of continuous improvement** on your GitHub repo across **at least two weeks**, shown by commit frequency and timestamps.

This format mirrors industry practice for documenting security investigations.

---

### Acceptable Level of Generative AI Tool Use

**Partnered Generative AI tool use is required** as an integral part of the coursework, but **transparency is required**[

**Partnered Work (P1) includes:**
* Research further concepts.
* Write/generate/troubleshoot scripts to facilitate analysis.
* Report generation and improvements (README report, script crafting).

---

### Report Structure and Key Sections 

| Section | Weight | Description |
| :--- | :--- | :--- |
| **Introduction** | 10%  | Provide an overview of the SOC context, the BOTSv3 exercise, and the objectives of your investigation. Clearly define scope and assumptions. |
| **SOC Roles & Incident Handling Reflection** | 10% | Reflect on how SOC tiers, responsibilities, and incident handling methodologies relate to BOTSv3. Discuss prevention, detection, response, and recovery phases. |
| **Installation & Data Preparation** | 15% | Document Splunk installation, dataset ingestion, and validation steps. Provide supporting evidence (screenshots/configs). Justify setup choices in the context of SOC infrastructure. |
| **Guided Questions** | 40% | Choose and answer **ONE SET** of BOTSv3's **200-level questions** using Splunk queries and analysis. Present answers clearly, with supporting evidence (screenshots, query outputs, dashboards). Explain the SOC relevance of each answer. |
| **Conclusion, References and Presentation** | 5% | Summarise findings, key lessons, and SOC strategy implications. Highlight improvements for detection and response. Professionally structured, correctly referenced (IEEE style), and clearly written. |

---

### Evidence Presentation - Video and GitHub (20%)

#### Video Presentation (10%)
* Maximum **10 minute** recorded presentation.
* Summarises your key findings from BOTSv3.
* Demonstrates selected Splunk queries/dashboards.
* Reflects on SOC operations and incident response lessons learned.
* Is clear, professional, and suitable for a security management audience.

#### Continuous Github Improvements (10%)
* Evidence of continuous work being done in a span of **at least 4 weeks** (not including holidays) evidenced in Github pushes to show progress.
* The repo must be public for showcase.

---

### Key Expectations 

* Demonstrate deep understanding of SOC structures, roles, and responsibilities.
* Show practical Splunk analysis with accurate answers to BOTSv3 questions.
* Present evidence of critical reflection on SOC practices and incident handling.
* Use GitHub for professional technical documentation and continuous improvement.
* Deliver findings clearly in both **`README.md`** and video presentation.

---

### Report Guidelines 

* **Submission Format:** Public GitHub repository with a `README.md` as the report.
* **Word Count:** Max **2,000 words** (excluding appendices/screenshots).
* **Video Length:** Max **10 minutes**, YouTube unlisted link embedded in repo.
* **Continuous Improvement:** Repo must show commit activity across at least **4 weeks**.

### Submission Requirements 

* Provide answers on **DLE quiz**.
* **2000-word limit** incident writeup, inclusive of evidence. Writeup submitted as a **single PDF document to DLE**.
* Include **appendix** with completed Generative AI Declaration (not part of word limit).
* Video walkthrough (max 10 minutes).

---

### Question Set for Coursework 2

The focus is on AWS-related events, with some questions focusing on endpoint-related events. Provide answers on the DLE, but include evidence in your report.

| Q | Marks | Details | Hint/Guidance |
| :--- | :--- | :--- | :--- |
| **1** | 5 | List out the **IAM (Identity & Access Management) users** that accessed an AWS service (successfully or unsuccessfully) in Frothly's AWS environment?  | **Hint:** Use `aws:cloudtrail` as the source type. **Answer guidance:** Comma separated without spaces, in alphabetical order (Example: `ajackson,mjones,tmiller`). Refer to the provided AWS CloudTrail link. |
| **2** | 5 | What field would you use to alert that **AWS API activity has occurred without MFA** (multi-factor authentication)? | **Hint:** Use `aws:cloudtrail` as the source type. **Answer guidance:** Provide the full JSON path (Example: `iceCream.flavors.traditional`). Exclude events related to console logins. Keyword search with asterisks might be useful. Refer to provided links. |
| **3** | 5 | What is the **processor number** used on the **web servers**? | **Hint:** Use `hardware` as the source type in Splunk Search for hardware information. **Answer guidance:** Include any special characters/punctuation (Example: The processor number for Intel Core i7-8650U is `i7-8650U`). |
| **4** | 5 | **Bud accidentally makes an S3 bucket publicly accessible.** What is the **event ID** of the API call that enabled public access? | **Hint:** Use `aws:cloudtrail` as the source type to search for the `PutBucketAcl` event. **Answer guidance:** Include any special characters/punctuation. Refer to provided link. |
| **5** | 5 | What is **Bud's username**? | **Hint:** Use `aws:cloudtrail` as the source type. |
| **6** | 5 | What is the **name of the S3 bucket** that was made publicly accessible? | **Hint:** Use `aws:cloudtrail` as the source type. |
| **7** | 5 | What is the name of the **text file** that was **successfully uploaded into the S3 bucket** while it was publicly accessible? | **Hint:** Use `aws:s3:accesslogs`. HTTP status code might be helpful. Refer to provided link. **Answer guidance:** Provide just the file name and extension, not the full path (Example: `filename.docx`). |
| **8** | 5 | What is the **FQDN of the endpoint** that is running a **different Windows operating system edition** than the others? | **Hint:** Start with `winhostmon` as the source type. Expanding search to count operating systems and hosts will be helpful. |

---

### Grading Criteria

A detailed breakdown of how your work will be assessed is provided below.

| Criteria | Fail (<40%) | Pass (40-49%) | Merit (50-59%) | Merit (60-69%) | Distinction (70%+) | Weight |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Introduction** | No clear introduction, objectives missing. | Basic intro with vague scope. | Adequate intro with some SOC context. | Clear, structured intro with defined scope. | Professional, insightful intro; strong SOC contextualisation. | 10% |
| **SOC Roles & Incident Handling Reflection** | No reference to SOC processes. | Minimal discussion of SOC responsibilities. | Some understanding of SOC roles and incident handling methodologies. | Good explanation of SOC roles, escalation, and methodologies; response processes linked to findings. | Excellent critical reflection on SOC structures and professional-level insight. | 10% |
| **Installation & Data Preparation** | No evidence of Splunk setup or dataset ingestion. | Minimal description of setup, limited screenshots. | Adequate explanation of setup, dataset prepared with partial evidence. | Well-documented setup with comprehensive evidence and justification in SOC context. | Comprehensive documentation of Splunk installation/ingestion, critical justification of design choices. | 15% |
| **Guided Questions (BOTSv3 Q&A)** | BOTSv3 questions largely unanswered/incorrect. | Answers a few 200-level questions, limited evidence. | Accurate answers to a number of 200-level questions, some evidence provided. | Accurate answers to most 200-level questions, with strong evidence. | Complete, well-justified answers to all 200-level questions, comprehensive evidence and reflection. | 40% |
| **Conclusion, References & Professional Presentation** | No conclusion or irrelevant. Poor structure, no references, unclear writing. | Weak conclusion with limited connection to findings. | Adequate summary with some lessons learned. | Strong conclusion, clear lessons, SOC reflection. | Professional conclusion with synthesis of findings and forward-looking recommendations. | 5% |
| **Video Presentation** | No video submitted, or irrelevant content. | Video submitted but weak, poorly structured. | Clear explanation of findings but lacks polish. | Well-structured, professional summary of analysis. | Excellent, professional-quality presentation; clear, engaging, and strategic. | 10% |
| **Continuous Improvement (GitHub Commits)** | No evidence of ongoing work; single upload only. | Minimal commits with weak timestamps. | Some evidence of continuous improvement, limited frequency. | Regular commits over 2 weeks, clear progress in repo. | Excellent commit history showing continuous development, reflection, and professional repo management. | 10% |

---
