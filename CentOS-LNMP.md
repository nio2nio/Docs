### Configure Nginx repo for CentOS 7
```shell
$ vi /etc/yum.repos.d/nginx.repo

[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/mainline/centos/7/$basearch/
gpgcheck=0
enabled=1
```

### Install Nginx on CentOS 7
```shell
$ sudo yum install nginx
```

### Nginx command
```shell
$ sudo systemctl start nginx.service
$ sudo systemctl stop nginx.service
$ sudo systemctl restart nginx.service
$ sudo systemctl enable nginx.service
$ sudo systemctl disable nginx.service
$ sudo systemctl status nginx.service
```

### Firewall-cmd command
```shell
$ sudo firewall-cmd --zone=public --permanent --add-service=http
$ sudo firewall-cmd --zone=public --permanent --add-service=https
$ sudo firewall-cmd --zone=public --permanent --add-port=8080/tcp
$ sudo firewall-cmd --reload
```

### Configure Nginx server
* Config dir – **`/etc/nginx/`**
* Master/Global config file – **`/etc/nginx/nginx.conf`**
* Port 80 http config file – /etc/nginx/conf.d/default.conf
* Document root directory – **`/usr/share/nginx/html`**

### Installing PHP version 7.2
```shell
$ sudo yum install epel-release
$ sudo yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
$ sudo yum install yum-utils
$ sudo yum-config-manager --enable remi-php72
$ sudo yum update
$ sudo yum install php72 php72-php-fpm php72-php-gd php72-php-json php72-php-mbstring php72-php-mysqlnd php72-php-xml php72-php-xmlrpc php72-php-opcache
```

### Verification
```shell
$ php72 --version
$ php72 --modules
```

### Turn on PHP fpm for nginx
```shell
$ sudo systemctl start php72-php-fpm.service
$ sudo systemctl stop php72-php-fpm.service
$ sudo systemctl restart php72-php-fpm.service
$ sudo systemctl enable php72-php-fpm.service
$ sudo systemctl disable php72-php-fpm.service
$ sudo systemctl status php72-php-fpm.service
```

### Configure Nginx for using with PHP 7.2
```shell
$ egrep '^(user|group)' /etc/nginx/nginx.conf
# output: 
#  user nginx;
  
$ sudo vi /etc/opt/remi/php72/php-fpm.d/www.conf
# Set user and group to nginx:
user = nginx
group = nginx

$ sudo systemctl restart php72-php-fpm.service

# Update nginx.conf
$ sudo vi /etc/nginx/conf.d/default.conf
location ~ \.php$ {
    root /usr/share/nginx/html;
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    include        fastcgi_params;
    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
}

$ sudo systemctl restart nginx
```

### Install phpMyAdmin
```shell
$ sudo yum install -y phpmyadmin
```

### phpMyAdmin Nginx Configuration
```shell
$sudo vi /etc/nginx/conf.d/phpMyAdmin.conf
server {
	listen				                9481;
	server_name	                  localhost;
	root 	                        /usr/share/phpMyAdmin;
	charset			                  utf-8;
	
	access_log		                /var/logs/nginx/phpMyAdmin_access.log;
	error_log		                  /var/logs/nginx/phpMyAdmin_error.log;
	
	location / {
		index	                      index.html index.htm index.php;
	}
	
	error_page   500 502 503 504  /50x.html;
	location = /50x.html {
		root                        /usr/share/phpMyAdmin;
	}
	
	location ~ \.php$ {
		fastcgi_pass                127.0.0.1:9000;
		fastcgi_index               index.php;
		fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
		include                     fastcgi_params;
	}
	
	# deny access to apache .htaccess files
	location ~ /\.ht
    {
        deny all;
    }
}
```

### Issue: FastCGI sent in stderr: "PHP message: PHP Fatal error:  Call to undefined function __() in /usr/share/phpMyAdmin/libraries/core.lib.php on line 245"
```shell
sudo chown root:nginx -Rvf /var/opt/remi/php72/lib/php
```

