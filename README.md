# AWS-IAM-Cloudtrail-Lab

## Overview
    
The purpose of this lab is to create an AWS cloud security architecture that enforces least privilege access, monitors account activity, and alerts on suspicious logins. The lab leverages IAM, CloudTrail, CloudWatch and two isolated EC2 instances to simulate a secure and monitored enterprise environment. The setup was tested  by simulating failed logins, validating IAM policy enforcement using the IAM Policy Simulator, and confirming CloudWatch alarm triggers via email notifications.
  
## Skills and Tools Demonstrated
* **AWS Identity and Access Management (IAM):** Created user groups, policies using the principle of least privilege, tag-based resource access control, MFA enforcement policies.
* **AWS CloudTrail:** Logging management events, integration with CloudWatch for real-time alerting.
* **AWS CloudWatch:** Created metric filters and alarms for automated alerting. 
* **AWS GuardDuty** Deployed and managed continuous threat detection to identify malicious activity and potentially security risks.
* **Security Best Practices:** Principle of least privilege, MFA enforcement, real-time monitoring and alerts.

# EC2 instances

<img width="1401" height="311" alt="image" src="https://github.com/user-attachments/assets/5ae6ff97-a6be-4421-9601-1486b831dc59" />
  
After setting up the AWS root account I created two EC2 instances: a production environment and a development environment to simulate an enterprise environment.

# IAM User Groups and Policies
![groups](https://github.com/user-attachments/assets/b54df589-a3d7-4de1-ab27-073fe4d71d09)

Created two user groups for the two EC2 instances.
  
  
![developmentpolicy](https://github.com/user-attachments/assets/ad87a6b1-4b2e-47b3-bc91-39d23c9315be)
  
Policy for users in the dev group that allows all EC2 actions only for the development instance, allows describe actions for all EC2 resources and denies the ability to create and delete tags for all instances.
  
<img width="1071" height="837" alt="image" src="https://github.com/user-attachments/assets/f21019a6-7bb8-4b57-9392-d91073ff11e3" />
  
Same type of policy created for the production user group.
  
![users](https://github.com/user-attachments/assets/39a1c1cd-156a-4ce6-b331-d66605f81ca8)
  
Added users to both user groups.
  
![policySim](https://github.com/user-attachments/assets/49990533-1ee9-4fbb-b4cb-dda3c481ee60)
  
Policy Simulator used to ensure policies are working.
  
# MFA Enforcement
  
![MFAenforcement](https://github.com/user-attachments/assets/6116216f-54b5-4a21-8faa-9665c6d1e94b)
  
Policy created to force users to set up multi-factor authentication. The policy denies the user access to all AWS resources except the ones needed to set up MFA if they do not have MFA set up.

# Event logging with CloudTrail
  
![Cloudtrail](https://github.com/user-attachments/assets/ea90a6a5-5a99-461b-a8a0-101e5b44645e)
  
New CloudTrail trail to log management events like logins. The trail is configured to send logs to a CloudWatch log group.
  
# Metric Filter and Alarm Setup with CloudWatch  
  
<img width="1368" height="674" alt="image" src="https://github.com/user-attachments/assets/f72e262f-99f2-4ff2-a140-da4fb83d56d2" />
  
Metric filter created for the CloudWatch log group to detect failed logins.
  
<img width="1113" height="468" alt="image" src="https://github.com/user-attachments/assets/5d73115b-6060-412f-aab7-02dd7dc5aa9d" />
  
Suspicious login activity alarm created for the metric filter, threshold set to 3 or more failed login attempts.
  
## Testing the Alarm
  
![Alarm test](https://github.com/user-attachments/assets/27807dba-f08d-415c-8e5e-f6c3d2dee8b6)
  
![AlarmEmail](https://github.com/user-attachments/assets/25d6bff1-bd5e-417d-a5ad-2848b4bae46d)
  
  
Purposely failed to log in more than three times to ensure the alarm works.
  
  
#
  
# Threat Detection with GuardDuty
  
![guardduty](https://github.com/user-attachments/assets/0eda5f29-01dd-4293-ac66-e789c6037167)
  
Enabled AWS GuardDuty for continous threat detection and monitoring.
  
<img width="1352" height="552" alt="image" src="https://github.com/user-attachments/assets/07ec93a2-2fee-45b8-b1cc-9a7cbd28b43b" />
  
Data sources for GuardDuty include CloudTrail, DNS and VPC flow logs.

## Testing threat detection
  
![nmap](https://github.com/user-attachments/assets/7f7be3fb-f88b-4618-9894-d4a354cdfbca)
  
Performing an NMAP portscan from one EC2 instance to another.
  

![nmapdetected](https://github.com/user-attachments/assets/acae072b-b444-4e5e-84b3-788b5ace531e)
  
Outbound NMAP scan from the EC2 instance is detected and flagged with medium severity.
  
![sampleFindings](https://github.com/user-attachments/assets/d73719e8-b273-45a6-98c6-cc09d096d850)
  
Findings can also be generated with GuardDuty's generate sample findings feature.

#
