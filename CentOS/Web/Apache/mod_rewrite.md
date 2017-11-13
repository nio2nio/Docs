### Install Apache
```shell
$ sudo yum install -y httpd

# Start httpd service and enable it to start automatically
$ sudo systemctl start httpd.service
$ sudo systemctl enable httpd.service

# allow access to default apache port 80 using firewalld
$ sudo firewall-cmd --permanent --add-port=80/tcp
$ sudo systemctl restart firewalld.service
```

### Enable mod_rewrite module
```shell
$ sudo vi /etc/httpd/conf.modules.d/00-base.conf

# uncomment the following line
LoadModule rewrite_module modules/mod_rewrite.so

# restart httpd service
$ sudo systemctl restart httpd.service
```

### Enable .htaccess file
```shell
$ sudo vi /etc/httpd/conf/httpd.conf
<Directory /var/www/html>
  AllowOverride All
</Directory>

# restart httpd service
$ sudo systemctl restart httpd.service
```

### Configure rewrite module
RewriteRule pattern substitution [flags]
RewriteRule: This directive specifies the name of the the mod_rewrite directive that you want to use.
Pattern: This directive specifies a regular expression that matches the desired string
Substitution: This directive specifies the path of the actual URL of the page with the information you want to display.
Flags: A flag is a tag at the end of the Rewrite Rule directive that specifies optional parameters that can modify the rule.

example:
RewriteEngine On
RewriteBase /
RewriteCond %{HTTP_HOST} ^www\.(.*)$ [NC]
RewriteRule ^(.*)$ http://%1/$1 [R=301,L]
