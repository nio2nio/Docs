### Add a user
```shell
$ useradd cent
$ passwd cent
```

### Limit user who can switch to root as adminstrator user
```shell
$ usermod -aG wheel cent

$ vi /etc/pam.d/su
# Uncomment the following line
auth    required    pam_wheel.so use_uid
```

### sudo
```shell
$ visudo 
$ vi /etc/sudoers

# Allow people in group wheel to run all command
%wheel  ALL=(ALL)       ALL
```

### Forward root email to following user
```shell
$ vi /etc/aliases
# Umcomment last line and add user
root:       cent

$ newaliases
```
