### Hostname
```shell
# Set hostname
$ hostnamectl set-hostname your_hostname
```

### nmcli
```shell
# Show device
$ nmcli d

# Set IPv4 Address
$ nmcli c modify eth0 ipv4.addresses 10.0.0.30/24

# Set default gateway
$ nmcli c modify eth0 ipv4.gateway 10.0.0.1

# Set DNS
$ nmcli c modify eth0 ipv4.dns 10.0.0.1 

# Set DHCP (auto) Or Static (manual)
$ nmcli c modify eth0 ipv4.method manual

# Reload Setting
$ nmcli c down eth0; nmcli c up eth0 

# Show setting
$ nmcli d show eth0 

# Show status
$ ip addr show
```

### Disable IPv6
```shell
$ vi /etc/default/grub
# Line 6 Add...
GRUB_CMDLINE_LINUX="ipv6.disable=1 rd.lvm.lv=centos/root....."

# Apply changes
$ grub2-mkconfig -o /boot/grub2/grub.cfg 
$ reboot
```

### Use network interface name "ethX" (by default CentOS 7 use "enoX")
```shell
$ vi /etc/default/grub
# Line 6 Add ...
GRUB_CMDLINE_LINUX="net.ifnames=0 biosdevname=0 rd.lvm.lv=centos/root....."

# Apply changes
$ grub2-mkconfig -o /boot/grub2/grub.cfg 

# 將 Eno 網卡的設定檔用 mv 改名為 eth0
$ mv /etc/sysconfig/network-scripts/ifcfg-ens32 /etc/sysconfig/network-scripts/ifcfg-eth0

$ vi /etc/sysconfig/network-scripts/ifcfg-eth0
NAME=eth0

$ reboot
```
