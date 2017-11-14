### Verify mod_deflate is enabled or not
```shell
$ sudo httpd -M | grep deflate
```

### Configure mod_deflate
```shell
$ sudo vi /etc/httpd/conf.d/mod_deflate.conf
<filesMatch "\.(js|html|txt)$">
   SetOutputFilter DEFLATE
</filesMatch>
DeflateCompressionLevel 7
DeflateMemLevel 8
DeflateWindowSize 10

# DeflateCompressionLevel : This directive specify the compression level of file. By default, this level is 9. You can set up this level between 1 to 9.
# DeflateMemLevel : This directive specifies how much memory should be used by zlib for compression. The default value is 9 . You can set up this value between 1 to 9.
# DeflateWindowSize : This directive specifies the zlib compression window size. The default value is 15. You can set up this value between 1 to 15. Higher number means higher compression level, but it will use more server resources.

$ sudo systemctl restart httpd.service
```

### Test
```shell
$ wget --header="Accept-Encoding: gzip" http://your.ip/jquery-3.2.1.js
$ du -hs jquery-3.2.1.js
```

