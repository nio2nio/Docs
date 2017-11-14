### Install AWStats
```shell
$ sudo yum install -y epel-release
$ sudo yum install -y awstats
```

### Configure AWStats
```shell
$ sudo vi /etc/httpd/conf.d/awstats.conf
<Directory "/usr/share/awstats/wwwroot">
    Options None
    AllowOverride All
    <IfModule mod_authz_core.c>
        # Apache 2.4
        Require all granted
    </IfModule>
    <IfModule !mod_authz_core.c>
        # Apache 2.2
        Order allow,deny
        Allow from all
    </IfModule>
</Directory>
```

### Create an AWStats configuration file
```shell
$ sudo cp /etc/awstats/awstats.localhost.localdomain.conf /etc/awstats/awstats.example.com.conf
$ sudo vi /etc/awstats/awstats.example.com.conf
# Change to Apache log file, by default it's /var/log/apache2/access.log
LogFile="/var/www/exmaple.com/access.log"

# Change to the website domain name
SiteDomain="example.com"
HostAliases="www.example.com localhost 127.0.0.1"

# When this parameter is set to 1, AWStats adds a button on report page to allow to "update" statistics from a web browser
AllowToUpdateStatsFromBrowser=1</code></pre>

# restart httpd service
$ sudo systemctl restart httpd.service

# generate current logs
$ sudo /usr/share/awstats/wwwroot/cgi-bin/awstats.pl -config=example.com -update
```

### Set up Cron to update the logs
```shell
$ sudo vi /etc/crontab
*/30 * * * * root /usr/share/awstats/wwwroot/cgi-bin/awstats.pl -config=example.com -update
```

### Access AWStats in a browser
http://your.server.ip/awstats/awstats.pl?config=example.com
