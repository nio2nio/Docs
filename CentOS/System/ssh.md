### Installation
```shell
$ sudo yum install sshd*
```

### Configuration
```shell
$ sudo vi /etc/ssh/sshd_config
# Change Port
Port 51449
# 限制使用者登入
AllowUsers userAccount1 userAccount2 ...
# 取消root登入
PermitRootLogin no
```
