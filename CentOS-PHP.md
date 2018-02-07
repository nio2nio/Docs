### PHP
  * Installation
  ```shell
  sudo yum install php php-mbstring php-pear
  ```
  * Configuration (**`/etc/php.ini`**)
  ```shell
  # Line 878
  date.timezone = "Asia/Taipei"
  
  error_reporting = E_COMPILE_ERROR|E_RECOVERABLE_ERROR|E_ERROR|E_CORE_ERROR
  error_log = /var/log/php/error.log
  max_input_time = 30

  sudo systemctl restart httpd.service
  ```
  * Create Log Folder
  ```shell
  sudo mkdir /var/log/php
  sudo chown apache /var/log/php
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
  * Secure phpMyAdmin Instance (**`/etc/httpd/conf.d/phpMyAdmin`**)
  ```shell 
  # Comment out the existing lines
  # Alias /phpMyAdmin /usr/share/phpMyAdmin
  # Alias /phpmyadmin /usr/share/phpMyAdmin
  # And add your own
  Alias /new-entry /usr/share/phpMyAdmin
  
  sudo systemctl restart httpd.service
  ```
  
### Setting up a Web Server Authentication Gate
  > See Document [Here](/CentOS-Apache.md).
  
  
