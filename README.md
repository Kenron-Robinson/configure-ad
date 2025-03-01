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
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Make a virtual machine for the windows server. 
- Step 2 : Make a windows 10 virtual machine.
- Step 3 : Configure the windows server for active directory. 
- Step 4 : Practice by adding users using a script and interacting with active directory.

<h2>Deployment and Configuration Steps</h2>

<p align="center">
First step is to create a resource group, this one will be different from the other guide since we will be using a virtual machine that will act as a server for us.
<br />
<br />  
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/VM%20set%20up%201.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />  
This step will be the same as my networking guide, but be sure to to select the windows server for your image like in the photo. Follow the steps in the photos to finish creating the virtual machine 
<br />
<br />  
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/VM%20set%20up%201.5.PNG?raw=true" height="90%" width="80%"  />
<br />     
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/VM%20setup%202.0.PNG?raw=true" height="90%" width="80%"  />
<br />     
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/VM%20setup%202.5.PNG?raw=true" height="90%" width="80%"  />
<br />
<br /> 
Here  we have to set the ip to static so the private ip stays the same when the virtual machine powers down.
<br />
<br />    
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/VM%20setup%202.5.PNG?raw=true" height="90%" width="80%"  />



   
</p>
