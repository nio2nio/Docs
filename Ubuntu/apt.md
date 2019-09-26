## Behind Proxy Configuration
```bash
$ sudo vi /etc/apt/apt.conf
Acquire::http::Proxy "http://10.1.1.117:8088";
Acquire::https::Proxy "http://10.1.1.117:8088";

## Fix "Hash sum mismatch"
$ sudo vi /etc/apt/apt.conf.d/99fixbadproxy
Acquire::http::Pipeline-Depth 0;
Acquire::http::No-Cache true;
Acquire::BrokenProxy    true;
```

## APT Command Usage
+ Installing a Package
```bash
$ sudo apt install package_name
```
+ Find Location of Installed Package
```bash
$ sudo apt content package_name
```
+ Check All Dependencies of a Package
```bash
$ sudo apt depends package_name
```
+ Search for a Package
```bash
$ sudo apt search package_name
```
+ View Information About Package
```bash
$ sudo apt show package_name
```
+ Verify a Package for any Broken Dependencies
```bash
$ sudo apt check package_name
```
+ List Recommended Missing Packages of Given Package
```bash
$ sudo apt recommands package_name
```
+ Check Installed Package Version
```bash
$ sudo apt version package_name
```
+ Update System Packages
```bash
$ sudo apt update
```
+ Upgrade System
```bash
$ sudo apt upgrade
```
+ Remove Unused Packages
```bash
$ sudo apt autoremove
```
+ Clean Old Repository of Downloaded Packages
```bash
$ sudo apt autoclean
sudo apt clean
```
+ Remove Packages with its Configuration Files
```bash
$ sudo apt purge package_name
```
+ Install .Deb Package
```bash
$ sudo apt deb package.deb
```
+ Find Help While Using APT
```bash
$ apt help
```
