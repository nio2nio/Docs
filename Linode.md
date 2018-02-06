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

### SELINUX
> enforcing - SELinux security policy is enforced.
> permissive - SELinux prints warnings instead of enforcing.
> disabled - No SELinux policy is loaded.


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


