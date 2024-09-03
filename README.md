<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
For this lab, we are going to be creating two VMS that have the same VNET, we will be creating a Domain Controller (Windows Server 2022) and the other VM will be a Windows 10 OS. The Domain Controller will have Active Directory on it along with the 10,000+ users that we are going to create. Furthermore, we are going to join client-1 to the same DNS server as the Domain Controller so that all the users will have access to Client-1 computer. 
</p>

<p>
<img src="https://i.imgur.com/26DOUjs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
<img src="https://i.imgur.com/3dka2IS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After creating DC-1, you will need to change the DNS from dynamic to static. This is because whenever we have a server that is offering resources such as Active Directory we don't want DHCP to assign it an IP address. So, after it is changed to static we are going to use Remote Desktop to login into Client-1 and try to ping DC-1. At first the ping isn't going to work and that is when we are going to use Remote Desktop to login into DC-1 and remove the default ICMPv4 firewall that is placed within the server. And, once ICMPv4 is enabled you will see that it pings correctly.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
