# Azure-Cloud-Detection
We will analyze an environment for any threats/vulnerabilities that could compromise our network.
<p align="center">
<img src="https://i.imgur.com/DJmEXEB.png" alt="Traffic Examination"/>
</p>


<h2>Environments, Steps and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Microsoft Sentinel
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
<img src="https://i.imgur.com/0AiezB3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
5. Now we will create a Log Analytics workspace. This will give a us a place to collect and see the data from Azure resources we created/ are using., but in order to do this we must open up Microsoft Sentinel in the azure search bar. When you get to the Microsoft Sentinel home page click “create” then “create new workspace”. Choose the same resource group that you used for the VM and same region. Click review + create.
<br />
  
  <p>
<img src="https://i.imgur.com/6Tj1ViZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<br />
  
  <p>
<img src="https://i.imgur.com/6Tj1ViZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<br />
  
  <p>
<img src="https://i.imgur.com/6Tj1ViZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<br />
  
  <p>
<img src="https://i.imgur.com/6Tj1ViZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<br />
  
  <p>
<img src="https://i.imgur.com/6Tj1ViZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<br />
