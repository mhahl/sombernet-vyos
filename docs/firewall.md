Firewall Configuration
======================

## dcr01-ge-1.nsw01

```
set firewall all-ping enable
set firewall broadcast-ping disable
set firewall ipv6-recieve-redirects enable
set firewall ipv6-src-route enable
set firewall syn-cookies enable

set firewall name LAN-LOCAL default-action drop
set firewall name LAN-LOCAL description 'LAN to Router IPv4'
set firewall name LAN-LOCAL enable-default-log
set firewall name LAN-LOCAL rule 1 action 'accept'
set firewall name LAN-LOCAL rule 1 description 'accept all traffic'

set firewall name LOCAL-LAN default-action drop
set firewall name LOCAL-LAN description 'Router to LAN IPv4'
set firewall name LOCAL-LAN enable-default-log
set firewall name LOCAL-LAN rule 1 action 'accept'
set firewall name LOCAL-LAN rule 1 description 'accept all traffic'

set firewall name LAN-WAN default-action drop
set firewall name LAN-WAN description 'LAN to WAN IPv4'
set firewall name LAN-WAN enable-default-log
set firewall name LAN-WAN rule 1 action 'accept'
set firewall name LAN-WAN rule 1 description 'accept all traffic'

set firewall name LOCAL-WAN default-action 'drop'
set firewall name LOCAL-WAN description 'Router to WAN IPv4'
set firewall name LOCAL-WAN enable-default-log
set firewall name LOCAL-WAN rule 1 action 'accept'

set firewall name LOCAL-DMVPN default-action 'drop'
set firewall name LOCAL-DMVPN description 'Router to DMVPN'
set firewall name LOCAL-DMVPN enable-default-log
set firewall name LOCAL-DMVPN rule 1 action 'accept'

set firewall name DMVPN-LOCAL default-action 'drop'
set firewall name DMVPN-LOCAL description 'Router to DMVPN'
set firewall name DMVPN-LOCAL enable-default-log
set firewall name DMVPN-LOCAL rule 1 action 'accept'

set firewall name WAN-LAN default-action 'drop'
set firewall name WAN-LAN description 'WAN to LAN IPv4'
set firewall name WAN-LAN enable-default-log
set firewall name WAN-LAN rule 1 action 'accept'
set firewall name WAN-LAN rule 1 state established 'enable'
set firewall name WAN-LAN rule 1 state related 'enable'
set firewall name WAN-LAN rule 2 action 'drop'
set firewall name WAN-LAN rule 2 state invalid 'enable'

set firewall name WAN-LOCAL default-action 'drop'
set firewall name WAN-LOCAL description 'WAN to Router IPv4'
set firewall name WAN-LOCAL enable-default-log
set firewall name WAN-LOCAL rule 1 action 'accept'
set firewall name WAN-LOCAL rule 1 state established 'enable'
set firewall name WAN-LOCAL rule 1 state related 'enable'
set firewall name WAN-LOCAL rule 2 action 'drop'
set firewall name WAN-LOCAL rule 2 state invalid 'enable'
set firewall name WAN-LOCAL rule 3 action 'accept'
set firewall name WAN-LOCAL rule 3 description 'DHCP Replies'
set firewall name WAN-LOCAL rule 3 destination port '67,68'
set firewall name WAN-LOCAL rule 3 protocol 'udp'
set firewall name WAN-LOCAL rule 3 source port '67,68'
set firewall name WAN-LOCAL rule 100 action 'accept'
set firewall name WAN-LOCAL rule 100 description 'Allow IGMP'
set firewall name WAN-LOCAL rule 100 protocol 'igmp'
set firewall name WAN-LOCAL rule 101 description 'Allow ssh'
set firewall name WAN-LOCAL rule 101 destination port '22'
set firewall name WAN-LOCAL rule 101 protocol 'tcp'
set firewall name WAN-LOCAL rule 101 action 'accept'

set firewall zone LAN default-action drop
set firewall zone LAN from LOCAL firewall name LOCAL-LAN
set firewall zone LAN from WAN firewall name WAN-LAN
set firewall zone LAN interface eth1
set firewall zone LAN interface eth1.10

set firewall zone DMVPN default-action drop
set firewall zone DMVPN from LOCAL firewall name LOCAL-DMVPN
set firewall zone DMVPN interface tun0

set firewall zone LOCAL default-action drop
set firewall zone LOCAL from LAN firewall name LAN-LOCAL
set firewall zone LOCAL from WAN firewall name WAN-LOCAL
set firewall zone LOCAL from DMVPN firewall name DMVPN-LOCAL
set firewall zone LOCAL local-zone

set firewall zone WAN default-action drop
set firewall zone WAN from LOCAL firewall name LOCAL-WAN
set firewall zone WAN from LAN firewall name LAN-WAN
set firewall zone WAN interface eth0

```
