1. NodeJs
```bash
$ curl -sL https://deb.nodesource.com/setup_10.x | sudo bash

$ sudo apt update
$ sudo apt install gcc g++ make
$ sudo apt install nodejs

# Check Version
$ node -v
```

2. Yarn
```bash
$ curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
$ sudo apt-get update && sudo apt-get install yarn

# Check Version
$ yarn -v
```
