## Layer 2 VLAN Security

> Enabling trunking, including all trunk security mechanisms on the link between SW-1 and SW-2.
> <br>Cross-over cable
> <br>Many examples below:

#### On SW-1 and SW-2:

````
interface f0/23                       > interface de exemplo que está conectando eles

switchport mode trunk

switchport trunk native vlan 15       > vlan de exemplo

switchport nonegotiate

no shutdown
````

#### Enabling a management VLAN (VLAN 20) on SW-A, SW-B, SW-1 and SW-2: 

````
vlan 20

exit


interface vlan 20

ip address 192.168.20.1 255.255.255.0     > Defidindo o ip de gateway da nova interface e variando nos SWs
````

#### Ready for a new device to connect and receive the connection:

````
interface f0/1                            > interface de conexão do disposivo no sw

switchport access vlan 20

no shutdown
````

#### Enabling a new subinterface on router R1:

````
interface g0/0.3                            > sub-interface (exemplo)

encapsulation dot1q 20

ip address 192.168.20.100 255.255.255.0     > rede vlan
````

<br><br><br><br>

> Now implement the ACLs

