## BOSH Event Log Release

The Event Log Release provides a BOSH job for streaming Windows Event Logs to a syslog endpoint over TCP or UDP.

#### Example runtime-config manifest:

```yaml
---
releases:
- name: event-log
  version: REPLACE_ME

addons:
- name: event-log-addon
  jobs:
  - name: event-log-forwarder
    release: event_log
  include:
    stemcell:
    - os: windows2012R2
  properties:
    syslog:
      address: logs.papertrailapp.com
      port: REPLACE_ME
      protocol: tcp # udp is also accepted
```
