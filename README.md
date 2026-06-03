# AWS EC2 Security Hardening & Monitoring Lab

## Project Overview

This project demonstrates a hands-on **Cloud Security implementation on AWS** by deploying, securing, hardening, and monitoring an EC2 instance.

The lab follows industry security best practices including:

- Secure EC2 deployment
- Security Group hardening
- SSH key-based authentication
- Linux server hardening
- Least Privilege Access Control
- SSH configuration hardening
- CloudWatch monitoring & alerting

This project was completed as a practical cloud security portfolio project using **AWS Free Tier services**.

---

# Architecture Overview

```plaintext
Local Machine
      │
      │ SSH Key Authentication
      ▼
AWS EC2 Instance (Amazon Linux 2023)
      │
      ├── Security Group (My IP only)
      ├── SSH Hardening
      ├── Linux User Privilege Management
      └── CloudWatch Monitoring + SNS Alerts
```

---

# Technologies Used

| Technology | Purpose |
|------------|----------|
| AWS EC2 | Cloud Compute Instance |
| Amazon Linux 2023 | Server Operating System |
| Security Groups | Network Access Control |
| SSH | Secure Remote Access |
| Linux Administration | System Hardening |
| AWS CloudWatch | Monitoring & Alerting |
| SNS | Email Notifications |

---

# Project Workflow

---

## 1. Launch Secure EC2 Instance

Configured an AWS EC2 instance using **Amazon Linux 2023** and **t3.micro Free Tier**.

### Configuration:

- Region: Mumbai (`ap-south-1`)
- Instance Type: `t3.micro`
- Key Pair Authentication
- Secure Network Configuration

### Screenshot

![Launch EC2](screenshots/1.Launch%20EC2%20Instance.png)

---

## 2. Configure Security Group Rules

Implemented restrictive network controls using AWS Security Groups.

### Security Rule:

| Type | Port | Source |
|------|------|------|
| SSH | 22 | My IP Only |

This reduces unauthorized remote access exposure.

### Screenshot

![Security Group Rules](screenshots/8.Security%20Group%20rules.png)

---

## 3. Verify Running EC2 Deployment

Confirmed successful instance deployment and operational status.

### Screenshot

![EC2 Running Instance](screenshots/11.EC2%20Dashboard%20showing%20Instance%20running.png)

---

## 4. Secure SSH Access

Connected securely to EC2 using downloaded private key authentication.

### Command Used

```bash
ssh -i cloud-key.pem ec2-user@PUBLIC-IP
```

### Screenshot

![SSH Login](screenshots/14.Successful%20Login%20and%20.png)

---

## 5. Linux Security Hardening

Applied Linux hardening controls to strengthen server security posture.

### Actions Performed

- Updated packages
- Created dedicated admin user
- Configured sudo privileges
- Applied access control separation

### Commands Used

```bash
sudo dnf update -y
sudo adduser cloudadmin
sudo passwd cloudadmin
sudo usermod -aG wheel cloudadmin
```

### Screenshot

![Create Security User](screenshots/17.Create%20New%20Security%20User.png)

---

## 6. SSH Hardening Configuration

Configured secure SSH settings to reduce attack surface.

### Security Controls Applied

```plaintext
PermitRootLogin no
PasswordAuthentication no
MaxAuthTries 3
X11Forwarding no
```

### Validation Command

```bash
sudo grep -E "PermitRootLogin|PasswordAuthentication|MaxAuthTries|X11Forwarding" /etc/ssh/sshd_config
```

### Screenshot

![SSH Configuration Verification](screenshots/28.Verify%20Configuration.png)

---

## 7. CloudWatch Monitoring & Alerting

Configured AWS CloudWatch monitoring for proactive infrastructure visibility.

### Monitoring Configuration

- Metric: CPUUtilization
- Threshold: >80%
- SNS Email Notification
- Alarm Status Monitoring

### Screenshot

![Create Alarm](screenshots/31.Create%20Alarm-%20Select%20Metric.png)


---

## 8. CloudWatch Alarm Status

Validated successful alarm deployment and monitoring configuration.

### Screenshot

![Alarm State](screenshots/36.Alarm%20State%20OK.png)

---

# Security Controls Implemented

## Identity & Access Management

- SSH Key Authentication
- Separate Administrative User
- Sudo Privilege Management
- Principle of Least Privilege

## Network Security

- Security Group Hardening
- SSH Restricted to Trusted IP

## Host Security

- Linux Package Updates
- SSH Configuration Hardening
- Root Login Disabled
- Password Authentication Disabled

## Monitoring & Detection

- CloudWatch Metrics
- Alarm Threshold Configuration
- SNS Email Notifications

---

# Key Commands Used

## Update Server

```bash
sudo dnf update -y
```

## Create User

```bash
sudo adduser cloudadmin
```

## Add Admin Privileges

```bash
sudo usermod -aG wheel cloudadmin
```

## Edit SSH Config

```bash
sudo nano /etc/ssh/sshd_config
```

## Restart SSH Service

```bash
sudo systemctl restart sshd
```

---

# Lessons Learned

Through this project I gained practical experience with:

- AWS EC2 deployment
- Cloud infrastructure security
- Linux server administration
- SSH hardening
- Network access control
- Cloud monitoring & alerting
- Security best practices in AWS environments

---

# Future Improvements

Potential enhancements for this project:

- IAM Role Implementation
- AWS GuardDuty Integration
- AWS Config Compliance Rules
- AWS CloudTrail Logging
- Automated Infrastructure using Terraform
- Vulnerability Scanning Integration

---

## Author

**Nitin Sukthe**

Cloud Security | AWS | Linux Security | AI Security
