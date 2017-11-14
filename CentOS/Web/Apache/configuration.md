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
# KeepAlive sets whether the server allows more than one request per connection.
KeepAlive On

# MaxKeepAliveRequests is the maximum number of requests to serve on a TCP connection. If it is set to 0, unlimited requests will be allowed. The recommended value of MaxKeepAliveRequests is 500.
MaxKeepAliveRequests 500

# KeepAliveTimeout defines the number of seconds Apache will wait for the new request from connected clients before closing the connection.By default Keepalive is disabled in CentOS 7. If Keepalive is set to on, it is a good idea to set the KeepAliveTimeout value low. The recommended KeepAliveTimeout can be between 1 to 5.
KeepAliveTimeout 5

# Configure MPM Prefork
# StartServers: This directive sets the number of child server processes created on startup. It is a good idea to increase this number on a high-load server, so the server is ready to handle a lot of connections.
# MinSpareServers: This directive sets the minimum number of idle child server processes. This value will need to be tuned for high-load servers.
# MaxSpareServers: This directive sets the maximum number of idle child server processes. When there are more idle child server processes than defined by MaxSpareServers the idle process will be killed.
# MaxClients: This directive sets the maximum number of simultaneous requests that Apache will handle. When this limit has been reached, any other connection attempts will be queued. Number of MaxClients = (Total RAM memory – RAM memory used for other process except Apache process) / (Memory used by a single Apache process)
# MaxRequestsPerChild: This directive sets how many requests a child process will handle before terminating. Once the limit has been reached, the child process will die.
<IfModule prefork.c>
   StartServers        5
   MinSpareServers     5
   MaxSpareServers     10
   MaxClients          150
   MaxRequestsPerChild 3000
</IfModule>

# If AllowOverride is set to 'All', then Apache will attempt to open a .htaccess file in each directory that it visits.
DocumentRoot /vaw/www/html/website1
<Directory /> 
  AllowOverride All
</Directory>

# DNS Lookups
HostnameLookups Off

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
