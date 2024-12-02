<p align="center">

<img src="https://winaero.com/blog/wp-content/uploads/2018/06/Shared-Folder-Network-Icon.png"  height="30%" width="30%" alt="File sharing"/>
 
 <h1>Network File Sharing & Permissions</h1>
The objective of this lab was to investigate network file sharing and permissions in Azure, including configuring shared file systems, managing user access, and applying security policies to ensure proper access control in a cloud-based environment.

<br />


<h2>Environments and Technologies</h2>

- <b>Microsoft Azure</b> 
- <b>Remote Desktop</b>
- <b>Ping</b>

<h2>Operating Systems</h2>

- <b>Windows 10</b> (22H2)
- <b>Windows Server</b> (2022)
  <br />

<h2>Prerequisites</h2>
Complete the following lab series: <a href="https://github.com/gwendus/ADInfrastructureInAzure/blob/main/README.md">Preparing Active Directory Infrastructure in Microsoft Azure</a>
<br />

<h2>Create Sample File Shares with Permissions</h2>
1. Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin) <br>
2. Connect/log into Client-1 as a normal user (mydomain\<someuser>) <br>
3. On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
  <br>
  <br>
<img src="https://i.imgur.com/i36s0M6.png" height="80%" width="80%" alt="create 4 folders"/>
<br />
<br />

<b>Set the following permissions (share the folder):</b><br>

- Folder: “read-access”, Group: “Domain Users”, Permission: “Read”<br />
- Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”<br />
- Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”<br />
- (Skip accounting for now)<br />

<img src="https://i.imgur.com/Fzs2Gql.png" height="80%" width="80%" alt="give read access 2"/>
<br />
<br />
<br />

<img src="https://i.imgur.com/LJHtQvW.png" height="80%" width="80%" alt="give read access 1"/>
<br />
<br />
<h2>Accessing File Shares</h2>
On Client-1, navigate to the shared folder (start, run, \\dc-1)

<img src="https://i.imgur.com/Rxcu0gx.png" height="70%" width="70%" alt="dc1 folders"/>

<br />
<br />

Try to access the folders you just created. Which folders can you access? Which folders can you create stuff in? Does it make sense?
 <br/>

<img src="https://i.imgur.com/YlU6EyR.png" height="70%" width="70%" alt="folders in dc1"/>
<br />
<br />

For example: observe how "no-access" is completely inaccessible <br>
<br />
<img src="https://i.imgur.com/RrkUTmJ.png" height="70%" width="70%" alt="no access folder"/>

<br />
<br />

<h2>Testing Security Groups, Permission, and Access</h2>
Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”
<br/>
<img src="https://i.imgur.com/nti61lx.png" height="60%" width="60%" alt="new group lol"/>
<br />
<br />
<img src="https://i.imgur.com/HO9TDvg.png" height="60%" width="60%" alt="new group lol2"/>
<br />
<br />

On the “accounting” folder you created earlier, set the following permissions:
- Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”

 <br/>

<img src="https://i.imgur.com/NBiy39u.png" height="80%" width="80%" alt="accountants permissions"/>
<br />
<br />

On Client-1, as  <someuser>, try to access the accountants folder. It should fail.  <br/>

<img src="https://i.imgur.com/OVDrYXk.png" height="80%" width="80%" alt="cannot access accountants "/>
<br />
<br />

Log out of Client-1 as  <someuser>. <br />
<img src="https://i.imgur.com/YmT3U3W.png" height="80%" width="80%" alt="logout"/>
<br />
<br />


On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group
 <br/>

<img src="https://i.imgur.com/SyXfQad.png" height="80%" width="80%" alt="make big.fat part of the accts sg"/>
<br />
<br />

Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\ - Does it work now? <br/>

<img src="https://i.imgur.com/V2iiClb.png" height="80%" width="80%" alt="success"/>
<br />
<br />


<h2>Conclusions</h2>
Conclusion: This lab emphasized the importance of provisioning access and managing Active Directory and security groups in Azure to ensure secure, efficient resource control and minimize unauthorized access. <br/>

<img src="https://i.imgur.com/7ibcuxK.png" height="80%" width="80%" alt="overview"/>
<br />
<br />
You may now delete your resources in Azure if you are finished with the labs. It is useful to practice them several times to gain familiarity within the Active Directory Console.
