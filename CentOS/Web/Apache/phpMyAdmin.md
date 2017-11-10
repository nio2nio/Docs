## Install and Configure phpMyAdmin
```shell
$ sudo yum install -y epel-release
$ sudo yum install -y phpMyAdmin

# Specify IP Address
$ sudo vi /etc/httpd/conf.d/phpMyAdmin.conf
Require ip your_ip_address
Allow from your_ip_address

# Restart HTTPd Service
sudo systemctl restart httpd.service
```

## Secure phpMyAdmin Instance
```shell
$ sudo vi /etc/httpd/conf.d/phpMyAdmin
# Comment out the existing lines
# Alias /phpMyAdmin /usr/share/phpMyAdmin
# Alias /phpmyadmin /usr/share/phpMyAdmin
# And add your own
Alias /new-entry /usr/share/phpMyAdmin

# Restart HTTPd Service
$ sudo systemctl restart httpd.service
```

## Setting up a Web Server Authentication Gate
```shell
$ sudo vi /etc/httpd/conf.d/phpMyAdmin
<Directory /usr/share/phpMyAdmin/>
   AllowOverride All
   <IfModule mod_authz_core.c>
   . . .
</Directory>

# Create An .htaccess File
$ sudo vi /usr/share/phpMyAdmin/.htaccess
AuthType Basic
AuthName "Admin Login"
AuthUserFile /etc/httpd/pma_pass
Require valid-user

# Create the Password File for Authentication
# The -c flag indicates that this will create an initial file.
$ sudo htpasswd -c /etc/httpd/pma_pass username
```
