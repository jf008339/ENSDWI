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
 If the router is not connected to a DHCP server, configure the IP address of the WAN interface.
 ```
     interface GigabitEthernet 1
     no shutdown 
     ip address dhcp  
```
Configure tunnel parameters.
```
    config-transaction
     sdwan
      interface GigabitEthernet 2
       tunnel-interface
        encapsulation ipsec
        color lte
        end
```
Note: If an IP address is manually configured on the router, configure a default route as shown below. The IP address below indicates a next-hop IP address.
```
    config-transaction
     ip route 0.0.0.0 0.0.0.0 192.0.2.25
````
    Enable OMP to advertise VRF segment vroutes.



    sdwan
    omp
     no shutdown
     graceful-restart
     no as-dot-notation
     timers
     holdtime 15
     graceful-restart-timer 120
     exit
    address-family ipv4
     advertise ospf external
     advertise connected
     advertise static
     exit
    address-family ipv6
     advertise ospf external
     advertise connected
     advertise static
     exit
    address-family ipv4 vrf 1
     advertise bgp
     exit
    exit
     

    Configure the service VRF interface.



    config-transaction
     interface GigabitEthernet 2 
      no shutdown
      vrf forwarding 10
      ip address 192.0.2.2 255.255.255.0
      exit
     

Verify Configuration

Run the show ip vrf brief command to view information about the VRF interface.


Device# sh ip vrf brief
  Name                             Default RD            Interfaces
  10                               1:10                  Gi4
  11                               1:11                  Gi3
  30                               1:30
  65528                            <not set>             Lo65528


### vSmart
```
show omp routes {{ prefix }} [ received | advertised ] { detail }
```

## Real Time Commands

### vBond
* Orchestrator Valid vEdge Routers
