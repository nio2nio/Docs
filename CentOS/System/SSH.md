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
# Restart SSH Service
$ sudo systemctl restart sshd.service
# 設定開機啟動
$ sudo systemctl enable sshd.service
# 開啟防火牆
$ sudo firewall-cmd --permanent --zone=public --add-port=51449/tcp
```
