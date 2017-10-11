### Uninstall old version
```shell
$ sudo yum remove docker docker-common docker-selinux docker-engine
```

### Set up the repository
```shell
# Install required packages
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2

# Set up the stable repository
$ sudo yum-config-manager --add-repo https://download.docker.com/centos/docker-ce.repo

# Optional. Enable/disable the edge and test repository
$ sudo yum-config-manager --enable/--disable docker-ce-edge
$ sudo yum-config-manager --enable/--disable docker-ce-test
```

### Install Docker-CE
```shell
# Install the latest version of Docker CE.
$ sudo yum install docker-ce

# On production systems, you shoulkd install a specific version of Docker CE instead of always using the latest.
$ sudo yum list docker-ce --showduplicates | sort -r
$ sudo yum install <FULLY-QUALIFIED-PACKAGE-NAME>
```

### Start Docker
```shell
$ sudo systemctl start docker
$ sudo systemctl enable docker
```

### Add your user to the `docker` group
```shell
sudo usermod -aG docker $USER
```
