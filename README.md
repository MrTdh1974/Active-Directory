# Active-Directory
Creating Active Directory Through Azure VMs
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>

In this tutorial,  outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



Video Tutorial 

https://youtu.be/8UASdKZkg4U

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Set up our first virtual machine as the Domain Controller (DC-1), setting it as a Windows Server
- Step 2: Set DC-1 private IP address to static, remote desktop into DC-1 and turn off its firewall settings
- Step 3: Set up Client-1
- Step 4: Set up Client-1's DNS to DC-1's private IP address
- Step 5: Restart Client-1 
- Step 6: Remote desktop into Client-1, and open the Command Prompt
- Step 7: Ping DC-1's private IP address to ensure the proper connection 

<h2>Deployment and Configuration Steps</h2>

Video Tutorial
https://youtu.be/8UASdKZkg4U

<h2>Install Active Directory</h2>

* Remote back into DC-1. In the Server Manager, install Active Directory Domain Services
* In post-configuration, create a new forest (mydomain.com) and promote DC-1 as a Domain Controller, where it will 
  automatically restart
* After restart, log back into DC-1 as mydomain.com\labuser

<h2>Create Organizational Units(OU) and Admins in Active Directory</h2>

* In DC-1, Open up Windows Administrative Tools, and Select Active Directory Users and Computers (ADUC)
* Create 3 Organizational Units
* First OU named _EMPLOYEES for employee users
* Second OU named _ADMINS for administrative users
* Third OU named _Clients for the client
* Create a new user named "Jane Brown" with the username jane_admin and add her to the Domain Admins security group
* Log out and log back into DC-1 as mydomain.com\jane_admin, which will be used for the duration of this project. 


<h2>Join Client-1 to the Domain</h2>

* Login in to Client-1 using the local admin account labuser, then join it to the domain mydomain.com
* Once joined, restart Client-1 and verify that it appears in the ADUC in the COMPUTERS container
* Move Client-1 into the _CLIENTS OU for organizational purposes

<h2>Create Additional Users with Powershell Script and Verify Access</h2>

* Log into DC-1 as jane_admin and open Powershell ISE as an administrator
* Copy and paste script from checklist into Powershell ISE
* Run script, as it will create multiple user accounts in Active Directory
* Once completed, check ADUC ensure the new users are created into the _EMPLOYEES OU
* Attempt to log into Client-1 with one of the newly created users to verify that things are working correctly.

<h2>Configuring Lockouts and Enabling GPO</h2>

Video Tutorial

https://youtu.be/GtzV5pxa8wA

* Log back into DC-1 as jane_admin
* Bring up Group Policy Management Console (gpmc)
* Double-click on MYDOMAIN.COM, and click on "Linked Group Policy Objects"
* Right-click on DEFAULT DOMAIN POLICY, then click "Edit"
* Click on COMPUTER CONFIGURATION
* Click on POLICIES
* Click on WINDOWS SETTINGS
* Click on SECURITY SETTINGS
* Click on ACCOUNT POLICIES
* Click on ACCOUNT LOCKOUT DURATION and set the necessary parameters (lockout duration: 30 min, locked out after 5 tries) reset after 10 min)
* Log out of Client-1, then try logging back into Client-1 as one of the verified users with the incorrect password.
* After the account locks, go back into Active Directory, find the user, right-click onto the profile, click on ACCOUNT, and then proceed to check the box that says UNLOCK ACCOUNT.
* Log back into Client-1, open COMMAND PROMPT as an admin, and type in "gpupdate /force" to change the Group Policy

  <h2>Conclusion</h2>

  In this lab, we created an infrastructure for installing and deploying Active Directory. Through the Azure portal, we created
  both a Domain Controller and a Client machine, and ensured that they were able to communicate with one another. We installed
  Active Directory Domain Services. We created a new domain, as well created Organizational Units (OUs), and an admin with Active
  Directory Users and Computers (ADUC). We created users through a script, using Powershell ISE as administrator, then logged into
  the client as one of the created users. 

  We configured Remote Desktop access for the domain users, configured locked accounts, enabled GPOs. This lab proved to be
  hands-on with the necessary Active Directory tasks. 
