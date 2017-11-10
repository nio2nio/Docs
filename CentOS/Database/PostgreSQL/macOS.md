### .bash_profile (如果沒有就建立新的)
```shell
$ vi .bash_profile
if [ -f ~/.bashrc ]; then
   source ~/.bashrc
fi
```

### .bashrc
```shell
$ vi .bashrc
PATH="/Applications/Postgres.app/Contents/Versions/latest/bin:$PATH"
```
#重開terminal console

