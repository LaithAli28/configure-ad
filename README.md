
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
- PowerShell ISE

<h2>Operating Systems Used </h2>

- Windows Server 2022-Domain Controller VM(DC-1)
- Windows 10 (21H2)-Client VM(Client-1)

<h2>High-Level Deployment and Configuration Steps</h2>

- Install Active Directory
- Create a Domain and Domain Admin User
- Add the Client-1 VM to the Domain
- Setup Remote Desktop for Non-Administrative Users on Client-1 VM
- Create new Non-Administrative Users and log into Client-1 with a new user

<h2>Deployment and Configuration Steps</h2>

<p>

  ![image alt](https://github.com/LaithAli28/configure-ad/blob/main/A1.png?raw=true)
 ![image alt](https://github.com/LaithAli28/configure-ad/blob/main/A2.png?raw=true)
</p>
<p>
Installing Active Directory and Creating Domain:
Within the DC-1 virtual machine, navigate to Server Manager and click "Add Roles and Features". Under Server Roles, select "Active Directory Domain Services" and click install. After this, we navigate to the "About" section in the Settings app, select "Rename this PC(advanced)" and click the Change button. This will allow you to enter your domain name(can be anything, will be mydomain.com for this lab). Once that's done click okay and restart the VM, and log back in with the username "mydomain.com\labuser". 
</p>
<br />

<p>
 
  ![image alt](https://github.com/LaithAli28/configure-ad/blob/main/A5.png?raw=true)
![image alt](https://github.com/LaithAli28/configure-ad/blob/main/A6.png?raw=true)
</p>
<p>
Creating a Domain Admin User: In Active Directory Users and Computers (ADUC), create two Organizational Units (OU) called “_EMPLOYEES” and “_ADMINS” (THIS IS VERY IMPORTANT, MUST BE ENTERED EXACTLY AS SHOWN) by right clicking on my domain, hover over "New", and click "Orgizational Unit". Create a new employee with the name “Jane Doe” and the username of “jane_admin”. Add jane_admin to the “Domain Admins” Security Group. Finally, log out and close the connection to the Domain Controller virtual machine and log back in as “mydomain.com\jane_admin”. This would become the main Administrative account for the Domain.
</p>
<br />

<p>

 ![image alt](https://github.com/LaithAli28/configure-ad/blob/main/A7.png?raw=true)
 ![image alt](https://github.com/LaithAli28/configure-ad/blob/main/A8.png?raw=true)
</p>
<p>
Joining Client-1 Virtual machine to the Domain: Login to the Client-1 virtual machine as "labuser" and join the domain(the same way we joined with DC-1, in the "About" section), the computer will restart. Login to the Domain Controller virtual machine and verify that Client-1 virtual machine shows up in ADUC. Create a new Orgizational Unit (OU) named “_CLIENTS” and drag Client-1 into it. 
</p>
<br />

</p>

 ![image alt](https://github.com/LaithAli28/configure-ad/blob/main/A9.png?raw=true)
<p>
Setup Remote Desktop Connection for Non-Administrative Users on Client-1 VM: Login to the Client-1 virtual machine as "mydomain.com\jane_admin". Right click on the "Start" menu and select "System", navigate to “Remote Desktop”, click on "Select users that can remotely access this PC" and allow “Domain Users” access to Remote Desktop Connection. You can now log into Client-1 virtual machine as a Non-Administrative User. This only works for this particular system, you’d want to do this by creating a Group Policy that allows you to change many systems at once in a company setting.

</p>
<br />

</p>
 
 ![image alt](https://github.com/LaithAli28/configure-ad/blob/main/A12.png?raw=true)
<p>
Creating additional Non-Administrative Users and login to Client-1 virtual machine as a new user: Login to the Domain Controller virtual machine as a Domain Admin. Open PowerShell ISE as an admin. Create a new file and paste the contents of the script into it(the script creates a large number of accounts automatically). Run the script and observe the accounts being created. When finished, open Active Directory Users and Computers and observe the accounts under "_EMPLOYEES". You can now login to the Client-1 virtual machine as any one of the new non-administrative accounts. The script sets the password for each of the accounts created, and the password is located in the script file. You have now completed the Deployment of Microsoft Active Directory in the Cloud with Microsoft Azure!
</p>
<br />

