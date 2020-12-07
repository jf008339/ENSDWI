# Cisco ENSDWI Command Reference

## CLI

### vEdge
OTP Activation
```
request vedge-cloud activate chassis-number {{ chassis_number }} token {{ token }}
```
Check the status of the activation
```
show control connections
```
Verifiy Localized/Centralized Policies
```
show run policy
```
### cEdge CSR1000v
OTP Activation
```
request platform software sdwan vedge_cloud activate chassis-number {{ chassis_number }} token {{ token }}
```
Check certificate details:
```
show control local-properties
showcertificate validity
show certificate installed
show certificate root-ca-cert
```
Verify Localized Policies
```
show sdwan running-config | sec policy|route-map
```
BGP
```
show bgp vpnv4 un all
show bgp vpnv4 un all summ
```
Configure service VRFs
```
    config-transaction
     vrf definition 10
      rd 1:10
      address-family ipv4
       exit-address-family
       exit
     address-family ipv6
      exit-address-family
      exit
    exit
```
Configure the tunnel interface to be used for overlay connectivity. Each tunnel interface binds to a single WAN interface. For example, if the router interface is Gig0/0/2, the tunnel interface number is 2.
```
    config-transaction
     interface Tunnel 2
      no shutdown
      ip unnumbered GigabitEthernet1
      tunnel source GigabitEthernet1
      tunnel mode sdwan
      exit
 ```
Run the show ip vrf brief command to view information about the VRF interface.
```
Device# sh ip vrf brief
  Name                             Default RD            Interfaces
  10                               1:10                  Gi4
  11                               1:11                  Gi3
  30                               1:30
  65528                            <not set>             Lo65528
```
The policy is viewable with the “show policy from-vsmart” command.
```
!
BR2-vEdge-1# show policy from-vsmart
from-vsmart data-policy _GUEST_ACCESS_VPN_Gu_-1821888509
 direction from-service
 vpn-list GUEST_ACCESS_VPN
  sequence 1
   match
    destination-data-prefix-list BOGON_ADDR
   action drop
    count GUEST_DROPPED_PKTS_-837951389
  sequence 11
   match
    source-ip 0.0.0.0/0
   action accept
    count GUEST_DIA_PKTS_-837951389
    nat use-vpn 0
    no nat fallback
  default-action drop
from-vsmart lists vpn-list GUEST_ACCESS_VPN
 vpn 3
from-vsmart lists data-prefix-list BOGON_ADDR
 ip-prefix 10.0.0.0/8
 ip-prefix 100.64.0.0/10
 ip-prefix 127.0.0.0/8
 ip-prefix 172.16.0.0/12
 ip-prefix 192.168.0.0/16
```
### vSmart
```
show omp routes {{ prefix }} [ received | advertised ] { detail }
```
## Real Time Commands

### vBond
* Orchestrator Valid vEdge Routers
