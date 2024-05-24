# azure-network-protocols

---

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Exploring Network Traffic with Wireshark</h1>
In this endeavor, we delve into the intricacies of network traffic using Wireshark across various protocols. <br />

<h2>Environments and Technologies Utilized</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Command Line Interface (CLI)
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Employed </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Actions and Insights</h2>

<p>
</p>
<p>
Welcome aboard! Our first step is to create (2) VMs on Azure. One VM will run on Linux while the other will operate on Windows 10. Both VMs should have (2) CPUs and be interconnected on the same VNET. Once this setup is complete, proceed to the Windows VM and download Wireshark. You can acquire Wireshark from [this link](https://www.wireshark.org/download.html). After installation, launch Wireshark and apply a filter for ICMP Traffic exclusively. ICMP, a network layer protocol, is instrumental in relaying messages regarding network connection issues. By filtering Wireshark to exclusively capture ICMP packets and pinging the private IP address of our Linux VM, we can observe the packets visually.
</p>
<br />
<p>
<img src="https://i.imgur.com/IIUShxp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Let's scrutinize each packet individually to discern the precise data being transmitted in each ping, as depicted in the image below.
</p>
<br />
<p>
<img src="https://i.imgur.com/GLxSIG3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Subsequently, we'll initiate a perpetual ping towards the Linux VM using the 'ping -t' command. This will sustain the ping process until manually halted. While the Windows VM is engaged in pinging the Linux VM, navigate to the Linux VM and enact a blockade on inbound ICMP traffic within its firewall. This action will halt the reception of echo replies from the Linux VM. Implement the block by creating a new Network Security Group (NSG) on the Linux VM configured to obstruct ICMP. Restoration of ICMP traffic can be accomplished by permitting ICMP within the NSG.
</p>
<br />
<img src="https://i.imgur.com/5vXO75R.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/Asl80tN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
Moving forward, utilize the Windows VM to establish an SSH connection with the Linux VM. SSH access will facilitate entry into the Linux VM's CLI. Configure Wireshark to exclusively capture SSH packets. Upon executing the SSH command "ssh labuser@10.0.0.5" (private IP address) on the Windows VM, Wireshark will promptly commence capturing SSH packets, as illustrated below.
</p>
<br />
<img src="https://i.imgur.com/zteR41r.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Let's now leverage Wireshark to filter for the Dynamic Host Configuration Protocol (DHCP), which operates on UDP ports 67 and 68. DHCP is instrumental in assigning IP addresses to client machines. Initiate a request for a new IP address using the command "ipconfig /renew". The ensuing traffic can be observed below.
</p>
<br />
<img src="https://i.imgur.com/vU8fpQf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Proceeding further, let's delve into DNS (Domain Name Server) traffic by filtering it on Wireshark in a similar manner. Initiate DNS traffic by executing the command "nslookup www.google.com." This command solicits the DNS server for Google's IP address. DNS traffic is routed through port number 53. 
</p>
<br />
<img src="https://i.imgur.com/VMcwmsO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly, filter for RDP (Remote Desktop Protocol) traffic, which operates on port 3389. This protocol facilitates remote desktop connections from your desktop to the Virtual Machines hosted in Azure. 
</p>
<br />
<img src="https://i.imgur.com/VxXGv6X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
