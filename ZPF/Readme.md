## Configuring ZPF - (Política de zonas) 

#### In router:

````
configure terminal

zone security IN-ZONE       > IN-ZONE é o nome escolido para o exemplo
exit

zone security OUT-ZONE      > OUT-ZONE é o nome escolido para o exemplo
exit
````

####  Creating an ACL that defines internal traffic:

````
access-list 101 permit ip 192.168.3.0 0.0.0.255 any   > Nesse exemplo o ip 192.168.3.0 está dentro da zona
````

### Creating a class map referencing the internal traffic ACL:

````
class-map type inspect match-all IN-NET-CLASS-MAP     > IN-NET-CLASS-MAP é o nome escolido para o exemplo

match access-group 101                                > O mesmo da acl

exit
````

#### Creating a policy map to determine what to do with matched traffic:

````
polity-map type inspect IN-2-OUT-PMAP                 > IN-2-OUT-PMAP é o nome escolido para o exemplo

class type inspect IN-NET-CLASS-MAP                   > Especificando a classe de refenrecia para a inspeção

inspect

exit

exit 
````

#### Creating a pair of zones:

````
zone-pair security IN-2-OUT-ZPAIR source IN-ZONE destination OUTZONE 

service-policy type inspect IN-2-OUT-PMAP

exit
````

#### Interfaces:

````
interface g0/1                        > Está presente dentro da zona, 192.168.3.0

zone-member security IN-ZONE

exit


interface s0/0/1                      > Fora da zona

zone-member security OUT-ZONE

exit
````

#### Verifiyng:

````
show policy-map type inspect zone-pair sessions   > Se existir uma conexão ssh, será mostrada
````

