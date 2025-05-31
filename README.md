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

- Set up a Resource Group and a Virtual Machine (VM) in Azure.
- Install the osTicket requirements.
- Install osTicket itself.


<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/yogBGNS.png" height="80%" width="80%"/> 
</p>
<p>

## Step 1: VM Setup & Prerequisites

1. **Create VM in Azure**
   - Name: `osticket-vm`
   - OS: Windows 10, 4 vCPUs
   - Username: `labuser`
   - Password: `osTicketPassword1!`

2. **Connect via RDP** and extract `osTicket-Installation-Files.zip` to Desktop.

3. **Install Dependencies**
   - Enable **IIS with CGI**:  
     `Control Panel → Programs → Turn Windows features on/off → IIS → Application Development → [x] CGI`
   - Install from `osTicket-Installation-Files`:
     - `PHPManagerForIIS_V1.5.0.msi`
     - `rewrite_amd64_en-US.msi`
     - `VC_redist.x86.exe`
     - `mysql-5.5.62-win32.msi` (MySQL root/root)
   - Unzip `php-7.3.8-nts-Win32-VC15-x86.zip` to `C:\PHP`
   - Register PHP in IIS:  
     PHP Manager → Register: `C:\PHP\php-cgi.exe`
   - Restart IIS (Stop/Start)

<p>
<img src="https://i.imgur.com/LddZPLP.png" height="80%" width="80%"/> 
</p>
<p>

## Step 2: osTicket File Setup

1. Unzip `osTicket-v1.15.8.zip` → Copy `upload` to:  
   `C:\inetpub\wwwroot\osTicket`

2. In IIS:
   - Enable PHP extensions:
     - `php_imap.dll`
     - `php_intl.dll`
     - `php_opcache.dll`

3. Configure:
   - Rename `ost-sampleconfig.php` → `ost-config.php`  
     (Located in `osTicket\include`)
   - Set permissions on `ost-config.php`:
     - Disable inheritance
     - Remove all
     - Add `Everyone: Full Control`

<p>
<img src="https://i.imgur.com/bxkZkbl.png" height="80%" width="80%"/> 
</p>
<p>

## Step 3: Final Setup & Cleanup

1. **Database**:
   - Install **HeidiSQL**
   - Create DB: `osTicket`
   - Login: `root` / `root`

2. **Browser Setup**:
   - Navigate: `http://localhost/osTicket`
   - Complete install:
     - Helpdesk Name
     - Admin Email
     - MySQL: `osTicket` / root / root

3. **Post-Install**:
   - Delete: `C:\inetpub\wwwroot\osTicket\setup`
   - Set `ost-config.php` to **Read-only**
