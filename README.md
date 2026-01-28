# Install and Configure GitLab on Ubuntu Server 24.04

This step-by-step tutorial explains how to install, configure, and secure GitLab Community Edition (CE) on Ubuntu Server 24.04.

## 1. Prerequisites
Ubuntu Server 24.04 LTS
A non-root user with sudo privilegesAt 
least:
* 4 GB RAM (8 GB recommended)
* 2 CPU cores
* 20 GB disk space (40+ GB recommended)

Check system:
```
lsb_release -a
free -h
df -h
```

## 2. Update the System
```
sudo apt update && sudo apt upgrade -y
sudo reboot
```

## 3. Set Hostname
```
sudo hostnamectl set-hostname gitlab
exec bash
```
Edit hosts file  **/etc/hosts** and add 
`127.0.0.1 gitlab.local`


## 4. Install Required Dependencies
`sudo apt install -y curl openssh-server ca-certificates tzdata perl`

Verify SSH service

```
sudo systemctl enable ssh
sudo systemctl start ssh
```
## 5. Configure Firewall
Enable firewall and allow required ports:
```
sudo ufw allow OpenSSH
sudo ufw allow http
sudo ufw allow https
sudo ufw enable
sudo ufw status
```

## 6. Install GitLab Repository
Add GitLab package repository:
``` 
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash 
```

## 7. Install GitLab Community Edition
Set your GitLab external URL before installation:
```  
sudo EXTERNAL_URL="http://gitlab.local" apt install gitlab-ce -y 
```

## 8. Initial GitLab Configuration
Reconfigure GitLab 
``` 
sudo gitlab-ctl reconfigure
```
Check GitLab status:
``` 
sudo gitlab-ctl status
```

![image](/uplodes/Gitlab-status.png)

##  9. Access GitLab Web Interface

Open your browse
``` 
http://gitlab.local/users/sign_in
```
![image](/uplodes/gitlab-inteface.png)


Default Admin User <br> 
**Username:** root <br> 
**Password:** cat /etc/gitlab/initial_root_password
![image](/uplodes/root-password.png)
