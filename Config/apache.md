### Installation
```shell
$ sudo yum install httpd
$ sudo systemctl start httpd.service
$ sudo systemctl enable httpd.service
```

### Configure Firewall
```shell
sudo firewall-cmd --zone=public --permanent --add-service=http ex:Service Name
sudo firewall-cmd --zone=public --permanent --add-port=5432/tcp ex:Port/Protocol (TCP/UDP)
sudo firewall-cmd --reload
```

### SELinux
```shell
sudo setsebool -P httpd_can_network_connect on
sudo setsebool -P httpd_can_network_connect_db on
```
