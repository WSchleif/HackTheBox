---
layout: post
title:  "AD Administration Lab"
date:   2025-07-08 17:52:42 +0000
categories: blog
---

Site: Hack the Box

Activity: Lab

Date: 7/10/2025

Summary: 

Actions Taken:
Task 1: Manage Users
  I opened PowerShell and used xfreerdp to connect to a AD connected Windows machine.  Once logged into to the Windows Machine, I navigated to the AD Service Manager to add 3 new users using the GUI.  I then searched for inactive users and deleted their accounts using the find function because I was not given information on which department these 2 employees were working in before they left the company.  Finally, I had to resolve a user ticket.  I used the find function to locate a user who had locked their account and reset their password and unlocked their account, ensuring they were required to change their password on their next login.

Task 2: Manage Groups and Other Organizational Units
  In the AD Service Manager, I navigated to the correct path to add a new Organizational Unit.  Within the new OU, I added a new user group with a local domain group scope and a security group type.  I proceeded to add the 3 new users I created in Task 1 to the new user group.  

Task 3: Manage Group Policy Objects
  
