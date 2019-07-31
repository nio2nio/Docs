* NGINX
```bash
$ sudo apt update && sudo apt install nginx
```

* MySQL
```bash
$ sudo apt install mysql-server

# Configuration
$ sudo mysql_secure_installation
```

* PHP
```bash
$ sudo apt install php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-zip php-curl

# Configuration
$ sudo vi /etc/php/7.2/fpm/php.ini

file_uploads = On
allow_url_fopen = On
memory_limit = 256M
upload_max_filesize = 100M
post_max_size = 100M
max_execution_time = 360
date.timezone = Asia/Taipei
# Display Error Message
error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT
display_errors = on

# Restart php7.2-fpm Service
$ sudo systemctl restart php7.2-fpm.service

# NGINX Configuration
$ sudo vi /etc/nginx/sites-available/default

# pass PHP scripts to FastCGI server
server {
  client_max_body_size 100M;
  
  location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    
    # With php-fpm (or other unix sockets):
    fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
    # With php-cgi (or other tcp sockets):
    # fastcgi_pass 127.0.0.1:9000;
  }  
}

# Restart NGINX Service
$ sudo systemctl restart nginx.service
```

* phpMyAdmin
```bash
$ sudo apt install phpmyadmin

# NGINX Configuration
$ sudo vi /etc/nginx/sites-available/default
server {
  location /phpmyadmin {
    root /usr/share/;
    index index.php index.html index.htm;
    location ~ ^/phpmyadmin/(.+\.php)$ {
        try_files $uri =404;
        root /usr/share/;
        fastcgi_pass unix:/run/php/php7.2-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include /etc/nginx/fastcgi_params;
    }

    location ~* ^/phpmyadmin/(.+\.(jpg|jpeg|gif|css|png|js|ico|html|xml|txt))$ {
        root /usr/share/;
    }
  }
}

# Restart NGINX Service
$ sudo systemctl restart nginx.service

# Set phpMyAdmin Admin
$ sudo mysql

$ CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
$ GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' WITH GRANT OPTION;
$ FLUSH PRIVILEGES;
```
```

