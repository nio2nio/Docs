### Install Software Update (Yum)
  * Proxy Configuration
  ```shell
  vi /etc/yum.conf
  proxy=http://ip:port
  ```
  * Epel (Extra Packages for Enterprise Linux 7)
  ```shell
  yum install -y epel-release
  ```
  
  * Cheat Sheet
  ```shell
  yum install package
  # 升級全部套件
  yum update
  yum update package
  # 升級全部套件及發行版本
  yum upgrade
  yum remove package
  yum clean (/var/cache/yum)
  
  # 查詢
  yum info package
  yum search keyword
  yum list package
  # 查詢所有可更新的套件
  yum list updates
  # 查詢所有已安裝的套件
  yum list installed
  # 查詢特定檔案存在於什麼套件之中
  yum provides 檔案名稱
  yum provides */檔案名稱
  yum resolvedep 檔案名稱
  
  # 套件組
  yum grouplist
  yum groupinstall "Group Name"
  yum groupupdate "Group Name"
  yum groupremove "Group Name"
  yum groupinfo "Group Name"
  
  # 當安裝套件時出現錯誤訊息:pkgKey xxx doesn't exist in repo base
  yum clean metadata
  ```
  
### Set the Hostname
```shell
sudo hostnamectl set-hostname host.example.com
```

### nmcli
  * Show device
  ```shell
  nmcli d
  ```
  * Set IPv4 Address
  ```shell
  nmcli c modify eth0 ipv4.addresses 10.0.0.30/24
  ```
  * Set default gateway
  ```shell
  nmcli c modify eth0 ipv4.gateway 10.0.0.1
  ```
  * Set DNS
  ```shell
  nmcli c modify eth0 ipv4.dns 10.0.0.1 
  ```
  * Set DHCP (auto) Or Static (manual)
  ```shell
  nmcli c modify eth0 ipv4.method manual
  ```
  * Reload configuration
  ```shell
  nmcli c down eth0; nmcli c up eth0 
  ```
  * Show configuration
  ```shell
  nmcli d show eth0 
  ```
  * Show status
  ```shell
  ip addr show
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

vi /etc/pam.d/su
auth    required    pam_wheel.so use_uid (uncomment this line)

# In CentOS 6 a wheel group is disabled by default for sudo access.
vi /etc/sudoers 
/usr/sbin/visudo
%wheel  ALL=(ALL)   ALL (uncomment this line)
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
  
### Bash History
  * bash 會將使用者執行過的歷史指令都儲存在 **`.bash_history`** 這個檔案中，由於 bash 並不會即時將新的指令寫入 .bash_history，所以這個只能查看使用者過去執行過的指令
  ```shell
  cat /home/user/.bash_profile
  ```
  * **`w`** 指令可以列出 Linux 系統上目前有哪些使用者登入，並且顯示每個使用者正在執行的指令
  
### Use Fail2Ban for SSH Login Protection

### FirewallD


