# Azure-Cloud-Detection
We will analyze an environment for any threats/vulnerabilities that could compromise our network.
<p align="center">
<img src="https://i.imgur.com/5HhsRuT.png" alt="Traffic Examination"/>
</p>


<h2>Environments, Steps and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Microsoft Sentinel (SIEM)
- Azure Log Analytics
- KQL to query logs
- Congifure windows security policies
- Utilize data connectors to bring data into Sentinel and analyze it

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)


<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/IfUofIq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
1. Create a resource group in Azure. Create a name and select your region.
</p>
<br />

<p>
<img src="https://i.imgur.com/6Tj1ViZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
2. Create a Virtual Machine and use the same resource group that you created before. Choose the same region as the resource group. Choose Windows 10 where it says “image” , that is the OS our VM will run on. And where you see “size” choose a size that says 2vcpu’s or more. For this project 2vcpu’s is just fine. Make sure to create a username and password. We will need this to Remote Desktop into the VM later. For public inbound ports just keep it as is with “RDP 3389 Allowed”, we will change that later for security purposes. Check the box at the bottom and click review+create. VM will validate and then click create. 
<br />

<p>
<img src="https://i.imgur.com/6sx42m7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/SqoH7TS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. Next step we will setup Microsoft Defender For Cloud (type that in Azure search bar). This is because our VM is set for RDP 3389 which allows us access to the VM but it also will allow others access as well if they were to do a port scan and discover our IP address and we don’t want that to happen. If you do not have Microsoft Defender For Cloud you will need to click upgrade so it can be added to your free subscription for 30 days. On the bottom left side of the screen select “Environment Settings” and then select your subscription.  Where it says “select Defender Plan” click ENABLE ALL.  (After the lab is done just make sure to disable those features for defender). Go back to the Microsoft Defender for cloud home page, scroll down and select “workload protections” and select Just In Time VM access and enable JIT to the VM you created. JIT is a service that willingly grant access to your VM when it is necessary on time based restrictions and it also implements Least Privilege giving the option to restrict certain IP addresses. JIT will prevent brute force attacks. 

</p>
<br />

<p>
<img src="https://i.imgur.com/kEAtvxk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
4. Next we will go to our Virtual machine that we created. Click on “Connect” and choose “My IP” and click Request access.  Request access will validate and then it will say “approved” (give it a little time).  Click on the networking tab and you will see that our VM is protected by JIT (Just In Time) access rule on port 3389 RDP. This means that only we have access to this virtual machine. Anybody else who tries to access it will be denied since they do not have permission.
<br />
  
<p>
<img src="https://i.imgur.com/0PYPzjq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>    
</p>
<p>
5. Now we will create a Log Analytics workspace. This will give a us a place to collect and see the data from Azure resources we created/are using, but in order to do this we must open up Microsoft Sentinel in the azure search bar. When you get to the Microsoft Sentinel home page click “create” then “create new workspace”. Choose the same resource group that you used for the VM and same region. Click review + create.
<br />
  
<p>
<img src="https://i.imgur.com/vGPobyV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DlUP0iJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>    
</p>
<p>
6. After your workspace is finished creating choose your workspace you just created and click add.
<br />
  
  <p>
<img src="https://i.imgur.com/cqzmrl8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
7. The Microsoft Sentinel home screen should appear after your workspace is finished deploying. 
<br />
  
  <p>
<img src="https://i.imgur.com/piNFVKO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  
</p>
<p>
8. We currently don't have any data coming into our SIEM (security information & event management) so we will click Data Connectors under configuration and we will be able to choose what kind of data we want incoming from whatever resources we choose.
<br />
  
<p>
<img src="https://i.imgur.com/Ex90VyD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
9. In the search bar type WINDOWS and select 'Windows Security Events via AMA' and then click open connector page. 
<br />
  
  <p>
<img src="https://i.imgur.com/Y9tXEm1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
10. Click 'create data collection rule'
<br />

<p>
<img src="https://i.imgur.com/hHaaeFF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
11. Create a name for your 'rule' and click next resources. 
<br />
  
  <p>
<img src="https://i.imgur.com/U0jijhb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
12. Click add resources and select the Virtual Machine you created. CLick add and then 'Next Collect' and make sure "All security rules' is selectec and click 'create = review' and then click 'create'. 
<br />
  
  <p>
<img src="https://i.imgur.com/NXcUW3h.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
13. Go back to the Microsoft Sentinel page and you'll see that the Windows Security Events via AMA has been connected. 
<br />
  
  <p>
<img src="https://i.imgur.com/Xkvcro8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
14. Now that we have our SIEM setup. We need to log into our Virtual Machine so we can colect some Log Analytics. Go to your virtual machine and look for the public  IP address. Copy it and open your remote desktop and past the IP address in it or if you are on MAC then download Microsoft Remote Desktop and install it and paste the IP address to connect. You will need your username and pasword that we created earlier to gain access to your VM. 
<br />
  
  <p>
<img src="https://i.imgur.com/2e0kifj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
15. After we log into our VM go to the start menu and search for "Event Viewer".
<br />
  
  <p>
<img src="https://i.imgur.com/pNQSVwZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
16. Open it and click on 'Windows Logs' and select SECURITY. As you can see there a few other logs you can view like SETUP, SYSTEM and APPLICATION, but we are focusing on Security for this lab. When you click on security you will see a list of things, search for the number '4624' and click it. On the bottom portion of the page we can see the log data showing next to 'Computer:' we have successfully logged into our VM and the date and time we logged in. 
<br />
  
  <p>
<img src="https://i.imgur.com/oWLNXKv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
17. Now lets go back to our Azure account and we will open up Microsoft Sentinel to view the log data in our SIEM. This is a perfect place to for cyber security professionals to view data securely and effectively in this centralized location. When you get to the main page of Sentinel click on 'Logs'. 
<br />
  
  <p>
<img src="https://i.imgur.com/fqYxL5K.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
18. Next we will be introducing KQL which stands for Kustko Query Language. This is the language we will use to retrieve the data from the event logs. Follow the basic KQL I have written in the photo. Lets take a dive into what the first word on each line will help us to achieve. "SecurityEvent" is refering to the event viewer we looked at from our Virtual Machine. Remeber all the log data that was in there, this where we are pulling from. "Where" is refering to the place in the logs that we want pulled and that is 4624 which is our successful log in from out VM. "project" will give us the time/date, computer and account that was used to log on. Now lets RUN our KQL, click RUN! Now we can see all of the time we have successfully attempted to log into our VM. That's pretty cool!But guess what? There's no account name. We will have to create this when we make our Analytic Rule since Sentinel does not automatically generate the account name.  
<br />
  
  <p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
19. (TO BE CONTINUED, RAN INTO SOME VM ISSUES) We will create a task schedule. This will allow us to set our system to do what we want at a specific time to generate alerts. Lets go back into our VM 
<br />
