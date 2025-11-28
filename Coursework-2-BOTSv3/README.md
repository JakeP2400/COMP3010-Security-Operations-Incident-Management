# 🛡️ Project 2: Splunk Incident Analysis (BOTSv3 Dataset)

This project has involved using Splunk to aanalyse the BOTSv3 dataset (Boss of the SOC). The full report will be available once completed with a video walkthrough.

### Summary of My Findings

As detailed in the full report, the investigation successfully answered the three key questions:

1.  **List out the IAM users that accessed an AWS service (successfully or unsuccessfully) in Frothly's AWS environment?**
    * Using the command **index="botsv3" earliest=0 sourcetype="aws:cloudtrail"**, looking at the **userIdentity.userName88 field, we can see that the users who accessed an AWS service were **bstoll,btun,splunk_access,web_admin**. This is evidenced in (./Screenshots/Q1).
    * An alternative method to clicking the field would be, to use the command **index=botsv3 sourcetype="aws:cloudtrail"
    | stats count by userIdentity.userName** and to then view the "Statistics" tab which would show the four IAM users. In this case confirming **bstoll,btun,splunk_access,web_admin**. This is evidenced in (./Screenshots/Q1).

2. **What field would you use to alert that AWS API activity has occurred without MFA?**
    * Using the command **fieldsummary** and **search field**, I have been able to find two fields which contain MFA, and after viewing the values of both against the event types, by analysing using the statistics tab, it shows that "additionalEventData.MFAUsed" has only been using for an eventType of "AwsConsoleSignIn" whereas **userIdentity.sessionContext.attributes.mfaAuthenticated** has beeen used for aan eventType of **AwsApiCall** which demonstrates the API activity.

3. **What is the processor number used on the web servers?**
    * Using the command **index="botsv3" sourcetype="hardware"**, we can view that the events output as a result of this are 3 Events which contain hardware information. By analysing these, the value of **CPU_TYPE** is **Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz**, and when put into the form requested is **E5-2676**.

4. **Bud accidentally makes an S3 bucket publically accessible. What is the eventID of the API call that enabled public access?**
    * Using the command **index="botsv3" sourcetype="aws:cloudtrail" eventName=PutBucketAcl**, we can see the events of "PutBucketAcl", this event sets the ACL (Access Control List) of an existing bucket. By analysing both events, we can see the ACL (Access Control List) of both is [""], meaning it is publically available. Therefore the earlier event caused the S3 bucket to be publically available, which is the eventID **ab45689d-69cd-41e7-8705-5350402cf7ac**.

5. **What is Bud's username?**"
    * Using the event from the previous question, we can find the field of "userName" in this case the content is "bstoll", indicating that user who made the S3 bucket publically available is bstoll, and as we know this is Bud, **Buds username is bstoll**.
