## Port Security

#### On switch:

```
interface range f0/1 – 2                      > interface de exemplo

switchport port-security                      > Habilitando as portas de segurança
 
switchport port-security maximum 1            > Setando o maximo de dispositivos que podem acessar a porta

switchport port-security mac-address sticky   > O switch irá aprender dinamicamente os endereços macs vinculados 
                                                as portas; adicionado os endereços à running-config.

switchport port-security violation restrict   > Descarta os pacotes desconhecidos quando outro dispositivo se
                                                conecta na porta; também gera logs de violação


interface range f0/3 - 24, g0/1 - 2           > (Exemplos)  Desabilite interfaces não utilizadas 
shutdown
```

#### Verifying the port security:

```
show run | begin interface

show port-security

show port-security address

show port-security interface f0/2            > (exemplo de interface)
```
