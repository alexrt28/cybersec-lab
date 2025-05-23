# ⚙️ DVWA + LAMP Stack Setup

This section documents how I set up the LAMP stack (Linux, Apache, MySQL, PHP) and deployed DVWA (Damn Vulnerable Web App) on my Ubuntu Server VM.
---

##  Summary of This Setup

✅ LAMP stack installed successfully  
✅ DVWA downloaded, configured, and permissioned  
✅ MySQL database and user created  
✅ Apache port changed from 80 to 8080  
✅ DVWA setup complete and working in browser

---

##  Step 1: Update System Packages

```bash
# Update and upgrade system packages
sudo apt update && sudo apt upgrade -y

```

## Step 2: Install Apache, PHP, and MySQL server
```bash
sudo apt install -y apache2 php php-mysql mysql-server

```


## Step 3: DVWA to Apache Web Directory
```
# Change to the Apache web root directory
cd /var/www/html

# Clone the DVWA GitHub repo
sudo git clone https://github.com/digininja/DVWA.git
```

## Step 4: Set Permissions for DVWA
```
sudo chown -R www-data:www-data DVWA
sudo chmod -R 755 DVWA
```

## Step 5: Configure DVWA Database Credentials
```
# Edit the DVWA config file
sudo nano /var/www/html/DVWA/config/config.inc.php
```
![Image](https://github.com/user-attachments/assets/46ea19c9-7b1e-416c-b90d-f436b6ba0bf4)

##  Step 6: Create DVWA Database and User in MySQL
```
# Log into MySQL as root
sudo mysql -u root -p
# SQL commands to run inside MySQL:
CREATE DATABASE dvwa;
CREATE USER 'dvwa_user'@'localhost' IDENTIFIED BY 'p@ssw0rd';
GRANT ALL ON dvwa.* TO 'dvwa_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## Step 7: Fix DVWA Access by Changing Apache Port
```
#Tried to access DVWA using port 80
http://<ubuntu-ip>/DVWA/setup.php

# ❌ This didn’t work — page didn’t load
# Change Apache port in ports.conf
sudo nano /etc/apache2/ports.conf

# Change:
Listen 80
# To:
Listen 8080
# Update virtual host file
sudo nano /etc/apache2/sites-available/000-default.conf

# Change:
 <VirtualHost *:80>
# To:
 <VirtualHost *:8080>
# Restart Apache
sudo systemctl restart apache2
```
![Image](https://github.com/user-attachments/assets/26930fb5-2c77-4ad8-8446-c1bc2b17a3a4)

## Step 9: Access and Initialize DVWA
```
# Access DVWA via browser on port 8080
http://localhost:8080/DVWA/setup.php
# OR
http://<your-ubuntu-ip>:8080/DVWA/setup.php
```
![Image](https://github.com/user-attachments/assets/7e0c5fbd-2c78-43c1-a7d3-62bad81ed10d)
```bash
#Select Setup DVWA and Click Create/Reset Database
#Login page appears automatically/ if not click login link that appears.
```
![Image](https://github.com/user-attachments/assets/789b87b7-ef97-48cd-a21e-3e7fec849f8e)
```
Login to DVWA using default username and password.
```
![Image](https://github.com/user-attachments/assets/a2a6772d-a826-49f5-9d39-e351dd240f5a)




