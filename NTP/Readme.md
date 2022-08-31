## Configuring NTP

```
enable

show ntp status

show clock detail

configure terminal

ntp server server_ntp_ip

ntp authenticate

ntp trusted-key 1

ntp authenticationkey 1 md5 the_password
```

#### verifying ntp settings:

```
show clock detail

show ntp status
```
