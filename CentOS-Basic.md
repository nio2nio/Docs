### Install Software Update (Yum)
  * Proxy Configuration (**`/etc/yum.conf`**)
  ```shell
  proxy=http://ip:port
  ```
  * Install Epel (Extra Packages for Enterprise Linux 7)
  ```shell
  yum install epel-release
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
  * Add new user
  ```shell
  useradd new_user && passwd new_user
  usermod -aG wheel new_user
  ```
  * Configuration (**`/etc/pam.d/su`**)
  ```
  auth    required    pam_wheel.so use_uid (uncomment this line)
  ```
  * Configuration (**`/etc/sudoers`**) Or visudo
  ```shell
  %wheel  ALL=(ALL)   ALL (uncomment this line)
  ```

### Sudo (**`/etc/sudoers`**)
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
  * Show selinux status
  > **`enforcing`** - SELinux security policy is enforced.<br>
  > **`permissive`** - SELinux prints warnings instead of enforcing.<br>
  > **`disabled`** - No SELinux policy is loaded.
  ```shell
  # Show status
  getenforce
  ```
  * Configuration (**`/etc/selinux/config`**)
  ```shell
  SELinux=disabled
  ```
  * Reboot
  ```shell
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
  * SSH Daemon Options (**`/etc/ssh/sshd_config`**)
  ```shell
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
  * **`w`** 指令可以列出 Linux 系統上目前有哪些使用者登入，並且顯示每個使用者正在執行的指令
  
### Vim
  * Set Alias (**`/etc/profile`**)
  ```shell
  alias vi='vim'
  
  # Reload
  source /etc/profile
  ```
  * Configuration (**`~/.vimrc`**)
  ```shell
  set nocompatible

  set encoding=utf-8
  set fileencoding=utf-8
  set fileformats=unix,dos

  set backup
  set backupdir=~/backup
  set history=50

  set ignorecase
  # Highlights matched words
  set smartcase
  set hlsearch
  set incsearch

  set number
  # Highlights parentheses
  set showmatch

  # Show color display
  syntax on
  # Change colors for comments 
  highlight Comment ctermfg=LightCyan
  set wrap
  ```
  
### Zip
  * Installation
  ```shell
  yum install zip unzip
  ```
  * Zip
  ```shell
  # 壓縮目錄 (將data目錄下的所有檔案壓縮到file.zip，指令無須加上zip副檔名)
  zip file data/*
  # 將data目錄下所有檔案及子目錄壓縮到file.zip
  zip -r file data/*
  ```
  * Unzip
  ```shell
  # 將file.zip解壓縮到當前目錄
  unzip file.zip
  # 解壓縮檔內其中一個檔案
  unzip file.zip test.php
  # 解壓縮到指定目錄
  unzip file.zip -d /home/phpini
  ```
  
### Use Fail2Ban for SSH Login Protection

### FirewallD


