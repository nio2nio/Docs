* FirewallD is frontend controller for iptables used to implement persistent network traffic rules.
  1. FirewallD uses **zones** and **services** instead of chain and rules.
  2. It manages rulesets dynamically, allowing updates **without breaking existing sessions and connections**.

* Installing and Managing FirewallDPermalink
  ** To start the service and enable FirewallD on boot
  ```shell
  sudo systemctl start firewalld.service
  sudo systemctl enable firewalld.service
  ```
