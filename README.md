<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup resources in Azure: Domain Controller and Client
- Ensure connectivity between the Client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your Domain (jessedomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and log into Client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

<p>
  We are going to create two Virtual Machines in an Azure Virtual Network. When we create these VMs each one will also have a Network Interface Card NIC and both will automatically be assigned an IP address from the DHCP server. Usually when you have a server that is offering services to other computers, you don’t want the IP address to change or be dynamic. Therefore, we do not want DHCP to assign an IP address to our Domain Server as it will be offering Active Directory services. 
</p>
<p>
<img src="https://i.imgur.com/jL8Uv6k.png" height="80%" width="80%" alt="xxx"/>
</p>
<p>
Normally when you create VMs in a Virtual Network all the IP addressing is setup automatically through the hidden DNS in the Virtual Network. However, for a client computer to join a Domain, it needs to use the Domain Controller as the DNS Server. When we install Active Directory on a server and turn that server into a Domain Controller, a DNS service is actually installed on the Domain Controller as well. Therefore, we need to use the IP address of the Domain Controller as the DNS Server for the Client computer. 
</p>
<br />
<br />
<br />
<br />

<p>
<img src=".png" height="80%" width="80%" alt="xxx"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
<br />
<br />
<br />

<p>
<img src=".png" height="80%" width="80%" alt="x"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
<br />
<br />
<br />

<p>
<img src=".png" height="80%" width="80%" alt="x"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
<br />
<br />
<br />

<p>
<img src=".png" height="80%" width="80%" alt="x"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
<br />
<br />
<br />

<p>
<img src=".png" height="80%" width="80%" alt="x"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
<br />
<br />
<br />

<p>
<img src=".png" height="80%" width="80%" alt="x"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
<br />
<br />
<br />

<p>
<img src=".png" height="80%" width="80%" alt="x"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
<br />
<br />
<br />

<p>
<img src=".png" height="80%" width="80%" alt="x"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
<br />
<br />
<br />

<p>
<img src=".png" height="80%" width="80%" alt="x"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
<br />
<br />
<br />
