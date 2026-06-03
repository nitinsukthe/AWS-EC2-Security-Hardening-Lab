# Linux Hardening Commands

## Update System

```bash
sudo dnf update -y
```

## Create User

```bash
sudo adduser cloudadmin
```

## Add Sudo Privileges

```bash
sudo usermod -aG wheel cloudadmin
```

## SSH Hardening

```bash
sudo nano /etc/ssh/sshd_config
```

## Restart SSH

```bash
sudo systemctl restart sshd
```
