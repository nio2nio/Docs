### Install Vim
```shell
$ sudo yum install -y vim
```

### Set Alias
```shell
$ sudo vi /etc/profile
alias vi='vim'

# reload
$ source /etc/profile
```

### Config Vim
```shell
$ vi ~/.vimrc
# use extended function of vim (no compatible with vi)
set nocompatible

set encoding=utf-8
set fileencoding=utf-8
set fileformats=unix,dos

set backup
set backupdir=~/backup

set history=50

set ignorecase
# Highlights matched words
set smartcase
set hlsearch
set incsearch

set number
# Visualize break($) or tab(^I)
set list
# Highlights parentheses
set showmatch

# Show color display
syntax on
# Change colors for comments 
highlight Commnet ctermfg=LightCyan

# Wrap lines
set wrap
```
