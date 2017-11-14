### Install WebDAV Module
```shell
$ sudo httpd -M | grep fs
dav_fs_module (shared)
```

### Configure the WebDAV directory
```shell
$ sudo mkdir /var/www/html/webdav
$ sudo chown -R apache:apache /var/www/html/webdav
$ sudo chmod -R 755 /var/www/html/webdav
```

### Set up password authentication
```shell
$ sudo htpasswd -c /etc/httpd/.htpasswd dev
$ sudo chown root:apache /etc/httpd/.htpasswd
$ sudo chmod 640 /etc/httpd/.htpasswd
```

### Configure an Apache Virtual Host for WebDAV
```shell
$ sudo vi /etc/httpd/conf.d/webdav.conf
DavLockDB /var/www/html/DavLock
<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/html/webdav/
  ErrorLog /var/log/httpd/error.log
  CustomLog /var/log/httpd/access.log combined
  Alias /webdav /var/www/html/webdav
  <Directory /var/www/html/webdav>
    DAV On
    AuthType Basic
    AuthName "webdav"
    AuthUserFile /etc/httpd/.htpasswd
    Require valid-user
  </Directory>
</VirtualHost>

# restart httpd.service
$ sudo systemctl restart httpd.service
```

### Test WebDAV
```shell
$ sudo yum install -y cadaver
$ cadaver http://your.ip/webdav
```
