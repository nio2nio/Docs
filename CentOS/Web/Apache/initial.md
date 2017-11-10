### Installation
```shell
$ sudo yum install httpd

# Remove welcome page
$ sudo rm -fr /etc/httpd/conf.d/welcome.conf

# Start httpd service
$ sudo systemctl start httpd.service
$ sudo systemctl enable httpd.service
```

### Configure httpd
```shell
$ sudo vi /etc/httpd/conf/httpd.conf
ServerAdmin root@your.domain
ServerName your.domain:80

<Directory "/var/www/html">
  AllowOverride All
  ...
</Directory />

<IfModule dir_module>
  DirectoryIndex index.html index.cgi index.php
</IfModule>

ServerTokens Prod
KeepAlive On

# Restart httpd service
$ sudo systemctl restart httpd.service
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

### Create test page
```shell
$ sudo vi /var/www/html/index.html
<html>
  <body>
    <div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">
      Test Page
    </div>
  </body>
</html>
```
