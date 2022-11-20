# Security Onion

## salt ref
```
sudo salt \* cmd.run 'COMMAND TO EXECUTE'
sudo salt \* cmd.run system.set_system_date_time 'YYYY-MM-DD'
```


## OLD Sec Onion Ref
BPF.conf

`/etc/nsm/capture_int/`

Snort Options: Add `-F /etc/nsm/sensor_/bpf.conf`

Edit `/etc/nsm/sensor_/bpf.conf`
```
(not host X.X.X.X)
```
Restart Service
`nsm_sensor_ps-restart --only-pcap`

Restart Bro
`nsm_sensor_ps-restart --only-bro`

Bro Tagging
bro `8200_post_tagging`

`[source_ip]` & `[destination_ip]`

works on all logs except 'files.log'
`[ips]` field only works on 'files.log'

`/etc/nsm/securityonion.conf` Contains days to keep indices 'open'
