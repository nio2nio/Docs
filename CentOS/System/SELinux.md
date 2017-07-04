### SELinux
>**enforcing** - SELinux security policy is enforced.<br>
>**permissive** - SELinux prints warnings instead of enforcing.<br>
>**disabled** - No SELinux policy is loaded.
``` shell
# Show status
$ getenforce

# Configure SELinux
$ vi /etc/selinux/config
SELinux=disabled

# Reboot
$ reboot