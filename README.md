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
- Join Client-1 computer to your Domain (jessedomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and log into Client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

<p>
  We are going to create two Virtual Machines in an Azure Virtual Network. When we create these VMs each one will also have a Network Interface Card (NIC) and both will automatically be assigned an IP address from the DHCP server. Usually when you have a server that is offering services to other computers, you don’t want the IP address to change or be dynamic. Therefore, we do not want DHCP to assign an IP address to our Domain Server as it will be offering Active Directory services. 
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

<p>
  First we are going to create two Virtual Machines, 1st VM with Windows Server as our Domain Controller (DC-1) and 2nd VM with Windows 10 which will be our Client computer (Client-1). 
</p>
<p>
<img src="https://imgur.com/8FHVBwj.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Next, we need to manually set the private IP address of our Domain Controller (DC-1) from dynamic to static so that the DCHP Server will not assign the Domain Controller an IP address. DC-1's private IP address is manually assigned as 10.0.0.4. 
</p>
<p>
  <img src="https://imgur.com/rBsJopP.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
  We need to also confirm both VMs are on the same Virtual Netowrk seen as below
</p>
<p>
  <img src="https://i.imgur.com/uKfzntZ.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Next we need to ensure connectivity between the Client and the Domain Controller. So we are going to Remote Desktop login to the Client and ping the Domain Controller's private IP address using ping -t (non-stop perpetual ping)
</p>
<p>
  <img src="https://i.imgur.com/E1mWacn.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
  When we ping DC-1 from Client-1, we see that it fails. So we are going to open a hole in DC-1's Firewall to ensure that we can ping it. 
</p>
<p>
  <img src="https://i.imgur.com/eAr4EgO.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
  We are going to open another instance of Remote Desktop and login to DC-1.  Go to Windows Firewall Advanced Security and Enable ICMPv4 so that we can ping DC-1 from Client-1. Navigate to Inbound Rules, filter by ICMPv4 Protocol, and Enable ICMP Echo Request as shown below
</p>
<p>
  <img src="https://i.imgur.com/KR9ZmWi.png" height="80%" width="80%" alt="xx"/>
  <br/>
  <br/>
  <img src="https://i.imgur.com/t97ShvG.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Now we can see ping is successful; ensuring there is connectivity between Client-1 and DC-1.
</p>
<p>
  <img src="https://i.imgur.com/b55ZhVz.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Next, we are going to install Active Directory on DC-1 and promote it into a Domain Controller, then restart and log back into the Domain Controller. 
</p>
<p>
  <img src="https://i.imgur.com/Pc4o6es.png" height="80%" width="80%" alt="xx"/>
  <br/>
  <img src="https://i.imgur.com/4f8SgXr.png" height="80%" width="80%" alt="xx"/>
</p>
