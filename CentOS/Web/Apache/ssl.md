### Install SSL
```shell
$ sudo yum install -y mod_ssl openssl
```

### Create certificate
```shell
# Generate a private key ca.key with 2048-bit encryption.
$ sudo openssl genrsa -out ca.key 2048

# Generate the certificate signing request cs.csr
$ sudo openssl req -new -key ca.key -out ca.csr

# Generate a self-signed certificate ca.crt of X509 type valid for 365 keys.
$ sudo openssl x509 -req -days 365 -in ca.csr -signkey -out ca.crt

# Copy all of the certificate files to the necessary directories.
$ sudo cp ca.crt /etc/pki/tls/certs
$ sudo cp ca.key /etc/pki/tls/private
$ sudo cp ca.csr /etc/pki/tls/private
```

### Configure SSL
```shell
$ sudo vi /etc/httpd/conf.d/ssl.conf
DocumentRoot "/var/www/html"
ServerName your.domain:443
SSLEngine on
SSLProtocol -All +TLSv1 +TLSv1.1 +TLSv1.2
SSLCertificateFile /etc/pki/tls/certs/ca.crt
SSLCertificateKeyFile /etc/pki/tls/private/ca.key

# Restart httpd.service
$ sudo systemctl restart httpd.service
```


