The Docker daemon uses the `HTTP_PROXY`, `HTTPS_PROXY`, and `NO_PROXY` environment variables in its start-up environment to configure HTTP or HTTPS proxy behavior.

You cannot configure these environment variables using the `daemon.json` file.

This example overrides the default docker.service.file.

### 1. Create a systemd drop-in directory for the docker service
```shell
$ mkdir -p /etc/systemd/system/docker.service.d
```
### 2. Create a file called /etc/systemd/system/docker.service.d/http-proxy.conf
```shell
[Service]
Environment="HTTP_PROXY=http://proxy.example.com:80/"
```

### 3. Create a file called /etc/systemd/system/docker.service.d/https-proxy.conf
```shell
[Service]
Environment="HTTPS_PROXY=https://proxy.example.com:443/"
```

### 4. Flush changes
```shell
sudo systemctl daemon-reload
```

### 5. Restart Docker
```shell
sudo systemctl restart docker
```

### 6. Verify that the configuration has been loaded
```shell
$ sudo systemctl show --property=Environment docker
```
