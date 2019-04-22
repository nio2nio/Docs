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
$ sudo vi /etc/nginx/site-available/default
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

