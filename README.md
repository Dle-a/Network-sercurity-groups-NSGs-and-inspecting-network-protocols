# Network-sercurity-groups-NSGs-and-inspecting-network-protocols<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04



<h2>The Set-Up
Within Azure, i set up two VMs within the same virtual network to ensure that they are able to communicate with each other. One VM running Windows 10 Pro and the other using Ubuntu. The Windows VM will connect to the other via the command line/PowerShell.



Actions and Observations
<p>
<img width="729" alt="image" src="https://github.com/user-attachments/assets/cdc94504-6054-48d3-b5a6-d906dcbac3bf" />
</p>

Using Remote Desktop Connection, I connect to the Windows VM using its public IP address. From there, I installed Wireshark in order to begin inspecting traffic.


<p>
<img width="838" alt="Annotation 2025-02-10 220142" src="https://github.com/user-attachments/assets/6e24b069-0321-4198-95fc-e465daf2bc21" />
</p>


Within Wireshark, I filtered for ICMP (Internet Control Message Protocol) traffic and opened PowerShell to execute a command called ping. Ping utilizes ICMP, which is used by devices in a network to communicate problems within data transmition. I used ping to see if I can communicate with the Ubuntu VM using its private IP address and with google.com. Afterwards, I used a perpetual ping to the Ubuntu VM in order to see how network security groups work. I executed the perpetual ping with the command: ping -t (ip address).


<br />






![Screenshot 2025-02-10 162627](https://github.com/user-attachments/assets/5a7ca5a6-108e-49e5-9894-07fe1eaee108)


<p>
Within the Azure portal, I opened the networking settings for the Ubuntu VM and added an inbound security rule to block ICMP traffic. I make sure to have the priority higher than SSH (300) to ensure the rule applies first.

</p><img width="641" alt="Annotation 2025-02-10 220113" src="https://github.com/user-attachments/assets/217c9400-b511-41e7-a40c-4ec756e81ab3" />

<p>
Upon returning to the Windows VM, I notice that the ICMP traffic is blocked now that the inbound security rule is in place. After changing the rule to allow traffic again, the perpetual ping resolves without timing out.

</p>
<br />
<img width="590" alt="image" src="https://github.com/user-attachments/assets/1c2672cd-e36c-460d-9a25-25dba6925a00" />

<p>
</p>
<p>
To finish my lab, I decided to observe RDP traffic. The filter for Wireshark is tcp.port == 3389. There is non-stop traffic because RDP is constantly showing me a live stream from one computer to another (in my case, my computer accessing the VM that is hosted on Azure) and thus traffic is always transmitted.

Lessons Learned
The purpose of this lab is for me to see how different protocols and ports are utilized in a network between devices. While this lab does not exactly allow me to troubleshoot, it still serves a purpose to gather information. While troubleshooting, I need to utilize different tools like Wireshark and the command line to see how traffic flows in a network through ports and protocols. Familiarity and an inquisitive mind are key to success !</p>
<br />
