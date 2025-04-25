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




