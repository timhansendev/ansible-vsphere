# Ansible and VSphere Demo
Demonstration of deploying RHEL VM's using Ansible on VSphere 7.0+

#### Requirements:

- Ansible Tower deployed on RHEL8 or similar OS. 

- VSphere 7.0 (Not tested on any other version)  

- RHEL VM Template on VSphere

- [Pyvomi](https://github.com/vmware/pyvmomi) installed on Tower Node(s).

- Dynamic Inventory Source from Vsphere needs the following source variables, as well as valid credentials to login.
```
compose:
  ansible_host: guest.ipAddress
  ansible_ssh_host: guest.ipAddress
  ansible_uuid: 99999999 | random | to_uuid
  availablefield: availableField
  configissue: configIssue
  configstatus: configStatus
  customvalue: customValue
  effectiverole: effectiveRole
  guestheartbeatstatus: guestHeartbeatStatus
  layoutex: layoutEx
  overallstatus: overallStatus
  parentvapp: parentVApp
  recenttask: recentTask
  resourcepool: resourcePool
  rootsnapshot: rootSnapshot
  triggeredalarmstate: triggeredAlarmState
filters:
- runtime.powerState == "poweredOn"
- "'rhel8' in tags"
keyed_groups:
- key: tags
  prefix: ""
  separator: ""
- key: config.guestId
  prefix: ''
  separator: ''
- key: '"templates" if config.template else "guests"'
  prefix: ''
  separator: ''
plugin: community.vmware.vmware_vm_inventory
properties:
- availableField
- configIssue
- configStatus
- customValue
- datastore
- effectiveRole
- guestHeartbeatStatus
- layout
- layoutEx
- name
- network
- overallStatus
- parentVApp
- permission
- recentTask
- resourcePool
- rootSnapshot
- snapshot
- triggeredAlarmState
- value
- capability
- config
- guest
- runtime
- storage
- summary
strict: false
with_nested_properties: true
with_tags: true
```

### Running 
Import repository via a new project in Tower to run against your nodes.
