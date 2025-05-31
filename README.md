# osticket-prereq

<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>

# osTicket Installation on Azure Windows 10 VM

This guide documents the setup of osTicket v1.15.8 on a Windows 10 VM in Azure using IIS, PHP, and MySQL.

## 💻 VM Configuration

- **VM Name**: osticket-vm  
- **OS**: Windows 10  
- **vCPUs**: 4  
- **Username**: labuser  
- **Password**: osTicketPassword1!

## ✅ Step-by-Step Setup

### Step 1: Connect to VM

1. Deploy the VM in Azure.
2. Connect via **Remote Desktop** (RDP).

---

### Step 2: Prepare Environment

1. Unzip `osTicket-Installation-Files.zip` to Desktop.
2. Enable **IIS with CGI**:
   - Control Panel → Programs → Turn Windows features on/off:
     - `Internet Information Services > World Wide Web Services > Application Development Features > CGI`
3. Install:
   - **PHP Manager**: `PHPManagerForIIS_V1.5.0.msi`
   - **URL Rewrite Module**: `rewrite_amd64_en-US.msi`
   - **VC++ Redistributable**: `VC_redist.x86.exe`
4. Create directory: `C:\PHP`
5. Unzip `php-7.3.8.zip` to `C:\PHP`

---

### Step 3: Install and Configure MySQL

1. Install MySQL 5.5.62: `mysql-5.5.62-win32.msi`
   - Choose **Typical Setup**
   - Use **Standard Configuration**
   - Username: `root`, Password: `root`
2. Install **HeidiSQL**
3. Open HeidiSQL → New Session
   - Connect with `root/root`
   - Create database: `osTicket`

---

### Step 4: Configure IIS and Deploy osTicket

1. Open **IIS Manager as Admin**
2. Register PHP:
   - PHP Manager → `Register new PHP version` → `C:\PHP\php-cgi.exe`
   - Restart IIS
3. Unzip `osTicket-v1.15.8.zip`
   - Copy `upload` folder to `C:\inetpub\wwwroot`
   - Rename folder to `osTicket`
4. In IIS:
   - Navigate to `Sites > Default Web Site > osTicket`
   - Click `Browse *:80`
5. Enable PHP extensions:
   - `php_imap.dll`
   - `php_intl.dll`
   - `php_opcache.dll`
6. Rename config file:
   - `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php` → `ost-config.php`
7. Set Permissions:
   - Disable inheritance
   - Remove all existing permissions
   - Add `Everyone` → Full Control

---

### Step 5: Complete osTicket Setup

1. Visit: [http://localhost/osTicket](http://localhost/osTicket)
2. Fill in:
   - Helpdesk name
   - Default email
   - Admin account
   - MySQL info:
     - DB: `osTicket`
     - Username: `root`
     - Password: `root`
3. Click **Install Now!**
4. After successful install:
   - Delete: `C:\inetpub\wwwroot\osTicket\setup`
   - Set `ost-config.php` to **Read-only**

<img width="763" alt="image" src="[https://github.com/user-attachments/assets/d6097b14-f8bd-4758-8535-935fb4385eb0](https://imgur.com/a/yo3sx7x)" /> 
