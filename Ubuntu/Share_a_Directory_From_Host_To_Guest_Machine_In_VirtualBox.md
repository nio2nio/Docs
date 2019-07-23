1. Install **virtualbox-guest-utils**
```bash
$ sudo apt install virtualbox-guest-utils
```

2. Add user to **vboxsf**
```bash
$ sudo adduser username vboxsf
```

3. Mount share folder
```bash
$ sudo mount -t vboxsf share_folder mount_point
```
