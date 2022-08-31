## Configuring ACLs

```
ip access-list standard list_name
or
ip access-list extended list_name

deny any 
or
permit any
```
> Exemplos na pagina da <a href="https://www.cisco.com/c/pt_br/support/docs/ip/access-lists/26448-ACLsamples.html">cisco</a>


##### Checking applications

```
show access-lists
```

#### On interface 

```
interface <f/g>

ip access-group list_name out
or
ip access-group list_name in
```
> Não é boa prática aplicar listas de acesso enquanto a interface está ativa, evite se possível.

##### Checking applications

```
show access-lists

show run
or
show ip interface <f/g>
```
<br>
<br>
<br>

#### Comando para auxiliar no detalhamento das configurações: 
##### Também serve para aplicar as permissões:

```
access-list ?
access-list 100 ?
```

#### Permitir ou negar todos os outros tráfegos normalmente:

```
permit ip any any
or
deny ip any any 
```

#### Deletar uma lista:

```
no ip access-list extended/standard list_name
```

#### Deletar uma linha:

```
no line_number
```

<br><br><br>


-----------------------------

<br><br><br><br>

## ACL IPV6

```
ipv6 access-list list_name

interface <f/g>

ipv6 traffic-filter list_name in/out
```
