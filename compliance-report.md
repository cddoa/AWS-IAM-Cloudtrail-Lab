# AWS Cloud Environment Compliance Assessment

## Executive Summary
The AWS lab environment in this project is designed to test how industry-standard governance and compliance frameworks can be integrated with cloud-native security services. 
The lab simulates a secure enterprise environment by implementing IAM with least-privilege and MFA enforcement, CloudTrail and CloudWatch for audit logging and monitoring, GuardDuty for continuous threat detection, and Lambda for automated incident response.
The purpose of this assessment is to measure the lab’s alignment with ISO 27001:2022 Annex A security controls to identify strengths and highlight areas for improvement.

## Scope
Systems: AWS account, IAM users/roles, EC2 instances, S3 storage, AWS security monitoring services\
Compliance Framework: ISO 27001:2022

## Control Mapping

| AWS feature | ISO 27001 Annex A Control | Description | Effectiveness | Risk if Absent |
|-----|-----|-----|-----|-----|
|IAM Role Restrictions|5.15 - Access control|Enforces least privilege and MFA|Effective, tested with IAM policy simulator|Unauthorized access, privilege escalation|
|CloudTrail Logging|8.15 - Logging|Logs all AWS account activity|Effective, logs are stored indefinitely|Inability to detect anomalies|
|CloudWatch Alerts|8.15 - Logging/8.16 - Monitoring activities|Sends alerts via email on suspicious activity|Effective, alerts are triggered when tested|Delayed incident response|
|GuardDuty|8.16 - Monitoring activities|Detects malicious activity|Effective, simulated activity was detected|Undetected breaches|
|Lambda Automation|5.26 - Response to information security incidents|Quarantines EC2 instance when compromised|Effective, instance is quarantined when tested | Incident response delays
|S3 Tagging and Encryption| 5.13 Labeling of Information/8.24 Use of Cryptography| Resource tagging and enforced encryption | Effective | Non-compliance with data classification and storage policies
