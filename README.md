# Network Troubleshoot
This Repository Contains `network.troubleshoot` Ansible Collection.

## Description
The `network.troubleshooting` application provides platform-agnostic single entry point
to perform the network troubleshooting.This collection also act as core for other network validated
content collections.

**Capabilities**
- Troubleshoot: `troubleshoot` operation enables users to performs collective predefined relevant network health-checks and perform assertion and validation based on the gathered information. 
- Health-Checks: `health-checks` operation enables users to perform certain health-checks and return the status.
- List: `list` operation returns the resources which allows troubleshooting
 
### Usage
This platform-agnostic role enables the user to troubleshoot the network issues by analyzing the information gathered through ansible network modules.The tasks offered by this role could be observed below:

## OSPF troubleshooting
```yaml
run.yml
---
- hosts: network
  tasks:
  - name: Network Troubleshooting
    ansible.builtin.include_role:
      name: network.troubleshoot.run
    vars:
      operation: troubleshoot
      resources:
      - ospf
      - bgp
```

#### Output.
```yaml
run.yml
---
{
    status: success,
  [
    {
    name: ospf_routing,
    status: "success",
    },
    {
    name: bgp_routing,
    status: "success",
    }
  ]
}
```
#### display result with detailed output.
```yaml
run.yml
---
- hosts: network
  tasks:
  - name: Network Troubleshooting
    ansible.builtin.include_role:
      name: network.troubleshoot.run
    vars:
      operation: troubleshoot
      detail: true
      resources:
      - ospf
```

#### Output.
```yaml
run.yml
---
{
    status: failure,
[
    {
    name: ospf_routing
    status: "failed",
    failures:[
        "area_id_mismatch"
        ],
    health-checks:[
        is_ospf_enabled: {
            status: success,
        },
        is_l1_up: {
            status: success,
        },
        is_l2_up: {
            status: success,
        }, 
        is_interface_passive: {
            status: success,
        },
        is_acl_blocking_ospf_hello: {
            status: success,
        },
        broadcast_link_subnet_mismatch: {
            status: success,
        },  
        hello_interval_mismatch: {
            status: success,
        },  
        dead_interval_mismatch: {
            status: success,
        },  
        authentication_type_mismatch: {
            status: success,
        },  
        area_id_mismatch: {
        status: Failure,
        msg: {
             r1: network 121.110.0.0 0.0.255.255 area 1,
             r2: network 121.110.0.0 0.0.255.255 area 0
        },
        is_reachable: {
            status: success
        },
        }  

    ]
    }
]
}
```
