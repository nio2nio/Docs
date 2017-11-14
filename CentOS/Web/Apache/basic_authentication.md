### Configure apache to allow .htaccess authentication
```shell
$ sudo vi /etc/httpd/conf/httpd.conf
<Directory /var/www/html>
  AllowOverride AuthConfig
</Directory>
```

### Create password file with htpasswd
```shell
# Only use -c the first time you create the file. Do not use -c when you add a user in the future.
$ sudo htpasswd -c /etc/httpd/.htpasswd user1
$ sudo htpasswd /etc/httpd/.htpasswd user2
$ sudo chown apache:apache /etc/httpd/.htpasswd
$ sudo chmod 0600 /etc/httpd/.htpasswd
```

### Configure apache password authentication
```shell
$ sudo vi /var/www/html/.htaccess
AuthType Basic
AuthName "Your Auth Name"
AuthUserFile /etc/httpd/.htpasswd
Require valid-user
```
