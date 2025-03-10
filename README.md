<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This guide outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />




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
 Follow the installation steps for active directory  
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
 Now click on "Promote this server to a domain controller" and follow the steps. At some point it will ask to set up a forest, you can name it anything you may like but be sure to remember it.
 <br />
 <br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Promote%20server%20to%20domain%20controller%20(After%20AD%205)%20.PNG?raw=true" height="90%" width="80%"  />
 <br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Promote%20server%201.PNG?raw=true" height="90%" width="80%"  />
 <br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Promote%20server%202.PNG?raw=true" height="90%" width="80%"  />
 <br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Promote%20server%203.PNG?raw=true" height="90%" width="80%"  />
 <br />
 <br />
  Here be sure to remember this name, but of course name it whatever wish .
 <br />
 <br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Promote%20server%204.%20PNG.PNG?raw=true" height="90%" width="80%"  />
  <br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Promote%20server%205.PNG?raw=true" height="90%" width="80%"  />
 <br />
 <br />
 Now restart the virtual machine but be sure to login with the netbios domain name you set up before. It should look like this "mydomain.com\labuser
" but use the name you chose with the orginal login. Once you are in we will start by setting up the organizational unit.Search for "Active Directory Users and Computers".
<br />
<br />
 <img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/AD%20OU%20setup.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
 Click on the dropdown arrow next to the domain name, then click on the domain name and in the right panel, right click and go to new and add a new organizational unit. One for admins and one for employees.
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/AD%20OU%20setup%201.PNG?raw=true" height="90%" width="80%"  />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/AD%20OU%20setup%202.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
Once this is done go to the admins section you just created and add a new user.
<br />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/AD%20making%20an%20admin%20.PNG?raw=true" height="90%" width="80%"  />
<br />
<br /> 
 Here set up the users name, password, and email. This user will be admin and we will be logging in as this user throughout the rest of the guide.
 Note that the username for this user will have the domain name in the beginning. same as when you logged on before.
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/AD%20making%20a%20admin%201%20(After%20AD%20OU)%20.PNG?raw=true" height="90%" width="80%"  />
<br />
<br /> 
Uncheck the first box because you will be setting the password here.
<br />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/AD%20making%20a%20admin%202.PNG?raw=true" height="90%" width="80%"  />
<br />
<br /> 
Now our user is in the admin section but they are not considered a admin yet we have to set it inside of the security group. Right click on the user and select properties.
<br />
<br />  
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/AD%20setting%20a%20admin%20.PNG?raw=true" height="90%" width="80%"  />
<br />
<br /> 
 go to the "Member Of" section, click add and a window should show up.
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/AD%20setting%20a%20admin%202.PNG?raw=true" height="90%" width="80%"  />
<br />
<br /> 
 Within this window copy whats in the image. This will add the user to the group as admin giving them exclusive permissions. After this login into the client virtual machine as the orignal admin user (The username you used to make the machine with the domain added to the front of it).
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/AD%20setting%20a%20admin%203.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
 Once Logged in go to windows settings,then the about page. On the right side panel click on "rename pc(advanced)". A window should show up, right below network id click the change button.
<br />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Joining%20the%20client%20with%20the%20domain.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
 Here you will need to put the domain name (Netbios domain) of the domain you want to connect to.
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Joining%20the%20client%20to%20the%20domain%201.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
 Here you will also use your admin's username and password.
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Joining%20the%20client%20to%20the%20domain%202.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
Now log back into the domain controller virtual machine and verify that the client virtual machine is showing in active directory. Go to the computers section to see it. 
<br />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/verifing%20client%201%20is%20in%20the%20domain.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
 Next we have to give permissions for all remote users to be able to connect to the domain. Go to the windows search bar and go to settings, then go to remote desktop. Note you are doing this on the client vm as your admin.
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Jane_admin%20giving%20permissions%20to%20domain%20uesrs.PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
Same process as last time when we added our admin to the security group. This time you will type "Domain Users".
<br />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Jane_admin%20permissions%20domain%20users%202.PNG?raw=true" height="90%" width="80%"  />
<br />  
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Jane_admin%20domain%20users%203.PNG?raw=true" height="90%" width="80%"  />
<br />
<br /> 
Once this is done go back to the active directory within the domain controller and add a Organizational unit called clients. Then drag client 1 into that OU (Organizational Unit).
<br />
<br />  
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Create%20a%20new%20OU%20called%20clients%20(After%20verfing%20the%20client%20vm%20is%20in%20the%20domain).PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
Now that this is done you will need to log into the domain controller as your admin.
<br />
<br />
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Signing%20back%20in%20as%20admin%20(Jane_admin).PNG?raw=true" height="90%" width="80%"  />
<br />
<br />
Once signed in go to the windows search bar an open powershell_ise as admin. Create a new file and paste the script into the file. Link for the script "https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1".
<br />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Creating%20users%20as%20jane_admin.PNG?raw=true" height="90%" width="80%"  />
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Creating%20users%20as%20jane_admin%20.PNG?raw=true" height="90%" width="80%"  />
<br /> 
<br />
 Click on the green arrow next to the help button to run the script. let it run until you have 50 users, its set to make 10000 but you really on need 30 to 50 to experiment with.
<br /> 
<br /> 
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Creating%20users%20as%20jane_admin%203.PNG?raw=true" height="90%" width="80%"  />
<br />  
<img src="https://github.com/Kenron-Robinson/configure-ad/blob/main/images/Creating%20users%20as%20jane_admin%204.PNG?raw=true" height="90%" width="80%"  />
<br /> 
<br /> 

 
<h3>This concludes the set up portion for active directory. This will give you what you need to expriment with account lockouts,resetting passwords, and giving users certain permissions from within active directory. I hope with this guide it was simple and easy to follow.  </h3>




   
</p>
