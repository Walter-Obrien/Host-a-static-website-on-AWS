---

# Host a Static Website on AWS

This project demonstrates how to host a static HTML web application on AWS, utilizing various AWS services to ensure high availability, security, and scalability. The project architecture involves deploying a static website on EC2 instances within a Virtual Private Cloud (VPC), with enhanced fault tolerance and security measures.

## Project Architecture

The following AWS resources were configured and used in this project:

1. **Virtual Private Cloud (VPC):**
   - Configured a VPC with both public and private subnets across two different availability zones for redundancy and high availability.

2. **Internet Gateway:**
   - Deployed an Internet Gateway to enable connectivity between the VPC and the wider Internet.

3. **Security Groups:**
   - Established Security Groups as a network firewall to control inbound and outbound traffic to and from the EC2 instances.

4. **Availability Zones:**
   - Utilized two Availability Zones to enhance system reliability and fault tolerance.

5. **Public Subnets:**
   - Deployed infrastructure components like the NAT Gateway and Application Load Balancer in public subnets.

6. **EC2 Instance Connect Endpoint:**
   - Implemented an EC2 Instance Connect Endpoint for secure connections to assets within both public and private subnets.

7. **Private Subnets:**
   - Positioned web servers (EC2 instances) within private subnets for enhanced security.

8. **NAT Gateway:**
   - Enabled instances in the private application and data subnets to access the Internet via the NAT Gateway.

9. **EC2 Instances:**
   - Hosted the website on EC2 instances deployed in private subnets.

10. **Application Load Balancer:**
    - Employed an Application Load Balancer to evenly distribute web traffic to an Auto Scaling Group of EC2 instances across multiple Availability Zones.

11. **Auto Scaling Group:**
    - Utilized an Auto Scaling Group to automatically manage EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.

12. **Version Control:**
    - Stored web files on GitHub for version control and collaboration.

13. **Certificate Manager:**
    - Secured application communications using AWS Certificate Manager.

14. **Simple Notification Service (SNS):**
    - Configured SNS to send alerts about activities within the Auto Scaling Group.

15. **Route 53:**
    - Registered the domain name and set up a DNS record using Route 53.

## Prerequisites
Before deploying the web application, ensure you have:
  - An AWS account with necessary permissions to create and manage the resources mentioned.
  - A registered domain name.
  - Git installed on your local machine for version control.

## Deployment

1. **Clone the GitHub Repository**
   
```bash
git clone https://github.com/Walter-Obrien/Host-a-static-website-on-AWS.git
```

2. **Deploy the Web Application**
Use the following bash script to set up the web server and deploy the web application on an EC2 instance:

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/Walter-Obrien/Host-a-static-website-on-AWS.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R Host-a-static-website-on-AWS/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf Host-a-static-website-on-AWS

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

3. **Configure DNS**
  - Use Route 53 to create a DNS record for your domain, pointing to the Application Load Balancer.

5. **Monitor and Scale**
  - Monitor the Auto Scaling Group via the AWS Management Console.
  - Adjust scaling policies if necessary to handle varying traffic loads.

## Repository Link
The project is available on GitHub: [Host a Static Website on AWS](https://github.com/Walter-Obrien/Host-a-static-website-on-AWS.git)

## Security
  - The web servers are hosted in private subnets to minimize exposure to the Internet.
  - SSL/TLS is configured using AWS Certificate Manager to secure the website.

## Monitoring and Alerts
  - AWS SNS is set up to send notifications regarding scaling events and other critical activities.

## Conclusion
This project outlines the steps required to host a static website on AWS, utilizing a variety of AWS services to ensure the solution is secure, scalable, and highly available. The architecture is designed to support production-grade static websites with minimal maintenance and high reliability.

---
