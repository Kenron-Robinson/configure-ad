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
Here  we have to set the ip to static so the private ip stays the same when the virtual machine powers down. In the networking section click on network settings, make sure you are on the server virtual machine.
<br />
<br />    
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/VM%20setup%203.0.PNG?raw=true" height="50%" width="40%"  />
<br />
<br />
 In this section click on the "Network interface /ip configuration" Link thats there.
<br />
<br />  
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/VM%20setup%203.5.PNG?raw=true" height="90%" width="80%"  />
<br />
<br /> 
Here you want to edit the ipconfig at the bottom.
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/VM%20setup%204.0.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
Change it from dynamic to static.
<br />
<br />  
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/VM%20setup%204.5.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
 Now use remote desktop to log into the server/domain controller virtual machine. should look like this when you sign in 
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/server%20step%201.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
 Here you will need to disable the windows firewall. Go to the control panel, search for it in the windows search bar. In the control panel section select system security. Should look like this.:
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/server%20step%202.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
Click on windows defender firewall properties and disable the firewall. do this for the domain,private, and public profiles.:
<br />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/server%20step%203.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
Now after that is done, we have to create the client virtual machine. Be sure to add this virtual machine to the same region and virtual network as the server/Domain controller. Follow thses steps. 
<br />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/2%20VM%20setup%201%20.PNG?raw=true" height="90%" width="80%"  />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/2%20VM%20setup%202.PNG?raw=true" height="90%" width="80%"  />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/2%20VM%20setup%203.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
After this virtual machine is set up you will need to give the virtual machine the same ip address as the domain controller. Its pretty much the same steps as with the domain controller except you need to make changes to the ip.
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/2%20VM%20DNS%20change%20to%20server%20private%20IP.PNG?raw=true" height="90%" width="80%"  />
 <br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/2%20VM%20dns%20ip%20change%202.PNG?raw=true" height="90%" width="80%"  />
 <br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/2%20VM%20dnc%20ip%20change.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
When this is done, Log into the client virtual machine. Open up powershell by searching for it in the windows search bar and ping the domain controller.
<br />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Capture%202%20VM%20ping%20to%20the%20server%20.PNG?raw=true" height="90%" width="80%"  />
<br />
<br /> 
Now run ipconfig /all in powershell to ensure that the ip address is the same as the domain controller.
<br />
<br />  
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/2%20VM%20confirm%20to%20the%20server%20.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
 This concludes the virtual machines set up. Now we move onto the configuration of active directory. Log back into the server/domain controller, click on add roles and features inside of the server manager.
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Installing%20AD.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
 Follow the installation steps for the active directory  
<br />
<br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Installing%20AD%201.PNG?raw=true" height="90%" width="80%"  />
 <br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Installing%20AD%202.PNG?raw=true" height="90%" width="80%"  />
 <br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Installing%20AD%203.PNG?raw=true" height="90%" width="80%"  />
 <br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Installing%20AD%204.PNG?raw=true" height="90%" width="80%"  />
 <br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Installing%20AD%205.PNG?raw=true" height="90%" width="80%"  />
 <br />
 <br />





   
</p>
