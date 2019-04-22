## NGINX
+ Install NGINX 
```bash
$ sudo apt install nginx
```
+ Commands
```bash
$ sudo systemctl start|stop|restart nginx.service
$ sudo systemctl status nginx.service
```

## MySQL
+ Install MySQL
```bash
$ sudo apt install mysql-server mysql-client
```
+ Configure root password
```bash
$ sudo mysql
mysql> use mysql;
mysql> UPDATE mysql.user SET authentication_string=PASSWORD('your_password'), plugin='mysql_native_password' WHERE user='root';
mysql> flush privileges;
```
+ Restart mysql service
```bash
$ sudo systemctl restart mysql.service
$ mysql -u root -p
```

## PHP
+ Install PHP 7.2
```bash
$ sudo apt-get install php7.2 php7.2-fpm php7.2-mysql
```

## Configuration
+ NGINX
```bash
$ sudo vi /etc/nginx/sites-available/default
root /var/www;

location ~ \.php$ {
  include snippets/fastcgi-php.conf;
  fastcgi_pass 127.0.0.1:9000;
}

$ sudo systemctl restart nginx.service
```
+ PHP
```bash
$ sudo vi /etc/php/7.2/fpm/pool.d/www.conf
listen = 127.0.0.1:9000

$ sudo systemctl restart php7.2-fpm.service
```

## phpMyAdmin
+ Install
```bash
$ sudo apt install phpmyadmin
# During the installation, it will prompt you to select a web server to configure. Nginx isn’t in the list, so press the Tab key and hit OK to skip this step.
# Create a new database and let dbconfig-common to configure it.
```
+ NGINX
```bash
$ sudo vi /etc/nginx/sites-available/phpmyadmin.conf
server {
  listen 80;
  listen [::]:80;
  server_name _;
  root /usr/share/phpmyadmin/;
  index index.php index.html index.htm index.nginx-debian.html;

  access_log /var/log/nginx/phpmyadmin_access.log;
  error_log /var/log/nginx/phpmyadmin_error.log;

  location / {
    try_files $uri $uri/ /index.php;
  }

  location ~ ^/(doc|sql|setup)/ {
    deny all;
  }

  location ~ \.php$ {
    fastcgi_pass 127.0.0.1:9000;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
    include snippets/fastcgi-php.conf;
  }

  location ~ /\.ht {
    deny all;
  }
}

$ sudo ln -s /etc/nginx/sites-available/phpmyadmin.conf /etc/nginx/sites-enabled/phpmyadmin.conf
```
+ Test and restart NGINX service
```bash
$ sudo nginx -t
$ sudo systemctl restart nginx.service
```
