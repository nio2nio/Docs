### Installation [Repository](https://yum.postgresql.org/repopackages.php)
```shell
sudo yum install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-centos96-9.6-3.noarch.rpm
sudo yum groupinstall "PostgreSQL Database Server 9.6 PGDG"
```

### Initiate the database
```shell
sudo /usr/pgsql-9.6/bin/postgresql96-setup initdb
```

### Setup database user authentication method (**`/var/lib/pgsql/9.6/data/pg_hba.conf`**)
```shell
# Modify the authentication method of IPv4 local connections to md5
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
# IPv6 local connections:
host    all             all             ::1/128                 md5
```

### Setup PostgreSQL listening addresses (**`/var/lib/pgsql/9.6/data/postgresql.conf`**)
```shell
listen_addresses = '*'
port = 5432
```

### Start PostgreSQL service
```shell
sudo systemctl start postgresql-9.6.service
sudo systemctl enable postgresql-9.6.service
```

### Setup database credentials
```shell
sudo -u postgres psql

# Reset postgres password
\password postgres
\q
```
