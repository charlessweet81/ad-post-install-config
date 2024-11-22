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

<h3>Part II: Create a Domain Admin User</h3> TK

<h4>Step 1: Open Active Directory Users and Computers (ADUC)</h4>

<img src="https://i.imgur.com/uIBtlR5.png" height="80%" width="80%" alt=""/>

On DC-1, open Active Directory Users and Computers from the Start menu.

<h3>Step 2: Set Client-1’s DNS Settings to DC-1’s Private IP</h3>

<img src="https://i.imgur.com/MlCUQ6t.png" height="80%" width="80%" alt=""/>

- Once the VM is created, navigate to Virtual Machines and select Client-1.
- Under Settings, click Networking.
- Select the NIC attached to Client-1 and go to DNS Servers.
- Set the DNS server to Custom and input DC-1’s Private IP Address.
- Save the changes.

<h3>Step 3: Restart Client-1</h3>

<img src="https://i.imgur.com/FRe2Vj0.png" height="80%" width="80%" alt=""/>

- From the Azure Portal, select Client-1.
- Click Restart to apply the DNS changes.

<h3>Step 4: Login to Client-1</h3>

<img src="https://i.imgur.com/cdemX9a.png" height="80%" width="80%" alt=""/>

- Connect to Client-1 using RDP (same method as DC-1).
- Login with:
  - Username: labuser.
  - Password: Cyberlab123!

<h3>Step 5: Test Connectivity</h3>
<img src="https://i.imgur.com/4HdBb4U.png" height="80%" width="80%" alt=""/>

- Open a Command Prompt or PowerShell on Client-1.
- Run the following command:
  - ping <DC-1 Private IP>
- Ensure you see replies from DC-1's private IP.

<h3>Step 6: Verify DNS Settings</h3>
<img src="https://i.imgur.com/ROvkxrC.png" height="80%" width="80%" alt=""/>

- From Client-1, open PowerShell.
- Run the following command:
  - ipconfig /all
- Verify that the DNS Server is set to DC-1’s private IP.
