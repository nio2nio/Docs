### Enable UserDir 
See Document [Here](/CentOS/Web/Apache/UserDir.md).

### Configure Virtual Hostings
```shell
$ sudo vi /etc/httpd/conf.d/vhost.conf
<VirtualHost *:80>
  DocumentRoot /var/www/html
  ServerName www.vastuna.com
</VirtualHost>

<VirtualHost *:80>
  DocumentRoot /var/www/vastuna
  Servername vastuna.ddns.net
  ServerAdmin webadmin@vastuna.ddns.net
  ErrorLog logs/vastuna-error_log
  CustomLog logs/vastuna-access_log combined
</VirtualHost>

<VirtualHost *:80>
  DocumentRoot /var/www/gun-drill
  ServerName gun-drill.ddns.net
  ServerAdmin webadmin@gun-drill.ddns.net
  ErrorLog logs/gun-drill-error.log
  CustomLog logs/gun-drill-access_log combined
</VirtualHost>
```
