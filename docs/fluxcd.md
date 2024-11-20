---
title: FluxCD
layout: page
parent: Keycloak
grand_parent: Identity and Access Management
---

The repository that defines the flux configuration for keycloak is located at https://github.com/lsc-sde/iac-flux-keycloak



## Network Policies

```mermaid
flowchart LR
    all([all services]) -->|Ingress ALL| svc[Keycloak] 
    svc -->|Egress ALL|all
```

| Direction | Ports/Type | Description |
| --- | --- | --- |
| Ingress | All | Allows all traffic inbound. TODO: This needs to be refined |
| Egress | All | Allows all traffic to egress. TODO: This needs to be refined |

