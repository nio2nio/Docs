### PHP
  * Installation
  ```shell
  sudo yum install php php-mbstring php-pear
  ```
  * Configuration (**`/etc/php.ini`**)
  ```shell
  # Line 878
  date.timezone = "Asia/Taipei"

  sudo systemctl restart httpd.service
  ```
  
### phpMyAdmin
  * Installation
  ```shell
  sudo yum install -y epel-release
  sudo yum install -y phpMyAdmin
  ```
  * Configuration (**`/etc/httpd/conf.d/phpMyAdmin.conf`**)
  ```shell
  Require ip your_ip_address
  Allow from your_ip_address
  
  sudo systemctl restart httpd.service
  ```
  * Secure phpMyAdmin Instance
  ```shell (**`/etc/httpd/conf.d/phpMyAdmin`**)
  # Comment out the existing lines
  # Alias /phpMyAdmin /usr/share/phpMyAdmin
  # Alias /phpmyadmin /usr/share/phpMyAdmin
  # And add your own
  Alias /new-entry /usr/share/phpMyAdmin
  
  sudo systemctl restart httpd.service
  ```
  
### Setting up a Web Server Authentication Gate
  > See Document [Here](/CentOS-Apache.md).
  
  
