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
      <li>Create a new virtual machine (VM) in VirtualBox (or another virtualization platform) using the steps outlined in the </li>
   </ul>
   [prevous project.](https://github.com/SomoneL/Setting-Up-Virtual-Machines-Using-VirtualBox)
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
</ol>
<h2>Step 2: Promote the Server to a Domain Controller</h2>
<ol>
   <li>Install Active Directory Domain Services (AD DS):</li>
   <ul>
      <li>Open Server Manager and click on Add roles and features.</li>
   </ul>
   <br/>
   <img src="https://imgur.com/297vxr3.png" height="40%" width="40%" alt="script"/>
   <br/>
   <ul>
      <li>Select Active Directory Domain Services (AD DS), select Add Features, and follow the prompts to install the role.</li>
   </ul>
   <br/>
   <img src="https://imgur.com/7mOyAeg.png" height="40%" width="40%" alt="script"/>
   <br/>
   <br/>
   <img src="https://imgur.com/itw0t6K.png" height="40%" width="40%" alt="script"/>
   <br/>
   <li>Promote Server to Domain Controller:</li>
   <ul>
      <li>After installation, click on the flag icon in Server Manager and select Promote this server to a domain controller.</li>
   </ul>
   <br/>
   <img src="https://imgur.com/O6kMSLS.png" height="40%" width="40%" alt="script"/>
   <br/>
   <ul>
      <li>Choose Add a new forest and enter a domain name (e.g., mydomain.local). 
         <br/>
      </li>
      <br/>
      <img src="https://imgur.com/yplSKi6.png" height="40%" width="40%" alt="script"/>
      <br/>   
   </ul>
   <ul>
      <li>Set the Forest Functional Level and Domain Functional Level to Windows Server 2016 or higher.
      </li>
      </ul
      <ul>
         <li>Enter a Directory Services Restore Mode (DSRM) password and complete the installation then restart your server when prompted to do so. Sign back in after your server restarts. You will now see your domain name and login. </li>
      </ul>
      <br/>
      <img src="https://imgur.com/3EnTNOD.png" height="40%" width="40%" alt="script"/>
      <br/>
</ol>
<h2>Step 3: Set Up Active Directory Users and Computers</h2>
<ol>
<li>Open Active Directory Users and Computers:</li>
<ul>
<li>In Server Manager, click Tools and select Active Directory Users and Computers.</li>
</ul>
<br/>
<img src="https://imgur.com/KafsZLo.png" height="40%" width="40%" alt="script"/>
<br/>
<li>Create Organizational Units (OUs):</li>
<ul>
<li>In the right menu, rick click your domain and select New > Organizational Unit. We will name it '_ADMINS' and we will create this to put our admin account that we will work with in. Think of it like a folder in Active Directory. </li>
</ul>
<br/>
<img src="https://imgur.com/bmbhuFq.png" height="40%" width="40%" alt="script"/>
<br/>   
<br/>
<img src="https://imgur.com/hi9KKun.png" height="40%" width="40%" alt="script"/>
<br/>  
<li>Create User Accounts:</li>
<ul>
<li>Right-click the _ADMINS OU and select New > User.</li>
</ul>
<br/>
<img src="https://imgur.com/fR3sh3c.png" height="40%" width="40%" alt="script"/>
<br/> 
<ul>
<li>Fill in the user details and set a password. Choose whether the user must change their password on first login.(using the 'a-' naming convention signals to us this is an admin account.</li>
</ul>
<br/>
<img src="https://imgur.com/UI3dQDc.png" height="40%" width="40%" alt="script"/>
<br/>
<br/>
<img src="https://imgur.com/epuUsH0.png" height="40%" width="40%" alt="script"/>
<br/>   
</li></ul>
<li>Make Created Account a Domain Admin</li>
<ul>
<li>Right click your newly created user > Properties > Member Of tab > Add > 'domain admins' > Check Names > Ok    </li>
<br/>
<img src="https://imgur.com/6CRbKPP.png" height="40%" width="40%" alt="script"/>
<br/>    
</ul>
<ul>
<li>Test this account by signing out of your current account and signing in with the user credentials you just created. Be sure to select "Other user" before attempting to sign in. </li></ul>
<br> <img src="https://imgur.com/DYdxjFx.png" height="40%" width="40%" alt="script" "/>
<br/>
   
<li>Join Client Computers to the Domain(REMOVE FROM TUTORIAL???????)</li>
<img src="https://i.imgur.com/y0pv2di.png" height="40%" width="40%" alt="script" "/>
<br/>
<ul>
<li>On any client machine, (such as your Windows 10 VM. Click below for tutorial).
[Setting Up Virtual Machines Using Virtual Box](https://github.com/SomoneL/Setting-Up-Virtual-Machines-Using-VirtualBox)  
Right-click This PC, select Properties, and then click Change settings under Computer name.</li>
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
<li>I will be creating a new group policy that will prevent the users in the group from being able to change thier password??????</li>
<ol>
   <li>Install Group Policy Management Feature:</li>
   <ul>
      <li>Sign back into your original account and Open Server Manager and click Tools > Group Policy Management</li>
   </ul>
   <ul>
      <li>Navigate to the Group Policy Objects folder located in your created domain folder and create a new Group Policy Object (GPO).</li>
   </ul>
     <br> <img src="https://imgur.com/yNKHxuh.png" height="30%" width="30%" alt="script"/>
   <br/>
   <li>Access All Group Policies provided by the System</li>
   </ul>
   <ul>
      <li>Right click on your newly created GPO > Edit > Open the folders User Configuration > Policies > Administrative Templates > System. This shows all of the available Group Policies provided by the system. </li>
   </ul>
   <img src="https://imgur.com/dAmt1iu.png" height="30%" width="30%" alt="script"/>
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
      <li>Right-click your new GPO and select Edit.</li>
   </ul>
   <ul>
      <li>The Group Policy Management Editor will open, allowing you to configure settings for users and computers.</li>
   </ul>
   <ul>
      <li>Examples of GPO settings:</li>
      <ul>
         <li>Password Policy: Navigate to Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy to enforce password complexity and expiration.</li>
      </ul>
      <ul>
         <li>Software Restriction Policies: Use Computer Configuration > Policies > Windows Settings > Security Settings > Software Restriction Policies to control which software can run.</li>
      </ul>
   </ul>
   <li>Link the GPO to an OU:</li>
   <ul>
      <li>In the Group Policy Management console, right-click on the OU where you want to apply the GPO (e.g., Users or Workstations).</li>
   </ul>
   <ul>
      <li>Select Link an Existing GPO and choose the GPO you just created.</li>
   </ul>
   <ul>
   </ul>
   <li>Test the Group Policy</li>
   <ul>
      <li>On the client computer (Windows 10), log in as a user that is part of the domain.</li>
   </ul>
   <ul>
      <li>Open Command Prompt and run the following command to update Group Policy: gpupdate /force</li>
   </ul>
   <ul>
      <li>Log off and log back in to see if the Group Policy settings have been applied.</li>
   </ul>
   <ul>
</ol>
<h2>Step 6: Documenting and Analyzing Your Results</h2>
<ol>
<li>Review the Group Policies:</li>
<ul>
<li>Go back to Group Policy Management to review which GPOs are linked to which OUs.</li>
</ul>
<ul>
<li>Ensure that the policies are correctly applied and functioning by testing on the client machines.</li>
</ul>
<br/>
<img src="https://i.imgur.com/tBsG67J.png" height="40%" width="40%" alt="script"/>
<br/>
<li>Troubleshooting:</li>
<ul>
<li>If the policies are not applying as expected, use Resultant Set of Policy (RSoP) or gpresult command to diagnose issues: gpresult /r</li>
</ul>
</li></ul>
</ol>
<h2>Step 7: Conclusion</h2>
In this project, I demonstrated the deployment of Windows Server 2019 as a domain controller and the configuration of Group Policy Management to manage users and computers in an Active Directory environment. Through this process, I successfully applied security policies and user configurations across the domain. This project showcases my ability to set up server environments and efficiently manage systems using Group Policy, which is essential for maintaining a secure and well-organized IT infrastructure.     
<ol></ol>
