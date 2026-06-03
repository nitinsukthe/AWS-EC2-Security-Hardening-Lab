# Linux Hardening

## Update Packages

```bash
sudo dnf update -y
```

## Create User

```bash
sudo adduser cloudadmin
```

## Assign Sudo

```bash
sudo usermod -aG wheel cloudadmin
```
