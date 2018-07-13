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
* Config dir – /etc/nginx/
* Master/Global config file – /etc/nginx/nginx.conf
* Port 80 http config file – /etc/nginx/conf.d/default.conf
* Document root directory – /usr/share/nginx/html
