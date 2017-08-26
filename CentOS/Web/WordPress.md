### 1. Update System
```shell
$ sudo yum update -y
```

### 2. Install LAMP
```shell
$ sudo yum install httpd mariadb mariadb-server php php-common php-mysql php-gd php-xml php-mbstring php-mcrypt php-xmlrpc unzip wget -y
```

### 3. Start Apache and MariaDB Service
```shell
$ sudo systemctl start httpd.service
$ sudo systemctl start mariadb.service
$ sudo systemctl enable httpd.service
$ sudo systemctl enable mariadb.service
```

### 4. Configuring MariaDB for WordPress
```shell
# Secure MariaDB
sudo mysql_secure_installation

# Create Database
$ sudo mysql -u root -p
> CREATE DATABASE wordpress;
> GRANT ALL PRIVILEGES on wordpress.* TO 'wpuser'@'localhost' IDENTIFIED BY 'P@ssw0rd';
> FLUSH PRIVILEGES;
> exit
```

### Installing and Configuring WordPress
```shell
# Get the latest version of WordPress
$ wget http://wordpress.org/latest.tar.gz
$ tar -zxvf latest.tar.gz
$ sudo cp -avr wordpress/* /var/www/html/
$ sudo mkdir /var/www/html/wp-content/uploads

# Assign proper ownership and permissions
$ sudo chown apache:apache -R /var/www/html

# Configure WordPress
$ cd /var/www/html
$ sudo mv wp-config-sample.php wp-config.php
$ sudo vi wp-config.php
define('DB_NAME', 'wordpress');
define('DB_USER', 'user');
define('DB_PASSWORD', 'password');
```

### HTTP Environment
```shell
$ sudo vi /etc/httpd/conf/httpd.conf
<Directory "/var/www/html">
  Options Indexes FollowSymLinks
  AllowOverride All
  Require all granted
</Directory>



