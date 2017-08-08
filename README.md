## BOSH Event Log Release

The Event Log Release provides a BOSH job for streaming Windows Event Logs to a syslog endpoint over TCP or UDP.

#### Example manifest:

```yaml
---
name: event_log_deployment
director_uuid: REPLACE_ME

releases:
- name: event_log
  version: latest

stemcells:
- alias: windows
  os: windows2012R2
  version: latest

update:
  canaries: 0
  canary_watch_time: 60000
  max_in_flight: 1
  update_watch_time: 60000

instance_groups:
- name: event_log_job
  azs: [z1]
  instances: 1
  jobs:
  - name: event_log_forwarder
    release: event_log
    properties:
      syslog:
        address: logs.papertrailapp.com
        port: REPLACE_ME
        protocol: tcp # udp is also accepted
  vm_type: REPLACE_ME
  stemcell: windows
  networks:
  - name: default
```
