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

<IfModule dir_module>
  DirectoryIndex index.html index.cgi index.php
</IfModule>

# Hide the Apache version
ServerSignature Off
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
<Directory /var/www/html> 
  AllowOverride All
  ...
</Directory>

# Turn off directory listing
<Directory /var/www/html>
    Options -Indexes
</Directory>

# By default Apache follows symbolic links (symlinks). Turning this off is recommended for security.
<Directory /var/www/html>
  Options -FollowSymLinks 
</Directory>

# Turn off server-side includes (SSI) and CGI execution
<Directory /var/www/html>
  Options -ExecCGI -Includes
</Directory>

# You can limit the requests size by using the Apache directive LimitRequestBody in combination with the Directory tag. This can help protect your web server from a denial of service (DOS) attack.
<Directory /var/www/html>
  LimitRequestBody 204800
</Directory>

# Disallow browsing outside the document root
# Unless you have a specific need, it is recommended to restrict Apache to being only able to access the document root.
<Directory />
  Options None
  Order deny,allow
  Deny from all
</Directory>

# DNS Lookups
HostnameLookups Off

# Secure Apache from clickjacking attacks
# Clickjacking, also known as "User Interface redress attack," is a malicious technique to collect an infected user's clicks. Clickjacking tricks the victim (visitor) into clicking on an infected site. To avoid this, you need to use X-FRAME-OPTIONS to prevent your website from being used by clickjackers.
Header append X-FRAME-OPTIONS "SAMEORIGIN"

# Disable ETag
# ETags (entity tags) are a well-known point of vulnerability in Apache web server. ETag is an HTTP response header that allows remote users to obtain sensitive information like inode number, child process ids, and multipart MIME boundary. ETag is enabled in Apache by default.
FileETag None

# HTTP request methods
# Apache support the OPTIONS, GET, HEAD, POST, CONNECT, PUT, DELETE, and TRACE method in HTTP 1.1 protocol. Some of these may not be required, and may pose a potential security risk. It is a good idea to only enable HEAD, POST, and GET for web applications.
<Directory /var/www/html>
  <LimitExcept GET POST HEAD>
    deny from all
  </LimitExcept>
</Directory>

# Secure Apache from XSS attacks
# Cross-site scripting (XSS) is one of the most common application-layer vulnerabilities in Apache server. XSS enables attackers to inject client-side script into web pages viewed by other users. Enabling XSS protection is recommended.
<IfModule mod_headers.c>
  Header set X-XSS-Protection "1; mode=block"
</IfModule>

# Protect cookies with HTTPOnly flag
# You can protect your Apache server from most of the common Cross Site Scripting attacks using the HttpOnly and Secure flags for cookies.
<IfModule mod_headers.c>
  Header edit Set-Cookie ^(.*)$ $1;HttpOnly;Secure
</IfModule>

# Restart httpd service
$ sudo systemctl restart httpd.service
```

### Disable unneccesary modules
```shell
$ sudo vi /etc/httpd/conf.modules.d/00-base.conf
# Insert a # at the beginning of the following lines to disable the modules
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