### Install unixODBC (libodbc.so, libtdsS.so, isql and isqlinst)
```shell
$ yum install unixODBC, unixODBC-devel

$ sudo vi /etc/odbcinst.ini
  [SyBase]
  Description     = ODBC for SyBase
  Driver          = /usr/lib64/libtdsodbc.so
  Setup           = /usr/lib64/libtdsS.so
  FileUsage       = 1

$ odbcinst -d -q
  [PostgreSQL]
  [MySQL]
  [SyBase]
```
#### PHP PDO
```php
$host = '10.1.2.3';
$port = '5000';
$database = 'YSP2';
$user = 'user';
$pass = 'xxxx';

try {
  $conn = new PDO('odbc:Driver={SyBase};Server=' . $host . ';Port=' . $port . ';Database=' . $database . ';UID=' . $user . ';PWD=' . $pass . ';        clientcharset=UTF-8');
} catch (PDOException $ex){
  echo $ex->getMessage();
}
```
```shell
$sudo vi /etc/odbc.ini
  [WMS]
  Driver          = /usr/lib64/libtdsodbc.so
  Setup           = /usr/lib64/libtdsS.so
  Description     = PPP (SyBase)
  Track           = No
  Server          = 10.1.2.3
  Database        = YSP2
  Port            = 5000
  
$ sudo isql WMS user pass
```

### Install freetds (libtdsodbc.so and tsql)
```shell
$ yum install freetds, freetds-devel

$ tsql -C
Compile-time settings (established with the "configure" script)
                            Version: freetds v0.95.81
             freetds.conf directory: /etc
     MS db-lib source compatibility: yes
        Sybase binary compatibility: yes
                      Thread safety: yes
                      iconv library: yes
                        TDS version: 4.2
                              iODBC: no
                           unixodbc: yes
              SSPI "trusted" logins: no
                           Kerberos: yes
                            OpenSSL: no
                             GnuTLS: yes

```

