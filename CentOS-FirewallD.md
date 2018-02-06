### FirewallD is frontend controller for iptables used to implement persistent network traffic rules.
  * FirewallD uses **`zones`** and **`services`** instead of chain and rules.
  * It manages rulesets dynamically, allowing updates **`without breaking existing sessions and connections`**.

## Installing and Managing FirewallDPermalink
  * To start the service and enable FirewallD on boot
  ```shell
  sudo systemctl start firewalld.service
  sudo systemctl enable firewalld.service
  ```
  * To stop and disable it
  ```shell
  sudo systemctl stop firewalld.service
  sudo systemctl disable firewalld.service
  ```
  * Check the firewall status
  ```shell
  sudo firewall-cmd --state
  ```
  * To view the status of the FirewallD daemon
  ```shell
  sudo systemctl status firewalld.service
  ```
  * To reload a FirewallD configuration
  ```shell
  sudo firewall-cmd --reload
  ```
  
### Configuring FirewallD
  * **`/usr/lib/FirewallD`** holds default configurations like default zones and common services. Avoid updating them because those files will be overwritten by each firewalld package update.
  * **`/etc/firewalld`** holds system configuration files. These files will overwrite a default configuration.
  
### Configuration SetsPermalink
  * Firewalld uses two configuration sets: **`Runtime`** and **`Permanent`**. `Runtime configuration changes are not retained on reboot or upon restarting FirewallD whereas permanent changes are not applied to a running system`.
  * By default, firewall-cmd commands apply to runtime configuration but using the **`--permanent`** flag will establish a persistent configuration.
  * Add the rule to both the permanent and runtime sets.
  ```shell
  sudo firewall-cmd --zone=public --add-service=http --permanent
  sudo firewall-cmd --zone=public --add-service=http
  ```
  * Add the rule to the permanent set and reload FirewallD.
  ```shell
  sudo firewall-cmd --zone=public --add-service=http --permanent
  sudo firewall-cmd --reload
  ```
  
### Firewall Zones
  * To view the default zone
  ```shell
  sudo firewall-cmd --get-default-zone
  ```
  * To change the default zone
  ```shell
  sudo firewall-cmd --set-default-zone=internal
  ```
  * To see the zones used by your network interface(s)
  ```shell
  sudo firewall-cmd --get-active-zones
  ```
  * To get all configurations for a specific zone
  ```shell
  sudo firewall-cmd --zone=public --list-all
  ```
  * To get all configurations for all zones
  ```shell
  sudo firewall-cmd --list-all-zones
  ```
  
### Working with ServicesPermalink
  * The configuration files for the default supported services are located at /usr/lib/firewalld/services and user-created service files would be in /etc/firewalld/services.
  * To view the default available services
  ```shell
  sudo firewall-cmd --get-services
  ```
  * To enable or disable the HTTP service
  ```shell
  sudo firewall-cmd --zone=public --add-service=http --permanent
  sudo firewall-cmd --zone=public --remove-service=http --permanent
  ```
  
### Allowing or Denying an Arbitrary Port/ProtocolPermalink
  ```shell
  sudo firewall-cmd --zone=public --add-port=12345/tcp --permanent
  sudo firewall-cmd --zone=public --remove-port=12345/tcp --permanent
  ```
  
### Port Forwarding
  * Forwards traffic from port 80 to port 12345 on the same server
  ```shell
  sudo firewall-cmd --zone="public" --add-forward-port=port=80:proto=tcp:toport=12345
  ```
  * To forward a port to a different server
  ```shell
  # Activate masquerade in the desired zone
  sudo firewall-cmd --zone=public --add-masquerade
  
  # Forwards traffic from local port 80 to port 8080 on a remote server located at the IP address: 123.456.78.9
  sudo firewall-cmd --zone="public" --add-forward-port=port=80:proto=tcp:toport=8080:toaddr=123.456.78.9
  ```
  
### Constructing a Ruleset with FirewallD
  ```shell
  # Assign the dmz zone as the default zone to eth0
  sudo firewall-cmd --set-default-zone=dmz
  sudo firewall-cmd --zone=dmz --add-interface=eth0
  
  # Add permanent service rules for HTTP and HTTPS to the dmz zone
  sudo firewall-cmd --zone=dmz --add-service=http --permanent
  sudo firewall-cmd --zone=dmz --add-service=https --permanent
  
  # Reload FirewallD
  sudo firewall-cmd --reload
  ```
  
### Rich Rules
  * Rich rules syntax is extensive but fully documented in the firewalld.richlanguage(5) man page (or see man firewalld.richlanguage in your terminal). Use --add-rich-rule, --list-rich-rules and --remove-rich-rule with firewall-cmd command to manage them.
  * Allow all IPv4 traffic from host 192.168.0.14
  ```shell
  sudo firewall-cmd --zone=public --add-rich-rule 'rule family="ipv4" source address=192.168.0.14 accept'
  ```
  * Deny IPv4 traffic over TCP from host 192.168.1.10 to port 22
  ```shell
  sudo firewall-cmd --zone=public --add-rich-rule 'rule family="ipv4" source address="192.168.1.10" port port=22 protocol=tcp reject'
  ```
  * Allow IPv4 traffic over TCP from host 10.1.0.3 to port 80, and forward it locally to port 6532.
  ```shell
  sudo firewall-cmd --zone=public --add-rich-rule 'rule family=ipv4 source address=10.1.0.3 forward-port port=80 protocol=tcp to-port=6532'
  ```
  * Forward all IPv4 traffic on port 80 to port 8080 on host 172.31.4.2 (masquerade should be active on the zone).
  ```shell
  sudo firewall-cmd --zone=public --add-rich-rule 'rule family=ipv4 forward-port port=80 protocol=tcp to-port=8080 to-addr=172.31.4.2'
  ```
  * To list your current Rich Rules
  ```shell
  sudo firewall-cmd --list-rich-rules
  ```
