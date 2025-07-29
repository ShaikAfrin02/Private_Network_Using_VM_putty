**📌 Project Overview**

This mini project demonstrates how to set up a private network using VirtualBox VMs, PuTTY for SSH, and configure communication between a web server and a database server using NAT and Bridged Networking.

It also includes a simple PHP-based web form hosted on the web server that collects user data and uploads files, storing the information into a MySQL database hosted on the DB server.

**⚙️ Tools & Technologies Used**

VirtualBox (VM creation)

PuTTY (SSH Client)

Apache2 (Web Server)

MySQL Server

PHP

NAT and Bridged Networking (VirtualBox)

Ubuntu Linux OS (on VMs)

**🏗️ Network Setup**
Created two Virtual Machines (Ubuntu OS):

Web Server VM

DB Server VM (cloned from webserver)

Network Configurations:

NAT Adapter: For internet access inside VM.

Bridged Adapter: For private IP communication between VMs.

Configured static IPs like:

Web Server: 192.168.30.10

DB Server: 192.168.30.5

SSH Access:

Used PuTTY to connect from host machine to VMs via private IPs.

**🖥️ Web Server Setup**
Installed Apache2, PHP, and necessary modules.

Hosted a user_data_form.php page in /var/www/html/.

Created an uploads directory:

bash
Copy
Edit
sudo mkdir -p /var/udc/uploads
sudo chmod -R 777 /var/udc/uploads

**🗄️ Database Server Setup**
Installed MySQL Server.

Created a database named udc:

sql
Copy
Edit
CREATE DATABASE udc;
USE udc;
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    age INT,
    country VARCHAR(255)
);
Created a MySQL user:

sql
Copy
Edit
CREATE USER 'udc123'@'%' IDENTIFIED BY 'Root@123';
GRANT ALL PRIVILEGES ON udc.* TO 'udc123';
FLUSH PRIVILEGES;

**💡 PHP Web Page Functionality**
The web form accepts:

User Name

Age

Country

File Upload (e.g., image or document)

On form submission:

User data is inserted into the MySQL users table.

The file is uploaded to the /var/udc/uploads/ directory on the web server.

PHP Code (Hosted on Web Server):

php
Copy
Edit
$servername = "192.168.30.5"; 
$username = "udc123"; 
$password ="Root@123"; 
$dbname = "udc";
$conn = new mysqli($servername, $username, $password, $dbname);
...


Data saved in MySQL udc.users

File saved to /var/udc/uploads/

Success message displayed on the browser.

**📚 Learnings & Takeaways**
Virtual networking using NAT + Bridged Adapter

Web-DB communication across VMs

PHP-MySQL integration

File handling in PHP

Use of SSH tools like PuTTY

VM cloning and port configuration

**📁 How to Run (Quick Steps)**
Clone the repo.

Start your VirtualBox VMs.

Place the user_data_form.php in /var/www/html/.

Open the page from browser via http://<web-server-ip>/user_data_form.php

Fill form and submit.
