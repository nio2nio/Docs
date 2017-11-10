## Transfer root privilege to a user.
```shell
$ sudo vi /etc/sudoers
cent    ALL=(ALL)       ALL
```

## Restrict users to execute some commands
```shell
$ sudo vi /etc/sudoers
Cmnd_Alias SHUTDOWN = /sbin/halt, /sbin/shutdown, /sbin/poweroff, /sbin/reboot, /sbin/init

centALL=(ALL)ALL, !SHUTDOWN
```

## Transfer some commands with root privilege to users in a group.
```shell
$ sudo vi /etc/sudoers
Cmnd_Alias USERMGR = /usr/sbin/useradd, /usr/sbin/userdel, /usr/sbin/usermod, /usr/bin/passwd

%usermgr ALL=(ALL) USERMGR
```

## The logs for sudo are kept in '/var/log/secure', but there are many kind of logs in it. So if you'd like to keep only sudo's log in a file
```shell
$ sudo vi /etc/sudoers
# Add at the last line
Defaults syslog=local1

$ sudo vi /etc/rsyslog.conf
# line 54
*.info;mail.none;authpriv.none;cron.none;local1.none   /var/log/messages

# Add the line
local1.*  /var/log/sudo.log

# Restart Syslog Service
sudo systemctl restart rsyslog.service
```
