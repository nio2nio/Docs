### Create certificate
```shell
$ cd /etc/pki/tls/certs 
$ sudo make server.key

# remove passphrase from private key
$ openssl rsa -in server.key -out server.key 

$ sudo make server.csr
$ sudo openssl x509 -in server.csr -out server.crt -req -signkey server.key -days 3650
```

### Configure SSL
```shell
$ sudo yum -y install mod_ssl
DocumentRoot "/var/www/html"
ServerName your.domain:443
SSLProtocol -All +TLSv1 +TLSv1.1 +TLSv1.2
SSLCertificateFile /etc/pki/tls/certs/server.crt
SSLCertificateKeyFile /etc/pki/tls/certs/server.key

# Restart httpd.service
$ sudo systemctl restart httpd.service
```


