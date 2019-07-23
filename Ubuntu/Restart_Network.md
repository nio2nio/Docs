1. **Network Manager Service**
```bash
$ sudo service network-manager restart
```

2. **systemd**
```bash
$ sudo systemctl restart NetworkManager.service
```

3. **nmcli**
```bash
$ sudo nmcli networking off
$ sudo nmcil networking on
```

4. **ifup** & **ifdown**
```bash
$ sudo ifdown -a && sudo ifup -a
```
