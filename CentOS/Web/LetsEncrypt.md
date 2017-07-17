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

# Paste the following settings from the site AFTER the end of the VirtualHost block
# from https://cipherli.st/
# and https://raymii.org/s/tutorials/Strong_SSL_Security_On_Apache2.html
SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH
SSLProtocol All -SSLv2 -SSLv3
SSLHonorCipherOrder On
# Disable preloading HSTS for now.  You can use the commented out header line that includes
# the "preload" directive if you understand the implications.
#Header always set Strict-Transport-Security "max-age=63072000; includeSubdomains; preload"
Header always set Strict-Transport-Security "max-age=63072000; includeSubdomains"
Header always set X-Frame-Options DENY
Header always set X-Content-Type-Options nosniff
# Requires Apache >= 2.4
SSLCompression off
SSLUseStapling on
SSLStaplingCache "shmcb:logs/stapling-cache(150000)"
# Requires Apache >= 2.4.11
# SSLSessionTickets Off

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

