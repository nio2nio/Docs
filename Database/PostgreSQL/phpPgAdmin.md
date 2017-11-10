### Apache
See Document [Here](/CentOS/Web/Apache.md).

### PHP 5 And Extensions
```shell
$ sudo yum install php php-pgsql
```

### Install and configure PostgreSQL
[Repository](https://yum.postgresql.org/repopackages.php)
```shell
$ sudo yum install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-centos96-9.6-3.noarch.rpm
$ sudo yum groupinstall "PostgreSQL Database Server 9.6 PGDG"

# Initiate the database
$ sudo /usr/pgsql-9.6/bin/postgresql96-setup initdb

# Setup database user authentication method
$ sudo vi /var/lib/pgsql/9.6/data/pg_hba.conf
# Modify the authentication method of IPv4 local connections to md5
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
# IPv6 local connections:
host    all             all             ::1/128                 md5

# Setup PostgreSQL listening addresses
$ sudo vi /var/lib/pgsql/9.6/data/postgresql.conf
listen_addresses = '*'
port = 5432

$ Start PostgreSQL service
$ sudo systemctl start postgresql-9.6.service
$ sudo systemctl enable postgresql-9.6.service
```

### Setup database credentials
```shell
sudo -u postgres psql

# Reset postgres password
\password postgres
\q
```

### Install and configure phpPgAdmin
```shell
$ sudo yum install phpPgAdmin

# Configure phpPgAdmin as accessible from outside
$ sudo vi /etc/httpd/conf.d/phpPgAdmin.conf
# Apache 2.4
Require all granted
# Apache 2.2
Allow from all

# Modify the config.inc.php file
$ sudo vi /etc/phpPgAdmin/config.inc.php
$conf['servers'][0]['host'] = 'localhost';
$conf['owned_only'] = false;

# Allow postgres login to phpPgAdmin
$conf['extra_login_security'] = false;

# Reload PostgreSQL and httpd service
$ sudo systemctl start postgresql-9.6.service
$ sudo systemctl reload httpd.service
```
### Visit phpPgAdmin from browser
**http://YourServerIP/phpPgAdmin/**
