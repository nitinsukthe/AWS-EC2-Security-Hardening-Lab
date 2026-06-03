# AWS EC2 Security Hardening & Monitoring Lab

![AWS](https://img.shields.io/badge/AWS-Cloud%20Security-orange)
![Linux](https://img.shields.io/badge/Linux-Security-blue)
![CloudWatch](https://img.shields.io/badge/CloudWatch-Monitoring-red)


---

# Project Overview

This project demonstrates a practical **Cloud Security implementation on AWS** focused on deploying, securing, hardening, and monitoring an Amazon EC2 instance.

The lab follows real-world cloud security practices including:

- Secure AWS EC2 deployment
- Security Group hardening
- SSH Key Authentication
- Linux Server Hardening
- SSH Security Configuration
- Least Privilege Access Control
- CloudWatch Monitoring & Alerting

The project was built using AWS Free Tier services and documented as a professional cloud security portfolio project.

---

# Project Objectives

The goal of this project was to:

✔ Deploy a secure AWS EC2 environment

✔ Configure restrictive network access policies

✔ Implement secure SSH authentication

✔ Harden Linux server configuration

✔ Configure monitoring & alerting

✔ Demonstrate foundational cloud security skills

---

# Architecture Overview

```plaintext
Local Machine
     │
     │ SSH Key Authentication
     ▼
AWS EC2 Instance (Amazon Linux 2023)
     │
     ├── Security Group Hardening
     │      └── SSH Restricted To My IP
     │
     ├── Linux Hardening
     │      ├── Package Updates
     │      ├── Admin User Creation
     │      └── Least Privilege Access
     │
     ├── SSH Security Hardening
     │      ├── Root Login Disabled
     │      ├── Password Login Disabled
     │      └── MaxAuthTries Configured
     │
     └── CloudWatch Monitoring
            └── SNS Email Alerts
```

---

# Technologies Used

| Technology | Purpose |
|------------|----------|
| AWS EC2 | Cloud Compute |
| Amazon Linux 2023 | Server Operating System |
| Security Groups | Network Access Control |
| SSH | Secure Remote Access |
| Linux Administration | Host Hardening |
| CloudWatch | Monitoring |
| SNS | Alert Notifications |

---

# Implementation Walkthrough

---

# Exercise 1 — Launch Secure AWS EC2 Instance

The first stage of the project involved deploying a secure EC2 instance inside AWS.

## Configuration Used

| Setting | Value |
|----------|--------|
| Region | ap-south-1 (Mumbai) |
| OS | Amazon Linux 2023 |
| Instance Type | t3.micro |
| Authentication | SSH Key Pair |
| Storage | Default |

The EC2 instance was launched using AWS Console and configured using Free Tier eligible resources.

---

## Step 1 — Launch EC2 Instance

Opened AWS EC2 Dashboard and initiated secure instance deployment.

### Screenshot

![Launch EC2](screenshots/1.Launch%20EC2%20Instance.png)
![Launch EC2](screenshots/2.Choose%20Instance%20OS.png)
![Launch EC2](screenshots/3.Choose%20Instance%20type.png)
![Launch EC2](screenshots/4.Create%new%20Key%20pair.png)
![Launch EC2](screenshots/5.Save%20Safe%20cloud-%20key%20file.png)


---

## Step 2 — Configure Security Group Rules

Security Groups were configured using the principle of **minimum exposure**.

SSH access was restricted using:

| Protocol | Port | Source |
|----------|------|---------|
| SSH | 22 | My IP Only |

This reduces unauthorized remote access attempts.

### Screenshot

![Security Group Rules](screenshots/02-security-group-rules.png)

---

## Step 3 — Verify EC2 Deployment

After launch completion, the instance status was verified.

Expected result:

- Running state
- Health checks passed
- Public IPv4 assigned

### Screenshot

![EC2 Running](screenshots/03-ec2-running.png)

---

# Exercise 2 — Connect Securely To EC2

SSH key authentication was used to establish secure remote access.

---

## SSH Command Used

```bash
ssh -i cloud-key.pem ec2-user@PUBLIC-IP
```

Windows PowerShell and Linux terminal both support this connection method.

---

## Successful Authentication

Connection to the EC2 server verified successful deployment and key-based access.

### Screenshot

![SSH Login](screenshots/04-successful-ssh-login.png)

---

# Exercise 3 — Linux Security Hardening

After successful login, Linux hardening procedures were applied.

---

## Update System Packages

Security updates were installed to ensure the operating system contained the latest patches.

### Command

```bash
sudo dnf update -y
```

---

## Create Dedicated Administrative User

A separate administrative account was created.

### Commands

```bash
sudo adduser cloudadmin
sudo passwd cloudadmin
sudo usermod -aG wheel cloudadmin
```

This follows **Least Privilege Access Control** practices.

### Screenshot

![Create Security User](screenshots/05-create-security-user.png)

---

# SSH Security Hardening

SSH configuration was hardened to reduce brute-force and credential-based attacks.

---

## Secure SSH Configuration

The SSH daemon configuration file was modified:

### File

```bash
sudo nano /etc/ssh/sshd_config
```

### Security Controls Applied

```plaintext
PermitRootLogin no
PasswordAuthentication no
MaxAuthTries 3
X11Forwarding no
```

---

## Restart SSH Service

```bash
sudo systemctl restart sshd
```

---

## Validate Configuration

```bash
sudo grep -E "PermitRootLogin|PasswordAuthentication|MaxAuthTries|X11Forwarding" /etc/ssh/sshd_config
```

### Screenshot

![SSH Verification](screenshots/06-ssh-config-verification.png)

---

# Exercise 4 — Configure Security Group Firewall Controls

AWS Security Groups functioned as the cloud firewall layer.

Firewall controls were reviewed to ensure:

- SSH restricted to trusted IP
- No unrestricted inbound exposure
- Controlled access policy enforced

These settings align with cloud network security best practices.

---

# Exercise 5 — Configure CloudWatch Monitoring

AWS CloudWatch monitoring was configured to provide infrastructure visibility and alerting.

---

## Alarm Configuration

Metric selected:

```plaintext
EC2 → CPUUtilization
```

Threshold configured:

```plaintext
CPU > 80%
```

SNS email notifications were enabled for alert delivery.

---

## Create Monitoring Alarm

### Screenshot

![CloudWatch Metric](screenshots/07-cloudwatch-alarm-metric.png)

---

## Alarm Status Validation

Successful monitoring deployment verified.

### Screenshot

![Alarm Status](screenshots/08-cloudwatch-alarm-ok.png)

---
# Security Controls Implemented

This project applied multiple layers of cloud security controls across infrastructure, host security, access management, and monitoring.

---

## Identity & Access Security

Implemented controls:

✔ SSH Key Authentication

✔ Dedicated Administrative User

✔ Least Privilege Access Control

✔ Sudo Privilege Management

---

## Network Security

Configured AWS Security Groups to reduce attack exposure.

Controls implemented:

✔ SSH restricted to trusted IP

✔ No unrestricted inbound SSH exposure

✔ Controlled firewall configuration

---

## Host Security

Linux server hardening controls applied:

✔ System Package Updates

✔ Root Login Disabled

✔ Password Authentication Disabled

✔ SSH Configuration Hardening

✔ Brute Force Risk Reduction

---

## Monitoring & Detection

Monitoring visibility established using AWS CloudWatch.

Implemented:

✔ CPU Utilization Monitoring

✔ CloudWatch Alarm Configuration

✔ SNS Email Notifications

✔ Alerting Workflow

---

# Key Commands Used

## Update Linux Packages

```bash
sudo dnf update -y
```

---

## Create Administrative User

```bash
sudo adduser cloudadmin
```

---

## Assign Administrative Privileges

```bash
sudo usermod -aG wheel cloudadmin
```

---

## Edit SSH Configuration

```bash
sudo nano /etc/ssh/sshd_config
```

---

## Restart SSH Service

```bash
sudo systemctl restart sshd
```

---

## SSH Connection Command

```bash
ssh -i cloud-key.pem ec2-user@PUBLIC-IP
```

---

# Lessons Learned

Through this project I gained practical experience in:

- AWS EC2 deployment
- Cloud infrastructure security
- Linux administration
- Security Group management
- SSH hardening
- Least privilege access control
- CloudWatch monitoring
- Security alerting workflows

---

# Future Improvements

Potential improvements for future iterations:

- AWS IAM Policies & Roles
- CloudTrail Logging
- AWS GuardDuty Integration
- AWS Config Compliance Rules
- Terraform Infrastructure Automation
- Vulnerability Scanning Integration

---


# Conclusion

This project demonstrates foundational cloud security skills including AWS infrastructure deployment, Linux security hardening, access control management, cloud monitoring, and security best practices.

The implementation reflects practical security engineering concepts used in cloud environments and serves as a portfolio-ready cloud security project.

---

# Author

**Nitin Sukthe**

Cloud Security | AWS | Linux Security | AI Security
