<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployment and Configuration </h1>


<p>This tutorial is designed to provide a comprehensive understanding of deploying and optimizing an Active Directory system.

</p>

<h2>Overview </h2>

The goal is to install and set up Active Directory on the designated Domain Controller (DC-1) virtual machine and create a new Active Directory forest. This includes establishing and managing user accounts with administrative privileges. The Client-1 virtual machine will be joined to the domain to ensure seamless communication. Remote Desktop access will be configured for non-administrative users to improve accessibility while maintaining security protocols.

<h2>Prerequisites</h2>

- <a href="https://github.com/ncgriffin/ad-azuresetup"> On-premises Active Directory Deployed in the Cloud </a>



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Configuration Steps</h2>

<h3>&#9312; Install Active Directory in DC-1</h3>

- In the Server Manager dashboard, click 'Add Roles and Features' and continue the setup
<img width="736" alt="AD-setup" src="https://imgur.com/cQnpkfN.png">

<p>

</p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Select Active Directory Domain Services and finish the installation </strong> </p>
<p>
</p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9313; Promote DC-1 to Domain Controller </h3>

- Once the installation is done, notice the flag on the Server Manager
- Click on the flag and promote DC-1 to Domain Controller

<img width="242" alt="notif" src="https://imgur.com/4W04gBQ.png">


<p><strong>.</strong></p>
<p><strong>.</strong></p>

-  Next, we will select 'Add a new forest' and set the Root domain name to “mydomain.com”
<p>
<img width="565" alt="my domain" src="https://imgur.com/ovGgm26.png"> </p>
  
- Finish setup and restart DC-1
- Log back into Remote Desktop with your username credentials following with "@mydomain.com" 


<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9314; Create an Admin in Active Directory </h3>

- Once DC-1 has rebooted, click on tools and select Active Directory Users and Computers
- Right click on mydomain.com; select -> New -> Organizational Unit and click on Organizational Unit
<img width="438" alt="Users" src="https://imgur.com/VESNQeS.png">


<br>
<br>
<br>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> We will create two OU's labeled "_EMPLOYEES" and "_ADMINS" </strong></p>

<img width="450" alt="admins" src="https://imgur.com/vsSxufF.png">


<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong>Right click on Users and create a new user named "Jane Doe" with the username "jane_admin"</strong></p>

<img width="323" alt="jane doe" src="https://imgur.com/n9RKfcz.png">


<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong>We will change Jane Doe into an admin account by right clicking her name and adding her to the “Domain Admins” security group</strong></p>

<img width="412" alt="add to group" src="https://imgur.com/n9RKfcz.png">



<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong>Logout of DC-1 and sign back in with Jane Doe’s credentials</strong></p>

<img width="337" alt="jane login" src="https://imgur.com/EnnzYVs.png">

<p><strong>.</strong></p>
<p><strong>.</strong></p>


<h3>&#9315; Join Client-1 to Domain </h3>

<p><strong> For Client-1 to join the domain, the DNS server must be changed. Therefore we will set it's DNS server as DC-1's private IP address</strong></p>

- In the Azure Portal, select Client-1 -> Networking -> Network interface -> Settings -> DNS Server

<img width="735" alt="dns servers" src="https://imgur.com/9bKXViA.png">



<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong>Select a custom DNS server and type in the private IP address of DC-1 and restart Client-1 virtual machine in Azure</strong></p>

<img width="356" alt="dns servers2" src="https://imgur.com/5hhy1Ac.png">

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Now log back in to Client-1 using your original credentials. Click start and go to Settings -> Rename this PC (advanced) -> Change and add “mydomain.com” and login with the admin credentials previously created (jane_admin) </strong></p>

<img width="297" alt="remote desktop first login" src="https://imgur.com/OsjB5gK.png">

<br>

<p> <strong>Once Client-1 has been added, the VM will restart.</strong></p>


<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9316; Setup Remote Desktop for non-administrative users </h3>

- Log back into Client-1 using "jane_admin" credentials and open Settings -> Remote Desktop -> User Accounts and click “Select users that can remotely access this PC”
- Add Domain Users

<br>


<img width="343" src="https://imgur.com/R2sxVPR.png">

<p><strong>This allows normal users to login to Client-1</strong></p>

<br>

<p><strong>.</strong></p>
<p><strong>.</strong></p>



<h2> Final Thoughts </h2>

<p>
We've successfully completed the Active Directory Deployment and Configuration phase. By configuring Active Directory on the Domain Controller, we established our infrastructure, created a forest and administrator account, and integrated Client-1 into the domain. </p>








