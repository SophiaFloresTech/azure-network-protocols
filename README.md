<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Actions and Observations</h2>

<p>
</p>
<p>
First you will need to create two Virtual Machines on Microsoft Azure. One machine will be use Linux and the other will use Windows 10. Both will have two cpus and they must be on the same virtual network. Once that is done go on the Windows machine and download Wireshark. A link will be provided for the wireshark download. https://www.wireshark.org/download.html Once installed, open Wireshark and filter for ICMP Traffic only. ICMP is a network layer protocol that relays messages concerning network connection issues. When you filter wirehsark to only capture ICMP packets and ping the private IP address of the linux machine you can visually see the packets on wireshark. 
</p>
<br />
<p>
<img src="https://i.imgur.com/IIUShxp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
You can inspect each individual packet and see the data that is being sent in each ping as seen in the image below. 
</p>
<br />
<p>
<img src="https://i.imgur.com/GLxSIG3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, you will ping the Linux machine with the command ping -t. This will continually ping the machine until you decide to stop it. While the Windows machine is pinging the Linux machine, go to the Linux machine and block inbound ICMP traffic on it's firewall. Once thart is done you should stop recieving echo replys from the Linux machine. Next, block ICMP by creating a new Network Security Group on the Linux machine that will be set to block ICMP. You can allow the traffic by allowing ICMP on the Linux Network Security Groups page on Microsoft Azure. 
</p>
<br />
<img src="https://i.imgur.com/5vXO75R.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/Asl80tN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
You will then use the Windows machine to SSH to the Linux machine. Set the wireshark filter to capture SSH packets only. When yuo SSH into the Linux machine with the command prompt "SSH labuser@10.0.0.5" you can see that wireshark starts to immediately capture SSH packets.
</p>
<br />
<img src="https://i.imgur.com/zteR41r.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Use wireshark to filter for DHCP. DHCP is used to assign IP addresses to machines. You will request a new IP address with the command "ipconfig /renew". Once the command is entered wireshark will capture DHCP traffic.
</p>
<br />
<img src="https://i.imgur.com/vU8fpQf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
You will now set wireshark to filter DNS traffic. Initiate DNS traffic by typing in the command "nslookup www.google.com". This command essentially asks your DNS server what is google's IP address.
</p>
<br />
<img src="https://i.imgur.com/VMcwmsO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly, filter for RDP traffic. When "tcp.port==3389" is entered, traffic is spammed non stop due to you using Remote Desktop Protocol to connect to your Virtual Machine. 
</p>
<br />
<img src="https://i.imgur.com/VxXGv6X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
