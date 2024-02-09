<div align="center">
  <img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</div>

<h1>Exploring Network Traffic Using Wireshark</h1>
In this endeavor, we employ Wireshark to delve into network traffic encompassing various network protocols. <br />

<h2>Environments and Technologies Employed</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Command Line Interface (CLI)
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Utilized</h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Actions and Observations</h2>

<p>
</p>
<p>
Welcome to the project! Initially, you'll need to create (2) VMs on Azure. One machine will operate on Linux, and the other will run Windows 10. Both must possess (2) CPUs and be within the same VNET. Subsequently, on the Windows machine, download Wireshark. Here's the link for the download: <a href="https://www.wireshark.org/download.html">Wireshark Download Link</a>. Once installed, launch Wireshark and filter for ICMP Traffic exclusively. ICMP, a network layer protocol, relays messages pertaining to network connection issues. By filtering Wireshark to capture only ICMP packets and pinging the private IP address of our Linux machine, we can visualize the packets within Wireshark.
</p>
<br />
<p>
<img src="https://i.imgur.com/IIUShxp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Each packet can be inspected individually to observe the actual data being transmitted in each ping, as demonstrated in the image below.
</p>
<br />
<p>
<img src="https://i.imgur.com/GLxSIG3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Subsequently, we will continually ping the Linux machine using the 'ping -t' command from the Windows machine. While the Windows machine pings the Linux machine, we will navigate to the Linux machine and block inbound ICMP traffic on its firewall. Upon doing so, echo replies from the Linux machine will cease. To block ICMP, we'll create a new Network Security Group (NSG) on the Linux machine configured to block ICMP. We can subsequently re-enable the traffic by allowing ICMP within the NSG.
</p>
<br />
<img src="https://i.imgur.com/5vXO75R.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/Asl80tN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
Next, we'll use our Windows machine to establish an SSH connection to the Linux machine, providing access to its CLI. Additionally, we'll set the Wireshark filter to exclusively capture SSH packets. Upon SSH'ing into the Linux machine using the command "ssh labuser@10.0.0.5" (private IP address), Wireshark will immediately begin capturing SSH packets, as depicted below.
</p>
<br />
<img src="https://i.imgur.com/zteR41r.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We will proceed to filter for the Dynamic Host Configuration Protocol (DHCP) using Wireshark, which operates on UDP ports 67 and 68. DHCP assigns IP addresses to client machines. By executing the command "ipconfig /renew," we can observe this traffic, as illustrated below.
</p>
<br />
<img src="https://i.imgur.com/vU8fpQf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we'll analyze DNS (Domain Name Server) traffic by filtering for it in Wireshark. Initiating DNS traffic with the command "nslookup www.google.com" prompts our DNS server for Google's IP address. DNS traffic operates via port number 53.
</p>
<br />
<img src="https://i.imgur.com/VMcwmsO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly, we'll filter for RDP (Remote Desktop Protocol) traffic, functioning on port 3389. This is pertinent as we are utilizing Remote Desktop Protocol to connect from our desktop to our Virtual Machines in Azure.
</p>
<br />
<img src="https://i.imgur.com/VxXGv6X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
