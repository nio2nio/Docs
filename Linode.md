### Install Software Update
```shell
sudo yum update -y
```
### Set the Hostname
```shell
sudo hostnamectl set-hostname host.example.com
```

### Set the Timezone
```shell
# View the list of available time zones
sudo timedatectl list-timezones

# Set the Timezone
sudo timedatectl set-timezone 'Asia/Taipei'

# Check the time
date
```

### Add Limited User Account
```shell
useradd new_user && passwd new_user
usermod -aG wheel new_user

# In CentOS 6 a wheel group is disabled by default for sudo access.
vi /etc/sudoers 
/usr/sbin/visudo

# uncomment this line
%wheel  ALL=(ALL)   ALL
```

### Sudo (/etc/sudoers)
  * Transfer root privilege to a user.
  ```shell
  cent    ALL=(ALL)       ALL
  ```
  * Restrict users to execute some commands
  ```shell
  Cmnd_Alias SHUTDOWN = /sbin/halt, /sbin/shutdown, /sbin/poweroff, /sbin/reboot, /sbin/init
  centALL=(ALL)ALL, !SHUTDOWN
  ```
  * Transfer some commands with root privilege to users in a group.
  ```shell
  Cmnd_Alias USERMGR = /usr/sbin/useradd, /usr/sbin/userdel, /usr/sbin/usermod, /usr/bin/passwd
  %usermgr ALL=(ALL) USERMGR
  ```
  * The logs for sudo are kept in '/var/log/secure', but there are many kind of logs in it. So if you'd like to keep only sudo's log in a file
  ```shell
  # /etc/sudoers 
  Defaults syslog=local1
  
  # /etc/rsyslog.conf 
  *.info;mail.none;authpriv.none;cron.none;local1.none   /var/log/messages (line:54)
  local1.*  /var/log/sudo.log (add this line)
  
  # Restart syslog service
  sudo systemctl restart rsyslog.service
  ```
  
### SELINUX
> **`enforcing`** - SELinux security policy is enforced.<br>
> **`permissive`** - SELinux prints warnings instead of enforcing.<br>
> **`disabled`** - No SELinux policy is loaded.
```shell
# Show status
getenforce

# Configure SELinux
sudo vi /etc/selinux/config
SELinux=disabled

# Reboot
reboot
```

### Harden SSH Access
  * Create an Authentication Key-pairPermalink (On your own device)
  ```shell
  ssh-keygen -b 4096 
  ```
  * Upload the public key to your Linode
  ```shell
  ssh-copy-id demo_user@xxx.xxx.xxx.xxx
  ```
  * Set permissions for the public key directory and the key file itself
  ```shell
  sudo chmod 700 -R ~/.ssh && chmod 600 ~/.ssh/authorized_keys
  ```
  * SSH Daemon Options
  ```shell
  sudo vi /etc/ssh/sshd_config
  # Custom Port
  Port 513113
  
  # 限制使用者登入
  AllowUsers userAccount1 userAccount2 ...
  
  # Disallow root logins over SSH
  PermitRootLogin no

  # Disable SSH password authentication
  PasswordAuthentication no

  # Listen on only one internet protocol
  AddressFamily inet/inet6/any
  ```
  * Restart the SSH service to load the new configuration.
  ```shell
  sudo systemctl restart sshd.service
  ```
  * Firewall Configuration
  ```shell
  sudo firewall-cmd --zone=public --add-port=51449/tcp --permanent
  ```
### Use Fail2Ban for SSH Login Protection

### FirewallD


