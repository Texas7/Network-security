## Site-to-Site IPsec VPN

#### First
#### On Router:

```
show version             > Verifique se o Security Technology package está ativo
```

#### If not:

```
license boot module c1900 technology-package securityk9

write

reload
```

<br><br>


#### Creating an access-list:

```
access-list 110 permit ip 192.168.1.0 0.0.0.255 192.168.3.0 0.0.0.255
				                   "current network"        "destination"
```

#### De acordo com os métodos solicitadas
#### Configuring the IKE Phase 1 ISAKMP policy on Router1:

```
crypto isakmp policy 10

encryption aes 256

authentication pre-share

group 5

exit

crypto isakmp key vpnpa55 address 10.2.2.2    > Endereço do roteador de destino.
		             "set_key"
```

#### Configuring the IKE Phase 2 IPsec policy on Router1:

```
crypto ipsec transform-set VPN-SET esp-aes esp-sha-hmac
				 "set_name"

crypto map VPN-MAP 10 ipsec-isakmp

description conexão VPN com o router33

set peer 10.2.2.2                            > Ip da interface do roteador de destino   

set transform-set VPN-SET

match address 110                            > 110 é a access-list

exit
```

#### Apply:

```
interface s0/0/0           > Example

crypto map VPN-MAP
```

#### In other Router:
#### Configuring IPsec Parameters on Router33

#### Creating an access-list:

```
access-list 110 permit ip 192.168.3.0 0.0.0.255 192.168.1.0 0.0.0.255
				                   "current network"        "destination"
```

#### Configuring the IKE Phase 1 ISAKMP properties on Router33:

```
crypto isakmp policy 10

encryption aes 256

authentication pre-share

group 5

exit

crypto isakmp key vpnpa55 address 10.1.1.2    > Endereço do roteador de destino.
		             "same_key"
```

#### Configuring the IKE Phase 2 IPsec policy on Router33:

```
crypto ipsec transform-set VPN-SET esp-aes esp-sha-hmac
				                  "set_name"

crypto map VPN-MAP 10 ipsec-isakmp

description conexão VPN com o router1

set peer 10.1.1.2                              > Ip da interface do roteador de destino  

set transform-set VPN-SET

match address 110

exit
```

#### Apply:

```
interface s0/0/1        > Example

crypto map VPN-MAP
```

#### Verifing

```
show crypto ipsec sa
```

> Test ping
