### 服務
```shell
# Start service
$ sudo systemctl start firewalld.service

# Stop service
$ sudo systemctl stop firewalld.service

# Restart service
$ sudo systemctl restart firewalld.service

# Status
$ sudo systemctl status firewalld.service

# 開機啟動
$ sudo systemctl enable firewalld.service

# 移除服務
$ sudo systemctl disable firewalld.service
```

### 常用指令
```shell
# Reload
$ sudo firewall-cmd --reload

# 查看永久的設定
$ sudo firewall-cmd --zone=public --list-all --permanent

# 查看此 zone 所開的服務
$ sudo firewall-cmd --zone=public --list-all

# 查看 zone
$ sudo firewall-cmd --get-default-zone

# 在 加入 public zone 的 80 TCP 端口
$ sudo firewall-cmd --zone=public (--permanent) --add-port=80/tcp

# 在 刪除 public zone 的 80 端口
$ sudo firewall-cmd --zone=public (--permanent) --remove-port=80/tcp

# 加入可通過的 IP
$ sudo firewall-cmd --zone=public --add-source=192.168.1.1/24

# 移除可通過的 IP
$ sudo firewall-cmd --zone-public --remove-source=192.168.1.1/24
```
