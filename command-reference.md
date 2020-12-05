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

## Real Time Commands

### vBond
* Orchestrator Valid vEdge Routers
