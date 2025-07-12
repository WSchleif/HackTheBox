---
layout: post
title:  "WPA Password Attack"
date:   2025-07-11 00:00:00 +0000
categories: blog
---

**Site:**
-
Hack the Box

**Activity:**
-
Lab

**Objective:**
-
To gain access to a password-protected Wi-Fi network and retrieve a flag located on the network. 

**Tools Used:**
-
xfreerdp, airmon-ng, airodump-ng, aireplay-ng, hcspcapngtool, hashcat


**Summary:**
-
I remotely connected to a target machine, where I enable monitoring mode to scan for available Wi-Fi networks.  I executed a deauthentication attack on the client found and forced a reconnect to the access point, at which I saved the handshake to a .cap file.  I converted the .cap file to the correct format to use with Hashcat, where I then utilized Hashcat to crack the password hash and reveal the plain-text password.  Using the password, I successfully connected to the access point and retrieved a flag at 192.168.1.1.  

**Actions Taken:**
-
<ins>Step 1: Connect to target machine </ins>\
  I opened a bash terminal and used the following code to remotely connect to the target machine:
  <img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/8e9b6ed6-3c2f-4d03-9cfb-76621664d696" />

<ins>Step 2: Perform Wi-Fi Reconnaissance </ins>\
  I opened a bash terminal on the target machine and used the following code to enable monitoring mode on the wlan0 using airmon-ng:
  <img width="920" height="602" alt="image" src="https://github.com/user-attachments/assets/a1529476-d9cd-43e2-a71f-303b4b02f1d0" />
  *Monitor mode allows the Wi-Fi adapter to capture all packets in the air, including those not destined for the device, which is essential for capturing WPA handshakes.*
  
   Next, I used the following code and airodump-ng to scan for available Wi-Fi networks and their associated clients: 
  <img width="915" height="129" alt="image" src="https://github.com/user-attachments/assets/b51f4c7a-f153-42c8-81f6-31b97626ea7c" />
  **I initially encountered an error, where I had mistyped airodump-ng as airdump-ng, and then encountered another error where I needed root privileges to run the command, so I added sudo at the beginning**

<ins>Step 3: Deauthentication Attack</ins>\
 I then executed a deauthentication attack on the client found using the following code and aireplay-ng so it it forced to reconnect to the access point: 
 <img width="1045" height="319" alt="image" src="https://github.com/user-attachments/assets/3f1fdb10-86d0-4efb-ace8-92b5ec79e4dc" />
 *aireplay-ng forces a device to reconnect and enable me to retrieve a handshake, which is crucial to WPA password cracking*

<ins>Step 4: Extract the Hash</ins>\
  I extracted the hash from the .cap file for use with Hashcat using the following code and hcxpcapngtool: 
  <img width="1048" height="606" alt="image" src="https://github.com/user-attachments/assets/a90a483c-5feb-4750-86fa-8b05febc6e94" />
  *.cap files are not compatible with Hashcat, so you need to convert to a format compatible with Hashcat so you can crack the password*

<ins>Step 5: Crack the Password Hash</ins>\
  I proceeded to crack the hash using the 22000 option in Hashcat using the following code and Hashcat:
  <img width="1046" height="606" alt="image" src="https://github.com/user-attachments/assets/ec2c9b5d-f10e-40ab-8516-b8532ba471b4" />

  I revelead the cracked password using the following code and Hashcat:
  <img width="1042" height="605" alt="image" src="https://github.com/user-attachments/assets/be1fd131-536e-4b37-9205-d1d339ec456f" />

<ins>Step 6: Connect to the Network and Retrieve the Flag</ins>\
  I was then able to successfully connect to the network using the password and navigate to 192.168.1.1 to retrieve the flag located there:
  <img width="711" height="258" alt="image" src="https://github.com/user-attachments/assets/306e18c5-7143-466f-8a7b-9661a12fa47e" />


**Security Outcomes:** 
-
1) The Wi-Fi network was compromised
2) The Wi-Fi password was not strong enough to withstand password cracking using Hashcat
3) The flag was retrieved after gaining access to the wireless network and navigating to 192.168.1.1
  
**Lessons Learned:**
-  
I learned that using sudo in front of commands in Linux is often necessary to run them, as many require sudo access to execute.  I had to research how to successfully scan, deauthenticate, and force reconnect a client to a Wi-Fi access point to obtain the handshake.  I also had to research how to convert the .cap file to the correct format to use with Hashcat and crack the password.  
