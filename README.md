<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 11</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure virtual machine 
- os Ticket installation files
- RDP (port 3389) allowed on VM
- Enabling IIS in windows vm 
- 

<h2>Installation Steps</h2>


<p>
  In order for OS Ticket properly we would need to install/enable IIS in windows with CGI.
  1.Go into control panel -> Programs -> Turn Windows features on or off ->  enable Internet Information Services -> world wide web -> Application Development features -> check CGI -> click ok and close out. 
</p>
<p>
<img src="https://i.imgur.com/ELjVPpy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After CGI is enabled, install the following files from "osTicket-Installation-Files" folder in this order: PHP manager, Rewrite Module, VC redist.x86.exe, and MYSQL file. For the MySQL you will need to click Typical setup -> Launch configuration Wizard (default) -> create user and password. After installs are completed, create a new directory "C:\PHP" and unzip the folder PHP 7.3.8 inside it.
</p>
<p>
  <img width="726" alt="image" src="https://github.com/user-attachments/assets/b1d19b02-47a4-4cb5-8f2f-b32cb8fd4f09" />

</p>
<br />
<p>
We can now open ISS as an Admin, register PHP from within IIS (PHP manager -> C:\PHP\php-cgi.exe) and reload IIS.
Install osTicket v1..15.8 by unzipping it from the installation folder and copying it in “c:\inetpub\wwwroot” then renaming it to "osTicket". Reload IIS. In ISS, click on sites -> Default -> osTicket , on the far right click on "Browse *.80" this will take to the osticket setup page. Some extensions need to be enabled, go back to IIS, click on sites -> Default -> osTicket , Double click PHP manager, click on "Enable or disabale an extension" and enable php_imap.dll, php_intl.dll, and php_opache.dll. After enabled, refesh osTicket setup page and they should be enabled.
</p>
<p>
  <img width="763" alt="image" src="https://github.com/user-attachments/assets/d6097b14-f8bd-4758-8535-935fb4385eb0" />
</p>

<p>
Rename: ost-config.php
-	From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
-	To: C:\inetpub\wwwroot\osTicket\include\ost-config.php
</p>
<p>
  Assign permissions to ost-config.php : right click file -> properties -> Security -> advanced -> disable inheritence -> add -> select principal -> enter "Everyone" then "ok" -> click "Full control" then ok -> verify permissions under "Permissions entries".
</p>
<p>
  <img width="556" alt="image" src="https://github.com/user-attachments/assets/0a521448-d63c-4f1e-bbf0-4a2cff796935" />
</p>
<p>
  Continue setting up osTicket in setup page, enter information (name, email, user, password). Before finishing we need to install HeidiSQL from installation folder then: open -> create new session root/root -> connect session -> create database called "osTicket". This new data base will be used by osTicket and send data into it. Continue setting up osTicket in browser and fill out the infromation (same information you netered when database was created). Click "install now" and you should have osTicket installed!! In the same page at the bottom there will be some links to verify connectivity ( osTicket URL and Staff control panel)
</p>
<br />

<p>
<img width="583" alt="image" src="https://github.com/kuyaMERLIN/osticket-prereq/blob/main/Step5.png?raw=true" />

</p>
<p>

</p>
<br />
