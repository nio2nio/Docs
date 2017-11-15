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
```

### 搬家/轉移
```sql
-- 使用者重設密碼
UPDATE table_prefix_users SET `user_pass`='e10adc3949ba59abbe56e057f20f883e' WHERE `user_login`=@user_id;
-- 域名移轉
UPDATE table_prefix_options SET option_value = replace(option_value, 'old_domain', 'new_domain') WHERE option_name = 'home' OR option_name = 'siteurl';

UPDATE table_prefix_posts SET guid = replace(guid, 'old_domain', 'new_domain');
UPDATE table_prefix_posts SET post_content = replace(post_content, 'old_domain', 'new_domain');

### Drop All Table
DROP TABLE `XJe4v7Yi_commentmeta`;
DROP TABLE `XJe4v7Yi_comments`;
DROP TABLE `XJe4v7Yi_icl_content_status`;
DROP TABLE `XJe4v7Yi_icl_core_status`;
DROP TABLE `XJe4v7Yi_icl_flags`;
DROP TABLE `XJe4v7Yi_icl_languages`;
DROP TABLE `XJe4v7Yi_icl_languages_translations`;
DROP TABLE `XJe4v7Yi_icl_locale_map`;
DROP TABLE `XJe4v7Yi_icl_message_status`;
DROP TABLE `XJe4v7Yi_icl_node`;
DROP TABLE `XJe4v7Yi_icl_reminders`;
DROP TABLE `XJe4v7Yi_icl_string_positions`;
DROP TABLE `XJe4v7Yi_icl_string_status`;
DROP TABLE `XJe4v7Yi_icl_string_translations`;
DROP TABLE `XJe4v7Yi_icl_strings`;
DROP TABLE `XJe4v7Yi_icl_translate`;
DROP TABLE `XJe4v7Yi_icl_translate_job`;
DROP TABLE `XJe4v7Yi_icl_translation_batches`;
DROP TABLE `XJe4v7Yi_icl_translation_status`;
DROP TABLE `XJe4v7Yi_icl_translations`;
DROP TABLE `XJe4v7Yi_links`;
DROP TABLE `XJe4v7Yi_options`;
DROP TABLE `XJe4v7Yi_postmeta`;
DROP TABLE `XJe4v7Yi_posts`;
DROP TABLE `XJe4v7Yi_supsystic_tbl_columns`;
DROP TABLE `XJe4v7Yi_supsystic_tbl_diagrams`;
DROP TABLE `XJe4v7Yi_supsystic_tbl_rows`;
DROP TABLE `XJe4v7Yi_supsystic_tbl_tables`;
DROP TABLE `XJe4v7Yi_term_relationships`;
DROP TABLE `XJe4v7Yi_term_taxonomy`;
DROP TABLE `XJe4v7Yi_termmeta`;
DROP TABLE `XJe4v7Yi_terms`;
DROP TABLE `XJe4v7Yi_toolset_post_guid_id`;
DROP TABLE `XJe4v7Yi_usermeta`;
DROP TABLE `XJe4v7Yi_users`;
DROP TABLE `XJe4v7Yi_yoast_seo_links`;
DROP TABLE `XJe4v7Yi_yoast_seo_meta`;
```



