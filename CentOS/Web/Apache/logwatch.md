### Install logwatch
```shell
$ sudo yum install -y logwatch
```

### Configure logwatch
```shell
# The email report will be delivered to the local root user by default. To specify an alternate email address, create a new file called /etc/logwatch/conf/logwatch.conf and add the following line.
$ sudo vi /etc/logwatch/conf/logwatch.conf
MailTo = user@example.com

# The default log summary email will be in standard text format. 
Format = html

# The email sender can be changed from Logwatch to another local user or email address by setting the MailFrom value.
MailFrom = user@example.com

# The summary includes a list of services that list can be found in the /usr/share/logwatch/scripts/services/ directory. Those services can be excluded from the summary by prepending a hyphen to the Service name value.
Service = All
Service = "-ftpd-xferlog"

# Additional customizations to logwatch.conf can be found in the default global configuration file.
/usr/share/logwatch/default.conf/logwatch.conf
```

### 
```shell
# Run manually
/usr/sbin/logwatch --mailto user@example.com --format html --service secure
```
