---
layout: post
title:  "AD Administration Lab"
date:   2025-07-08 17:52:42 +0000
categories: blog
---

<ins>Site:</ins> Hack the Box

<ins>Activity:</ins> Lab

<ins>Date:</ins> 7/10/2025

<ins>Objective:</ins>\
Simulate IAM tasks in a Windows AD environment to secure user access and enforce policies.

<ins>Tools Used:</ins>\
PowerShell, xfreerdp, Active Directory Users and Computers, Group Policy Management Console.

<ins>Summary:</ins>\
Leveraging my GSEC and GCIH certifications, I completed a Hack The Box lab to manage user accounts, groups, Group Policy Objects (GPOs), and computers in a Windows Server 2022 AD environment. Tasks included provisioning users, configuring RBAC via groups and OUs, enforcing secure GPOs, and auditing access, follwing requirements for secure identity management and log auditing per NIST 800-53.

#<ins>Actions Taken:</ins>\
**Task 1: Manage Users**\
  I opened PowerShell and used xfreerdp to connect to a AD connected Windows machine using the following PowerShell code: 
  <img width="1232" height="27" alt="image" src="https://github.com/user-attachments/assets/af5336fd-e439-4681-b669-099b5d6457b6" />

  Once logged into to the Windows Machine, I navigated to the AD Service Manager to add 3 new users using the GUI.  I then searched for inactive users and deleted their accounts using the find function because I was not given information on which department these 2 employees were working in before they left the company.  Finally, I had to resolve a user ticket.  I used the find function to locate a user who had locked their account and reset their password and unlocked their account, ensuring they were required to change their password on their next login.

**Task 2: Manage Groups and Other Organizational Units**\
  In the AD Service Manager, I navigated to the correct path to add a new Organizational Unit.  Within the new OU, I added a new user group with a local domain group scope and a security group type.  I proceeded to add the 3 new users I created in Task 1 to the new user group.  

**Task 3: Manage Group Policy Objects**\
  In the AD Service Manager, I navigated to the Group Policies window.  I navigated to the correct path to copy an existing Group Policy Obiject and rename it for the new OU created in Task 2.  Once created, I edited some of the policies within the Group Policy Object to enable the command line prompt and disable all removable storage classes.  I then updated the password policy for the new Group Policy Object by making the minimum length longer than the default and enforcing password history to ensure new passwords are not repeated when making new ones.  

**Task 4: Add and Remove Computers to the Domain**\
  In the AD Service Manager, I navigated back to the Active Directory Users and Computers.  I added a new computer and moved it to the Security Analysts OU created in Task 2 for the new users to utilize and be able to log into.  

<ins>Security Outcomes:</ins> \
-Deleting inactive accounts reduced the attack surface, per NIST 800-53 (AC-2).\
-RBAC via groups and OUs ensured least privilege access.\
-GPO policies mitigated risks of unauthorized device usage and weak passwords.\
  
<ins>Lessons Learned:</ins>\
  This lab challenged me to master Active Directory (AD) management, a critical skill for implementing secure identity and access controls. Initially, I encountered PowerShell errors when creating users (e.g., incorrect syntax in New-ADUser commands), which I resolved by debugging the code and verifying parameters against Microsoft documentation, reinforcing my GSEC-trained attention to detail. Troubleshooting a Group Policy Object (GPO) that failed to apply due to incorrect OU linkage taught me the importance of precise configuration to enforce role-based access control (RBAC), aligning with NIST 800-53 standards. This experience strengthened my ability to manage secure access, mitigate risks through policy enforcement, and communicate technical processes clearly, leveraging my teaching background to document procedures effectively for diverse stakeholders.
