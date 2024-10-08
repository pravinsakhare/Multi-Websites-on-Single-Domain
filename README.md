# Hosting Multiple Websites on a Single AWS EC2 Instance Using Apache2

This document outlines the steps I followed to successfully host three distinct websites on a single AWS EC2 instance using Apache2.

## Prerequisites

- AWS account
- Basic knowledge of SSH and command line
- GitHub repository for managing the project code

### 1. Launch an EC2 Instance
- **Step 1:** Log in to your AWS Management Console and navigate to the EC2 Dashboard.
- **Step 2:** Launch a new EC2 instance using Ubuntu 20.04 (or your preferred OS).
- **Step 3:** Choose the instance type (e.g., t2.micro).
- **Step 4:** Configure security groups to allow HTTP (port 80) and the custom ports 8080, 8081, and 8082.
- **Step 5:** Download the key pair (.pem file) and launch the instance.

### 2. Connect to the EC2 Instance
- **Step 1:** Open your terminal and navigate to the directory containing your `.pem` file.
- **Step 2:** Use the following SSH command to connect to your instance:
  ```bash
  ssh -i "your-key.pem" ubuntu@your-ec2-public-ip'''

### Update Your System

```bash
sudo apt update && sudo apt upgrade -y
```
### 3. Install Apache Web Server

```bash
sudo apt install apache2 -y
```
### 4.Configure Apache to Listen on Multiple Ports
```bash
sudo nano /etc/apache2/ports.conf
```


![Screenshot (93)](https://github.com/user-attachments/assets/63c0b51b-9996-465b-b5fc-6110034662a0)



###4.	Add the following lines to make Apache listen on ports 8080, 8081, and 8082:
**•Listen 8080**
**•Listen 8081**
**•Listen 8082**

### 5.Set Up Virtual Hosts for Each Port
**•	Create 3 directories for your sites:**
```bash
sudo mkdir -p /var/www/site1/public_html
```bash
sudo mkdir -p /var/www/site2/public_html
```bash
sudo mkdir -p /var/www/site3/public_html
```

**•	Assign ownership to the www-data user:**
```bash
sudo chown -R www-data:www-data /var/www/site1/public_html
```
```bash
sudo chown -R www-data:www-data /var/www/site2/public_html
```
```bash
sudo chown -R www-data:www-data /var/www/site3/public_html
```
```bash
sudo nano /etc/apache2/sites-available/site1.conf
```
**Open nano editor and add this script for all three files just change virtualhost to 8081,8082 for other**
```
<VirtualHost *:8080>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/site1/public_html

    ErrorLog ${APACHE_LOG_DIR}/site1_error.log
    CustomLog ${APACHE_LOG_DIR}/site1_access.log combined

    <Directory /var/www/site1/public_html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```
![image](https://github.com/user-attachments/assets/4b687d9a-3df3-4da6-8681-86d72a3ed89e)

**Enable the sites:**
```bash
sudo a2ensite site1.conf
```
```bash
sudo a2ensite site2.conf
```
```bash
sudo a2ensite site3.conf
```
**sudo systemctl restart apache2**

### 6.	Configure the Security Group for inbound rules:

![Screenshot (96)](https://github.com/user-attachments/assets/e70ef66b-51c3-470b-9568-fb8a13d7e02a)


**.Create simple index.html file**

![Screenshot (93)](https://github.com/user-attachments/assets/56210555-3982-444c-bf00-47cdd506c895)

```bash
echo "<h1>Welcome to Site 1</h1>" | sudo tee /var/www/site1/public_html/index.html
```
```bash
echo "<h1>Welcome to Site 2</h1>" | sudo tee /var/www/site2/public_html/index.html
```
```bash
echo "<h1>Welcome to Site 3</h1>" | sudo tee /var/www/site3/public_html/index.html
```
### Udated Html Code (extra)
![image](https://github.com/user-attachments/assets/f1fe8915-7810-4007-a081-7f4ae96d6543)

### Launch your multiple websites using port public ip address & port numbers:

![Screenshot (102)](https://github.com/user-attachments/assets/e8554f32-2e61-4b01-af24-aa5ad8e3ba5b)

















 






