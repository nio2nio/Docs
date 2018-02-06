* FirewallD is frontend controller for iptables used to implement persistent network traffic rules.
  1. FirewallD uses **zones** and **services** instead of chain and rules.
  2. It manages rulesets dynamically, allowing updates **without breaking existing sessions and connections**.

* Installing and Managing FirewallDPermalink
  1. To start the service and enable FirewallD on boot
  ```shell
  sudo systemctl start firewalld.service
  sudo systemctl enable firewalld.service
  ```
  2. To stop and disable it
  ```shell
  sudo systemctl stop firewalld.service
  sudo systemctl disable firewalld.service
  ```
  3. Check the firewall status
  ```shell
  sudo firewall-cmd --state
  ```
  4. To view the status of the FirewallD daemon
  ```shell
  sudo systemctl status firewalld.service
  ```
  5. To reload a FirewallD configuration
  ```shell
  sudo firewall-cmd --reload
  ```
  
* Configuring FirewallD
  1. **`/usr/lib/FirewallD`** holds default configurations like default zones and common services. Avoid updating them because those files will be overwritten by each firewalld package update.
  2. `/etc/firewalld` holds system configuration files. These files will overwrite a default configuration.
