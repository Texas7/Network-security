## Tacacs+ server

#### On router: 

```
username Admin2 secret admin2pa55

tacacs-server host 192.168.2.2

tacacs-server key tacacspa55
```

#### configuring the AAA

```
aaa new-model

aaa authentication login default group tacacs+ local

line console 0 

login authentication default
```

#### Verifying:

```
end

write

exit
```
------------------------

## Radius Server

#### On router:

```
username Admin3 secret admin3pa55

radius-server host 192.168.3.2

radius-server key radiuspa55
```

#### configuring the AAA

```
aaa new-model

aaa authentication login default group radius local

line console 0 

login authentication default
```

#### Verifying:

```
end

write

exit
```
-----------------------------------------

<br>
<br>

## On server AAA (example): 

> Different keys for each type of the server !!!

![AAA server](https://user-images.githubusercontent.com/104938729/187741345-d015f60f-313b-46c6-a6c4-457ccca1a57f.png)





