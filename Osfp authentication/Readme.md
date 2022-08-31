## Configuring OSPF MD5 authentication for all the routers in area "0".

> repeat in others routers

````
router ospf 1

area 0 authentication message-digest

interface g0/0/0                 > somente nas interfaces de comunicação entre os roteadores

ip ospf message-digest-key 1 md5 the_password
````

#### Verify configurations:

```
show ip ospf interface
```
