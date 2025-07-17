# MarketPeak E-Commerce Platform Deployment

## Project Overview

This project demonstrates the complete deployment workflow of an e-commerce platform called "MarketPeak" using Git for version control, Linux environment for development, and AWS EC2 for cloud deployment. The platform features product listings, shopping cart functionality, and user authentication.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Step-by-Step Implementation](#step-by-step-implementation)
- [Deployment Architecture](#deployment-architecture)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)
- [Conclusion](#conclusion)

## Prerequisites

- AWS Account with EC2 access
- GitHub account
- Basic knowledge of Git, Linux commands, and web technologies
- SSH client for connecting to EC2 instance

## Project Structure

```
MarketPeak_Ecommerce/
├── README.md
├── index.html
├── css/
├── js/
├── images/
└── fonts/
```

## Step-by-Step Implementation

### 1. Version Control Setup with Git

#### 1.1 Initialize Local Git Repository

```bash
# Create project directory
mkdir MarketPeak_Ecommerce
cd MarketPeak_Ecommerce

# Initialize Git repository
git init
```

#### 1.2 Obtain E-Commerce Website Template

1. **Template Selection**: Downloaded a suitable e-commerce template from Tooplate
2. **Template Preparation**: Extracted the template files into the project directory
3. **Customization**: Made minor adjustments to fit the "MarketPeak" branding

#### 1.3 Stage and Commit Initial Code

```bash
# Configure Git user information
git config --global user.name "olugbedu"
git config --global user.email "adedejiolugbedu@gmail.com"

# Add files to staging area
git add .

# Initial commit
git commit -m "Initial commit with basic e-commerce site structure"
```

#### 1.4 Push to GitHub Repository

```bash
# Create remote repository connection
git remote add origin https://github.com/olugbedu/MarketPeak_Ecommerce.git

# Push code to GitHub
git push -u origin main
```

### 2. AWS EC2 Deployment

#### 2.1 EC2 Instance Setup

1. **Launch Instance**: Created Amazon Linux AMI EC2 instance
2. **Security Group**: Configured to allow HTTP (port 80) and SSH (port 22) traffic
3. **Key Pair**: Generated and downloaded key pair for SSH access
4. **Connection**: Connected to instance via SSH

```bash
ssh -i "MarketPeak_Ecommerce-key" ec2-user@18.118.109.77
```

#### 2.2 Clone Repository on Linux Server

**SSH Method Implementation:**

```bash
# Generate SSH key pair
ssh-keygen -t rsa -b 4096 -C "adedejiolugbedu@gmail.com"

# Display public key
cat ~/.ssh/MarketPeak_Ecommerce-git.pub

# Clone repository using SSH
git clone git@github.com:olugbedu/MarketPeak_Ecommerce.git
```

**Alternative HTTPS Method:**

```bash
# Clone using HTTPS
git clone https://github.com/olugbedu/MarketPeak_Ecommerce.git
```

#### 2.3 Web Server Installation

```bash
# Update system packages
sudo yum update -y

# Install Apache HTTP Server
sudo yum install httpd -y

# Start and enable Apache service
sudo systemctl start httpd
sudo systemctl enable httpd

# Verify service status
sudo systemctl status httpd
```

#### 2.4 Configure Apache for Website

```bash
# Clear default Apache directory
sudo rm -rf /var/www/html/*

# Copy website files to Apache directory
sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/

# Set proper permissions
sudo chown -R apache:apache /var/www/html/
sudo chmod -R 755 /var/www/html/

# Reload Apache service
sudo systemctl reload httpd
```

#### 2.5 Access and Verify Deployment

- Accessed website using EC2 public IP
- Verified all pages load correctly
- Tested responsive design and functionality

### 3. Continuous Integration and Deployment Workflow

#### 3.1 Development Branch Workflow

```bash
# Create and switch to development branch
git branch development
git checkout development

# Make changes and improvements
# ... (edit files) ...

# Stage changes
git add .

# Commit changes
git commit -m "Add new features or fix bugs"

# Push development branch
git push origin development
```

#### 3.2 Pull Request and Merging Process

1. **Create Pull Request**: Created PR on GitHub from development to main branch
2. **Code Review**: Reviewed changes for quality and functionality
3. **Merge Process**:

```bash
# Switch to main branch
git checkout main

# Merge development branch
git merge development

# Push merged changes
git push origin main
```

#### 3.3 Production Deployment

```bash
# SSH into production server
ssh -i "MarketPeak_Ecommerce-key" ec2-user@18.118.109.77

# Navigate to website directory
cd /var/www/html/

# Pull latest changes
git pull origin main

# Restart web server if needed
sudo systemctl reload httpd
```

#### 3.4 Testing and Validation

- Verified new features work in production environment
- Tested website responsiveness and functionality
- Confirmed all links and forms work correctly

## Deployment Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Developer     │    │     GitHub      │    │   AWS EC2       │
│   Local Env     │───▶│   Repository    │───▶│   Production    │
│                 │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
        │                        │                        │
        │                        │                        │
        ▼                        ▼                        ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Git Version   │    │   Code Storage  │    │   Apache Web    │
│   Control       │    │   & Backup      │    │   Server        │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## Troubleshooting

### Common Issues and Solutions

#### 1. SSH Connection Issues
```bash
# Fix key permissions
chmod 400 your-key.pem

# Verify security group settings allow SSH (port 22)
```

#### 2. Apache Service Issues
```bash
# Check Apache status
sudo systemctl status httpd

# View error logs
sudo tail -f /var/log/httpd/error_log
```

#### 3. File Permission Problems
```bash
# Fix ownership and permissions
sudo chown -R apache:apache /var/www/html/
sudo chmod -R 755 /var/www/html/
```

#### 4. Git Authentication Issues
```bash
# For HTTPS, use personal access token
# For SSH, ensure key is added to GitHub account
ssh -T git@github.com
```

## Best Practices Implemented

### 1. Version Control
- Used descriptive commit messages
- Implemented branch-based development workflow
- Regular commits with logical changes

### 2. Security
- Configured proper security groups
- Used SSH keys for secure authentication
- Set appropriate file permissions

### 3. Deployment
- Automated deployment process
- Implemented CI/CD workflow
- Regular testing and validation

### 4. Documentation
- Comprehensive README documentation
- Clear step-by-step instructions
- Troubleshooting guides

## Key Learnings

1. **Git Workflow**: Mastered branch management and collaborative development
2. **Linux Administration**: Gained experience with system administration tasks
3. **Cloud Deployment**: Understood AWS EC2 deployment and configuration
4. **Web Server Management**: Learned Apache configuration and management
5. **CI/CD Implementation**: Implemented automated deployment workflow

## Future Enhancements

- Implement HTTPS with SSL certificates
- Add database integration for dynamic content
- Set up monitoring and logging
- Implement automated testing
- Add load balancing for scalability

## Conclusion

This project successfully demonstrated the complete deployment lifecycle of an e-commerce platform using modern DevOps practices. The implementation covers:

- ✅ Version control with Git and GitHub
- ✅ Linux server administration
- ✅ AWS EC2 cloud deployment
- ✅ Apache web server configuration
- ✅ Continuous integration and deployment workflow
- ✅ Production environment management

The MarketPeak e-commerce platform is now successfully deployed and accessible via the AWS EC2 public IP address, with a robust workflow for future updates and maintenance.

---

**Project Repository**: [MarketPeak_Ecommerce](https://github.com/olugbedu/MarketPeak_Ecommerce)
