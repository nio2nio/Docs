### Apache Basic
  * Installation
  ```shell
  sudo yum install httpd
  ```
  * Service Management
  ```shell
  sudo systemctl start httpd.service
  sudo systemctl enable httpd.service
  ```
  * FirewallD
  ```shell
  sudo firewall-cmd --zone=public --permanent --add-service=http ex:Service Name
  sudo firewall-cmd --zone=public --permanent --add-port=5432/tcp ex:Port/Protocol (TCP/UDP)
  sudo firewall-cmd --reload
  ```
  * SELinux
  ```shell
  sudo setsebool -P httpd_can_network_connect on
  sudo setsebool -P httpd_can_network_connect_db on
  ```
  * Remove welcome page
  ```shell
  sudo rm -fr /etc/httpd/conf.d/welcome.conf
  ```

### Apache Cofiguration (**`/etc/httpd/conf/httpd.conf`**)
  * Index
  ```shell
  <IfModule dir_module>
    DirectoryIndex index.html index.cgi index.php<br>
  </IfModule>
  ```
  * Hide the Apache version
  ```shell
  ServerSignature Off
  ServerTokens Prod
  ```
  * **`KeepAlive`**: allows more than one request per connection.
  ```shell
  KeepAlive On
  ```
  * **`MaxKeepAliveRequests`** is the maximum number of requests to serve on a TCP connection. If it is set to 0, unlimited requests will be allowed. The recommended value of MaxKeepAliveRequests is 500.
  ```shell
  MaxKeepAliveRequests 500
  ```
  * **`KeepAliveTimeout`** defines the number of seconds Apache will wait for the new request from connected clients before closing the connection.By default Keepalive is disabled in CentOS 7. If Keepalive is set to on, it is a good idea to set the KeepAliveTimeout value low. The recommended KeepAliveTimeout can be between 1 to 5.
  ```shell
  KeepAliveTimeout 5
  ```
  * Configure MPM Prefork
  > **`StartServers`**: This directive sets the number of child server processes created on startup. It is a good idea to increase this number on a high-load server, so the server is ready to handle a lot of connections.<br>
  > **`MinSpareServers`**: This directive sets the minimum number of idle child server processes. This value will need to be tuned for high-load servers.<br>
  > **`MaxSpareServers`**: This directive sets the maximum number of idle child server processes. When there are more idle child server processes than defined by MaxSpareServers the idle process will be killed.<br>
  > **`MaxClients`**: This directive sets the maximum number of simultaneous requests that Apache will handle. When this limit has been reached, any other connection attempts will be queued. Number of MaxClients = (Total RAM memory – RAM memory used for other process except Apache process) / (Memory used by a single Apache process)<br>
  > **`MaxRequestsPerChild`**: This directive sets how many requests a child process will handle before terminating. Once the limit has been reached, the child process will die.
  ```shell
  <IfModule prefork.c>
     StartServers        5
     MinSpareServers     5
     MaxSpareServers     10
     MaxClients          150
     MaxRequestsPerChild 3000
  </IfModule>
  ```
  * Turn off directory listing
  ```shell
  <Directory /var/www/html>
      Options -Indexes
  </Directory>
  ```
  * By default Apache follows symbolic links (symlinks). Turning this off is recommended for security.
  ```shell
  <Directory /var/www/html>
    Options -FollowSymLinks 
  </Directory>
  ```
  * Turn off server-side includes (SSI) and CGI execution
  ```shell
  <Directory /var/www/html>
    Options -ExecCGI -Includes
  </Directory>
  ```
  * You can limit the requests size by using the Apache directive LimitRequestBody in combination with the Directory tag. This can help protect your web server from a denial of service (DOS) attack.
  ```shell
  <Directory /var/www/html>
    LimitRequestBody 204800
  </Directory>
  ```
  * Disallow browsing outside the document root. Unless you have a specific need, it is recommended to restrict Apache to being only able to access the document root.
  ```shell
  <Directory />
    Options None
    Order deny,allow
    Deny from all
  </Directory>
  ```
  * DNS Lookups
  ```shell
  HostnameLookups Off
  ```
  * Secure Apache from clickjacking attacks. Clickjacking, also known as "User Interface redress attack," is a malicious technique to collect an infected user's clicks. Clickjacking tricks the victim (visitor) into clicking on an infected site. To avoid this, you need to use X-FRAME-OPTIONS to prevent your website from being used by clickjackers.
  ```shell
  Header append X-FRAME-OPTIONS "SAMEORIGIN"
  ```
  * Disable ETag. ETags (entity tags) are a well-known point of vulnerability in Apache web server. ETag is an HTTP response header that allows remote users to obtain sensitive information like inode number, child process ids, and multipart MIME boundary. ETag is enabled in Apache by default.
  ```shell
  FileETag None
  ```
  * HTTP request methods. Apache support the OPTIONS, GET, HEAD, POST, CONNECT, PUT, DELETE, and TRACE method in HTTP 1.1 protocol. Some of these may not be required, and may pose a potential security risk. It is a good idea to only enable HEAD, POST, and GET for web applications.
  ```shell
  <Directory /var/www/html>
    <LimitExcept GET POST HEAD>
      deny from all
    </LimitExcept>
  </Directory>
  ```
  * Secure Apache from XSS attacks. Cross-site scripting (XSS) is one of the most common application-layer vulnerabilities in Apache server. XSS enables attackers to inject client-side script into web pages viewed by other users. Enabling XSS protection is recommended.
  ```shell
  <IfModule mod_headers.c>
    Header set X-XSS-Protection "1; mode=block"
  </IfModule>
  ```
  * Protect cookies with HTTPOnly flag. You can protect your Apache server from most of the common Cross Site Scripting attacks using the HttpOnly and Secure flags for cookies.
  ```shell
  <IfModule mod_headers.c>
    Header edit Set-Cookie ^(.*)$ $1;HttpOnly;Secure
  </IfModule>
  ```
  * Disable unneccesary modules
  ```shell
  sudo vi /etc/httpd/conf.modules.d/00-base.conf
  # Insert a # at the beginning of the following lines to disable the modules
  ```

### Basic Authentication
  * Configuration (**`/etc/httpd/conf/httpd.conf`**)
  ```shell
  <Directory /var/www/html>
    AllowOverride AuthConfig
  </Directory>
  ```
  * Create password file with htpasswd
  ```shell
  # Only use -c the first time you create the file. Do not use -c when you add a user in the future.
  sudo htpasswd -c /etc/httpd/.htpasswd user1
  sudo htpasswd /etc/httpd/.htpasswd user2
  sudo chown apache:apache /etc/httpd/.htpasswd
  sudo chmod 0600 /etc/httpd/.htpasswd
  ```
  * Configure apache password authentication
  ```shell
  sudo vi /var/www/html/.htaccess
  AuthType Basic
  AuthName "Your Auth Name"
  AuthUserFile /etc/httpd/.htpasswd
  Require valid-user
  ```
  
### User Directory
  * Configuration(**`/etc/httpd/conf.d/userdir.conf`**)
  ```shell
  # UserDir disabled
  UserDir public_html

  <Directory "/home/*/public_html">
    AllowOverride All
    Options None
    Require method GET POST OPTIONS
  </Directory>

  # Restart httpd service
  sudo systemctl restart httpd.service
  ```
  
  * Create a test page
  ```shell
  cd ~
  mkdir public_html
  chmod 711 /home/cent
  chmod 755 /home/cent/public_html
  vi ./public_html/index.html
  <html>
    <body>
      <div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">
        UserDir Test Page
      </div>
     </body>
  </html>

  # Visit http://your.domain/~cent/
  ```

### mod_deflate
  * Verify mod_deflate is enabled or not
  ```shell
  sudo httpd -M | grep deflate
  ```
  * Configuration (**`/etc/httpd/conf.d/mod_deflate.conf`**)
  > **`DeflateCompressionLevel`** : This directive specify the compression level of file. By default, this level is 9. You can set up this level between 1 to 9.<br>
  > **`DeflateMemLevel`** : This directive specifies how much memory should be used by zlib for compression. The default value is 9 . You can set up this value between 1 to 9.<br>
  > **`DeflateWindowSize`** : This directive specifies the zlib compression window size. The default value is 15. You can set up this value between 1 to 15. Higher number means higher compression level, but it will use more server resources.
  * Configure mod_deflate
  ```shell
  <filesMatch "\.(js|html|txt)$">
     SetOutputFilter DEFLATE
  </filesMatch>
  DeflateCompressionLevel 7
  DeflateMemLevel 8
  DeflateWindowSize 10

  sudo systemctl restart httpd.service
  ```
  * Test
  ```shell
  wget --header="Accept-Encoding: gzip" http://your.ip/jquery-3.2.1.js
  du -hs jquery-3.2.1.js
  ```
  
### mod_rewrite 
  * Enable mod_rewrite module
  ```shell
  sudo vi /etc/httpd/conf.modules.d/00-base.conf

  # uncomment the following line
  LoadModule rewrite_module modules/mod_rewrite.so

  # restart httpd service
  sudo systemctl restart httpd.service
  ```
  * Enable .htaccess file
  ```shell
  sudo vi /etc/httpd/conf/httpd.conf
  <Directory /var/www/html>
    AllowOverride All
  </Directory>

  restart httpd service
  ```
  * Configure rewrite module
  > Rule: **`RewriteRule pattern substitution [flags]`**<br>
  > **`RewriteRule`**: This directive specifies the name of the the mod_rewrite directive that you want to use.<br>
  > **`Pattern`**: This directive specifies a regular expression that matches the desired string.<br>
  > **`Substitution`**: This directive specifies the path of the actual URL of the page with the information you want to display.<br>
  > **`Flags`**: A flag is a tag at the end of the Rewrite Rule directive that specifies optional parameters that can modify the rule.
  ```shell
  RewriteEngine On
  RewriteBase /
  RewriteCond %{HTTP_HOST} ^www\.(.*)$ [NC]
  RewriteRule ^(.*)$ http://%1/$1 [R=301,L]
  ```

### Virtual Host
  * 設定虛擬主機
  ```shell
  #  建立虛擬目錄
  sudo makir -p /var/www/example.com/public_html

  # 變更擁有權
  sudo chown -R apache:apache /var/www/example.com/public_html

  # 變更目錄權限
  sudo chmod -R 755 /var/www

  # 建立設定檔目錄
  sudo mkdir /etc/httpd/sites-available
  sudo mkdir /etc/httpd/sites-enabled

  # 編輯Apache設定檔
  sudo vi /etc/httpd/conf/httpd.conf
  
  # 新增設定
  IncludeOptional sites-enabled/*.conf
  ```
  * 建立虛擬主機設定檔
  ```shell
  sudo vi /etc/httpd/sites-avialable/example.com.conf
  <VirtualHost *:80>
      ServerAdmin webmaster@dummy-host.example.com    
      ServerName www.coolexample.com
      ServerAlias coolexample.com 
      DocumentRoot /var/www/example.com/public_html 
      ErrorLog /var/www/example.com/error.log 
      CustomLog /var/www/example.com/requests.log combined 
  </VirtualHost>

  # 連結設定檔至site-enabled
  sudo ln -s /etc/httpd/site-available/example.com.conf /etc/httpd/site-enabled/example.com.conf
  
  sudo systemctl restart httpd.service
  ```
 
### SSL
  * Install SSL
  ```shell
  sudo yum install -y mod_ssl openssl
  ```
  * Create certificate
  ```shell
  # Generate a private key ca.key with 2048-bit encryption.
  sudo openssl genrsa -out ca.key 2048

  # Generate the certificate signing request cs.csr
  sudo openssl req -new -key ca.key -out ca.csr

  # Generate a self-signed certificate ca.crt of X509 type valid for 365 keys.
  sudo openssl x509 -req -days 365 -in ca.csr -signkey -out ca.crt

  # Copy all of the certificate files to the necessary directories.
  sudo cp ca.crt /etc/pki/tls/certs
  sudo cp ca.key /etc/pki/tls/private
  sudo cp ca.csr /etc/pki/tls/private
  ```
  * Configuration (**`/etc/httpd/conf.d/ssl.conf`**)
  ```shell
  DocumentRoot "/var/www/html"
  ServerName your.domain:443
  SSLEngine on
  SSLProtocol -All +TLSv1 +TLSv1.1 +TLSv1.2
  SSLCertificateFile /etc/pki/tls/certs/ca.crt
  SSLCertificateKeyFile /etc/pki/tls/private/ca.key

  sudo systemctl restart httpd.service
  ```
  
### Let's Encrypt
  * Install Required Software
  ```shell
  sudo yum install epel-release
  sudo yum install mod_ssl python-certbot-apache
  ```
  * Reqesting SSL Certificate From LetsEncrypt
  ```shell
  # Single domain
  sudo certbot --apache -d example.com
  # Multi domains or Sub-domain
  sudo certbot --apache -d example.com -d www.example.com
  # Generated certificates files will be located in /etc/letsencrypt/live
  ```
  * Apache SSL Configuration
  ```shell
  sudo vi /etc/httpd/conf.d/ssl.conf
  # Comment SSLProtocol, SSLCipherSuite 2 lines
  #SSLProtocol all -SSLv2
  #SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5:!SEED:!IDEA

  sudo vi /etc/httpd/conf/httpd.conf
  # Comment the following line (certbot will append automatically)
  #Include /etc/httpd/sites-available/example.com-le-ssl.conf

  sudo vi /etc/httpd/sites-available/example.com.conf
  # If you choose Redirect, certbot will append the following lines
  RewriteEngine on
  RewriteCond %{SERVER_NAME} =www.example.com [OR]
  RewriteCond %{SERVER_NAME} =example.com
  RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]

  sudo vi /etc/httpd/sites-available/example.com-le-ssl.conf
  SSLCertificateFile /etc/letsencrypt/live/example.com/cert.pem
  SSLCertificateKeyFile /etc/letsencrypt/live/example.com/privkey.pem
  Include /etc/letsencrypt/options-ssl-apache.conf
  SSLCertificateChainFile /etc/letsencrypt/live/example.com/chain.pem

  sudo vi /etc/letencrypt/options-ssl.apache.conf
  SSLEngine on
  SSLProtocol             all -SSLv2 -SSLv3
  SSLCipherSuite          ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA

  # Check apache configuration And Restart Service
  sudo apachectl configtest
  sudo systemctl restart httpd.service
  ```
  * Check Certificate Status
  > Visit https://www.ssllabs.com/ssltest/analyze.html?d=example.com&latest
  * Setting Auto Renewal
  ```shell
  # Renewal certificates
  sudo certbot renew

  # Log File: /var/log/letsencrypt/letsencrypt.log

  # Crontab
  sudo crontab -e
  30 2 * * * /usr/bin/certbot renew >> /var/log/le-renew.log
  ```
  
  ### AWStats
  * Installation
  ```shell
  sudo yum install epel-release
  sudo yum install awstats
  ```
  * Configuration (**`/etc/httpd/conf.d/awstats.conf`**)
  ```shell
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
  * Create an AWStats configuration file
  ```shell
  sudo cp /etc/awstats/awstats.localhost.localdomain.conf /etc/awstats/awstats.example.com.conf
  sudo vi /etc/awstats/awstats.example.com.conf
  # Change to Apache log file, by default it's /var/log/apache2/access.log
  LogFile="/var/www/exmaple.com/access.log"

  # Change to the website domain name
  SiteDomain="example.com"
  HostAliases="www.example.com localhost 127.0.0.1"

  # When this parameter is set to 1, AWStats adds a button on report page to allow to "update" statistics from a web browser
  AllowToUpdateStatsFromBrowser=1</code></pre>

  sudo systemctl restart httpd.service

  # generate current logs
  sudo /usr/share/awstats/wwwroot/cgi-bin/awstats.pl -config=example.com -update
  ```
  * Set up Cron to update the logs
  ```shell
  sudo vi /etc/crontab
  */30 * * * * root /usr/share/awstats/wwwroot/cgi-bin/awstats.pl -config=example.com -update
  ```
  * Access AWStats in a browser
  > http://your.server.ip/awstats/awstats.pl?config=example.com
  
### logwatch
  * Installation
  ```shell
  sudo yum install logwatch
  ```
  * Configuration (**`/etc/logwatch/conf/logwatch.conf`**)
  ```shell
  # The email report will be delivered to the local root user by default. To specify an alternate email address, create a new file called /etc/logwatch/conf/logwatch.conf and add the following line.
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
  * Run manually
  ```shell
  /usr/sbin/logwatch --mailto user@example.com --format html --service secure
  ```
