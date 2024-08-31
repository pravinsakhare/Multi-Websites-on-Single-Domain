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
```bash
sudo chown -R www-data:www-data /var/www/site2/public_html
```bash
sudo chown -R www-data:www-data /var/www/site3/public_html
```
```bash
sudo nano /etc/apache2/sites-available/site1.conf
```

 






