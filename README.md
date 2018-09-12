oVirt environment shutdown
=========

The `oVirt.shutdown-env` role iterates through all the entities (vms and hosts) in an oVirt/RHV cluster and performs a clean and ordered shutdown.
It also handles an Hosted-Engine and hyper-converged GlusterFS environment as a special case automatically detecting it.
The role is intended to be run only against the engine machine.

If on an Hosted-Engine environment, global maintenance mode will be set:
the user has to manually exit it in order to get the engine VM automatically powered up once needed. 

A startup mode is also available:
in the startup mode the role will bring up all the IPMI configured hosts and it
will unset the global maintenance mode if on an hosted-engine environment.
The startup mode will be executed only if the 'startup' tag is applied; shutdown mode is the default.
The startup mode requires the engine to be already up.

Requirements
------------

 * Ansible version 2.6 or higher
 * Python SDK version 4.2 or higher

Dependencies
------------

No.

Example Playbook
----------------

```yaml
---
- name: oVirt shutdown environment
  hosts: localhost
  connection: local
  gather_facts: false

  vars:
    engine_url: https://ovirt-engine.example.com/ovirt-engine/api
    engine_user: admin@internal
    engine_password: 123456
    engine_cafile: /etc/pki/ovirt-engine/ca.pem

  roles:
    - oVirt.shutdown-env
```

Demo
----
 Here a demo showing a clean and ordered shutdown of an hyper-converged hosted-engine environment with 3 hosts, 3 regular VMs plus the HE one.
[![asciicast](https://asciinema.org/a/vZJ6xFEU1POYyS8mEKF9lcV63.png)](https://asciinema.org/a/vZJ6xFEU1POYyS8mEKF9lcV63)

License
-------

Apache License 2.0
