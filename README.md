<h1>Active Directory Lab</h1>


<h2>Description</h2>
In this walkthrough, we'll learn to create an Active Directory home lab environment using Oracle VirtualBox. Configuring and running this lab will help in the understanding of how Active Directory and Windows networking work.

<h2>Utilities Used</h2>

- Oracle
- Windows 10 Iso
- Windows Server 2019 Iso


<h2> Installing Oracle:</h2>

<p align="center">
<img src="https://imgur.com/ajlnqkf.png" height="80%" width="80%"/>

Download and install VirtualBox from the official website, consider the option of using an older build if there's a warning advising against the latest version.
Obtain the Windows 10 ISO from Microsoft's official website, selecting the appropriate edition, language, and architecture.
Additionally, download the Windows Server 2019 ISO, choosing the desired edition, language, and architecture.

<p align="center">
<img src="https://imgur.com/aZSRgBa.png" height="80%" width="80%"/>

Fill out the required information and download both files to the same location. Open VirtualBox and create a new virtual machine for Server 2019.
Configure settings: allocate RAM (at least 2GB) and set up network adapters (one for internet, one internal). Start the VM and select the Server 2019 ISO.
Install Server 2019 with GUI (Standard Desktop Experience). Follow installation prompts, including accepting license agreements.
After installation, set password (e.g., "Password1") for the default administrator account.

<h2>Network Setting on Windows Server 2019</h2>

<p align="center">
<img src="https://imgur.com/Fql3Hlq.png" height="80%" width="80%"/>

Set up IP addresses for both NICs: one for internet (automatic) and one internal (manual) on your Windows Server 2019. Click on "Settings," then "Network," "Ethernet," and "Change adapter options." Rename PC to "DC" (Domain Controller) via system settings. Assign IP address 172.16.0.1 to the internal NIC with subnet mask 255.255.255.0 and DNS set to self (either 172.16.0.1 or loopback address). Close settings.

<p align="center">
<img src="https://imgur.com/QjBusg8.png" height="80%" width="80%"/>

Open "Add Roles and Features" and select the server.Choose "Active Directory Domain Services" and install.
Post-installation, click on the notification flag to promote the server to a domain controller. Select "Add new forest" and name the domain (e.g., mydomain.com). Then Proceed with default settings and set a password.
Complete the installation, and the server will automatically restart. Log in using the built-in admin account (now with mydomain\administrator).

<h2>Setting-up a user account</h2>

<p align="center">
<img src="https://imgur.com/GCd0B1B.png" height="80%" width="80%"/>

Log in with the built-in admin account (now mydomain\administrator). Create a dedicated domain admin account via "Start," "Administrative Tools," "Active Directory Users and Computers." Create an organizational unit named "MyAdmins" and create a new user with a naming convention (e.g., first initial, last name). Assign password "password1" and ensure "User must change password" is unchecked. Also, uncheck "Password never expires." Finish to create the account.

<p align="center">
<img src="https://imgur.com/UpH0Jax.png" height="80%" width="80%"/>

Go to "Tools" > "Routing and Remote Access," configure and enable NAT for internal clients to access the internet using one address. Select the public interface (named "Internet") for internet connection. Once configured, the status should show a green checkmark.

<p align="center">
<img src="https://imgur.com/p13t1G5.png" height="80%" width="80%"/>

Set up DHCP server on the domain controller to provide IP addresses for Windows 10 clients. Go to "Add Roles," select DHCP, and install. In "DHCP" under "Tools," create a scope (e.g., 172.16.0.100 - 172.16.0.200) with subnet mask 255.255.255.0. Configure DHCP options: set the router's IP address as the domain controller's internal NIC, and DNS server as the domain controller. Authorize the DHCP server and refresh to activate the scope.

<h2> Creating a Windows 10 VM</h2>

<p align="center">
<img src="https://imgur.com/bIDx2uW.png" height="80%" width="80%"/>

Create a Windows 10 virtual machine in VirtualBox with an internal NIC. Configure settings (RAM, processor, clipboard), then start the VM and install Windows 10 from the ISO. Complete the installation process, skipping product key and selecting Windows 10 Pro. Once installed, ensure the internet connection is functioning by checking IP configuration.

<p align="center">
<img src="https://imgur.com/ywpfoGN.png" height="80%" width="80%"/>

To finish up, go to Active Directory Users and Computers on the domain controller VM. Navigate to the Computer container to verify the client computer's domain membership. Then, switch back to the Windows 10 VM, login using domain credentials created earlier. After signing in, the profile is created, simulating a corporate network setup. Finally, ensure everything is functioning by checking the command line for domain membership and user details. This concludes the tutorial. 
