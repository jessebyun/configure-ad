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
  Next, we are going to start installation for Active Directory on DC-1 and promote it into a Domain Controller. Then we are going to add a new forest and name our domain. Once AD installation is complete, the VM will log off and we need to reconnect to it. 
</p>
<p>
  <img src="https://i.imgur.com/Pc4o6es.png" height="80%" width="80%" alt="xx"/>
  <br/>
  <img src="https://i.imgur.com/4f8SgXr.png" height="80%" width="80%" alt="xx"/>
  <br/>
  <img src="https://i.imgur.com/ox9rHPW.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
  When we remote desktop back into DC-1 it now became a Domain Controller; therefore, we have to login with the context of the domain. So we have to change the user name using Fully Qualifiied Domain Name (FQDN). 
</p>
<p>
  <img src="https://i.imgur.com/cmKPMaT.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Once the Domain Controller is online, we are going into Active Directory Users and Computers window. Here we can see it created a bunch of default items. If we click on user on subpane, we can see our user "labuser" is here. We can also see some default random Security Groups. If we go to Computers, we see that we don't have any computers yet. Under Domain Controllers, we can see 1 Domain Controller which is DC-1. This Domain Controller is a computer that has Active Directory running on it. 
</p>
<p>
  <img src="https://i.imgur.com/Mh5Pnn9.png" height="80%" width="80%" alt="xx"/>
  <br/>
  <img src="https://i.imgur.com/mUngpN4.png" height="80%" width="80%" alt="xx"/>
  <br/>
  <img src="https://imgur.com/mEeUwli.png" height="80%" width="80%" alt="xx"/>
   <br/>
  <img src=https://imgur.com/8beIpj8.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Then we are going to create couple Organizational Units (_ADMINS and _EMPLOYEES) inside AD. Which are just folders to organize stuff. Then we are going to create an administrative user. 
</p>
<p>
  <img src="https://i.imgur.com/Pq9ijlE.png" height="80%" width="80%" alt="xx"/>
  <br/>
  <img src="https://i.imgur.com/b8VhnO4.png" height="80%" width="80%" alt="xx"/>
  <br/>
  <img src="https://i.imgur.com/9hYhhnb.png" height="80%" width="80%" alt="xx"/>
  </p>
<br/>
<br/>
<br/>

<p>
  We can see we created an user John Doe in a folder called Admins, but this name is ambiguous and is just for the human eye. To make this an actual Domain Admin, we have to assign it to the Domain Admins Group. To do this, right-slick the user, properties, click tab member of. We can see that its member of Domain Users which is a group by default all Domain members are a part of. So we are going to add another group for Domain Admins. 
</p>
<p>
  <img src="https://i.imgur.com/HtUbuzc.png" height="80%" width="80%" alt="xx"/>
  <br/>
  <img src="https://i.imgur.com/rOkLRRs.png" height="80%" width="80%" alt="xx"/>
  <br/>
  <img src="https://i.imgur.com/rbcE6wn.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Next, we are going to log off and log back in as the administrator John Doe. We can open command prompt and type “whoami” to see we are logged in as “a-john.doe”, a member of “jessedomain”. 
</p>
<p>
  <img src="https://i.imgur.com/XdZvY0B.png" height="80%" width="80%" alt="xx"/>
  <br/>
  <img src="https://i.imgur.com/r6eZQnY.png" height="80%" width="80%" alt="xx"/>
</p>
<br/>
<br/>
<br/>

<p>
 Now we are going to join Client-1 computer to the Domain. After we do that, even though our accounts have not existed on Client-1 computer before, we’re going to be able to log into Client-1 with a-john.doe or technically any other account. 
</p>
<p>
<img src="https://i.imgur.com/jL8Uv6k.png" height="80%" width="80%" alt="xxx"/>
</p>
<br/>
<br/>
<br/>

<p>
   First, we need to set Client-1’s DNS settings to the Domain Controller’s private IP address. At the current state, the DNS settings for Client-1 is pointing to the DNS server in the VNET. To join the Domain, we have to use the Domain Controller as the DNS Server because the Domain Controller knows what jessedomain.com is. If we use the hidden DNS Server in the VNET, it will search the internet for a random jessedomain.com for a Domain Controller and it is going to fail. Once DC-1 becomes the DNS server for Client, DC-1 can tell Client-1 which IP address to use to join it. 

Before we change the DNS settings, we are going to try to join our Domain to see what happens. If we go to CMD and type ipconfig /all we can see that the DNS server is using a public IP address. So we are going to go to SETTINGS, ABOUT, RENAME THIS PC (ADVANCED), CHANGE domain, and type in our Domain. We can see it says: Active Directory Domain Controller for domain "jessedomain" could not be contacted. Because it reached out to the public DNS server to find jessedomain but there is none. 
</p>
<p>
  <img src="https://i.imgur.com/An2k3pe.png" height="80%" width="80%" alt="xxx"/>
</p>
<br/>
<br/>
<br/>

<p>
  From the Azure Portal, set Client-1's DNS settings to the DC-1's private IP address. Once it finishes updating, we are going to restart Client-1 from the portal and it will flush the DNS cache. 
</p>
<p>
  <img src="https://i.imgur.com/iBF0QeJ.png" height="80%" width="80%" alt="xxx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Now we are going to log back into Client-1 and try to join it to the Domain again. First, we open command prompt, when we type "whoami" and "hostname", we can see we are logged in as "labuser" on Client-1 computer. We have a successful ping with 10.0.0.4 (our DC-1 Domain Controller) and when we type "ipconfig /all" we can see our DNS Server is the private IP address of the Domain Controller. Now we are going to join Client-1 to the Domain and this time we get the login prompt and we are going to enter credentials for John Doe which is the admin for the Domain jessedomain.com. 
</p>
<p>
  <img src="https://imgur.com/XdUQKDS.png" height="80%" width="80%" alt="xxx"/>
  <br/>
  <img src="https://i.imgur.com/cu1e4pj.png" height="80%" width="80%" alt="xxx"/>
  <br/>
  <img src="https://i.imgur.com/QFb5r3x.png" height="80%" width="80%" alt="xxx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Now that Client-1 has joined the Domain we will be able to login to Client-1 with our Domain admin account. Even though John Doe account has never exsisted on Client-1, because Client-1 is now part of the Domain, essentially John Doe can login to that computer or any other computer that is part of the domain. Right now only Domain Admins are allowed to remotely login to Client-1, so now we are going to set it up so that all Domain users can also login to Client-1. So we are going back into SYSTEM SETTINGS, REMOTE DESKTOP, Select users that can remotely access this PC, and we can see list is empty and only Administrators can remote login. 
</p>
<p>
  <img src="https://i.imgur.com/XSQPH1t.png" height="80%" width="80%" alt="xxx"/>
</p>
<br/>
<br/>
<br/>

<p>
  We are going to add Users/Groups, type Domain and check name to list all the Domain Groups, and we are going to add the built-in Domain Users Group. This group automatically adds all the domain users in this security group. 
</p>
<p>
  <img src="https://i.imgur.com/nJaSHPN.png" height="80%" width="80%" alt="xxx"/>
    <br/>
    <img src="https://i.imgur.com/O5CNpac.png" height="80%" width="80%" alt="xxx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Now we are going to go back to DC-1 remote desktop and go to Active Directory Users and Computers. Here if we go into Users then open Domain Users, we can see all the users that are members of the Security Group Domain Users. This is the group we added to Client-1 so that we can also include all non-administrative users to be able to login to Client-1
</p>
<p>
  <img src="https://i.imgur.com/2fSynzC.png" height="80%" width="80%" alt="xxx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Now we are going to create a bunch of non-administrative users so that we can use one to login to Client-1. Go back into DC-1 as John Doe and open PowerShell ISE as an administrator. Create a new file and paste the contents of a script, run the script and observe the accounts being created. When finished open Active Directory Users and Computers and observe the accounts in the appropriate Oranizational Unit. 
</p>
<p>
  <img src="https://i.imgur.com/fGDH172.png" height="80%" width="80%" alt="xxx"/>
</p>
<br/>
<br/>
<br/>

<p>
  Now we are going to pick one random non-administrative user we just created and login to Client-1. If we open C:\Users, we can see all the users that logged into Client-1. 
</p>
<p>
  <img src="https://i.imgur.com/NvMtQuG.png" height="80%" width="80%" alt="xxx"/>
  <br/>
  <img src="https://i.imgur.com/eoGlIe4.png" height="80%" width="80%" alt="xxx"/>
</p>
<br/>
<br/>
<br/>
