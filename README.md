# Windows Server 2019 Deployment
<h2>Description</h2>
This project walks you through deploying Windows Server 2019 as a domain controller, setting up Active Directory Domain Services (AD DS), and managing users via Group Policy Management. Group Policies help you control security settings, software deployments, and user behavior on Windows systems within your domain.
<br />
<h2>Step 1: Install and Set Up Windows Server 2019 </h2>
<ol>
   <li>Download Windows Server 2019:</li>
   <ul>
      <li>Go to the Windows Server 2019 Evaluation Page and download the ISO file.</li>
   </ul>
   <li>Install Windows Server 2019 on a Virtual Machine or Physical Machine:</li>
   <ul>
      <li>Create a new virtual machine (VM) in VirtualBox (or another virtualization platform) using the steps outlined in the previous project.</li>
   </ul>
   <ul>
      <li>Use the Windows Server 2019 ISO as the startup disk and install the server.</li>
   </ul>
   <ul>
      <li>Follow the on-screen instructions to install Windows Server 2019 Standard (Desktop Experience).</li>
   </ul>
   <li>Set Administrator Password</li>
   <ul>
      <li>After installation, create a strong password for the Administrator account.</li>
   </ul>
   <ul>
      <li>Leave the default options selected unless you require custom settings.</li>
   </ul>
     <li>Configure Network Settings:</li>
   <ul>
      <li>Ensure that your server has a static IP address for stability in a network environment.</li>
   </ul>
   <ul>
      <li>To set a static IP address, open Network & Internet Settings and manually configure your IP, subnet, default gateway, and DNS server.</li>
   </ul>
</ol>


<h2>Step 2: Promote the Server to a Domain Controller</h2>
<ol>
   <li>Install Active Directory Domain Services (AD DS):</li>
   <ul>
      <li>Open Server Manager and click on Add roles and features.</li>
   </ul>
   <ul>
      <li>Select Active Directory Domain Services (AD DS) and follow the prompts to install the role.</li>
   </ul>
   <li>Promote Server to Domain Controller:</li>
   <ul>
      <li>After installation, click on the flag icon in Server Manager and select Promote this server to a domain controller.</li>
   </ul>
   <ul>
      <li>Choose Add a new forest and enter a domain name (e.g., yourdomain.local). 
         <br/>
         <img src="https://i.imgur.com/xLBPzXn.png" height="40%" width="40%" alt="script"/>
         <br/>
      </li>
   </ul>
   <ul>
      <li>Set the Forest Functional Level and Domain Functional Level to Windows Server 2016 or higher.
         <br/>
         <img src="https://i.imgur.com/eVUHNRy.png" height="40%" width="40%" alt="script"/>
         <br/>
      </li>
   </ul
      <ul>
      <li>Enter a Directory Services Restore Mode (DSRM) password and complete the installation.</li>
   </ul>
  <li>Restart the Server:</li>
   <ul>
      <li>Right-click on your domain (e.g., yourdomain.local) and choose New > Organizational Unit.</li>
   </ul>
   <ul>
      <li>Name the OU (e.g., Users or Workstations). This will help you organize and apply specific policies to users and computers.</li>
   </ul>
</ol>



<h2>Step 3: Set Up Active Directory Users and Computers</h2>
<ol>
   <li>Open Active Directory Users and Computers:</li>
   <ul>
      <li>In Server Manager, click Tools and select Active Directory Users and Computers.</li>
   </ul>
   <br/>
   <img src="https://i.imgur.com/7V1Ieb7.png" height="40%" width="40%" alt="script"/>
   <br/>
   <li>Create Organizational Units (OUs):</li>
   <img src="https://i.imgur.com/HsDzzg6.png" height="40%" width="40%" alt="script"/>
   <br/>
   <ul>
      <li>Once the server has been promoted to a domain controller, the system will restart automatically.</li>
   </ul>
   <li>Create User Accounts:</li>
   <img src="https://i.imgur.com/y0pv2di.png" height="40%" width="40%" alt="script" "/>
   <br/>
  <ul>
      <li>Right-click the Users OU and select New > User.</li>
   </ul>
  <ul>
      <li>Fill in the user details and set a password. Choose whether the user must change their password on first login.</li>
   </ul>
   </li></ul>
    <li>Join Client Computers to the Domain</li>
   <img src="https://i.imgur.com/y0pv2di.png" height="40%" width="40%" alt="script" "/>
   <br/>
  <ul>
      <li>On any client machine (such as your Windows 10 VM), right-click This PC, select Properties, and then click Change settings under Computer name.</li>
   </ul>
  <ul>
      <li>In System Properties, click Change and join the computer to your new domain by entering the domain name (e.g., yourdomain.local).</li>
   </ul>
   <ul>
      <li>You’ll need to provide the Administrator account credentials for the domain.</li>
   </ul>
   </li></ul>
</ol>



<h2>Step 4: Install Group Policy Management </h2>
<ol>
   <li>Install Group Policy Management Feature:</li>
   <ul>
      <li>Open Server Manager and click Add roles and features.</li>
   </ul>
   <ul>
      <li>On the Features screen, check the box for Group Policy Management.</li>
   </ul>
   <ul>
      <li>Follow the prompts to complete the installation.</li>
   </ul>
   <ul>
      <li>Create groups for specific roles (e.g., admin, user, guest) by running the following code:</li>
   </ul>
   <img src="https://i.imgur.com/RXI5kjZ.png" height="30%" width="30%" alt="script"/>
   <br/>
   <li>Assign Permissions to Groups</li>
   </ul>
   <ul>
      <li>Use the chmod and chown commands to set directory permissions.</li>
   </ul>
   <img src="https://i.imgur.com/9c335UK.png" height="30%" width="30%" alt="script"/>
   <li>Enforce Access Control</li>
   <ul>
      <li>Verify permissions by switching to different users and testing to see if you can access the created directories.</li>
   </ul>
   <img src="https://i.imgur.com/pY3M8ON.png" height="30%" width="30%" alt="script"/>
</ol>



<h2>Step 5: Create and Apply Group Policies</h2>
<ol>
   <li>Open Group Policy Management:</li>
   <ul>
      <li>In Server Manager, click Tools and select Group Policy Management.</li>
   </ul>
   <ul>
      <li>Must include uppercase, lowercase, numbers, and special characters.</li>
   </ul>
   <ul>
      <li>Prevent the reuse of the last five passwords.</li>
   </ul>
   <ul>
      <li>Implement password expiration policies: Set passwords to expire every 60 days on all machines (via Group Policy for Windows and /etc/login.defs for Linux).</li>
   </ul>
   <li>Create a New Group Policy Object (GPO):</li>
   <ul>
      <li>In the Group Policy Management window, expand your domain (e.g., yourdomain.local).</li>
   </ul>
   <ul>
      <li>Right-click Group Policy Objects and select New.
   </ul>
     <ul>
      <li>Name the new GPO (e.g., Security Policy for Users).</li>
   </ul>
   <li>Edit the Group Policy:</li>
   <ul>
      <li>Right-click your new GPO and select Edit</li>
      <ul>
      <li>The Group Policy Management Editor will open, allowing you to configure settings for users and computers.</li>
   </ul>
      <ul>
         <li>Add the following line of code:</li>
         <img src="https://i.imgur.com/nsauMaI.png" height="40%" width="40%" alt="script"/>
         <br/>
         <li>auth required pam_tally2.so: Specifies the use of the pam_tally2 module, which keeps a tally of failed login attempts for user accounts.
         <li>deny = 3: Sets a limit of 3 failed login attempts before the account is locked.</li>
         <li>unlock_time=600: Configures the lockout period to 600 seconds (10 minutes). After this time, the account is automatically unlocked.</li>
         <li>onerr=fail: Ensures that if there’s an error in the PAM module, access is denied by default.</li>
         <li>audit: Enables logging of authentication attempts, including both successful and failed logins.</li>
         </li>
      </ul>
   </ul>
</ol>
<h2>Step 6: Monitor User Activity </h2>
<ol>
   <li>Enable Audit Logging</li>
   <ul>
      <li>Install auditd:</li>
   </ul>
   <br/>
   <img src="https://i.imgur.com/tBsG67J.png" height="40%" width="40%" alt="script"/>
   <br/>
   <li>Start and enable the service:</li>
   <img src="https://i.imgur.com/TWlGzOR.png" height="40%" width="40%" alt="script"/>
   <br/>
   <li>Define Audit Rules</li>
   <img src="https://i.imgur.com/y0pv2di.png" height="40%" width="40%" alt="script" "/>
   <br/>
   </li></ul>
</ol>
