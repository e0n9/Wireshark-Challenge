# Wireshark-Challenge
Security Blue Team - Introduction to Network Analysis Free Course: https://elearning.securityblue.team/home/courses/free-courses/introduction-to-network-analysis#content#analysis-with-wireshark#introduction-to-wireshark#activity-wireshark-challenge

## Objective

The purpose of this challenge is to gain hands-on familiarity with navigating around the Wireshark UI, applying various filters, and analyzing .pcap files. 

### Notes
The .pcap files can be downloaded from within the course content. Security Blue Team has assured that the files are not malicious, however I did get a warning when downloading them using Firefox. I chose to download them using my Kali Linux VM instead. Plus Kali Linux comes with Wireshark already installed.

### Skills Learned

- Proficiency in navigating around Wireshark
- Understanding of network analysis 

### Tools Used

- Wireshark

## Steps
PCAP 1
1. Which protocol was used over port 3942?

With the file opened in Wireshark, go to Statistics > Endpoints > UDP > Right-click the line with Port 3942 > Apply as Filter > Selected > Head back to main screen

![image](https://github.com/user-attachments/assets/84c18121-a5c1-4801-b35d-97f77897f0dd)

Ans: SSDP

2. What is the IP address of the host that was pinged twice?

Enter "icmp" into the display filter field. We see 2 ICMP ping requests to 8.8.4.4

![image](https://github.com/user-attachments/assets/e3c30827-efa3-4b67-8f17-7b5cdf080c63)

Ans: 8.8.4.4

3. How many DNS query response packets were captured?

Type "dns" into the display filter, select the first packet that shows "Standard query response".

![image](https://github.com/user-attachments/assets/83c0ccbf-8a98-4a6a-946b-d16c55c936a1)

At the bottom left panel, click on the drop-down for Domain Name System (response) > Flags > Right click "Response: Message is a response" > Apply as Filter " Selected. Check the number of packets displayed on the bottom right panel.

<img width="811" alt="Screenshot 2025-04-25 142653" src="https://github.com/user-attachments/assets/07b1835e-d7d4-43b6-b15e-1e9bb22ac587" />

Ans: 90

4. What is the IP address of the host which sent the most number of bytes?

Go to Statistics > Endpoints > IPv4 > Tx Bytes (toggle it to display in descending order)

<img width="443" alt="Screenshot 2025-04-25 143652" src="https://github.com/user-attachments/assets/77ce2e36-1981-46ce-a44a-7ede7cd995d8" />

Ans: 115.178.9.18

PCAP 2
1. What is the WebAdmin password?

Go to Statistics > Protocol Hierachy. It makes sense that I should be looking at HTTP traffic in this case.

<img width="661" alt="Screenshot 2025-04-25 145138" src="https://github.com/user-attachments/assets/36db367d-45ca-423e-99f5-dece4f80593e" />

Type "http" into display filter, there is a GET request under Packet 2141, for a password.txt file. 

![image](https://github.com/user-attachments/assets/2d2f7597-3786-48fd-a95c-eb773eea8a0f)

Right click on packet > Follow > HTTP Stream

![image](https://github.com/user-attachments/assets/2756973d-fb63-461c-a7fe-b4914fc6c64b)

Ans: sbt123

2. What is the version number of the attacker’s FTP server?

From Question 1, we can deduce the source IP address of the attacker as well. In the display filter, type in "ftp and ip.src == 192.168.56.1". Select Packet 4243. On the bottom left panel, click to drop down File Transfer Protocol (FTP) to show the version of the FTP server (pyftpdlib).

![image](https://github.com/user-attachments/assets/66a3f19e-1271-46b0-9fd8-474bca38041b)

Ans: 1.5.5

3. Which port was used to gain access to the victim Windows host?

From Question 1, we deduce that the source IP address (attacker) is 192.168.56.1, and the target (destination) IP address is 192.168.56.103. Using "ip.src == 192.168.56.1 and ip.dst == 192.168.56.103 and tcp.flags.ack == 1" as display filter, this displays all packets from the attacker to the target with ACK flag set. Scrolling up to the very first packet, we see the port used by the attacker to first gain access to the target.

![image](https://github.com/user-attachments/assets/df7d5dc8-571c-477b-8072-1e86a8f5b91a)

Ans: 8081

4. What is the name of a confidential file on the Windows host?

Using Packet 4130 from the previous question, Right click > Follow > TCP Stream. Find "confidential".

<img width="365" alt="Screenshot 2025-04-25 221431" src="https://github.com/user-attachments/assets/e8708a6b-5c0c-4420-bae8-6f8d2e3a7376" />

Ans: Employee_Information_CONFIDENTIAL.txt

5. What is the name of the log file that was created at 4:51 AM on the Windows host?

Using the same TCP Stream has the previous question, type ".log" into Find, look for a log file created at 4:51 AM.

![image](https://github.com/user-attachments/assets/1ffb0d3a-5b6b-4993-8d24-ce4680a6f72c)

Ans: LogFile.log
