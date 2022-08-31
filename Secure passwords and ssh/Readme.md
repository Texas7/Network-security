## Configuring secure passwords and ssh


#### Disable DNS lookup:

```
no ip domain-lookup
```

#### Set the domain name to netsec.com (ex):

```
ip domain-name netsec.com
```

#### Create a user of your choosing with a strong encrypted password:

```
username any_user secret any_password
```

#### Generate 1024-bit RSA keys:

```
crypto key generate rsa
1024
```

#### Configure all VTY lines for SSH access and use the local user profiles for authentication:

```
line vty 0 4
transport input ssh
login local
```
#### Access the command prompt on the desktop:

```
SSH -l username target
```
