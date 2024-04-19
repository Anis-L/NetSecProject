**Firewall Configuration**

**Hostname**
- `hostname ASAv-DMZ-I` (Set the hostname)

**Enable Password**  
- `enable password cisco` (Set encrypted enable password)

**Interface Configuration**

*Outside Interface (to Edge Router)*
- `interface GigabitEthernet0/0` 
- `description Link to vIOS-EDGE-I` (Interface description)
- `nameif OUTSIDE` (Name the interface as OUTSIDE)
- `security-level 0` (Set security level to 0 for outside interface)
- `ip address 195.1.1.130 255.255.255.252` (Set interface IP address)

*Inside Interface (to DMZ Switch)* 
- `interface GigabitEthernet0/1`
- `description Link to vIOS-DMZ-I`
- `nameif INSIDE` 
- `security-level 100` (Set higher security level for inside)
- `ip address 195.1.1.133 255.255.255.252`

**FTP Mode**
- `ftp mode passive` (Set passive mode for FTP)

**Timezone**
- `clock timezone UTC+2 2` (Set timezone to UTC+2)

**DNS Lookup**
- `dns domain-lookup INSIDE` (Lookup DNS from inside interface) 

**DNS Server Group**
- `dns server-group DefaultDNS`
- `name-server 195.1.1.161` (Add DNS server)

**Network Objects**
- `object network serv-dmz-i` (Define network object for serv-dmz-i host)
- `host 195.1.1.161`
- `object network public_add` (Define network object for public address range)
- `subnet 195.1.1.0 255.255.255.0` 
- `object network google_dns1` (Define network objects for Google DNS servers)
- `host 8.8.8.8`
- `object network google_dns2`
- `host 8.8.4.4`
- `object network vios-edge-i_gi0_0` (Define network object for vios-edge-i interface)
- `host 195.1.1.129`
- `object-group network google_dns` (Create network object group for Google DNS)
- `network-object object google_dns1`
- `network-object object google_dns2`
**Access Control List**
- `access-list out-to-ins extended permit tcp object public_add object public_add eq ssh` (Permit SSH from public network)
- `access-list out-to-ins extended permit icmp object public_add object public_add echo` (Permit ICMP echo from public network)
- `access-list out-to-ins extended permit tcp any object serv-dmz-i range www https` (Permit web traffic to serv-dmz-i)
- `access-list out-to-ins extended permit icmp object-group google_dns object public_add echo-reply` (Permit ICMP echo-reply from Google DNS to public network)
- `access-list out-to-ins extended permit udp object vios-edge-i_gi0_0 object serv-dmz-i eq domain` (Permit DNS traffic from vios-edge-i to serv-dmz-i)
**Logging Configuration**
- `logging enable` (Enable logging)
- `logging console informational` (Set logging level for console)
- `logging monitor informational` (Set logging level for monitor)
- `logging buffered informational` (Set logging level for buffer)
- `logging trap notifications` (Log notifications)
- `logging host INSIDE 195.1.1.161` (Set logging host)
**Access Group**
- `access-group out-to-ins in interface OUTSIDE` (Apply ACL to interface)

**Static Routes**
- `route OUTSIDE 0.0.0.0 0.0.0.0 195.1.1.129`
- `route INSIDE 195.1.1.192 255.255.255.192 195.1.1.134`
- `route OUTSIDE INSIDE 195.1.1.160 255.255.255.224 195.1.1.134`

**AAA Authentication**
- `aaa authentication ssh console LOCAL` (Authentication for SSH/console)
- `aaa authentication serial console LOCAL`

**Telnet Timeout**
- `telnet timeout 5` (Set Telnet timeout)
**SSH Settings**
- `ssh 195.1.1.0 255.255.255.128 OUTSIDE` (Allow SSH from specific network on outside interface)
- `ssh timeout 60` (Set SSH timeout)
- `crypto key generate rsa modulus 4096`
- `ssh version 2` (Set SSH version to 2)
- `ssh key-exchange group dh-group14-sha1%` (Set SSH key exchange group)

**Console Timeout**
- `console timeout 0` (Disable console timeout)

**NTP Server**
- `ntp server 195.1.1.161` (Configure NTP server)

**Username/Password**
- `username admin password cisco` (Set admin user password)

**Class Map**
- `class-map inspection_default` (Default inspection class map)

**Policy Maps**
- `policy-map type inspect http http_map` (Define HTTP inspection policy map)
- `parameters`
- `protocol-violation action drop-connection log` (Action for protocol violations)
- `policy-map type inspect dns migrated_dns_map_1` (Define DNS inspection policy map)
- `parameters`
- `policy-map global_policy` (Define global policy map)
- `class inspection_default`