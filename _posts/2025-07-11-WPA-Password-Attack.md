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
In this HackTheBox challenge, I conducted a wireless penetration test to capture and crack a WPA password, demonstrating proficiency in network security assessment. Using the aircrack-ng suite, I successfully scanned for access points, captured a WPA handshake through a targeted deauthentication attack, and cracked the password with a dictionary attack. This exercise showcased my skills in packet analysis, strategic problem-solving, and the use of industry-standard tools while adhering to ethical hacking principles. The outcome highlighted the critical need for strong password policies to mitigate brute-force vulnerabilities, reinforcing my ability to identify and address real-world security risks. This project reflects my readiness to contribute to cybersecurity roles by delivering thorough and responsible vulnerability assessments. 

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
This challenge highlighted critical vulnerabilities in WPA-protected wireless networks and their implications for organizational security. Key outcomes include:

* Vulnerability Identification: The successful capture and cracking of the WPA handshake exposed the risks of weak passwords, particularly those susceptible to dictionary attacks. This underscores the need for organizations to enforce strong, complex passphrases to mitigate brute-force attacks.

* Attack Vector Analysis: The deauthentication attack demonstrated how attackers can exploit client-AP interactions to capture handshakes. This insight emphasizes the importance of monitoring for unauthorized deauthentication attempts and implementing intrusion detection systems to alert on suspicious activity.

* Mitigation Recommendations: To secure wireless networks against similar attacks, organizations should:

  * Use strong, unique WPA2/WPA3 passphrases (at least 12 characters, avoiding common words).

  * Disable WPS (Wi-Fi Protected Setup) to prevent alternative attacks like Pixie Dust.

  * Implement MAC address filtering or enterprise-grade authentication (e.g., WPA2-Enterprise with RADIUS) for enhanced security.

  * Regularly audit network configurations to detect misconfigurations or weak encryption protocols.

* Broader Security Implications: This exercise highlighted the importance of a defense-in-depth approach, combining strong password policies, network monitoring, and user education to reduce the attack surface. As a security professional, I can apply these insights to assess and strengthen wireless network configurations in enterprise environments.

By completing this challenge, I demonstrated my ability to identify, exploit, and propose mitigations for wireless network vulnerabilities, skills directly applicable to roles in penetration testing and network security.
  
**Lessons Learned:**
-  
This HackTheBox challenge provided a hands-on opportunity to deepen my understanding of wireless network security and penetration testing methodologies. Key takeaways include:

* Proficiency with Industry-Standard Tools: I gained practical experience using the aircrack-ng suite (airodump-ng, aireplay-ng, aircrack-ng) to perform wireless network reconnaissance, packet capture, and password cracking. This reinforced my ability to select and apply appropriate tools for specific attack vectors, a critical skill in penetration testing.

* Attention to Detail in Packet Analysis: Capturing a valid WPA handshake required precise configuration of tools (e.g., setting the correct channel and BSSID) and careful monitoring of packet captures. This process honed my ability to analyze network traffic and troubleshoot issues, such as ensuring the Wi-Fi adapter was in monitor mode.

* Strategic Problem-Solving: The challenge demanded a systematic approach, from scanning for access points to executing a deauthentication attack and cracking the password. This strengthened my ability to break down complex problems into manageable steps, a valuable skill for assessing and exploiting vulnerabilities in real-world environments.

* Ethical Hacking Mindset: Conducting this attack in a controlled environment underscored the importance of ethical considerations in cybersecurity. I ensured all actions complied with HackTheBox’s guidelines, reinforcing my commitment to responsible and authorized testing practices.

These lessons have enhanced my technical expertise and prepared me to tackle real-world wireless security assessments with confidence and precision.
