# Network-security

----------------------

## Gerenciamento do Cisco IOS

#### Entrar no modo privilegiado:

```
Router>enable 
Router# 
```

#### Configuração de horário:

```
Router#clock set “hh:mm:ss” “DD Mês AAAA” 
```
> OBS: Mês deve ser em inglês
<br>

#### Entrar no modo de configuração global:

```
Router#configure terminal 
Router(config)#
```

#### Configuração de nome: 

```
Router(config)#hostname R1 
R1(config)# 
```

#### Configuração de banner de aviso:

```
R1(config)#banner motd #ACESSO RESTRITO#
```

#### Configuração de senha para acesso ao modo privilegiado:

```
R1(config)#enable secret "senha"
```

#### Desativar resolução dinâmicas de nome :

```
R1(config)#no ip domain lookup
```

#### Configuração de acesso por console:

```
R1(config)#line console 0 
R1(config-line)#login local
```

#### Configuração de acesso TELNET :

```
R1(config)#line vty 0 4 
R1(config-line)#login local 
```
> ESQUECE ESSE TREM !!!!

#### Criptografar todas as senhas:

```
Router(config)#service password-encryption 
```

#### Configuração de interface:

```
LAN: g0/0 e g0/1 
WAN: s0/0/0 e s0/0/1 
R1(config)#interface "tipo de interface" 
R1(config-if)#description “LINK-TO-LAN-A”                (descrição da interface) 
R1(config-if)#ip address "end ip" "mascara de subrede"   (endereça a interface) 
R1(config-if)#no shutdown                                (habilita a interface) 
```


#### Configuração de Serviço DHCP:

```
R1(config)#ip dhcp pool "nome" 
R1(dhcp-config)#network "end de rede" "mascara de subrede" 
R1(dhcp-config)#default-router "end IP do gateway da rede" 
R1(dhcp-config)#dns-server "end IP do servidor DNS"                     (utilize se precisar incluir o endereço do Server DNS) 
R1(dhcp-config)#exit 
R1(config)#ip dhcp excluded-address "end IP a ser excluido do pool"     (utilize este comando se for necessário 
                                                                        excluir algum endereço IP a ser atribuído 
                                                                        pelo servidor. Exemplo: Endereços estáticos
                                                                        não devem fazer parte pool do servidor, 
                                                                        como Gateway, Servidores e Impressoras.)
```

#### Configuração de rota estática: 

```
R1(config)#ip route “endereço de rede de destino” “máscara” “porta de saída”
```

#### Configuração de usuário e senha para acesso ao FTP server:

```
R1(config)#ip ftp username “usuário” 
R1(config)#ip ftp password “senha”
```

####  Visualização do arquivo de configuração:

```
R1#show running-config
```

#### Salvar arquivo de configuração

```
R1#write 
Or 
R1#copy running-config startup-config
```

<br>
<br>
<br>
<br>

--------------------------

### On Pc

#### Teste de acesso remoto TELNET a partir do PC no Command Prompt:

```
PC>telnet "end IP de destino"
```

#### Realizar o Backup de arquivos contidos no FTP Server para o PC:

```
> Efetuar login com usuário e senha
PC>ftp “end do servidor ftp” 
 
> Visualizar os arquivos contidos no servidor 
ftp>dir 

> Baixar os arquivos 
ftp>get “nome do arquivo” 
ftp>quit 

> Visualizar arquivos baixados 
PC>dir
```

------------------------------

<br>
<br>
<br>
<br>

## Gerenciamento Básico de Switch

#### Configuração de horário:

```
Switch#clock set “hh:mm:ss” “DD Mês AAAA” 
```

#### Configuração de Interface de Gerenciamento: :

```
Switch(config)#interface vlan “ID” 
Switch(config-if)#ip address “end IP” “mask” 
Switch(config-if)#no shutdown 
```

### Configuração de Gateway Padrão:

```
Switch(config)#ip default-gateway “end IP”
```

### Configuração de Modo de Porta:

```
Switch(config-if)#duplex ? 
auto Enable AUTO duplex configuration 
full Force full duplex operation 
half Force half-duplex operation 
```

### Configuração de Velocidade de Porta:

```
Switch(config-if)#speed ? 
10 Force 10 Mbps operation 
100 Force 100 Mbps operation 
auto Enable AUTO speed configuration 
```

### Verificar tabela MAC:

```
Switch#show mac-address-table
```

#### Criação de VLAN:

```
Switch(config)#vlan “id” 
Switch(config-vlan)#name “nome”
```

#### Criar um range de interfaces seqüenciais:

```
Switch(config)#interface range f0/1-10 
Switch(config-if-range)# 
```

#### Criar um range de interfaces específicas: 

```
Switch(config)#interface range f0/1,f0/3,f0/5 
Switch(config-if-range)# 
```

#### Configurar porta em modo de acesso e associar a uma vlan:

```
Switch(config)#interface f0/1 
Switch(config-if)#switchport mode access 
Switch(config-if)#switchport access vlan “id” 
```

#### Configurar porta em modo tronco (via das vlan´s):

```
Switch(config)#interface f0/1 
Switch(config-if)#switchport mode trunk
```

#### Redefinir vlan´s permitidas no tronco sendo as não listadas negadas:

```
Switch(config-if)#switchport trunk allowed vlan id, id, id
```

#### Verificar troncos ativos na configuração:

```
Switch(config)#show interfaces trunk 
```

#### Verificar tabela de VLAN e associação de portas:

```
Switch#show vlan brief
```

----------------------------------------

<br>
<br>
<br>
<br>

## Roteamento Inter-Vlan (subinterface + protocolo de entroncamento 802.1q)

## Configuração do Router

#### Criação de subinterface e entroncamento:

```
Subinterface a partir da interface g0/0 

Router(config)#interface g0/0.”id de vlan” Exemplo g0/0.10 (Vlan 10)
Router(config-subif)#encapsulation dot1Q "id de vlan" 
Router(config-subif)#ip address "end ip” “mascara” 

OBS: Crie 1 subinterface por VLAN 
Exemplo (VLAN 10 = g0/0.10 VLAN 20 = g0/0.20 VLAN 30 = g0/0.30) 
```

#### A ativação da interface é efetuada na interface física:

```
Router(config)#interface g0/0 
Router(config-if)#no shutdown
```

#### Configuração do DHCP snooping: 

```
Switch(config)#ip dhcp snoopinp 
Switch(config)#ip dhcp snooping vlan "id" 
Switch(config)#interface f0/1 (a porta que está conectada ao server DHCP) 
Switch(config-if)# ip dhcp snooping trust 
```
> No Switch !!!

--------------------------












