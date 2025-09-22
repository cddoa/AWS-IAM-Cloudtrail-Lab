# AWS Cloud Environment Compliance Assessment

## Executive Summary
The AWS lab environment in this project is designed to test how industry-standard governance and compliance frameworks can be integrated with cloud-native security services. 
The lab simulates a secure enterprise environment by implementing IAM with least-privilege and MFA enforcement, CloudTrail and CloudWatch for audit logging and monitoring, GuardDuty for continuous threat detection, and Lambda for automated incident response.
The purpose of this assessment is to measure the lab’s alignment with ISO 27001:2022 Annex A security controls to identify strengths and highlight areas for improvement.

## Scope
Systems: AWS account, IAM users/roles, EC2 instances, S3 storage, AWS security monitoring services\
Compliance Framework: ISO 27001:2022

## Control Mapping

| AWS feature | ISO 27001 Annex A Controls | Description | Effectiveness | Risk if Absent |
|-----|-----|-----|-----|-----|
|IAM Role Restrictions|5.15 - Access control, 5.16 Identity management, 5.18 Access rights|Enforces least privilege and MFA|Effective, tested with IAM policy simulator|Unauthorized access, privilege escalation|
|EC2 Instance Tags|5.9 - Inventory of information and other associated assets|Maintains inventory of cloud resources|Partially effective, needs systematic tagging|Non-compliance with asset classification policies|
|CloudTrail Logging|8.15 - Logging|Logs all AWS account activity|Partially effective, log retention policy not explicitly configured|Inability to detect anomalies|
|CloudWatch Alerts|8.15 - Logging/8.16 - Monitoring activities|Sends alerts via email on suspicious activity|Effective, alerts are triggered when tested|Delayed incident response|
|GuardDuty|8.16 - Monitoring activities, 5.25 - Assessment and decision on information security events|Detects malicious activity|Effective, simulated activity was detected|Undetected breaches|
|Lambda Automation|5.26 - Response to information security incidents|Quarantines EC2 instance when compromised|Effective, instance is quarantined when tested | Incident response delays
|S3 Bucket Tagging| 5.12 - Classification of Information, 5.13 - Labeling of Information | Classifies and labels data stored in S3 buckets | Partially effective, CloudTrail logs stored but no systematic tagging | Non-compliance with data classification policies, unclear data sensitivity levels
|S3 Bucket Encryption|8.24 - Use of Cryptography|Encrypts data at rest|Partially effective, Likely enabled by default for CloudTrail but not explicitly verified|Non-compliance with data storage policies, data confidentiality breach|

## Risk Analysis
Risk analysis conducted using a 5x5 risk matrix
* Likelihood: 1-5
* Impact: 1-5
* Risk score: Likelihood x Impact

|Asset|Threat|Likelihood|Impact|Risk Score|Justification|
|-|-|-|-|-|-|
|S3 CloudTrail logs | Data breach via misclassification|4|4| 16 | S3 buckets do not have classification tags, could be exposed through overpermissive bucket policies|
|EC2 Instances| Unauthorized privilege escalation, lateral movement | 3 | 4 | 12 |Lack of specific security tags, production and development instances lack network segmentation creating lateral movement risk, mitigated by IAM policy|
|IAM User Accounts| Insider threat and account hijacking | 3 | 4 |12 | No user deprovisioning process, terminated users can retain access|
|IAM groups and policies|Identity management failures|2|4|8|No automated user lifecycle management, risk of manual misconfigurations|
|CloudWatch alerts|Insufficient threat detection |2|4|8|Only basic failed login alarms configured|
|GuardDuty Findings|Insuficient threat detection and assessment|2|3|6|Potential for false negatives and no formal process for traiging findings|
|AWS Infrastructure|Physical security breach|1|3|3|Physical data center security managed by AWS, relies on AWS phyiscal security standards|
|Lambda Functions|Function compromise|1|2|2|Minimal attack surface| 
