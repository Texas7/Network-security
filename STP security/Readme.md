## Configuring STP

> Examples:

Network (interfaces):

![5](https://user-images.githubusercontent.com/104938729/187757235-e0bd97ea-b8aa-4e71-96b8-f727ed0330d4.png)

<br><br><br><br>

![1](https://user-images.githubusercontent.com/104938729/187748447-57f6fc3c-3a81-4d9a-87fd-028f3f8c1509.png)

> Determine the current root bridge

<br>

#### From central:

```
show spanning-tree
```

![2](https://user-images.githubusercontent.com/104938729/187748683-16a91aa1-8ceb-4413-bfc2-20bdc771b9e5.png)

>Which switch is the current root bridge ?
> <br> Current root is SW-1

<br>

#### Based on the current root bridge, what is the resulting spanning tree?

![3](https://user-images.githubusercontent.com/104938729/187754819-d2e735ab-0062-4f0d-92c3-73d4623e3e78.png)

<br>

#### Atribuindo a Central como a root bridge:

```
spanning-tree vlan 1 root primary
```
<br>

#### Atribuindo o SW-1 como a root bridge secundária:

```
spanning-tree vlan 1 root secondary
```
<br>

#### Verifying the spanning-tree configuration.
#### On Central:

```
show spanning-tree
```

![4](https://user-images.githubusercontent.com/104938729/187755794-7f6c7f52-d1bc-4313-8d07-a6f2997276d7.png)

<br>

#### Protecting Against STP Attacks
#### From SW-A and SW-B:

> Permitir que as portas se tornem ativas mais rapidamente:

```
interface range f0/1 – 4
spanning-tree portfast
```
<br>

#### Enabling BPDU guard on all access ports:

```
interface range f0/1 – 4
spanning-tree bpduguard enable
```
<br>

#### Enabling root guard.
#### On SW-A and SW-B:

````
interface range f0/23 – 24
spanning-tree guard root
````






