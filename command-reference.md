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

### cEdge CSR1000v
```
request platform software sdwan vedge_cloud activate chassis-number {{ chassis_number }} token {{ token }}
```

## Real Time Commands

### vBond
* Orchestrator Valid vEdge Routers
