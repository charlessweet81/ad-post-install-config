<p align="center">
<img src="https://i.imgur.com/pJSsvpx.png" alt=""/>
</p>

<h1>Deploying Active Directory</h1>
<p>
his tutorial walks you through the process of setting up a Domain Controller (DC) and a Client in Microsoft Azure, showcasing how to configure network connections and test functionality in a controlled virtual environment. By deploying a Windows Server as a Domain Controller (DC-1) and a Windows 10 machine as a client (Client-1), we’ll explore how to configure private networks, assign static IPs, and test connectivity between virtual machines.

Through this step-by-step guide, you’ll gain practical experience in:

- Establishing a domain environment in Azure.
- Configuring DNS settings and testing network connectivity.
- Troubleshooting and ensuring seamless communication between virtual machines.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop

<h2>Operating Systems Used</h2>

- Windows Server 2022</b>

<h2>List of Steps</h2>

- Part I: Install Active Directory on DC-1
  - Step 1: Install Active Directory Domain Services (AD DS)
  - Step 2: Promote DC-1 to a Domain Controller
  - Step 3: Log Back Into DC-1
- Part II: Create a Domain Admin User
  - Step 1: Open Active Directory Users and Computers (ADUC)
  - Step 2: Create Organizational Units (OUs)
  - Step 3: Create a New User (Jane Doe)
  - Step 4: Add Jane Doe to the "Domain Admins" Group
  - Step 5: Log In as Jane Admin
- Part III: Join Client-1 to the Domain
  - Step 1: Log Into Client-1
  - Step 2: Join Client-1 to the Domain
  - Step 3: Verify Client-1 in ADUC
  - Step 4: Move Client-1 to the _CLIENTS OU

<h2>Installation Steps</h2>
<h3>Part 1: Install Active Directory on DC-1</h3>

<h4>Step 1: Install Active Directory Domain Services (AD DS)</h4>

<img src="https://i.imgur.com/H3yOLKi.png" height="80%" width="80%" alt=""/>

- Log into DC-1 using the credentials:
  - Username: labuser.
  - Password: Cyberlab123!.
- Open the Server Manager on DC-1.
- Click on Add Roles and Features.
- In the wizard:
  - Select Role-based or feature-based installation.
  - Choose the server (DC-1) from the server pool.
  - Select Active Directory Domain Services and click Next.
- Confirm the installation and click Install.
- Wait for the installation to complete and do not restart yet.

<h4>Step 2: Promote DC-1 to a Domain Controller</h4>

<img src="https://i.imgur.com/dc07sEq.png" height="80%" width="80%" alt=""/>

- After the AD DS installation is complete, click on the Promote this server to a domain controller link in Server Manager.
- In the Deployment Configuration window:
  - Select Add a new forest.
  - Enter your domain name (e.g., mydomain.com).
  - Click Next through the options, setting up:
  - Forest Functional Level: Windows Server 2016 or higher.
  - Create a Directory Services Restore Mode (DSRM) password.
- Click Install to promote the server.
- After the installation, the server will restart automatically.

<h4>Step 3: Log Back Into DC-1</h4>

<img src="https://i.imgur.com/xmHmeuy.png" height="80%" width="80%" alt=""/>

- Once DC-1 restarts, log in as:
  - Username: mydomain.com\labuser
  - Password: Cyberlab123!

<h3>Part II: Create a Domain Admin User</h3> 

<h4>Step 1: Open Active Directory Users and Computers (ADUC)</h4>

<img src="https://i.imgur.com/uIBtlR5.png" height="80%" width="80%" alt=""/>

On DC-1, open Active Directory Users and Computers from the Start menu.

<h3>Step 2: Create Organizational Units (OUs)</h3>

<img src="https://i.imgur.com/woWbf1N.png" height="80%" width="80%" alt=""/>

- Inside the _ADMINS OU:
  - Right-click the OU and select New > User.
  - Enter the following:
    - First Name: Jane.
    - Last Name: Doe.
    - Username: jane_admin.
- Set the password to Cyberlab123!.
- Complete the wizard and create the user.

<h3>Step 4: Add Jane Doe to the "Domain Admins" Group</h3>

<img src="https://i.imgur.com/CowJbIQ.png" height="80%" width="80%" alt=""/>

- In ADUC, right-click on jane_admin and select Properties.
- Go to the Member Of tab.
- Click Add, search for Domain Admins, and add the user to the group.
- Click OK to save.

<h3>Step 5: Log In as Jane Admin</h3>

<img src="https://i.imgur.com/HUEcGSt.png" height="80%" width="80%" alt=""/>

- Log out of DC-1 and log back in using the credentials:
  - Username: mydomain.com\jane_admin.
  - Password: Cyberlab123!.
- From now on, use jane_admin as your admin account.

<h3>Part III: Join Client-1 to the Domain</h3> 

<h3>Step 1: Log Into Client-1</h3>

<img src="https://i.imgur.com/4HdBb4U.png" height="80%" width="80%" alt=""/>

- Log into Client-1 using the local admin credentials:
  - Username: labuser.
  - Password: Cyberlab123!.

<h3>Step 2: Join Client-1 to the Domain</h3>

<img src="https://i.imgur.com/b7GT7t4.png" height="80%" width="80%" alt=""/>

- On Client-1, open Settings > System > About.
- Click Join a domain under Device specifications.
- Enter the domain name (e.g., mydomain.com) and click Next.
- Provide the domain admin credentials:
  - Username: mydomain.com\jane_admin.
  - Password: Cyberlab123!.
- Restart Client-1 when prompted.

<h3>Step 3: Verify Client-1 in ADUC</h3>

<img src="https://i.imgur.com/2Dal3Ka.png" height="80%" width="80%" alt=""/>

- Log back into DC-1 as jane_admin.
- Open Active Directory Users and Computers (ADUC).
- Expand your domain and verify that Client-1 appears under the Computers container.

<h3>Step 4: Move Client-1 to the _CLIENTS OU</h3>

<img src="https://i.imgur.com/pDELfsE.png" height="80%" width="80%" alt=""/>

- In ADUC, create a new OU named _CLIENTS:
  - Right-click the domain name and select New > Organizational Unit.
  - Name it _CLIENTS.
- Drag and drop Client-1 from the Computers container into the _CLIENTS OU.
