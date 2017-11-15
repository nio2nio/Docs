### Install Required Software
```shell
# EPEL Repository
$ sudo yum install epel-release
# SSL and certbot
$ sudo yum install mod_ssl python-certbot-apache
```

### Reqesting SSL Certificate From LetsEncrypt
```shell
# Single domain
$ sudo certbot --apache -d example.com
# Multi domains or Sub-domain
$ sudo certbot --apache -d example.com -d www.example.com
# Generated certificates files will be located in /etc/letsencrypt/live
```

### Apache SSL Configuration
```shell
$ sudo vi /etc/httpd/conf.d/ssl.conf
# Comment SSLProtocol, SSLCipherSuite 2 lines
#SSLProtocol all -SSLv2
#SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5:!SEED:!IDEA

$ sudo vi /etc/httpd/conf/httpd.conf
# Comment the following line (certbot will append automatically)
#Include /etc/httpd/sites-available/example.com-le-ssl.conf

$ sudo vi /etc/httpd/sites-available/example.com.conf
# If you choose Redirect, certbot will append the following lines
RewriteEngine on
RewriteCond %{SERVER_NAME} =www.example.com [OR]
RewriteCond %{SERVER_NAME} =example.com
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]

$ sudo vi /etc/httpd/sites-available/example.com-le-ssl.conf
SSLCertificateFile /etc/letsencrypt/live/example.com/cert.pem
SSLCertificateKeyFile /etc/letsencrypt/live/example.com/privkey.pem
Include /etc/letsencrypt/options-ssl-apache.conf
SSLCertificateChainFile /etc/letsencrypt/live/example.com/chain.pem

$ sudo vi /etc/letencrypt/options-ssl.apache.conf
SSLEngine on
SSLProtocol             all -SSLv2 -SSLv3
SSLCipherSuite          ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA

# Check apache configuration
$ sudo apachectl configtest

# Restart httpd.service
$ sudo systemctl restart httpd.service
```

### Check Certificate Status
> https://www.ssllabs.com/ssltest/analyze.html?d=example.com&latest

### Setting Auto Renewal
```shell
# Renewal certificates
$ sudo certbot renew

# Log File: /var/log/letsencrypt/letsencrypt.log

# Crontab
$ sudo crontab -e
30 2 * * * /usr/bin/certbot renew >> /var/log/le-renew.log
```

